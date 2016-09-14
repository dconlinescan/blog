# MySQL起步

### MySQL关键概念

**数据库**

由一个或多个数据表组成

**数据表**

数据的矩阵，看起来像一个电子表格，如：

| id | title | intro | date | rating |
| :-- | :-- | :-- | :-- | :-- |
| 121745 | 叶问3 | 又一武林力作！ | 2016 | 6.4 |
| 26542 | 青蛇 | 二蛇与法海 | 1993 | 8.5 |
| 121747 | 唐人街探案 | 陈思诚王宝强携妻上阵 | 2015 | 7.5 |
| 112562 | 功夫 | 周星驰爆笑功夫片 | 2004 | 7.6 |
| 30230 | 十二生肖 | 成龙勇救失踪兽首 | 2012 | 6.7 |

**表头**

每列的名称，如上面表格的第一行。

**列**

相同数据类型的数据集合，如上面表中的title，列中每个值的数据类型相同。

**行**

一组相关的数据，如上面表中每部电影的信息。

**主键**

主键的值在当前列中唯一，可以使用主键来查询数据，如果上面表中的id。

### 安装

**linux CentOS7下安装**

```
# 通过yum安装，MariaDB是MySQL的一个分支，完全兼容MySQL
yum install mariadb-server mariadb
```

```
# 启动
systemctl start mariadb

**mac下安装**

```
# 通过brew安装
brew install mysql

# 初始化数据库
unset TMPDIR
mysql_install_db --verbose --user=`whoami` --basedir="$(brew --prefix mysql)" --datadir=/usr/local/var/mysql --tmpdir=/tmp
```

```
# 启动
mysql.server start
```

## 操作

### 配置

**root账号登录**

```
mysql -u root -p
```

**设置root密码**

```
# 默认root密码为空
set password for 'root'@'localhost' =password('password');
```

### 增

**创建数据库**

```
create database 数据库名 [选项];
```

```
# 选中数据库
use 数据库名;
```

> 创建：皮成，2016-09-10
