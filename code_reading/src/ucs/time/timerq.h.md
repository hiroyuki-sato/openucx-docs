# src/ucs/time/timerq.h

## 構造体

### ucs_timer 構造体

ucs_timer_t構造体は、識別子idを持ち、スケジューリングの間隔を管理するintervalと、絶対的なexpire時刻を持つ構造体です。

絶対的な時間は??
intervalの単位は??


```C
typedef struct ucs_timer {
    ucs_time_t                 expiration;/* Absolute timer expiration time */
    ucs_time_t                 interval;  /* Re-scheduling interval */
    int                        id;
} ucs_timer_t;
```

```C
/**
 * @ingroup UCS_RESOURCE
 *
 * UCS time units.
 * These are not necessarily aligned with metric time units.
 * MUST compare short time values with UCS_SHORT_TIME_CMP to handle wrap-around.
 */
typedef unsigned long   ucs_time_t;
```

### ucs_timer_queue 構造体

```C
typedef struct ucs_timer_queue {
    ucs_spinlock_t             lock;
    ucs_time_t                 min_interval; /* Expiration of next timer */
    ucs_timer_t                *timers;      /* Array of timers */
    unsigned                   num_timers;   /* Number of timers */
} ucs_timer_queue_t;
```

複数のucs_timer_tをキュートして管理する構造体
個数を管理するための、num_timersを持っている
min_interval??
変更をする前にロックを取得するためにlockを持っている



### ucs_timerq_for_each_expired 

利用例

```C
    ucs_timerq_for_each_expired(timer, timerq, current_time, {
        expired_timers[num_timers++] = timer->id;
        if (num_timers >= max_timers) {
            break; /* Keep timers which we don't have room for in the queue */
        }
    })
```
