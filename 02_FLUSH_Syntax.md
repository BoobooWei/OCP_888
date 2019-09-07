# FLUSH Syntax

## 官方帮助

[FLUSH Syntax](https://dev.mysql.com/doc/refman/8.0/en/flush.html)

## 语法明细

```sql
FLUSH [NO_WRITE_TO_BINLOG | LOCAL] {
    flush_option [, flush_option] ...
  | tables_option
}

flush_option: {
    BINARY LOGS
  | ENGINE LOGS
  | ERROR LOGS
  | GENERAL LOGS
  | HOSTS
  | LOGS
  | PRIVILEGES
  | OPTIMIZER_COSTS
  | RELAY LOGS [FOR CHANNEL channel]
  | SLOW LOGS
  | STATUS
  | USER_RESOURCES
}

tables_option: {
    TABLES
  | TABLES tbl_name [, tbl_name] ...
  | TABLES WITH READ LOCK
  | TABLES tbl_name [, tbl_name] ... WITH READ LOCK
  | TABLES tbl_name [, tbl_name] ... FOR EXPORT
}
```

## 重点

### flush tables for export

```sql
FLUSH TABLES tbl_name [, tbl_name] ... WITH READ LOCK
```

此语句刷新并获取指定表的读锁定。该语句首先获取表的独占元数据锁，因此它等待打开这些表的事务完成。然后，语句从表缓存中刷新表，重新打开表，获取表锁（如 LOCK TABLES ... READ），并将元数据锁从独占降级为共享。在语句获取锁并降级元数据锁之后，其他会话可以读取但不能修改表。

由于此语句获取表锁，因此LOCK TABLES除了RELOAD使用任何FLUSH 语句所需的权限之外，还必须具有每个表的 权限。

此语句仅适用于现有基TEMPORARY) 表（非表。如果名称引用基表，则使用该表。如果引用TEMPORARY表，则忽略该 表。如果名称适用于视图， ER_WRONG_OBJECT则会发生错误。否则，发生 ER_NO_SUCH_TABLE错误。

使用UNLOCK TABLES释放锁， LOCK TABLES以释放锁和收购其他的锁，或 START TRANSACTION释放锁，并开始一个新的事务。

此FLUSH TABLES变体使表能够在单个操作中刷新和锁定。它为FLUSH TABLES有活动时不允许 的限制提供了一种解决方法 LOCK TABLES ... READ。

此语句不执行隐式 UNLOCK TABLES，因此如果在有活动时使用该语句，则会导致错误，LOCK TABLES或者在未首先释放获取的锁定的情况下再次使用该语句时会导致错误 。

如果打开了刷新的表 HANDLER，则会隐式刷新处理程序并丢失其位置。

FLUSH TABLES tbl_name [, tbl_name] ... FOR EXPORT

此FLUSH TABLES变体适用于InnoDB表格。它确保已将对指定表的更改刷新到磁盘，以便在服务器运行时可以创建二进制表副本。

声明的作用如下：

1. 它获取指定表的共享元数据锁。只要其他会话具有已修改这些表或为其保存表锁的活动事务，该语句就会阻塞。获取锁后，该语句将阻止尝试更新表的事务，同时允许只读操作继续。

2. 它检查表的所有存储引擎是否支持FOR EXPORT。如果没有，则发生 ER_ILLEGAL_HA错误并且语句失败。

3. 该语句通知存储引擎每个表以使表准备好导出。存储引擎必须确保将所有挂起的更改写入磁盘。

4. 该语句将会话置于锁定表模式，以便在FOR EXPORT 语句完成时不会释放先前获取的元数据锁。

该 FLUSH TABLES ... FOR EXPORT声明要求您拥有SELECT每个表的权限。由于此语句获取表锁，因此LOCK TABLES除了RELOAD使用任何FLUSH 语句所需的权限之外，还必须具有每个表的权限。

此语句仅适用于现有的基（非TEMPORARY）表。如果名称引用基表，则使用该表。如果它引用 TEMPORARY表，则忽略它。如果名称适用于视图， ER_WRONG_OBJECT则会发生错误。否则， ER_NO_SUCH_TABLE会发生错误。

InnoDB支持FOR EXPORT具有自己的 .ibd 文件文件的表（即，在innodb_file_per_table 启用设置的情况下创建的表 ）。InnoDB确保在FOR EXPORT语句通知任何更改已刷新到磁盘时。这允许在FOR EXPORT语句生效时生成表内容的二进制副本，因为该 .ibd文件是事务一致的，并且可以在服务器运行时复制。FOR EXPORT不适用于InnoDB 系统表空间文件或InnoDB 具有FULLTEXT索引的表。

FLUSH TABLES ...FOR EXPORT分区InnoDB表支持 。

When notified by FOR EXPORT, InnoDB writes to disk certain kinds of data that is normally held in memory or in separate disk buffers outside the tablespace files. For each table, InnoDB also produces a file named table_name.cfg in the same database directory as the table. The .cfg file contains metadata needed to reimport the tablespace files later, into the same or different server.

当FOR EXPORT语句完成， InnoDB将有刷新所有 脏页表中的数据文件。 在刷新之前合并任何 更改缓冲区条目。此时，表已锁定且处于静止状态：表在磁盘上处于事务一致状态，您可以将.ibd表空间文件与相应.cfg文件一起复制，以获得这些表的一致快照。

有关将复制的表数据重新导入MySQL实例的过程，请参见第15.6.3.7节“将表空间复制到另一个实例”





