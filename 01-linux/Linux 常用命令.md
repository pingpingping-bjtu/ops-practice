#### 文件与目录操作类（最基本）

- `ls`（ list directory contents）：查看目录内容，
```bash
[root@centos8 ~]# ls -l
总用量 4
#权限       硬链接数   所有者  所属组  文件大小  最后修改时间 文件或目录名称
drwxr-xr-x. 3 root root   28 5月  18 16:14 a
-rw-------. 1 root root 1139 5月  20 2025 anaconda-ks.cfg

 #   ls -a:显示所有目录和文件，包括隐藏的
 #   ls -h: 人类可读
  #  ls -t: 按照文件修改时间排序
 #   ls -R: 递归列出当前目录及所有子目录下的内容
 #   [root@centos8 ~]# ls -R
.:
a  anaconda-ks.cfg

./a:
a.txt  b

./a/b:
c

./a/b/c:
d

./a/b/c/d:
e

./a/b/c/d/e:

```
- `cd`：切换目录，`cd /var/log`
    
- `pwd`：显示当前目录
    
- `cp / mv / rm`：复制、移动、删除文件或目录
    
- `mkdir / rmdir`：创建或删除目录
    
- `touch`：创建空文件或修改文件时间戳
    
- `find / locate`：查找文件，如 `find / -name "*.log"`

```
find [查找路径] [匹配条件] [后续动作]

```
#### 文件查看与处理类

- `cat`：查看小文件
    
- `more / less`：分页查看文件

|more 命令中的快捷键|less 命令中的快捷键|功  能|
|---|---|---|
|无|方向键 ↑|向上滚动一行|
|Enter|方向键 ↓ 或Enter|向下滚动一行|
|b|Page UP 或 b|向上翻页|
|Space|Page Down 或 Space|向下翻页|
|Ctrl+C 或 q|q|退出分页显示模式|

- `tail / head`：查看文件头部或尾部，`tail -f` 追踪日志
    
- `grep`：文本搜索，配合日志分析很常用
    
- `cut / awk / sed`：文本处理，比如按列提取信息（可以举个 `awk '{print $1}'` 的例子）
    

#### 权限与用户管理

- `chmod / chown / chgrp`：修改权限、所有者、所属组
    
- `useradd / userdel / passwd`：用户管理
    
- `su / sudo`：切换用户，提升权限执行命令
    

#### 系统资源与进程管理

- `ps / top / htop`：查看进程，`top` 实时监控
    
- `kill / pkill / killall`：终止进程
    
- `free -h`：查看内存使用情况
    
- `df -h / du -sh`：磁盘使用情况
    
- `uptime / loadavg / vmstat / iostat`：系统负载情况
    
- `netstat / ss / lsof`：网络连接和端口占用情况
    

#### 软件安装与服务管理

- `yum / apt`：软件包安装、卸载
    
- `systemctl`：服务管理，如 `systemctl restart nginx`
    
- `service`：旧版服务管理命令
    

#### 网络配置与测试

- `ip a / ifconfig`：查看网络配置
    
- `ping / traceroute`：网络连通性测试
    
- `curl / wget`：网页请求与文件下载
    
- `scp / rsync`：远程文件传输
    

#### 日志与排错

- `journalctl`：查看系统日志
    
- `dmesg`：内核日志
    
- `/var/log` 下各种日志文件（比如 `/var/log/messages`, `/var/log/syslog`）
    

### 常见协议及服务端口（标准协议）

|协议/服务|默认端口|描述|
|---|---|---|
|HTTP|80|超文本传输协议|
|HTTPS|443|加密的 HTTP|
|FTP|21（命令）/ 20（数据）|文件传输协议|
|SSH|22|安全远程登录|
|Telnet|23|明文远程登录（不安全，已较少用）|
|DNS|53|域名解析（UDP 为主）|
|DHCP|67（服务器）/ 68（客户端）|动态主机配置协议|
|NTP|123|网络时间协议（UDP）|
|SNMP|161（查询）/ 162（Trap）|网络管理协议|

---

### 常见中间件端口

|中间件/数据库|默认端口|描述|
|---|---|---|
|MySQL|3306|关系型数据库|
|PostgreSQL|5432|关系型数据库|
|MongoDB|27017|文档型数据库|
|Redis|6379|缓存数据库（默认无认证）|
|Memcached|11211|分布式内存对象缓存系统|
|RabbitMQ|5672（AMQP）/ 15672（Web UI）|消息队列|
|Kafka|9092|分布式消息队列|
|Zookeeper|2181|协调服务（Kafka依赖）|
|Elasticsearch|9200（REST API）/ 9300（集群）|搜索引擎|
|Logstash|5044（Beats input）|日志收集器|
|Kibana|5601|ES 可视化界面|

---

### Web服务端口

|服务|默认端口|描述|
|---|---|---|
|Nginx|80/443|反向代理、静态服务|
|Apache|80/443|老牌 Web 服务器|
|Tomcat|8080（HTTP）/ 8005（shutdown）|Java Web 容器|
|Node.js|3000、5000 等|前端/后端自定义服务端口|
|Flask/Django|5000/8000|Python Web 开发框架|

---

### 运维相关服务工具端口

|工具/平台|默认端口|用途|
|---|---|---|
|Prometheus|9090|监控数据采集与查询|
|Node Exporter|9100|主机指标采集|
|Grafana|3000|监控可视化平台|
|Alertmanager|9093|告警管理|
|Jenkins|8080|持续集成平台|
|Kubernetes API|6443|K8s 控制平面 API|
|etcd|2379（客户端）/ 2380（集群通信）|分布式存储|

### 查看资源情况的命令

top                # 实时资源查看  
free -m            # 内存使用  
df -h              # 磁盘剩余  
du -sh *           # 目录占用  
iostat -dx 1       # 磁盘 I/O  
vmstat 1           # 整体系统状态  
ss -tuln           # 查看端口  
ps aux --sort=-%mem|head  # 内存高进程

### 查找目录下所有三十天之前修改的文件并删除

# 安全模式：先列出文件确认  
find /目标路径 -type f -mtime +30 -print  
​  
# 确认无误后执行删除  
find /目标路径 -type f -mtime +30 -delete  
​  
​  
时间有三种：文件的最近访问时间（以a开头）、文件状态最近被修改时间（以c开头）、文件数据最近被修改时间（以m开头）  
-amin, -cmin, -mmin，单位是分钟  
-atime, -ctime, -mtime，单位是天  
-amin +3     +3表示差值大于3  
-amin -3     -3表示差值小于3  
-amin 3     表示差值等于3  
-type测试文件类型是否匹配指定的文件类型  
find . -type f -user tom  
找出当前目录用户tom拥有的所有文件  
   
find . -type f -group sunk  
找出当前目录用户组sunk拥有的所有文件

### 根据内存使用情况进行排序，输出排序后的进程

ps -eo pid,user,%mem,comm --sort=-%mem | head -n 10

