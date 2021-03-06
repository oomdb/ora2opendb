### MySQL8.0 New Features
--- 
+ Features Added in MySQL 8.0
+ Features Deprecated in MySQL 8.0
+ Features Removed in MySQL 8.0

---
#### 一、Features Added
+ [MySQL Data dictionary](https://dev.mysql.com/doc/refman/8.0/en/data-dictionary.html)
+ [Atomic data definition statements (Atomic DDL)](https://dev.mysql.com/doc/refman/8.0/en/atomic-ddl.html)
+ [Upgrade procedure](https://dev.mysql.com/doc/refman/8.0/en/upgrading-what-is-upgraded.html)：MySQL 8.0.16版本开始，安装新版本数据库，在下次启动时，自动调用mysql_upgrade执行升级任务。
+ **Security and account management**
  + mysql库下的 grant授权表 存储引擎由 MyISAM 变为 InnoDB 。
  + [caching_sha2_password 认证插件](https://dev.mysql.com/doc/refman/8.0/en/caching-sha2-pluggable-authentication.html)：SHA-256算法实现，与sha256_password插件一样。比mysql_native_password插件更安全。caching_sha2_password是默认的认证插件。
  + [支持角色Roles](https://dev.mysql.com/doc/refman/8.0/en/roles.html) 
  + [包含用户账户类别](https://dev.mysql.com/doc/refman/8.0/en/account-categories.html)：通过 SYSTEM_USER 权限区分 系统用户 和 普通用户。
  + [授予全局权限](https://dev.mysql.com/doc/refman/8.0/en/partial-revokes.html):受系统变量 partial_revokes 控制。
  + GRANT ...  AS user [WITH ROLE]。
  + [密码管理策略](https://dev.mysql.com/doc/refman/8.0/en/password-management.html)
  + [支持FIPS模式](https://dev.mysql.com/doc/refman/8.0/en/fips-mode.html)
  + [运行时重配新连接的 SSL context](https://dev.mysql.com/doc/refman/8.0/en/using-encrypted-connections.html#using-encrypted-connections-server-side-runtime-configuration)
  + [OpenSSL 1.1.1支持TLS v1.3加密协议](https://dev.mysql.com/doc/refman/8.0/en/encrypted-connection-protocols-ciphers.html)
  + MySQL现在将授予命名管道上的客户端的访问控制设置为Windows上成功通信所必需的最小值：受 named_pipe_full_access_group 系统变量控制。
+ [Resource management](https://dev.mysql.com/doc/refman/8.0/en/resource-groups.html)
+ [Table encryption management](https://dev.mysql.com/doc/refman/8.0/en/innodb-tablespace-encryption.html#innodb-schema-tablespace-encryption-default)：受 default_table_encryption 和 table_encryption_privilege_check 系统变量控制，有 TABLE_ENCRYPTION_ADMIN 权限。
+ **InnoDB enhancements**
  + 最大 auto-increment 值持久化(MySQL服务重启)
  + 记录索引树冲突记录到redo log，保证 crash safe
  + [memcached 插件支持多get操作和range 查询](https://dev.mysql.com/doc/refman/8.0/en/innodb-memcached-multiple-get-range-query.html)
  + 支持死锁检测参数 innodb_deadlock_detect 动态调整
  + 新增INFORMATION_SCHEMA.INNODB_CACHED_INDEXES表，报告每个索引在InnoDB缓冲池中缓存的索引页数innodb_rollback_segments 系统参数定义每个undo表空间回滚段的数量，之前是整个MySQL实例
  + InnoDB 临时表创建在ibtmp1共享临时表空间中
  + InnoDB 表空间加密特性，支持：redo log 和 undo log 数据加密
  + [SELECT ... FOR SHARE 和 SELECT ... FOR UPDATE 语句支持 NOWAIT 和 SKIP LOCKED 选项](https://dev.mysql.com/doc/refman/8.0/en/innodb-locking-reads.html#innodb-locking-reads-nowait-skip-locked)
  + 支持 ALTER TABLE [ADD|DROP|COALESCE|REORGANIZE|REBUILD] PARTITION，使用 ALGORITHM={COPY|INPLACE} 和 LOCK 语句。
  + [InnoDB使用MySQL data dictionary存储引擎相关的数据字典信息](https://dev.mysql.com/doc/refman/8.0/en/data-dictionary.html)
  + mysql系统表和数据字典表开始存储在mysql.ibd独立表空间中，之前是存放在mysql数据库目录个人InnoDB表空间文件中
  + 独立undo表空间，MySQL 8.0.14+开始，支持undo表空间的CREATE/DROP/ALTER 在线操作
  + innodb_undo_log_truncate 系统参数默认开启
  + innodb_rollback_segments 系统参数定义每个undo表空间回滚段的数量，之前是整个MySQL实例回滚段的数量
  + innodb_max_dirty_pages_pct_lwm 默认值从 0 变为 10，innodb_max_dirty_pages_pct 默认值从 75 变为 90
  + [innodb_autoinc_lock_mode 系统参数默认值为 2](https://dev.mysql.com/doc/refman/8.0/en/innodb-auto-increment-handling.html#innodb-auto-increment-lock-modes)
  + 支持重命名通用表空间，ALTER TABLESPACE ... RENAME TO 
  + [新增innodb_dedicated_server系统参数，默认关闭，自动配置 innodb_buffer_pool_size/innodb_log_file_size/innodb_flush_method 3个参数值](https://dev.mysql.com/doc/refman/8.0/en/innodb-dedicated-server.html)
  + 新增 INFORMATION_SCHEMA.INNODB_TABLESPACES_BRIEF 表空间视图
  + 内置压缩库 zlib library 版本从 1.2.3 变为 1.2.11
  + 序列化字典信息（SDI）存在于除temp表空间和undo表空间文件之外的所有InnoDB表空间文件中
  + [支持 原子DDL](https://dev.mysql.com/doc/refman/8.0/en/atomic-ddl.html)
  + [MySQL服务停止时，可以通过innodb_directories选项move表空间文件到新位置](https://dev.mysql.com/doc/refman/8.0/en/innodb-moving-data-files-offline.html)
  + [redo log 优化](https://dev.mysql.com/doc/refman/8.0/en/optimizing-innodb-logging.html)：新增 innodb_log_wait_for_flush_spin_hwm/innodb_log_spin_cpu_abs_lwm/innodb_log_spin_cpu_pct_hwm 3个参数 以及 innodb_log_buffer_size 系统参数可在线动态调整
  + MySQL 8.0.12+版本，undo支持对lob对象的细微更新（100 bytes 以内 ）
  + [在线DDL操作](https://dev.mysql.com/doc/refman/8.0/en/innodb-online-ddl-operations.html)MySQL 8.0.12+版本，ALTER TABLE 操作支持 ALGORITHM=INSTANT，如：添加列/添加、删除虚拟列/添加、删除列默认值/修改ENUM 或者 SET 列的定义/修改索引类型/重命名表。
  + MySQL 8.0.13+版本，TempTable存储引擎支持存储BLOB类型列。之前存储在 internal_tmp_disk_storage_engine 系统变量中。
  + MySQL 8.0.13+版本，InnoDB 静态数据（data-at-rest）加密特性支持general表空间。之前只支持独立表空间。
  + 禁用 innodb_buffer_pool_in_core_file 系统变量，使用此变量，core_file 变量必须开启 & OS必须支持 madvise()。
  + MySQL 8.0.13+版本，用户临时表和内部临时表存储在session会话临时表空间，之前存错在global临时表空间（ibtmp1）。innodb_temp_tablespaces_dir 和 INNODB_SESSION_TEMP_TABLESPACES 表，ibtmp1存储用户创建临时表空间的回滚段信息。
  + MySQL 8.0.14+版本，InnoDB 支持并发聚焦索引扫描，不支持二级索引。innodb_parallel_read_threads 参数设置大于1。默认是 4。
  + MySQL 8.0.14+版本，启用 innodb_dedicated_server  系统参数。
  + MySQL 8.0.14+版本，CREATE TABLESPACE语句的 ADD DATAFILE 字句是可选的，且不需要FILE权限。
  + [MySQL 8.0.16+版本，temptable_use_mmap 和 temptable_max_ram 系统变量](https://dev.mysql.com/doc/refman/8.0/en/internal-temporary-tables.html#internal-temporary-tables-engines)
  + [MySQL 8.0.16+版本，InnoDB 静态数据（data-at-rest）加密特性支持mysql系统表空间](https://dev.mysql.com/doc/refman/8.0/en/innodb-tablespace-encryption.html)
  + [MySQL 8.0.16+版本，新增 innodb_spin_wait_pause_multiplier 系统参数](https://dev.mysql.com/doc/refman/8.0/en/innodb-performance-spin_lock_polling.html)
+ [Character set support](https://dev.mysql.com/doc/refman/8.0/en/charset-unicode-sets.html)：默认字符集从 latin1 变为 utf8mb4，包含新的collations，如：utf8mb4_ja_0900_as_cs。
+ **JSON enhancements**
  + 增加 ->> 操作符，等价于 JSON_UNQUOTE(JSON_EXTRACT()) ，如：col->>"$.path" = JSON_UNQUOTE(col->"$.path")
  + 增加JSON聚合函数：JSON_ARRAYAGG() / JSON_OBJECTAGG()
  + 增加JSON实用函数：JSON_PRETTY() 
  + ORDER BY 排序JSON值，排序键是可变长度，而不是一部分固定的1K大小。
  + [MySQL 8.0.2+版本开始，支持部分、就地更新JSON列的值。使用 JSON_SET()/JSON_REPLACE()/JSON_REMOVE() 方法，RBR必须设置binlog_row_value_options=PARTIAL_JSON参数值](https://dev.mysql.com/doc/refman/8.0/en/json.html#json-partial-updates)
  + [MySQL 8.0.2+版本开始，新增JSON实用函数，JSON_STORAGE_SIZE() 和 JSON_STORAGE_FREE()](https://dev.mysql.com/doc/refman/8.0/en/json-utility-functions.html)
  + [MySQL 8.0.2+版本开始，XPath表达式支持范围，如：$[1 to 5]](https://dev.mysql.com/doc/refman/8.0/en/json.html#json-paths)
  + [添加符合 RFC 7396 的 JSON合并函数，如： JSON_MERGE_PATCH()，JSON_MERGE()函数重命名为JSON_MERGE_PRESERVE()](https://dev.mysql.com/doc/refman/8.0/en/json-modification-functions.html)
  + [支持重复key，最后的重复key获取，和之前的版本不一样，是首个获胜](https://dev.mysql.com/doc/refman/8.0/en/json.html#json-normalization)
  + [MySQL 8.0.4+版本开始，新增JSON_TABLE() 函数](https://dev.mysql.com/doc/refman/8.0/en/json-table-functions.html)
+ [Data type support](https://dev.mysql.com/doc/refman/8.0/en/data-type-defaults.html)： BLOB, TEXT, GEOMETRY, 和 JSON 数据类型,支持expressions作为默认值。
+ **Optimizer**
  + [支持不可见索引（invisible indexes）](https://dev.mysql.com/doc/refman/8.0/en/invisible-indexes.html)
  + [支持降序索引（descending indexes）](https://dev.mysql.com/doc/refman/8.0/en/descending-indexes.html)
  + [支持表达式索引（Functional key parts）](https://dev.mysql.com/doc/refman/8.0/en/create-index.html)
  + [MySQL 8.0.14+ 版本，在准备阶段删除where条件中的常量表达式，而不是等到优化阶段](https://dev.mysql.com/doc/refman/8.0/en/outer-join-optimization.html)
  + [MySQL 8.0.16+ 版本，支持 Constant-Folding Optimization ](https://dev.mysql.com/doc/refman/8.0/en/constant-folding-optimization.html)
  + [MySQL 8.0.16+ 版本，半连接优化，IN 子查询可以转换为 EXISTS 子查询](https://dev.mysql.com/doc/refman/8.0/en/semi-joins.html)
+ [Common table expressions](https://dev.mysql.com/doc/refman/8.0/en/with.html)：CTE 支持 nonrecursive 和 recursive 两种类修改。
+ [Window functions](https://dev.mysql.com/doc/refman/8.0/en/window-functions.html)
+ [Lateral derived tables](https://dev.mysql.com/doc/refman/8.0/en/lateral-derived-tables.html)
+ **Aliases in single-table DELETE statements**：MySQL 8.0.16+版本开始支持
+ [Regular expression support](https://dev.mysql.com/doc/refman/8.0/en/regexp.html)：支持 REGEXP_LIKE()/REGEXP/RLIKE、REGEXP_INSTR()、 REGEXP_REPLACE()、 REGEXP_SUBSTR()函数， 系统变量 regexp_stack_limit 和 regexp_time_limit 控制资源消耗。
+ Internal temporary tables：TempTable替换MEMORY，作为默认内部内存临时表存储引擎。受系统变量internal_tmp_mem_storage_engine 和 temptable_max_ram 控制。
+ [Logging](https://dev.mysql.com/doc/refman/8.0/en/error-log.html)：受系统变量 log_error_services  控制。
+ **Backup lock**：允许在线备份过程中执行DML操作。需要 BACKUP_ADMIN 权限，支持 LOCK INSTANCE FOR BACKUP 和 UNLOCK INSTANCE 语法。
+ [Replication](https://dev.mysql.com/doc/refman/8.0/en/json.html#json-partial-updates)：使用compact二进制格式，支持JSON documents 的部分更新，受系统参数binlog_row_value_options = PARTIAL_JSON 控制。
+ [Connection management](https://dev.mysql.com/doc/refman/8.0/en/client-connections.html)：允许专门为管理连接 配置TCP/IP端口。
+ **Configuration**：整个MySQL中主机名的最大允许长度已从以前的60个字符提高到255个ASCII字符。主要分布在 mysql system schema, Performance Schema, INFORMATION_SCHEMA, 和 sys schema;CHANGE MASTER TO 的 MASTER_HOST值；SHOW PROCESSLIST 输出的 host 列；账户名中的host名称；主机相关的命令选型和系统变量。
+ **Plugins**：之前是C 或者 C++，目前只能是 C++。
+ [C API](https://dev.mysql.com/doc/refman/8.0/en/c-api-asynchronous-interface.html)：MySQL CAPI 现在支持异步函数，用于与MySQL服务器进行非阻塞通信。

---
#### 二、Features Deprecated
+ utf8mb3字符集弃用，建议使用utf8mb4字符集
+ sha256_password密码认证弃用，建议使用超集caching_sha2_password替换
+ [validate_password插件弃用，可以通过安装组件调用](https://dev.mysql.com/doc/refman/8.0/en/validate-password-transitioning.html)
+ ALTER TABLESPACE 和 DROP TABLESPACE ENGINE 弃用
+ SQL MODE值 PAD_CHAR_TO_FULL_LENGTH 弃用
+ FLOAT 和 DOUBLE列 AUTO_INCREMENT 弃用
+ FLOAT(M,D) 和 DOUBLE(M,D) 指定位数语法弃用
+ 非标准操作符 &&, ||（除非SQL MODE值PIPES_AS_CONCAT指定）, 和 ! 弃用，使用AND, OR, 和 NOT 替换
+ JSON合并函数JSON_MERGE()弃用，使用JSON_MERGE_PRESERVE() 替换
+ SQL_CALC_FOUND_ROWS查询修饰符 和 FOUND_ROWS() 函数弃用
+ MySQL 8.0.13+ 版本，CREATE TEMPORARY TABLE 字句 TABLESPACE = innodb_file_per_table 和 TABLESPACE = innodb_temporary 弃用
+ [mysql_upgrade客户端程序弃用](https://dev.mysql.com/doc/refman/8.0/en/upgrading-what-is-upgraded.html)
+ server选项--no-dd-upgrade 弃用，使用--upgrade 替换。

---
#### 三、Features Removed
+ innodb_locks_unsafe_for_binlog 系统参数删除，使用 READ COMMITTED 事务隔离级别替换。
+ information_schema_stats 参数被 information_schema_stats_expiry 参数替代。
+ MySQL 8.0.3+，IS视图依赖InnoDB系统表被数据字典表中的内部系统视图所替代。受影响的InnoDB INFORMATION_SCHEMA 视图被重命名。
+ 账户管理特性
    + 创建用户使用 CREATE USER 代替 GRANT 操作，同时 SQL Mode值 NO_AUTO_CREATE_USER 也被删除了。
    + GRANT 修改账户属性 被替换为 ALTER USER 语法，如：权限认证、SSL、资源限制等。
    + IDENTIFIED BY PASSWORD 'hash_string' 语法 被替换为 IDENTIFIED WITH auth_plugin AS 'hash_string'，因此 log_builtin_as_identified_by_password 系统参数也被删除了。
    + PASSWORD()函数删除，同时 SET PASSWORD ... = PASSWORD('auth_string') 语法失效。
    + old_passwords 系统变量删除。
+ 查询缓存QC
	+ FLUSH QUERY CACHE 和 RESET QUERY CACHE 语句被删除。
	+ query_cache_limit, query_cache_min_res_unit, query_cache_size, query_cache_type, query_cache_wlock_invalidate 系统变量被删除。
	+ Qcache_free_blocks, Qcache_free_memory, Qcache_hits, Qcache_inserts, Qcache_lowmem_prunes, Qcache_not_cached, Qcache_queries_in_cache, Qcache_total_blocks 状态变量被删除。
	+ checking privileges on cached query, checking query cache for query, invalidating query cache entries, sending cached result to client, storing result in query cache, Waiting for query cache lock 线程状态被删除。
	+ SQL_CACHE SELECT 修饰符。
	+ SQL_NO_CACHE SELECT 修饰符。
	+ ndb_cache_check_time 系统变量 和 have_query_cache 系统变量。
+ --ignore-db-dir 选项 和 ignore_db_dirs 系统参数被删除。
+ 系统变量 tx_isolation 和 tx_read_only 被替换为 transaction_isolation 和 transaction_read_only。
+ 系统变量 sync_frm 被删除。
+ 系统变量 secure_auth 和 --secure-auth 客户端选项被删除，mysql_options() C API函数 MYSQL_SECURE_AUTH 被删除。
+ 系统变量 multi_range_count 被删除。
+ 系统变量 log_warnings 和 --log-warnings 服务器选项 被 log_error_verbosity 系统变量替代。
+ 系统变量 sql_log_bin 全局（global）被删除，会话（session）级别被保留。
+ 系统变量 metadata_locks_cache_size 和 metadata_locks_hash_instances 被删除。
+ 系统变量 date_format, datetime_format, time_format, and max_tmp_tables 被删除。
+ 兼容的SQL modes被删除：DB2, MAXDB, MSSQL, MYSQL323, MYSQL40, ORACLE, POSTGRESQL, NO_FIELD_OPTIONS, NO_KEY_OPTIONS, NO_TABLE_OPTIONS。
+ GROUP BY 字句的 ASC 或者 DESC 限制符被删除。
+ EXPLAIN 语句的 EXTENDED 和 PARTITIONS 关键字被移除，因为默认启用。
+ 加密函数移除：ENCODE()、DECODE()、ENCRYPT()、DES_ENCRYPT() 和 DES_DECRYPT()，--des-key-file 选项，have_crypt 系统变量，FLUSH语句的DES_KEY_FILE选项，CMake选项HAVE_CRYPT。考虑使用函数 SHA2() / AES_ENCRYPT() / AES_DECRYPT() 代替 ENCRYPT() 函数。
+ MySQL 8.0，只留下相应的 ST_ 和 MBR 函数。
+ [GIS函数中 WKB字符串 或者 geometry参数，Geometry参数被删除](https://dev.mysql.com/doc/refman/8.0/en/gis-wkb-functions.html)
+ 解析器在SQL语句中不在把 \N 当做NULL的同义词，建议使用NULL代替。如：SELECT \N FROM DUAL; 结果是NULL。
+ 移除 PROCEDURE ANALYSE() 语法。
+ 客户端：--ssl 和 --ssl-verify-server-cert 选项被移除，使用 --ssl-mode=REQUIRED 代替 --ssl=1 或者 --enable-ssl；使用 --ssl-mode=DISABLED 代替 --ssl=0, --skip-ssl, 或者 --disable-ssl；使用 --ssl-mode=VERIFY_IDENTITY 代替 --ssl-verify-server-cert 。服务端的--ssl选项保持不变。
+ 服务端选项 --temp-pool 移除。
+ 服务端选项 --ignore-builtin-innodb 和 ignore_builtin_innodb 系统变量移除。
+ ALTER DATABASE 语句的UPGRADE DATA DIRECTORY NAME字句 和 Com_alter_db_upgrade 状态变量移除。
+ mysql_install_db 安装程序被移除，mysqld程序的--bootstrap选项被移除，CMake选项INSTALL_SCRIPTDIR被移除。使用mysqld程序带 --initialize 或者 --initialize-insecure 代替。
+ 通用分区处理程序已从MySQL服务器中删除，--partition 和 --skip-partition 选项被移除，SHOW PLUGINS 或者 INFORMATION_SCHEMA.PLUGINS 表不再显示分区相关的记录。目前只有InnoDB 和 NDB 存储引擎支持本地分区。非INNODB存储引擎分区表升级存在分歧。
+ INFORMATION_SCHEMA不再维护系统和状态变量信息。表GLOBAL_VARIABLES, SESSION_VARIABLES, GLOBAL_STATUS, SESSION_STATUS 删除，使用PS代替，show_compatibility_56系统变量移除；状态变量Slave_heartbeat_period, Slave_last_heartbeat, Slave_received_heartbeats, Slave_retried_transactions, Slave_running删除，使用PS代替。
+ Performance Schema 的setup_timers表删除，以及表performance_timers 中的TICK行。
+ libmysqld内置库移除。
	+ mysql_options()选项 MYSQL_OPT_GUESS_CONNECTION, MYSQL_OPT_USE_EMBEDDED_CONNECTION, MYSQL_OPT_USE_REMOTE_CONNECTION, 和 MYSQL_SET_CLIENT_IP
	+ mysql_config选项 --libmysqld-libs, --embedded-libs, 和 --embedded
	+ CMake 选项 WITH_EMBEDDED_SERVER, WITH_EMBEDDED_SHARED_LIBRARY, 和 INSTALL_SECURE_FILE_PRIV_EMBEDDEDDIR
	+ 未文档化的 mysql --server-arg 选项
	+ mysqltest 选项 --embedded-server, --server-arg, 和 --server-file
	+ mysqltest_embedded 和 mysql_client_test_embedded 测试程序
+ mysql_plugin 实用程序移除，替代方案：服务启动选项 --plugin-load 或者 --plugin-load-add ；运行时的INSTALL PLUGIN 语句。
+ resolveip 实用程序移除，使用 nslookup, host, 或者 dig 代替。
+ resolve_stack_dump 实用程序移除.
+ [服务端error codes被删除](https://dev.mysql.com/doc/refman/8.0/en/mysql-nutshell.html#mysql-nutshell-removals)
+ INFORMATION_SCHEMA 库的 INNODB_LOCKS 和 INNODB_LOCK_WAITS 表移除，使用 Performance Schema 库的 data_locks 和 data_lock_waits 表代替。
+ InnoDB不再支持压缩临时表，innodb_strict_mode 启动时（默认启用）， CREATE TEMPORARY TABLE 带 ROW_FORMAT=COMPRESSED 或者 KEY_BLOCK_SIZE 将报错，如果 innodb_strict_mode禁用，非压缩临时表将被创建 并产生warnings。
+ 当创建表空间数据文件不在MySQL数据目录下时，InnoDB不再创建 .isl 文件。innodb_directories 选项支持表空间独立于数据文件目录之外。
+ InnoDB文件格式变量被移除：innodb_file_format、innodb_file_format_check、innodb_file_format_max、innodb_large_prefix ，之前时为了兼容MySQL 5.1之前版本保留的。同时 I_S库 INNODB_TABLES 和 INNODB_TABLESPACES 表中的FILE_FORMAT列被移除。
+ innodb_support_xa 系统变量移除，默认支持XA事务的2PC。
+ DTrace支持被删除。
+ JSON_APPEND()函数被移除，使用JSON_ARRAY_APPEND() 函数代替。
+ MySQL 8.0.13+版本，删除了在共享InnoDB表空间中放置表分区的支持，共享表空间包括InnoDB系统表空间和通用表空间。
+ 不支持在SET以外的语句中设置用户变量，MySQL 8.0.13+开始废弃，MySQL 9.0删除。
+ --ndb perror 选项被 ndb_perror 程序代替。
+ innodb_undo_logs 变量移除，使用innodb_rollback_segments 变量代替。
+ Innodb_available_undo_logs 状态变量移除，使用 SHOW VARIABLES LIKE 'innodb_rollback_segments'; 代替。
+ MySQL 8.0.14+版本， innodb_undo_tablespaces 参数不需要配置。
+ ALTER TABLE ... UPGRADE PARTITIONING 语句被删除。
+ [MySQL 8.0.16+版本，internal_tmp_disk_storage_engine 系统变量移除，磁盘内置临时表总是使用InnoDB 存储引擎](https://dev.mysql.com/doc/refman/8.0/en/internal-temporary-tables.html#internal-temporary-tables-engines-disk)
