# MySQL起步

### 安装

**linux CentOS下安装**

```
# 通过yum安装
yum install -y mysql mysql-server mysql-deve

# mysql，mysql客户端
# mysql-server、mysql-deve，mysql服务端
```

```
# 启动
service mysqld start

# 重启
service mysqld restart
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

> 创建：皮成，2016-09-10
