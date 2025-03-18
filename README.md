# Углубленный анализ производительности

1. На кластере с дефолтными настройками выполняем:

````
 pgbench -c 50 -j 2 -P 60 -T 600 postgres

````

Результат:

````
transaction type: <builtin: TPC-B (sort of)>
scaling factor: 100
query mode: simple
number of clients: 50
number of threads: 2
maximum number of tries: 1
duration: 600 s
number of transactions actually processed: 613322
number of failed transactions: 0 (0.000%)
latency average = 46.936 ms
latency stddev = 65.332 ms
initial connection time = 68.221 ms
tps = 1022.092787 (without initial connection time)

````

2.  Меняем настройки на следующие:
````
shared_buffers = 2GB
effective_cache_size = 6GB
maintenance_work_mem = 512MB
checkpoint_completion_target = 0.9
wal_buffers = 16MB
default_statistics_target = 100
random_page_cost = 1.5
work_mem = 20971kB
huge_pages = off
min_wal_size = 1GB
max_wal_size = 4GB
fsync=off
synchronous_commit=off
track_activity_query_size=1048576
````

3. Выполняем тестирование еще раз:
````
transaction type: <builtin: TPC-B (sort of)>
scaling factor: 100
query mode: simple
number of clients: 50
number of threads: 2
maximum number of tries: 1
duration: 600 s
number of transactions actually processed: 2020278
number of failed transactions: 0 (0.000%)
latency average = 13.813 ms
latency stddev = 36.793 ms
initial connection time = 71.767 ms
tps = 3366.499943 (without initial connection time)
````

Видим, что tps увеличилось в 3 раза, изменение настроек дало хороший результат.
