#  src/ucs/time/timerq.c

- [ ] ucs_timerq_init
- [ ] ucs_timerq_cleanup
- [ ] ucs_timerq_add
- [ ] ucs_timerq_remove

### ucs_timerq_init

```
ucs_status_t ucs_timerq_init(ucs_timer_queue_t *timerq)
```

timerqの初期化を行う

* lock: spinlockの初期化
* timers: NULL
* num_timers: 0
* min_interval: UCS_TIME_INFINITY

```
#define UCS_TIME_INFINITY  ULLONG_MAX
```

### ucs_timerq_cleanup

```
void ucs_timerq_cleanup(ucs_timer_queue_t *timerq)
```

* num_timersが0より多かったら警告(削除忘れがある)
* メモリの解放(timerq->timers);
* ロックの廃棄



### ucs_timerq_add
### ucs_timerq_remove
