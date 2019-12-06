## UCS ASYNC SIGNAL BLOCKのインターフェース

### ヘッダ定義

* UCS_ASYNC_SIGNAL_BLOCK(_async)
* UCS_ASYNC_SIGNAL_UNBLOCK(_async)
* UCS_ASYNC_SIGNAL_IS_RECURSIVELY_BLOCKED(_async)

### 構造体

```C
typedef struct ucs_async_signal_context {
    pid_t               tid;         /* Thread ID to receive the signal */
    int                 block_count; /* How many times this context is blocked */
    pthread_t           pthread;     /* Thread ID for pthreads */
    timer_t             timer;
} ucs_async_signal_context_t;
```

## ucs_async_ops_t

* [x] init
* [x] cleanup
* [ ] block
* [ ] unblock
* [x] context_init
* [x] context_cleanup
* [x] context_try_block
* [x] context_unlock
* [ ] add_event_fd
* [ ] remove_event_fd
* [ ] modify_event_fd
* [ ] add_timer
* [ ] remove_timer


| func | signal func |
|------|--|
| init | ucs_async_signal_global_init |
| cleanup | ucs_async_signal_remove_timer |
| block | ucs_async_signal_block_all |
| context_init | ucs_async_signal_init |
| context_cleanup | ucs_async_signal_cleanup |
| context_try_block | ucs_async_signal_try_block |
| context_unlock | ucs_async_signal_unblock |
| add_event_fd | |
| remove_event_fd | |
| modify_event_fd | |
| add_timer | ucs_async_signal_timerq_add_timer |
| remove_timer | |

### ucs_async_signal_global_init

pthread_mutex_init を使ってucs_async_signal_global_context.timers_lockの初期化

### ucs_async_signal_remove_timer

ucs_async_signal_global_context.event_count のカウンターが0か確認
0じゃなかったら、警告を出力

ucs_async_signal_global_context.timers_lockのmutexを、pthread_mutex_destroyで削除


### ucs_async_signal_init

`ucs_async_context_t`構造体に初期値をセットする行う`ucs_async_signal_context`構造体の初期値設定

* block_count: 0
* tid: ucs_get_tid
* pthread: pthread_self
* timer: NULL

```C
pid_t ucs_get_tid(void)
{
#ifdef SYS_gettid
    return syscall(SYS_gettid);
#elif defined(HAVE_SYS_THR_H)
    long id;

    thr_self(&id);
    return (id);
#else
#error "Port me"
#endif
}
```

### ucs_async_signal_cleanup

`async->signal.block_count`が0より大きかったら警告を出す。
それいがいは特になにもしない

### ucs_async_signal_try_block

block_countが0より大きかったら0を返す
そうでない場合、UCS_ASYNC_SIGNAL_BLOCKを呼び出す。
その後1を返す。

ロックが取れたら、1、とれなかったら0を返す。

```C
#define UCS_ASYNC_SIGNAL_BLOCK(_async) \
    { \
        ucs_assert((_async)->signal.tid == ucs_get_tid()); \
        ++(_async)->signal.block_count; \
        ucs_memory_cpu_fence(); \
    }
```

```C
#define ucs_memory_cpu_fence()        ucs_compiler_fence()
```

```C
/**
 * Prevent compiler from reordering instructions
 */
#define ucs_compiler_fence()       asm volatile(""::: "memory")
```

### ucs_async_signal_unblock

UCS_ASYNC_SIGNAL_UNBLOCK を呼び出す。内部ではblock_countをデクリメントするだけ

```
#define UCS_ASYNC_SIGNAL_UNBLOCK(_async) \
    { \
        ucs_memory_cpu_fence(); \
        --(_async)->signal.block_count; \
    }
```

### ucs_async_signal_block_all

```C
static void ucs_async_signal_block_all()
{
    pthread_mutex_lock(&ucs_async_signal_global_context.event_lock);
    if (ucs_async_signal_global_context.event_count > 0) {
        ucs_async_signal_allow(0);
    }
    pthread_mutex_unlock(&ucs_async_signal_global_context.event_lock);
}
```

### ucs_async_signal_timerq_add_timer

```
ucs_async_signal_timerq_add_timer(ucs_async_signal_timer_t *timer, int tid,
                                  int timer_id, ucs_time_t interval)
```

```C
/*
 * Per-thread system timer and software timer queue. We can dispatch timers only
 * on the same thread which added them.
 */
typedef struct ucs_async_signal_timer {
    pid_t                      tid;          /* Thread ID */
    timer_t                    sys_timer_id; /* System timer ID */
    ucs_timer_queue_t          timerq;       /* Queue of timers for the thread */
} ucs_async_signal_timer_t;
```

関数呼び出し時に引数として渡された、ucs_async_signal_timer_t 構造体の`timer->tid`が0だったら(この変数にはスレッドの番号が入る)
引数で渡されたスレッドIDを設定する。
ucs_timerq_initを使ってtimerqを初期化する

TODO

```
uid = (timer - ucs_async_signal_global_context.timers);
```

ucs_async_signal_sys_timer_create を呼び出す(後述)

作成したタイマーをucs_timerq_addでタイマーキューに追加
(interval をここでセット)


```
sys_interval = ucs_timerq_min_interval(&timer->timerq);
status = ucs_async_signal_sys_timer_set_interval(timer->sys_timer_id,
                                                 sys_interval);
```





#### ucs_async_signal_sys_timer_create

```
ucs_async_signal_sys_timer_create(int uid, pid_t tid, timer_t *sys_timer_id)
```

sigevent構造体の初期化を行う

* ev.sigev_notify: SIGEV_THREAD_IDをセットする。これによりsigev_notify_thread_idで指定したスレッドにsignalを送る
* ev.sigev_signo: タイマーexpire時に送るシグナルの種類
* ev.sigev_value.sival_int: uid シグナルハンドラーに渡すユーザデータ
* ev.sigev_notify_thread_id: シグナルを送るスレッド

タイマーを作成する
timer_create(CLOCK_REALTIME, &ev, &timer);

タイマーの識別IDが格納された、timer変数の値を呼び出し時に渡されたsys_timer_idにコピーする


