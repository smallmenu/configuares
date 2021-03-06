```
[client]
quick  # 快速导入导出
socket = /tmp/mysql.sock
default-character-set = utf8
port = 3306

[mysqld]
server-id = 1
socket = /tmp/mysql.sock
character-set-server = utf8
datadir = /www/mysql
user = mysql
port = 3306
max_allowed_packet = 64M
default-storage-engine = InnoDB
tmp_table_size = 256M  # 临时表大小
max_heap_table_size = 256M  # 默认16M ，内存表大小限制，当order group很多时如果过小，如果内存表不够，会使用磁盘严重影响性能
event_scheduler = 1  # 事件调度，show processlist
back_log = 256  # 连接数相关，默认很小
max_connections = 1024      # 连接数，默认很小
max_connect_errors = 10240
sync_binlog = 0  # 默认0，由操作系统控制刷新性能好，安全性低，1表示每次事务刷新，
sync_relay_log = 1000  # 默认10000，同上，建议主从模式开启
sync_relay_log_info = 1000 
wait_timeout = 36000  # 默认288000 客户端空闲超市
net_read_timeout = 600  # 默认30  读取超时  进行大量数据操作的时候需要增大该值
net_write_timeout = 600  #  默认60  进行大量数据操作的时候需要增大该值
thread_cache_size = 32 # 应观测服务器运行Threads_created状态，决定值范围
thread_stack = 1024K  # 默认 256K
skip-name-resolve
skip-external-locking
slave-skip-errors = 1032,1062,126,1114,1146,1048,1396

# -------------- #
# MyISAM Options #
# -------------- #
query_cache_type = OFF  # 查询缓存，关闭
query_cache_size = 0
query_cache_limit = 8M   # 默认1M
myisam_sort_buffer_size = 16M  # 默认8M

# -------------- #
# Buffer Options #
# -------------- #
bulk_insert_buffer_size = 1024M   # 默认8M，会影响MyISAM批量插入和导入性能
sort_buffer_size = 4M  # 默认256K
join_buffer_size = 4M  # 默认256K
key_buffer_size = 32M  # 默认8M
read_buffer_size = 1M  # 默认128K
read_rnd_buffer_size = 2M  # 默认256K

# -------------- #
# InnoDB Options #
# -------------- #
innodb_additional_mem_pool_size ＝ 8M
innodb_buffer_pool_size = 2G  # 内存大小，对于只使用InnoDB的独立MySQL服务器，应当配置物理内存75%左右，否则按照业务修改
innodb_data_file_path = ibdata1:128M:autoextend  # 数据增量大小
innodb_log_group_home_dir = /www/mysql/
innodb_flush_log_at_trx_commit = 2 # 刷盘机制，可设置为0，1，2，与性能相关
innodb_log_buffer_size = 64M
innodb_log_file_size = 512M  # 日志大小，不能随意修改，否则会导致启动失败，可以将原有的文件mv再重启
innodb_log_files_in_group = 2  # 日志组
innodb_lock_wait_timeout = 120
innodb_file_per_table = 1  # 独立表空间 5.6默认
innodb_rollback_on_timeout = 1   # 超时回滚
innodb_io_capacity = 200   # 与磁盘相关，默认是SATA。SAS, SSD应配置更高
innodb_io_capacity_max = 2000
innodb_read_io_threads = 4  # 读线程
innodb_write_io_threads = 4  # 写线程，读写根据CPU核数与业务来配置

# --------------- #
# Logging Options #
# --------------- #
binlog_format = MIXED   # 默认STATMENT，建议主从模式的日志格式MIXED
binlog_cache_size = 8M
expire_logs_days  = 30  # 日志保存时间

#long_query_time = 1  # 慢查询阀值 默认10s
#slow_query_log = ON  # 开启慢查询
#slow_query_log_file = /var/log/mysql/slow.log  # 慢查询日志
#log_queries_not_using_indexes = ON  # 未使用索引的查询记录
#log-slow-admin-statements = ON   # 主从相关
#log_slow_slave_statements = ON  # 主从相关
log-error = /var/log/mysql/mysql_error.log
log-bin = /var/log/mysql/binlog  # 主从复制相关
#relay-log-index = /var/log/mysql/relaylog-index
#relay-log-info-file = /var/log/mysql/relaylog-info
#relay-log = /var/log/mysql/relaylog

[mysqldump]
quick
max_allowed_packet = 512M
```
