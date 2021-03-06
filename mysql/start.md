# MySQL起步

## MySQL关键概念

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

**MySQL脚本**

由一条或多条MySQL语句组成，通过执行脚本可以完成对数据库的操作，脚本文件后缀一般`.sql`。

**语句**

MySQL脚本的基本组成单位，每条语句完成特定的操作，语句以分号`;`结束。

**标识符**

由字母、数据、下划线组成，用来命名数据库、表、列、变量等，第1个字符必须是字母或下划线。

**关键字**

有特定含义，不能作为标识符。

**函数**

实现数据库操作的一些高级功能，包括：字符串函数、数学函数、日期时间函数、搜索函数、加密函数、信息函数。

## 安装

**linux CentOS7下安装**

```
# 通过yum安装，MariaDB是MySQL的一个分支，完全兼容MySQL
yum install mariadb-server mariadb
```

```
# 启动
systemctl start mariadb
```

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

### 执行mysql脚本

```
# 命令行下执行，脚本文件在当前目录可直接写文件名，否则需要写完整路径
mysql -u root -p < hello.sql
```

```
# 进入mysql控制台执行，脚本文件在当前目录可直接写文件名，否则需要写完整路径
source hello.sql;
```

### 增

**创建数据库**

```
create database 数据库名 [选项];

# 如
create database videos;
```

```
# 选中数据库
use 数据库名;

# 选中名为videos的数据库
use videos;
```

**创建数据表**

```
# 括号内为各列的名称和数据类型描述，各列之间用逗号`,`分隔
create table table_name (columns);
```

```
# 创建名为movie的表
create table movie (
    id int unsigned not null primary key,
    title text not null,
    intro text not null,
    date year not null,
    rating int not null
) charste = utf8;
```

| 数据类型 | 描述 |
| :-- | :-- |
| int | 整数，范围(-2147483648~2147483647) |
| text | 字符串，最多65535个字符 |
| not null | 值不能为空 |
| primary key | 主键 |

**添加一行数据**

```
insert [into] 表名 [(列名1, 列名2, ...)] values (值1, 值2, ...);
```

```
# 在movie表中添加一行数据
insert into movie (id, title, intro, date, rating) valuse (121745, '叶问3', '又一武林力作！', 2016, 64);
```

```
# 列名是可选的
insert into movie valuse (26542, '青蛇', '二蛇与法海', 1993, 85);
```

**添加列**

```
alter table 表名 add 列名 列数据类型 [插入位置];
```

```
# 在movie表中添加名为actor的列
alter table movie add actor char(30);
```

```
# 在movie表title列后添加名为actor的列
alter table movie add actor char(30) after title;
```

### 删

**删除数据库**

```
drop database 数据库名;
```

```
# 删除videos数据库
drop database videos;
```

**删除表**

```
drop table 表名;
```

```
# 删除movie表
drop table movie;
```

**删除列**

```
alter table 表名 drop 列名;
```

```
# 删除movie表中的rating列
alter table movie drop rating;
```

**删除行**

```
delete from 表名称 where 删除条件;
```

```
# 删除moive表中id=26542的行
delete from movie where id=26542;
```

```
# 删除moive表中评分小于80的行
delete from movie where rating<80;
```

### 改

**重命名表**

```
alter table 表名 rename 新表名;
```

```
# 表 movie 更名为 tvplay
alter table tv rename tvplay;
```

**修改列**

```
alter table 表名 change 列名 新列名 数据类型;
```

```
# 列 intro 更名为 s_intro
alter table movie change intro s_intro char(30);
```

**更新数据**

```
update 表名称 set 列名称=值 where 更新条件;
```

```
# 将movie表中id为26542的行，评分值改为80
update movie set rating=80 where id=26542;
```

```
# 将movie表中所有行的评分值改为80
update movie set rating=80;
```

### 查

**查看已创建的数据库**

```
show databases;
```

**查看当前数据库中已创建的表**

```
show tables;
```

**查看表中的所有字段**

```
show full columns from 表名;
```

```
# 查看movie表中的所有字段信息
show full colunms from movie;
```

**查询表中的数据**

```
select 列名 from 表名 [查询条件];
```

```
# 查询movie表中评分大于80的id列数据
select id from movie rating>80;
```

```
# 查询movie表中评分大于80的所有列数据
select * from movie rating>80;
```

> 创建：皮成，2016-09-10
