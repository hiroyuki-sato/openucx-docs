## ucx_info

### Usage:

```
Usage: ucx_info [options]
At least one of the following options has to be set:
  -v              Show version information
  -d              Show devices and transports
  -b              Show build configuration
  -y              Show type and structures information
  -s              Show system information
  -c              Show UCX configuration
  -a              Show also hidden configuration
  -f              Display fully decorated output

UCP information (-u is required):
  -p              Show UCP context information
  -w              Show UCP worker information
  -e              Show UCP endpoint configuration
  -m              Show UCP memory map configuration (requires memory size as an argument)
  -u <features>   UCP context features to use. String of one or more of:
                    'a' : atomic operations
                    'r' : remote memory access
                    't' : tag matching
                    'w' : wakeup
                  Modifiers to use in combination with above features:
                    'e' : error handling

Other settings:
  -t <name>       Filter devices information using specified transport (requires -d)
  -n <count>      Estimated UCP endpoint count (for ucp_init)
  -D <type>       Set which device types to use when creating UCP context:
                    'all'  : all possible devices (default)
                    'shm'  : shared memory devices only
                    'net'  : network devices only
                    'self' : self transport only
  -h              Show this help message
```

### Show version information(-v)

`./ucx_info -v` outputs ucx version information.
It also output compiled option.

Example.

```
./ucx_info -v
# UCT version=1.7.0 revision c6f10df
# configured with: --enable-gtest \
  --enable-examples \
  --with-valgrind \
  --enable-profiling \
  --enable-frame-pointer \
  --enable-stats \
  --enable-memtrack \
  --enable-fault-injection \
  --enable-debug-data \
  --enable-mt --disable-numa
```

### Show devices and transports (-d)


`./ucx_info -d` show devices and transports information.

```
#
# Memory domain: posix
#     Component: posix
#             allocate: unlimited
#           remote key: 45 bytes
#           rkey_ptr is supported
#
#   Transport: mm
#      Device: posix
#
#      capabilities:
#            bandwidth: 12179.00 MB/sec
#              latency: 80 nsec
#             overhead: 10 nsec
#            put_short: <= 4294967295
#            put_bcopy: unlimited
#            get_bcopy: unlimited
#             am_short: <= 92
#             am_bcopy: <= 8K
#               domain: cpu
#           atomic_add: 32, 64 bit
#           atomic_and: 32, 64 bit
#            atomic_or: 32, 64 bit
#           atomic_xor: 32, 64 bit
#          atomic_fadd: 32, 64 bit
#          atomic_fand: 32, 64 bit
#           atomic_for: 32, 64 bit
#          atomic_fxor: 32, 64 bit
#          atomic_swap: 32, 64 bit
#         atomic_cswap: 32, 64 bit
#           connection: to iface
#             priority: 0
#       device address: 8 bytes
#        iface address: 16 bytes
#       error handling: none
#
#
# Memory domain: sysv
#     Component: sysv
#             allocate: unlimited
#           remote key: 40 bytes
#           rkey_ptr is supported
#
#   Transport: mm
#      Device: sysv
#
#      capabilities:
#            bandwidth: 12179.00 MB/sec
#              latency: 80 nsec
#             overhead: 10 nsec
#            put_short: <= 4294967295
#            put_bcopy: unlimited
#            get_bcopy: unlimited
#             am_short: <= 92
#             am_bcopy: <= 8K
#               domain: cpu
#           atomic_add: 32, 64 bit
#           atomic_and: 32, 64 bit
#            atomic_or: 32, 64 bit
#           atomic_xor: 32, 64 bit
#          atomic_fadd: 32, 64 bit
#          atomic_fand: 32, 64 bit
#           atomic_for: 32, 64 bit
#          atomic_fxor: 32, 64 bit
#          atomic_swap: 32, 64 bit
#         atomic_cswap: 32, 64 bit
#           connection: to iface
#             priority: 0
#       device address: 8 bytes
#        iface address: 16 bytes
#       error handling: none
#
#
# Memory domain: self
#     Component: self
#             register: unlimited, cost: 0 nsec
#           remote key: 16 bytes
#
#   Transport: self
#      Device: self
#
#      capabilities:
#            bandwidth: 6911.00 MB/sec
#              latency: 0 nsec
#             overhead: 10 nsec
#            put_short: <= 4294967295
#            put_bcopy: unlimited
#            get_bcopy: unlimited
#             am_short: <= 8K
#             am_bcopy: <= 8K
#               domain: cpu
#           atomic_add: 32, 64 bit
#           atomic_and: 32, 64 bit
#            atomic_or: 32, 64 bit
#           atomic_xor: 32, 64 bit
#          atomic_fadd: 32, 64 bit
#          atomic_fand: 32, 64 bit
#           atomic_for: 32, 64 bit
#          atomic_fxor: 32, 64 bit
#          atomic_swap: 32, 64 bit
#         atomic_cswap: 32, 64 bit
#           connection: to iface
#             priority: 0
#       device address: 0 bytes
#        iface address: 8 bytes
#       error handling: none
#
#
# Memory domain: tcp
#     Component: tcp
#
#   Transport: tcp
#      Device: vboxnet3
#
#      capabilities:
#            bandwidth: 1.13 MB/sec
#              latency: 62800 nsec
#             overhead: 50000 nsec
#             am_short: <= 8K
#             am_bcopy: <= 8K
#           connection: to iface
#             priority: 1
#       device address: 4 bytes
#        iface address: 2 bytes
#       error handling: none
#
#   Transport: tcp
#      Device: brbond0
#
#      capabilities:
#            bandwidth: 11.32 MB/sec
#              latency: 10960 nsec
#             overhead: 50000 nsec
#             am_short: <= 8K
#             am_bcopy: <= 8K
#           connection: to iface
#             priority: 1
#       device address: 4 bytes
#        iface address: 2 bytes
#       error handling: none
#
#   Transport: tcp
#      Device: brib0.8001
#
#      capabilities:
#            bandwidth: 11.32 MB/sec
#              latency: 10960 nsec
#             overhead: 50000 nsec
#             am_short: <= 8K
#             am_bcopy: <= 8K
#           connection: to iface
#             priority: 1
#       device address: 4 bytes
#        iface address: 2 bytes
#       error handling: none
#
#
# Memory domain: sockcm
#     Component: sockcm
#           supports client-server connection establishment via sockaddr
#   < no supported devices found >
#
# Memory domain: cma
#     Component: cma
#             register: unlimited, cost: 9 nsec
#
#   Transport: cma
#      Device: cma
#
#      capabilities:
#            bandwidth: 11145.00 MB/sec
#              latency: 80 nsec
#             overhead: 400 nsec
#            put_zcopy: unlimited, up to 16 iov
#  put_opt_zcopy_align: <= 1
#        put_align_mtu: <= 1
#            get_zcopy: unlimited, up to 16 iov
#  get_opt_zcopy_align: <= 1
#        get_align_mtu: <= 1
#           connection: to iface
#             priority: 0
#       device address: 8 bytes
#        iface address: 4 bytes
#       error handling: none
#
```


### Show build configuration (-b)

`ucx_info -b` show build configuration.

Example

```
./ucx_info -b
#define UCX_CONFIG_H
#define ENABLE_ASSERT             1
#define ENABLE_DEBUG_DATA         1
#define ENABLE_FAULT_INJECTION    1
#define ENABLE_MEMTRACK           1
#define ENABLE_MT                 1
#define ENABLE_PARAMS_CHECK       1
#define ENABLE_STATS              1
#define ENABLE_SYMBOL_OVERRIDE    1
#define HAVE_ATTRIBUTE_NOOPTIMIZE 1
#define HAVE_DECL_ASPRINTF        1
#define HAVE_DECL_BASENAME        1
#define HAVE_DECL_CPU_ISSET       1
#define HAVE_DECL_CPU_ZERO        1
#define HAVE_DECL_ETHTOOL_CMD_SPEED 1
#define HAVE_DECL_FMEMOPEN        1
#define HAVE_DECL_F_SETOWN_EX     1
#define HAVE_DECL_IBV_CREATE_SRQ  0
#define HAVE_DECL_IBV_EVENT_TYPE_STR 0
#define HAVE_DECL_IBV_GET_ASYNC_EVENT 0
#define HAVE_DECL_IBV_GET_DEVICE_NAME 0
#define HAVE_DECL_IBV_QUERY_GID   0
#define HAVE_DECL_IBV_WC_STATUS_STR 0
#define HAVE_DECL_MADV_FREE       0
#define HAVE_DECL_MADV_REMOVE     1
#define HAVE_DECL_POSIX_MADV_DONTNEED 1
#define HAVE_DECL_PR_SET_PTRACER  1
#define HAVE_DECL_SPEED_UNKNOWN   1
#define HAVE_DECL_STRDUPA         1
#define HAVE_DECL_STRERROR_R      1
#define HAVE_DECL_SYS_BRK         1
#define HAVE_DECL_SYS_IPC         0
#define HAVE_DECL_SYS_MADVISE     1
#define HAVE_DECL_SYS_MMAP        1
#define HAVE_DECL_SYS_MREMAP      1
#define HAVE_DECL_SYS_MUNMAP      1
#define HAVE_DECL_SYS_SHMAT       1
#define HAVE_DECL_SYS_SHMDT       1
#define HAVE_DECL___PPC_GET_TIMEBASE_FREQ 0
#define HAVE_DLFCN_H              1
#define HAVE_HW_TIMER             1
#define HAVE_INTTYPES_H           1
#define HAVE_LIBRT                1
#define HAVE_MALLOC_GET_STATE     1
#define HAVE_MALLOC_HOOK          1
#define HAVE_MALLOC_SET_STATE     1
#define HAVE_MEMORY_H             1
#define HAVE_PROFILING            1
#define HAVE_STDINT_H             1
#define HAVE_STDLIB_H             1
#define HAVE_STRERROR_R           1
#define HAVE_STRINGS_H            1
#define HAVE_STRING_H             1
#define HAVE_STRUCT_DL_PHDR_INFO  1
#define HAVE_SYS_STAT_H           1
#define HAVE_SYS_TYPES_H          1
#define HAVE_SYS_UIO_H            1
#define HAVE_UCM_PTMALLOC286      1
#define HAVE_UNISTD_H             1
#define HAVE___CLEAR_CACHE        1
#define HAVE___CURBRK             1
#define LT_OBJDIR                 ".libs/"
#define PACKAGE                   "ucx"
#define PACKAGE_BUGREPORT         ""
#define PACKAGE_NAME              "ucx"
#define PACKAGE_STRING            "ucx 1.7"
#define PACKAGE_TARNAME           "ucx"
#define PACKAGE_URL               ""
#define PACKAGE_VERSION           "1.7"
#define STDC_HEADERS              1
#define STRERROR_R_CHAR_P         1
#define UCM_BISTRO_HOOKS          1
#define UCS_MAX_LOG_LEVEL         UCS_LOG_LEVEL_TRACE_POLL
#define UCT_UD_EP_DEBUG_HOOKS     1
#define UCX_CONFIGURE_FLAGS       "--enable-gtest --enable-examples --with-valgrind --enable-profiling --enable-frame-pointer --enable-stats --enable-memtrack --enable-fault-injection --enable-debug-data --enable-mt --disable-numa"
#define UCX_MODULE_SUBDIR         "ucx"
#define VERSION                   "1.7"
#define restrict                  __restrict
#define test_MODULES              ":module"
#define ucm_MODULES               ""
#define uct_MODULES               ":cma"
#define uct_cuda_MODULES          ""
#define uct_ib_MODULES            ""
#define uct_rocm_MODULES          ""
#define ucx_perftest_MODULES      ""
```

### Show type and structures information (-y)

```
./ucx_info -y
UCS:
    sizeof(ucs_mpool_t) = ................. 16
    sizeof(ucs_mpool_chunk_t) = ........... 24
    sizeof(ucs_mpool_elem_t) = ............ 8
    sizeof(ucs_async_context_t) = ......... 80
    sizeof(ucs_async_handler_t) = ......... 48
    sizeof(ucs_async_ops_t) = ............. 104
    sizeof(ucs_async_pipe_t) = ............ 8
    sizeof(ucs_async_signal_context_t) = .. 24
    sizeof(ucs_async_thread_context_t) = .. 40
    sizeof(ucs_class_t) = ................. 40
    sizeof(ucs_config_field_t) = .......... 80
    sizeof(ucs_config_parser_t) = ......... 48
    sizeof(ucs_frag_list_t) = ............. 64
    sizeof(ucs_frag_list_elem_t) = ........ 32
    sizeof(ucs_frag_list_head_t) = ........ 24
    sizeof(ucs_ib_port_spec_t) = .......... 16
    sizeof(ucs_list_link_t) = ............. 16
    sizeof(ucs_memtrack_entry_t) = ........ 24
    sizeof(ucs_mpmc_queue_t) = ............ 24
    sizeof(ucs_callbackq_t) = ............. 264
    sizeof(ucs_callbackq_elem_t) = ........ 24
    sizeof(ucs_ptr_array_t) = ............. 88
    sizeof(ucs_queue_elem_t) = ............ 8
    sizeof(ucs_queue_head_t) = ............ 16
    sizeof(ucs_spinlock_t) = .............. 16
    sizeof(ucs_timer_t) = ................. 24
    sizeof(ucs_timer_queue_t) = ........... 32
    sizeof(ucs_twheel_t) = ................ 40
    sizeof(ucs_wtimer_t) = ................ 32
    sizeof(ucs_arbiter_t) = ............... 16
    sizeof(ucs_arbiter_group_t) = ......... 8
    sizeof(ucs_arbiter_elem_t) = .......... 32
    sizeof(ucs_pgtable_t) = ............... 48
    sizeof(ucs_pgt_entry_t) = ............. 8
    sizeof(ucs_pgt_dir_t) = ............... 136
    sizeof(ucs_pgt_region_t) = ............ 16
    sizeof(ucs_rcache_t) = ................ 208
    sizeof(ucs_rcache_region_t) = ......... 48

UCT:
    sizeof(uct_am_handler_t) = ............ 24
    sizeof(uct_base_iface_t) = ............ 1240
    sizeof(uct_completion_t) = ............ 16
    sizeof(uct_ep_t) = .................... 8
    sizeof(uct_mem_h) = ................... 8
    sizeof(uct_rkey_t) = .................. 8
    sizeof(uct_iface_t) = ................. 368
    sizeof(uct_iface_attr_t) = ............ 384
    sizeof(uct_iface_config_t) = .......... 24
    sizeof(uct_iface_mpool_config_t) = .... 8
    sizeof(uct_md_config_t) = ............. 1
    sizeof(uct_iface_ops_t) = ............. 368
    sizeof(uct_md_t) = .................... 16
    sizeof(uct_md_attr_t) = ............... 216
    sizeof(uct_md_ops_t) = ................ 88
    sizeof(uct_tl_resource_desc_t) = ...... 48
    sizeof(uct_rkey_bundle_t) = ........... 24
    sizeof(uct_tcp_ep_t) = ................ 128
    sizeof(uct_self_ep_t) = ............... 16


UCP:
    sizeof(ucp_context_t) = ............... 464
    sizeof(ucp_worker_t) = ................ 800
    sizeof(ucp_ep_t) = .................... 112
    sizeof(ucp_ep_ext_gen_t) = ............ 64
    sizeof(ucp_ep_ext_proto_t) = .......... 48
    sizeof(ucp_ep_match_entry_t) = ........ 40
    sizeof(ucp_ep_config_key_t) = ......... 80
    sizeof(ucp_ep_config_t) = ............. 1368
    sizeof(ucp_request_t) = ............... 232
    sizeof(ucp_recv_desc_t) = ............. 48
    sizeof(ucp_tag_recv_info_t) = ......... 16
    sizeof(ucp_mem_t) = ................... 40
    sizeof(ucp_rkey_t) = .................. 64
    sizeof(ucp_wireup_msg_t) = ............ 29
```

### Show system information (-s)

```
./ucx_info -s
# Timer frequency: 2600.000 MHz
# CPU model: SandyBridge
# Memcpy bandwidth:
#           4096 bytes: 30086.534 MB/s
#           8192 bytes: 35596.930 MB/s
#          16384 bytes: 25771.936 MB/s
#          32768 bytes: 18904.779 MB/s
#          65536 bytes: 17660.946 MB/s
#         131072 bytes: 17006.890 MB/s
#         262144 bytes: 15134.532 MB/s
#         524288 bytes: 13247.209 MB/s
#        1048576 bytes: 12340.522 MB/s
#        2097152 bytes: 7973.853 MB/s
#        4194304 bytes: 5494.552 MB/s
#        8388608 bytes: 4965.086 MB/s
#       16777216 bytes: 5150.871 MB/s
#       33554432 bytes: 5134.933 MB/s
#       67108864 bytes: 5110.253 MB/s
#      134217728 bytes: 5101.929 MB/s
#      268435456 bytes: 5128.126 MB/s
```

### Show UCX configuration (-c)

```
./ucx_info -c
UCX_LOG_LEVEL=WARN
UCX_LOG_FILE=
UCX_LOG_BUFFER=1K
UCX_LOG_DATA_SIZE=0
UCX_LOG_PRINT_ENABLE=n
UCX_MPOOL_FIFO=n
UCX_HANDLE_ERRORS=bt,freeze
UCX_ERROR_SIGNALS=ILL,SEGV,BUS,FPE
UCX_ERROR_MAIL_TO=
UCX_ERROR_MAIL_FOOTER=
UCX_GDB_COMMAND=gdb -quiet
UCX_DEBUG_SIGNO=HUP
UCX_LOG_LEVEL_TRIGGER=FATAL
UCX_WARN_UNUSED_ENV_VARS=y
UCX_ASYNC_MAX_EVENTS=1024
UCX_ASYNC_SIGNO=ALRM
UCX_STATS_DEST=
UCX_STATS_TRIGGER=exit
UCX_STATS_FILTER=*
UCX_STATS_FORMAT=full
UCX_MEMTRACK_DEST=
UCX_PROFILE_MODE=
UCX_PROFILE_FILE=
UCX_PROFILE_LOG_SIZE=4M
UCX_RCACHE_CHECK_PFN=n
UCX_MODULE_DIR=/usr/lib/ucx
UCX_MODULE_LOG_LEVEL=TRACE
UCX_MEM_LOG_LEVEL=WARN
UCX_MEM_ALLOC_ALIGN=16
UCX_MEM_EVENTS=y
UCX_MEM_MMAP_HOOK_MODE=bistro
UCX_MEM_MALLOC_HOOKS=y
UCX_MEM_MALLOC_RELOC=y
UCX_MEM_CUDA_RELOC=y
UCX_MEM_DYNAMIC_MMAP_THRESH=y
UCX_MM_ALLOC=md
UCX_MM_FAILURE=ERROR
UCX_MM_BW=12179MBps
UCX_MM_FIFO_SIZE=64
UCX_MM_SEG_SIZE=8K
UCX_MM_FIFO_RELEASE_FACTOR=0.500
UCX_MM_RX_MAX_BUFS=-1
UCX_MM_RX_BUFS_GROW=512
UCX_MM_FIFO_HUGETLB=n
UCX_MM_FIFO_ELEM_SIZE=128
UCX_POSIX_HUGETLB_MODE=y
UCX_POSIX_USE_SHM_OPEN=try
UCX_POSIX_DIR=/tmp
UCX_POSIX_USE_PROC_LINK=y
UCX_SYSV_HUGETLB_MODE=y
UCX_SELF_ALLOC=huge,thp,md,mmap,heap
UCX_SELF_FAILURE=ERROR
UCX_SELF_SEG_SIZE=8K
UCX_TCP_ALLOC=huge,thp,md,mmap,heap
UCX_TCP_FAILURE=ERROR
UCX_TCP_SEG_SIZE=8K
UCX_TCP_PREFER_DEFAULT=y
UCX_TCP_MAX_POLL=16
UCX_TCP_NODELAY=y
UCX_TCP_SNDBUF=auto
UCX_TCP_RCVBUF=auto
UCX_TCP_TX_MAX_BUFS=-1
UCX_TCP_TX_BUFS_GROW=8
UCX_TCP_RX_MAX_BUFS=-1
UCX_TCP_RX_BUFS_GROW=8
UCX_SOCKCM_BACKLOG=1024
UCX_NET_DEVICES=all
UCX_SHM_DEVICES=all
UCX_ACC_DEVICES=all
UCX_SELF_DEVICES=all
UCX_TLS=all
UCX_ALLOC_PRIO=md:sysv,md:posix,huge,thp,md:*,mmap,heap
UCX_SOCKADDR_TLS_PRIORITY=rdmacm,*
UCX_SOCKADDR_AUX_TLS=ud,ud_x
UCX_WARN_INVALID_CONFIG=y
UCX_BCOPY_THRESH=0
UCX_RNDV_THRESH=auto
UCX_RNDV_SEND_NBR_THRESH=256K
UCX_RNDV_THRESH_FALLBACK=inf
UCX_RNDV_PERF_DIFF=1.000
UCX_MAX_EAGER_RAILS=1
UCX_MAX_RNDV_RAILS=2
UCX_RNDV_SCHEME=auto
UCX_ZCOPY_THRESH=auto
UCX_BCOPY_BW=5800M
UCX_ATOMIC_MODE=guess
UCX_MAX_WORKER_NAME=32
UCX_USE_MT_MUTEX=n
UCX_ADAPTIVE_PROGRESS=y
UCX_SEG_SIZE=8K
UCX_TM_THRESH=1K
UCX_TM_MAX_BB_SIZE=1K
UCX_TM_FORCE_THRESH=8K
UCX_NUM_EPS=auto
UCX_RNDV_FRAG_SIZE=256K
UCX_MEMTYPE_CACHE=y
UCX_FLUSH_WORKER_EPS=y
UCX_UNIFIED_MODE=n
UCX_CMA_ALLOC=huge,thp,mmap,heap
UCX_CMA_FAILURE=ERROR
UCX_CMA_BW=11145MBps
```

### Show also hidden configuration (-a)
### Display fully decorated output (-f)


```
./ucx_info -f

#
# UCS global configuration
#

#
# UCS logging level. Messages with a level higher or equal to the selected will be printed.
# Possible values are: fatal, error, warn, info, debug, trace, data, func, poll.
#
# syntax:    [FATAL|ERROR|WARN|INFO|DEBUG|TRACE|REQ|DATA|ASYNC|FUNC|POLL]
#
UCX_LOG_LEVEL=WARN

#
# If not empty, UCS will print log messages to the specified file instead of stdout.
# The following substitutions are performed on this string:
#   %p - Replaced with process ID
#   %h - Replaced with host name
#
#
# syntax:    string
#
UCX_LOG_FILE=

#
# Buffer size for a single log message.
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_LOG_BUFFER=1K

#
# How much packet payload to print, at most, in data mode.
#
# syntax:    unsigned long
#
UCX_LOG_DATA_SIZE=0

#
# Enable output of ucs_print(). This option is intended for use by the library developers.
#
#
# syntax:    <y|n>
#
UCX_LOG_PRINT_ENABLE=n

#
# Enable FIFO behavior for memory pool, instead of LIFO. Useful for
# debugging because object pointers are not recycled.
#
# syntax:    <y|n>
#
UCX_MPOOL_FIFO=n

#
# Error handling mode. A combination of: 'bt' (print backtrace),
# 'freeze' (freeze and wait for a debugger), 'debug' (attach debugger)
#
# syntax:    comma-separated list of: [bt|freeze|debug]
#
UCX_HANDLE_ERRORS=bt,freeze

#
# Signals which are considered an error indication and trigger error handling.
#
# syntax:    comma-separated list of: system signal (number or SIGxxx)
#
UCX_ERROR_SIGNALS=ILL,SEGV,BUS,FPE

#
# If non-empty, send mail notification for fatal errors.
#
# syntax:    string
#
UCX_ERROR_MAIL_TO=

#
# Footer for error report email
#
# syntax:    string
#
UCX_ERROR_MAIL_FOOTER=

#
# If non-empty, attaches a gdb to the process in case of error, using the provided command.
#
# syntax:    string
#
UCX_GDB_COMMAND=gdb -quiet

#
# Signal number which causes UCS to enter debug mode. Set to 0 to disable.
#
# syntax:    system signal (number or SIGxxx)
#
UCX_DEBUG_SIGNO=HUP

#
# Log level to trigger error handling.
#
# syntax:    [FATAL|ERROR|WARN|INFO|DEBUG|TRACE|REQ|DATA|ASYNC|FUNC|POLL]
#
UCX_LOG_LEVEL_TRIGGER=FATAL

#
# Issue warning about UCX_ environment variables which were not used by the
# configuration parser.
#
# syntax:    <y|n>
#
UCX_WARN_UNUSED_ENV_VARS=y

#
# Maximal number of events which can be handled from one context
#
# syntax:    unsigned integer
#
UCX_ASYNC_MAX_EVENTS=1024

#
# Signal number used for async signaling.
#
# syntax:    system signal (number or SIGxxx)
#
UCX_ASYNC_SIGNO=ALRM

#
# Destination to send statistics to. If the value is empty, statistics are
# not reported. Possible values are:
#   udp:<host>[:<port>]   - send over UDP to the given host:port.
#   stdout                - print to standard output.
#   stderr                - print to standard error.
#   file:<filename>[:bin] - save to a file (%h: host, %p: pid, %c: cpu, %t: time, %u: user, %e: exe)
#
# syntax:    string
#
UCX_STATS_DEST=

#
# Trigger to dump statistics:
#   exit              - dump just before program exits.
#   signal:<signo>    - dump when process is signaled.
#   timer:<interval>  - dump in specified intervals (in seconds).
#
# syntax:    string
#
UCX_STATS_TRIGGER=exit

#
# Used for filter counters summary.
# Comma-separated list of glob patterns specifying counters.
# Statistics summary will contain only the matching counters.
# The order is not meaningful.
# Each expression in the list may contain any of the following wildcard:
#   *     - matches any number of any characters including none.
#   ?     - matches any single character.
#   [abc] - matches one character given in the bracket.
#   [a-z] - matches one character from the range given in the bracket.
#
# syntax:    comma-separated list of: string
#
UCX_STATS_FILTER=*

#
# Statistics format parameter:
#   full    - each counter will be displayed in a separate line
#   agg     - like full but there will also be an aggregation between similar counters
#   summary - all counters will be printed in the same line.
#
# syntax:    [full|agg|summary]
#
UCX_STATS_FORMAT=full

#
# Destination to output memory tracking report to. If the value is empty,
# results are not reported. Possible values are:
#   file:<filename>   - save to a file (%h: host, %p: pid, %c: cpu, %t: time, %u: user, %e: exe)
#   stdout            - print to standard output.
#   stderr            - print to standard error.
#
#
# syntax:    string
#
UCX_MEMTRACK_DEST=

#
# Profile collection modes. If none is specified, profiling is disabled.
#  - log   - Record all timestamps.
#  - accum - Accumulate measurements per location.
#
#
# syntax:    comma-separated list of: [accum|log]
#
UCX_PROFILE_MODE=

#
# File name to dump profiling data to.
# Substitutions: %h: host, %p: pid, %c: cpu, %t: time, %u: user, %e: exe.
#
#
# syntax:    string
#
UCX_PROFILE_FILE=

#
# Maximal size of profiling log. New records will replace old records.
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_PROFILE_LOG_SIZE=4M

#
# Registration cache to check that the physical page frame number of a found
# memory region was not changed since the time the region was registered.
#
#
# syntax:    <y|n>
#
UCX_RCACHE_CHECK_PFN=n

#
# Directory to search for loadable modules
#
# syntax:    string
#
UCX_MODULE_DIR=/usr/lib/ucx

#
# Logging level for module loader
#
#
# syntax:    [FATAL|ERROR|WARN|INFO|DEBUG|TRACE|REQ|DATA|ASYNC|FUNC|POLL]
#
UCX_MODULE_LOG_LEVEL=TRACE



#
# UCM configuration
#

#
# Logging level for memory events
#
# syntax:    [FATAL|ERROR|WARN|INFO|DEBUG|TRACE]
#
UCX_MEM_LOG_LEVEL=WARN

#
# Minimal alignment of allocated blocks
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_MEM_ALLOC_ALIGN=16

#
# Enable memory events
#
# syntax:    <y|n>
#
UCX_MEM_EVENTS=y

#
# MMAP hook mode
#  none   - don't set mmap hooks.
#  reloc  - use ELF relocation table to set hooks.
#  bistro - use binary instrumentation to set hooks.
#
#
# syntax:    [none|reloc|bistro]
#
UCX_MEM_MMAP_HOOK_MODE=bistro

#
# Enable using glibc malloc hooks
#
# syntax:    <y|n>
#
UCX_MEM_MALLOC_HOOKS=y

#
# Enable installing malloc symbols in the relocation table.
# This is unsafe and off by default, because sometimes glibc
# calls malloc/free without going through the relocation table,
# which would use the original implementation and not ours.
#
# syntax:    <y|n>
#
UCX_MEM_MALLOC_RELOC=y

#
# Enable installing CUDA symbols in the relocation table
#
# syntax:    <y|n>
#
UCX_MEM_CUDA_RELOC=y

#
# Enable dynamic mmap threshold: for every released block, the
# mmap threshold is adjusted upward to the size of the size of
# the block, and trim threshold is adjust to twice the size of
# the dynamic mmap threshold.
# Note: dynamic mmap threshold is disabled when running on valgrind.
#
# syntax:    <y|n>
#
UCX_MEM_DYNAMIC_MMAP_THRESH=y



#
# mm transport configuration
#

#
# Priority of methods to allocate intermediate buffers for communication
#
# syntax:    comma-separated list of: [thp|md|heap|mmap|huge]
# inherits:  UCX_ALLOC, UCX_ALLOC
#
UCX_MM_ALLOC=md

#
# Level of network failure reporting
#
# syntax:    [FATAL|ERROR|WARN|INFO|DEBUG|TRACE|REQ|DATA|ASYNC|FUNC|POLL]
# inherits:  UCX_FAILURE, UCX_FAILURE
#
UCX_MM_FAILURE=ERROR

#
# Effective memory bandwidth
#
# syntax:    bandwidth value: <number>[T|G|M|K]B|b[[p|/]s]
# inherits:  UCX_BW
#
UCX_MM_BW=12179MBps

#
# Size of the receive FIFO in the memory-map UCTs.
#
# syntax:    unsigned integer
#
UCX_MM_FIFO_SIZE=64

#
# Size of send/receive buffers for copy-out sends.
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_MM_SEG_SIZE=8K

#
# Frequency of resource releasing on the receiver's side in the MM UCT.
# This value refers to the percentage of the FIFO size. (must be >= 0 and < 1).
#
# syntax:    floating point number
#
UCX_MM_FIFO_RELEASE_FACTOR=0.500

#
# Maximal number of receive buffers for the interface. -1 is infinite.
#
# syntax:    integer
#
UCX_MM_RX_MAX_BUFS=-1

#
# How much buffers are added every time the receive memory pool grows.
# 0 means the value is chosen by the transport.
#
# syntax:    unsigned integer
#
UCX_MM_RX_BUFS_GROW=512

#
# Enable using huge pages for internal shared memory buffers.Possible values are:
#  y   - Allocate memory using huge pages only.
#  n   - Allocate memory using regular pages only.
#  try - Try to allocate memory using huge pages and if it fails, allocate regular pages.
#
# syntax:    <yes|no|try>
#
UCX_MM_FIFO_HUGETLB=n

#
# Size of the FIFO element size (data + header) in the MM UCTs.
#
# syntax:    unsigned integer
#
UCX_MM_FIFO_ELEM_SIZE=128



#
# posix memory domain configuration
#

#
# Enable using huge pages for internal buffers. Possible values are:
#  y   - Allocate memory using huge pages only.
#  n   - Allocate memory using regular pages only.
#  try - Try to allocate memory using huge pages and if it fails, allocate regular pages.
#
#
# syntax:    <yes|no|try>
# inherits:  UCX_MM_HUGETLB_MODE
#
UCX_POSIX_HUGETLB_MODE=y

#
# Use shm_open() for opening a file for memory mapping. Possible values are:
#  y   - Use only shm_open() to open a backing file.
#  n   - Use only open() to open a backing file.
#  try - Try to use shm_open() and if it fails, use open().
# If shm_open() is used, the path to the file defaults to /dev/shm.
# If open() is used, the path to the file is specified in the parameter bellow (DIR).
#
# syntax:    <yes|no|try>
#
UCX_POSIX_USE_SHM_OPEN=try

#
# The path to the backing file in case open() is used.
#
# syntax:    string
#
UCX_POSIX_DIR=/tmp

#
# Use /proc/<pid>/fd/<fd> to share posix file.
#  y   - Use /proc/<pid>/fd/<fd> to share posix file.
#  n   - Use original file path to share posix file.
#
#
# syntax:    <y|n>
#
UCX_POSIX_USE_PROC_LINK=y



#
# sysv memory domain configuration
#

#
# Enable using huge pages for internal buffers. Possible values are:
#  y   - Allocate memory using huge pages only.
#  n   - Allocate memory using regular pages only.
#  try - Try to allocate memory using huge pages and if it fails, allocate regular pages.
#
#
# syntax:    <yes|no|try>
# inherits:  UCX_MM_HUGETLB_MODE
#
UCX_SYSV_HUGETLB_MODE=y



#
# self transport configuration
#

#
# Priority of methods to allocate intermediate buffers for communication
#
# syntax:    comma-separated list of: [thp|md|heap|mmap|huge]
# inherits:  UCX_ALLOC
#
UCX_SELF_ALLOC=huge,thp,md,mmap,heap

#
# Level of network failure reporting
#
# syntax:    [FATAL|ERROR|WARN|INFO|DEBUG|TRACE|REQ|DATA|ASYNC|FUNC|POLL]
# inherits:  UCX_FAILURE
#
UCX_SELF_FAILURE=ERROR

#
# Size of copy-out buffer
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_SELF_SEG_SIZE=8K



#
# self memory domain configuration
#



#
# tcp transport configuration
#

#
# Priority of methods to allocate intermediate buffers for communication
#
# syntax:    comma-separated list of: [thp|md|heap|mmap|huge]
# inherits:  UCX_ALLOC
#
UCX_TCP_ALLOC=huge,thp,md,mmap,heap

#
# Level of network failure reporting
#
# syntax:    [FATAL|ERROR|WARN|INFO|DEBUG|TRACE|REQ|DATA|ASYNC|FUNC|POLL]
# inherits:  UCX_FAILURE
#
UCX_TCP_FAILURE=ERROR

#
# Size of copy-out buffer
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_TCP_SEG_SIZE=8K

#
# Give higher priority to the default network interface on the host
#
# syntax:    <y|n>
#
UCX_TCP_PREFER_DEFAULT=y

#
# Number of times to poll on a ready socket. 0 - no polling, -1 - until drained
#
# syntax:    unsigned integer
#
UCX_TCP_MAX_POLL=16

#
# Set TCP_NODELAY socket option to disable Nagle algorithm. Setting this
# option usually provides better performance
#
# syntax:    <y|n>
#
UCX_TCP_NODELAY=y

#
# Socket send buffer size
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_TCP_SNDBUF=auto

#
# Socket receive buffer size
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_TCP_RCVBUF=auto

#
# Maximal number of send buffers for the interface. -1 is infinite.
#
# syntax:    integer
#
UCX_TCP_TX_MAX_BUFS=-1

#
# How much buffers are added every time the send memory pool grows.
# 0 means the value is chosen by the transport.
#
# syntax:    unsigned integer
#
UCX_TCP_TX_BUFS_GROW=8

#
# Maximal number of receive buffers for the interface. -1 is infinite.
#
# syntax:    integer
#
UCX_TCP_RX_MAX_BUFS=-1

#
# How much buffers are added every time the receive memory pool grows.
# 0 means the value is chosen by the transport.
#
# syntax:    unsigned integer
#
UCX_TCP_RX_BUFS_GROW=8



#
# tcp memory domain configuration
#



#
# sockcm transport configuration
#

#
# Maximum number of pending connections for a listening socket.
#
# syntax:    unsigned integer
#
UCX_SOCKCM_BACKLOG=1024



#
# sockcm memory domain configuration
#



#
# UCP context configuration
#

#
# Specifies which network device(s) to use. The order is not meaningful.
# "all" would use all available devices.
#
# syntax:    comma-separated list of: string
#
UCX_NET_DEVICES=all

#
# Specifies which intra-node device(s) to use. The order is not meaningful.
# "all" would use all available devices.
#
# syntax:    comma-separated list of: string
#
UCX_SHM_DEVICES=all

#
# Specifies which accelerator device(s) to use. The order is not meaningful.
# "all" would use all available devices.
#
# syntax:    comma-separated list of: string
#
UCX_ACC_DEVICES=all

#
# Specifies which loop-back device(s) to use. The order is not meaningful.
# "all" would use all available devices.
#
# syntax:    comma-separated list of: string
#
UCX_SELF_DEVICES=all

#
# Comma-separated list of transports to use. The order is not meaningful.
#  - all    : use all the available transports.
#  - sm/shm : all shared memory transports.
#  - mm     : shared memory transports - only memory mappers.
#  - ugni   : ugni_rdma and ugni_udt.
#  - ib     : all infiniband transports.
#  - rc     : rc verbs (uses ud for bootstrap).
#  - rc_x   : rc with accelerated verbs (uses ud_x for bootstrap).
#  - ud     : ud verbs.
#  - ud_x   : ud with accelerated verbs.
#  - dc_x   : dc with accelerated verbs.
#  Using a \ prefix before a transport name treats it as an explicit transport name
#  and disables aliasing.
#
#
# syntax:    comma-separated list of: string
#
UCX_TLS=all

#
# Priority of memory allocation methods. Each item in the list can be either
# an allocation method (huge, thp, mmap, libc) or md:<NAME> which means to use the
# specified memory domain for allocation. NAME can be either a MD component
# name, or a wildcard - '*' - which expands to all MD components.
#
# syntax:    comma-separated list of: string
#
UCX_ALLOC_PRIO=md:sysv,md:posix,huge,thp,md:*,mmap,heap

#
# Priority of sockaddr transports for client/server connection establishment.
# The '*' wildcard expands to all the available sockaddr transports.
#
# syntax:    comma-separated list of: string
#
UCX_SOCKADDR_TLS_PRIORITY=rdmacm,*

#
# Transports to use for exchanging additional address information while
# establishing client/server connection.
#
# syntax:    comma-separated list of: string
#
UCX_SOCKADDR_AUX_TLS=ud,ud_x

#
# Issue a warning in case of invalid device and/or transport configuration.
#
# syntax:    <y|n>
#
UCX_WARN_INVALID_CONFIG=y

#
# Threshold for switching from short to bcopy protocol
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_BCOPY_THRESH=0

#
# Threshold for switching from eager to rendezvous protocol
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_RNDV_THRESH=auto

#
# Threshold for switching from eager to rendezvous protocol in ucp_tag_send_nbr().
# Relevant only if UCX_RNDV_THRESH is set to "auto".
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_RNDV_SEND_NBR_THRESH=256K

#
# Message size to start using the rendezvous protocol in case the calculated threshold is zero or negative
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_RNDV_THRESH_FALLBACK=inf

#
# The percentage allowed for performance difference between rendezvous and the eager_zcopy protocol
#
# syntax:    floating point number
#
UCX_RNDV_PERF_DIFF=1.000

#
# Maximal number of devices on which an eager operation may be executed in parallel
#
# syntax:    unsigned integer
#
UCX_MAX_EAGER_RAILS=1

#
# Maximal number of devices on which a rendezvous operation may be executed in parallel
#
# syntax:    unsigned integer
#
UCX_MAX_RNDV_RAILS=2

#
# Communication scheme in RNDV protocol.
#  get_zcopy - use get_zcopy scheme in RNDV protocol.
#  put_zcopy - use put_zcopy scheme in RNDV protocol.
#  auto      - runtime automatically chooses optimal scheme to use.
#
#
# syntax:    [get_zcopy|put_zcopy|auto]
#
UCX_RNDV_SCHEME=auto

#
# Threshold for switching from buffer copy to zero copy protocol
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_ZCOPY_THRESH=auto

#
# Estimation of buffer copy bandwidth
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_BCOPY_BW=5800M

#
# Atomic operations synchronization mode.
#  cpu    - atomic operations are consistent with respect to the CPU.
#  device - atomic operations are performed on one of the transport devices,
#           and there is guarantee of consistency with respect to the CPU. guess  - atomic operations mode is configured based on underlying
#           transport capabilities. If one of active transports supports
#           the DEVICE atomic mode, the DEVICE mode is selected.
#           Otherwise the CPU mode is selected.
#
# syntax:    [cpu|device|guess]
#
UCX_ATOMIC_MODE=guess

#
# Maximal length of worker name. Sent to remote peer as part of worker address.
#
# syntax:    unsigned integer
#
UCX_MAX_WORKER_NAME=32

#
# Use mutex for multithreading support in UCP.
# n      - Not use mutex for multithreading support in UCP (use spinlock by default).
# y      - Use mutex for multithreading support in UCP.
#
#
# syntax:    <y|n>
#
UCX_USE_MT_MUTEX=n

#
# Enable adaptive progress mechanism, which turns on polling only on active
# transport interfaces.
#
# syntax:    <y|n>
#
UCX_ADAPTIVE_PROGRESS=y

#
# Size of a segment in the worker preregistered memory pool.
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_SEG_SIZE=8K

#
# Threshold for using tag matching offload capabilities.
# Smaller buffers will not be posted to the transport.
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_TM_THRESH=1K

#
# Maximal size for posting "bounce buffer" (UCX internal preregistered memory) for
# tag offload receives. When message arrives, it is copied into the user buffer (similar
# to eager protocol). The size values has to be equal or less than segment size.
# Also the value has to be bigger than UCX_TM_THRESH to take an effect.
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_TM_MAX_BB_SIZE=1K

#
# Threshold for forcing tag matching offload mode. Every tag receive operation
# with buffer bigger than this threshold would force offloading of all uncompleted
# non-offloaded receive operations to the transport (e. g. operations with
# buffers below the UCX_TM_THRESH value). Offloading may be unsuccessful in certain
# cases (non-contig buffer, or sender wildcard).
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_TM_FORCE_THRESH=8K

#
# An optimization hint of how many endpoints would be created on this context.
# Does not affect semantics, but only transport selection criteria and the
# resulting performance.
#  If set to a value different from "auto" it will override the value passed
# to ucp_init()
#
# syntax:    unsigned long: <number> or "auto"
#
UCX_NUM_EPS=auto

#
# RNDV fragment size
#
#
# syntax:    memory units: <number>[b|kb|mb|gb], "inf", or "auto"
#
UCX_RNDV_FRAG_SIZE=256K

#
# Enable memory type(cuda) cache
#
#
# syntax:    <y|n>
#
UCX_MEMTYPE_CACHE=y

#
# Enable flushing the worker by flushing its endpoints. Allows completing
# the flush operation in a bounded time even if there are new requests on
# another thread, or incoming active messages, but consumes more resources.
#
# syntax:    <y|n>
#
UCX_FLUSH_WORKER_EPS=y

#
# Enable various optimizations intended for homogeneous environment.
# Enabling this mode implies that the local transport resources/devices
# of all entities which connect to each other are the same.
#
# syntax:    <y|n>
#
UCX_UNIFIED_MODE=n



#
# cma transport configuration
#

#
# Priority of methods to allocate intermediate buffers for communication
#
# syntax:    comma-separated list of: [thp|md|heap|mmap|huge]
# inherits:  UCX_ALLOC, UCX_ALLOC
#
UCX_CMA_ALLOC=huge,thp,mmap,heap

#
# Level of network failure reporting
#
# syntax:    [FATAL|ERROR|WARN|INFO|DEBUG|TRACE|REQ|DATA|ASYNC|FUNC|POLL]
# inherits:  UCX_FAILURE, UCX_FAILURE
#
UCX_CMA_FAILURE=ERROR

#
# Effective memory bandwidth
#
# syntax:    bandwidth value: <number>[T|G|M|K]B|b[[p|/]s]
# inherits:  UCX_BW
#
UCX_CMA_BW=11145MBps



#
# cma memory domain configuration
#


```
