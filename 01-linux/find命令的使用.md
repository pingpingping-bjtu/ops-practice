```bash
find [查找路径] [匹配条件] [后续动作]
- **查找路径**：不写默认是当前目录 `.`。
- **匹配条件**：可以组合多个条件（如同时满足名字和大小）。
```
## 🚀 常用场景与命令实例

1. 按文件名查找
- **精确查找**：`find /home -name "test.txt"`（在 /home 下查找名为 test.txt 的文件）
```bash
find a -name "a.txt"
a/b/a.txt
a/a.txt
```
- **模糊查找（不区分大小写）**：`find . -iname "*.jpg"`（查找当前目录下所有 .jpg 和 .JPG 图片）
```bash
#i表示忽略大小写
find a -iname "*.txt"
a/b/a.txt
a/a.txt
```
2. 按“文件类型”查找（`-type`）：常用参数f(文件)、d(目录)、l(软连接)

- **只找普通文件**：`find /var/log -type f -name "*.log"`
```bash
[root@centos8 ~]# find /var/log -type f -name "*.log"
/var/log/sssd/sssd.log
/var/log/sssd/sssd_implicit_files.log
/var/log/sssd/sssd_nss.log
/var/log/tuned/tuned.log
/var/log/audit/audit.log
/var/log/anaconda/anaconda.log
/var/log/anaconda/X.log
/var/log/anaconda/program.log
/var/log/anaconda/packaging.log
/var/log/anaconda/storage.log
/var/log/anaconda/lvm.log
/var/log/anaconda/dnf.librepo.log
/var/log/anaconda/hawkey.log
/var/log/anaconda/dbus.log
/var/log/anaconda/ks-script-8htldww0.log
/var/log/anaconda/ks-script-fswjgv4r.log
/var/log/anaconda/ks-script-rjf_1fmm.log
/var/log/anaconda/journal.log
/var/log/boot.log
/var/log/vmware-vmtoolsd-root.log
/var/log/vmware-vmsvc-root.log
/var/log/kdump.log
/var/log/dnf.log
/var/log/dnf.librepo.log
/var/log/dnf.rpm.log
/var/log/hawkey.log
/var/log/vmware-network.2.log
/var/log/vmware-network.1.log
/var/log/vmware-network.log

```

- **只找目录/文件夹**：`find . -type d -name "config"`

- **只找软链接**：`find /lib -type l`
3. 按“文件大小”查找（`-size`）：+代表大于，-代表小于

- **大于 100MB**：`find . -type f -size +100M`
- **小于 10KB**：`find /etc -type f -size -10k`
- **在 10MB 到 50MB 之间**：`find . -type f -size +10M -size -50M`
- 
4. 按“时间”查找（常用于清理日志）：

| m   | **m**odification time | **修改时间**   | 文件**内容**发生改变（如用 vim 修改了文字）。               |
| --- | --------------------- | ---------- | ----------------------------------------- |
| a   | **a**ccess time       | **访问时间**   | 文件被**读取**或执行（如用 cat 查看、或运行了该脚本）。          |
| c   | change time           | **状态改动时间** | 文件的**元数据**改变（如改了权限 chmod、改了所有者 chown、重命名） |

- **最近 7 天内修改过**：`find /var/log -mtime -7`
- **超过 30 天未被访问过**：`find . -atime +30`
- **最近 10 分钟内状态改变过**：`find . -ctime -10`

5. 按“权限与所属用户”查找:-perm 是权限，-user是所属用户
- **查找 777 高危权限文件**：`find . -type f -perm 777`
- **查找属于 nginx 用户的文件**：`find /www -user nginx`

## 进阶小技巧：查到后自动处理

`find` 最强大的地方在于可以把查找到的结果直接传递给后续命令处理。其固定后缀格式为：`-exec 命令 {} \;` （注意 `{} 和 \ 之间有空格`）。
- **自动删除**：`find /tmp -type f -mtime +7 -exec rm -f {} \;`（强制删除 /tmp 下超过 7 天的旧文件）
- **自动改权限**：`find . -type d -exec chmod 755 {} \;`（将当前目录下所有的文件夹权限改为 755）
- **自动搜索内容**：`find . -type f -name "*.conf" -exec grep "port" {} \;`（在所有 .conf 文件中查找含有 "port" 的行）


