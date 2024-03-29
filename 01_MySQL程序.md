# MySQL 程序

## 概览

| 分类                                      | 程序                        | 考点 | 作用                                                         |
| ----------------------------------------- | --------------------------- | ---- | ------------------------------------------------------------ |
| 启动和停止服务器                          | `mysql`                     | *    | SQL守护程序（即MySQL服务器）。要使用客户端程序，必须运行[**mysqld**](https://dev.mysql.com/doc/refman/5.7/en/mysqld.html)，因为客户端通过连接到服务器来访问数据库。请参见[第4.3.1节“ **mysqld** - MySQL服务器”](https://dev.mysql.com/doc/refman/5.7/en/mysqld.html)。 |
|                                           | `mysql_safe`                |      | 服务器启动脚本。[**mysqld_safe**](https://dev.mysql.com/doc/refman/5.7/en/mysqld-safe.html) 尝试启动[**mysqld**](https://dev.mysql.com/doc/refman/5.7/en/mysqld.html)。请参见 [第4.3.2节“ **mysqld_safe** - MySQL服务器启动脚本”](https://dev.mysql.com/doc/refman/5.7/en/mysqld-safe.html)。 |
|                                           | `mysql.server`              |      | 服务器启动脚本。此脚本用于使用System V样式运行目录的系统，该目录包含为特定运行级别启动系统服务的脚本。它调用 [**mysqld_safe**](https://dev.mysql.com/doc/refman/5.7/en/mysqld-safe.html)来启动MySQL服务器。请参见 [第4.3.3节“ **mysql.server** - MySQL服务器启动脚本”](https://dev.mysql.com/doc/refman/5.7/en/mysql-server.html)。 |
|                                           | `mysql.multi`               |      | 服务器启动脚本，可以启动或停止系统上安装的多个服务器。请参见 [第4.3.4节“ **mysqld_multi** - 管理多个MySQL服务器”](https://dev.mysql.com/doc/refman/5.7/en/mysqld-multi.html)。 |
| 多个程序在MySQL安装或升级期间执行设置操作 | `comp_err`                  |      | 该程序在MySQL构建/安装过程中使用。它编译错误源文件中的错误消息文件。请参见[第4.4.1节“ **comp_err** - 编译MySQL错误消息文件”](https://dev.mysql.com/doc/refman/5.7/en/comp-err.html)。 |
|                                           | `mysql_install_db`          | *    | 该程序初始化MySQL数据目录，创建 `mysql`数据库并使用默认权限初始化其授权表，并设置 `InnoDB` [系统表空间](https://dev.mysql.com/doc/refman/5.7/en/glossary.html#glos_system_tablespace)。当首次在系统上安装MySQL时，它通常只执行一次。请参见 [第4.4.2节“ **mysql_install_db** - 初始化MySQL数据目录”](https://dev.mysql.com/doc/refman/5.7/en/mysql-install-db.html)和 [第2.10节“安装后设置和测试”](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html)。 |
|                                           | `mysql_plugin`              |      | 该程序配置MySQL服务器插件。请参见 [第4.4.3节“ **mysql_plugin** - 配置MySQL服务器插件”](https://dev.mysql.com/doc/refman/5.7/en/mysql-plugin.html)。 |
|                                           | `mysql_secure_installation` | *    | 此程序使您可以提高MySQL安装的安全性。请参见[第4.4.4节“ **mysql_secure_installation** - 改进MySQL安装安全性”](https://dev.mysql.com/doc/refman/5.7/en/mysql-secure-installation.html)。 |
|                                           | `mysql_ssl_rsa_setup`       |      | 如果缺少这些文件，此程序将创建支持安全连接所需的SSL证书和密钥文件以及RSA密钥对文件。[**mysql_ssl_rsa_setup**](https://dev.mysql.com/doc/refman/5.7/en/mysql-ssl-rsa-setup.html)创建的文件 可用于使用SSL或RSA的安全连接。请参见 [第4.4.5节“ **mysql_ssl_rsa_setup** - 创建SSL / RSA文件”](https://dev.mysql.com/doc/refman/5.7/en/mysql-ssl-rsa-setup.html)。 |
|                                           | `mysql_tzinfo_to_sql`       |      | 此程序`mysql`使用主机系统zoneinfo 数据库（描述时区的文件集）的内容加载数据库中的时区表 。请参见 [第4.4.6节“ **mysql_tzinfo_to_sql** - 加载时区表”](https://dev.mysql.com/doc/refman/5.7/en/mysql-tzinfo-to-sql.html)。 |
|                                           | `mysql_upgrade`             |      | 该程序在MySQL升级操作后使用。它使用在较新版本的MySQL中进行的任何更改来更新授权表，并检查表中的不兼容性并在必要时进行修复。请参见 [第4.4.7节“ **mysql_upgrade** - 检查和升级MySQL表”](https://dev.mysql.com/doc/refman/5.7/en/mysql-upgrade.html)。 |
| 连接MySQL服务器的MySQL客户端程序          | `mysql`                     | *    | 用于以批处理方式交互式输入SQL语句或从文件执行它们的命令行工具。请参见 [第4.5.1节“ **mysql** - MySQL命令行客户端”](https://dev.mysql.com/doc/refman/5.7/en/mysql.html)。 |
|                                           | `mysqladmin`                |      | 执行管理操作的客户端，例如创建或删除数据库，重新加载授权表，将表刷新到磁盘以及重新打开日志文件。 [**mysqladmin**](https://dev.mysql.com/doc/refman/5.7/en/mysqladmin.html)还可用于从服务器检索版本，进程和状态信息。请参见 [第4.5.2节“ **mysqladmin** - 管理MySQL服务器的客户端”](https://dev.mysql.com/doc/refman/5.7/en/mysqladmin.html)。 |
|                                           | `mysqlcheck`                |      | 表维护客户端，用于检查，修复，分析和优化表。请参见[第4.5.3节“ **mysqlcheck** - 表维护程序”](https://dev.mysql.com/doc/refman/5.7/en/mysqlcheck.html)。 |
|                                           | `mysqldump`                 | *    | 将MySQL数据库作为SQL，文本或XML转储到文件中的客户端。请参见[第4.5.4节“ **mysqldump** - 数据库备份程序”](https://dev.mysql.com/doc/refman/5.7/en/mysqldump.html)。 |
|                                           | `mysqlimport`               |      | 使用的导出文本文件到其各自表的客户端[`LOAD DATA`](https://dev.mysql.com/doc/refman/5.7/en/load-data.html)。请参见 [第4.5.5节“ **mysqlimport** - 数据导入程序”](https://dev.mysql.com/doc/refman/5.7/en/mysqlimport.html)。 |
|                                           | `mysqlpump`                 |      | 将MySQL数据库作为SQL转储到文件中的客户端。请参见 [第4.5.6节“ **mysqlpump** - 数据库备份程序”](https://dev.mysql.com/doc/refman/5.7/en/mysqlpump.html)。 |
|                                           | `mysqlsh`                   |      | MySQL Shell是MySQL Server的高级客户端和代码编辑器。请参阅[MySQL Shell 8.0（MySQL 8.0的一部分）](https://dev.mysql.com/doc/mysql-shell/8.0/en/)。除了提供的SQL功能，类似于 [**mysql**](https://dev.mysql.com/doc/refman/5.7/en/mysql.html)，MySQL Shell还提供了JavaScript和Python的脚本功能，并包含用于MySQL的API。X DevAPI使您可以使用关系数据和文档数据，请参阅 [第19章，*将MySQL用作文档存储*](https://dev.mysql.com/doc/refman/5.7/en/document-store.html)。AdminAPI使您可以使用InnoDB集群，请参阅 [第20章*InnoDB集群*](https://dev.mysql.com/doc/refman/5.7/en/mysql-innodb-cluster-userguide.html)。 |
|                                           | `mysqlshow`                 |      | 显示有关数据库，表，列和索引的信息的客户端。请参见[第4.5.7节“ **mysqlshow** - 显示数据库，表和列信息”](https://dev.mysql.com/doc/refman/5.7/en/mysqlshow.html)。 |
|                                           | `mysqlslap`                 |      | 一个客户端，旨在模拟MySQL服务器的客户端负载并报告每个阶段的时间。它就像多个客户端正在访问服务器一样。请参见 [第4.5.8节“ **mysqlslap** - 加载仿真客户端”](https://dev.mysql.com/doc/refman/5.7/en/mysqlslap.html)。 |
| MySQL管理和实用程序                       | `innochecksum`              |      | 脱机`InnoDB`脱机文件校验和实用程序。请参见[第4.6.1节“ **innochecksum** - 离线InnoDB文件校验和实用程序”](https://dev.mysql.com/doc/refman/5.7/en/innochecksum.html)。 |
|                                           | `myisam_ftdump`             |      | 一种实用程序，用于显示有关`MyISAM`表中全文索引的信息 。请参见 [第4.6.2节“ **myisam_ftdump** - 显示全文索引信息”](https://dev.mysql.com/doc/refman/5.7/en/myisam-ftdump.html)。 |
|                                           | `myisamchk`                 |      | 用于描述，检查，优化和修复`MyISAM`表的实用程序 。请参见 [第4.6.3节“ **myisamchk**- MyISAM表维护实用程序”](https://dev.mysql.com/doc/refman/5.7/en/myisamchk.html)。 |
|                                           | `myisamlog`                 |      | 处理`MyISAM`日志文件内容的实用程序 。请参见 [第4.6.4节“ **myisamlog** - 显示MyISAM日志文件内容”](https://dev.mysql.com/doc/refman/5.7/en/myisamlog.html)。 |
|                                           | `mysql_config_editor`       | *    | 一种实用程序，使您可以将身份验证凭据存储在名为的安全加密登录路径文件中`.mylogin.cnf`。请参见 [第4.6.6节“ **mysql_config_editor** - MySQL配置实用程序”](https://dev.mysql.com/doc/refman/5.7/en/mysql-config-editor.html)。 |
|                                           | `mysqlbinlog`               | *    | 用于从二进制日志中读取语句的实用程序。二进制日志文件中包含的已执行语句的日志可用于帮助从崩溃中恢复。请参见 [第4.6.7节“ **mysqlbinlog** - 处理二进制日志文件的实用程序”](https://dev.mysql.com/doc/refman/5.7/en/mysqlbinlog.html)。 |
|                                           | `mysqldumpslow`             | *    | 用于读取和汇总慢查询日志内容的实用程序。请参见[第4.6.8节“ **mysqldumpslow** - 汇总慢速查询日志文件”](https://dev.mysql.com/doc/refman/5.7/en/mysqldumpslow.html)。 |
| MySQL程序开发实用程序                     | `mysql_config`              |      | 一个shell脚本，用于生成编译MySQL程序时所需的选项值。请参见[第4.7.1节“ **mysql_config** - 用于编译客户端的显示选项”](https://dev.mysql.com/doc/refman/5.7/en/mysql-config.html)。 |
|                                           | `my_print_defaults`         |      | 一个实用程序，显示选项文件的选项组中存在哪些选项。请参见 [第4.7.2节“ **my_print_defaults** - 从选项文件显示选项”](https://dev.mysql.com/doc/refman/5.7/en/my-print-defaults.html)。 |
|                                           | `resolve_stack_dump`        |      | 一种实用程序，用于将数字堆栈跟踪转储解析为符号。请参见[第4.7.3节“ **resolve_stack_dump** - 将数字堆栈跟踪转储解析为符号”](https://dev.mysql.com/doc/refman/5.7/en/resolve-stack-dump.html)。 |
| 杂项工具                                  | `lz4_decompress`            |      | 一个实用程序，用于解压缩 使用LZ4压缩创建的[**mysqlpump**](https://dev.mysql.com/doc/refman/5.7/en/mysqlpump.html)输出。请参见 [第4.8.1节“ **lz4_decompress** - 解压缩mysqlpump LZ4压缩输出”](https://dev.mysql.com/doc/refman/5.7/en/lz4-decompress.html)。 |
|                                           | `perror`                    |      | 显示系统或MySQL错误代码含义的实用程序。请参见[第4.8.2节“ **perror** - 显示MySQL错误消息信息”](https://dev.mysql.com/doc/refman/5.7/en/perror.html)。 |
|                                           | `replace`                   |      | 一种在输入文本中执行字符串替换的实用程序。请参见[第4.8.3节“**替换** - 字符串替换实用程序”](https://dev.mysql.com/doc/refman/5.7/en/replace-utility.html)。 |
|                                           | `resolveip`                 |      | 一种实用程序，用于将主机名解析为IP地址，反之亦然。请参见[第4.8.4节“ **解压缩** - 将主机名解析为IP地址或反之亦然”](https://dev.mysql.com/doc/refman/5.7/en/resolveip.html)。 |
|                                           | `zlib_decompress`           |      | 一个实用程序，用于解压缩 使用ZLIB压缩创建的[**mysqlpump**](https://dev.mysql.com/doc/refman/5.7/en/mysqlpump.html)输出。请参见 [第4.8.5节“ **zlib_decompress** - 解压缩mysqlpump ZLIB压缩输出”](https://dev.mysql.com/doc/refman/5.7/en/zlib-decompress.html) |
| 图形化工具                                | `MySQL Workbench`           |      | 用于管理MySQL服务器和数据库，创建，执行和评估查询，以及从其他关系数据库管理系统迁移模式和数据以供MySQL使用。 |
|                                           | `MySQL for Excel`           |      | MySQL for Excel是一个加载项，使您可以从Microsoft Excel中浏览MySQL模式，表，视图和过程。使用MySQL for Excel，您可以执行以下操作：1. 将MySQL数据导入Excel。 2. 将Excel数据作为新表导出到MySQL或将数据附加到现有表。 3. 直接从Excel中修改MySQL数据。 |
|                                           | `MySQL Notifier`            |      | MySQL Notifier是一个工具，使您可以通过驻留在Microsoft Windows任务栏中的指示器来监视和调整本地和远程MySQL服务器实例的状态。MySQL Notifier还通过其上下文菜单快速访问MySQL Workbench。 |



## mysqlbackup

企业版才有的工具，考试必考

[backup-commands-backup](https://dev.mysql.com/doc/mysql-enterprise-backup/8.0/en/backup-commands-backup.html)

考点：backup的三种方式

* backup-to-image 备份数据的单文件备份
* backup 备份目录
* backup-and-apply-log = backup + apply-log 备份数据的单文件备份+应用redolog
