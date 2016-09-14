# linux监控工具

### netstat

> 列出系统上所有的网络套接字连接情况，包括 tcp, udp 以及 unix 套接字。

```
# 列出所有端口
netstat -nltp
```

| 参数 | 描述 |
| :-- | :-- |
| -n | 禁用域名解析，默认会通过反向域名解析查找每个IP对应的主机名 |
| -l | 列出正在监控套接字 |
| -t | 列出TCP协议的连接状况 |
| -p | 显示进程信息 |

### firewall-cmd

> CentOS7后使用的防火墙，firewall-cmd命令用于防火墙的规划管理。

```
# 开启80端口
firewall-cmd --zone=public --add-port=80/tcp --permanent
```

| 参数 | 描述 |
| :-- | :-- |
| --zone | 指定信任级别，public: 允许指定的进入连接 |
| --add-port | 增加端口 |
| --permanent | 永久生效，不加则重启后失效 |

```
# 重启防火墙
firewall-cmd --reload
```

> 创建：皮成，2016.09.14
