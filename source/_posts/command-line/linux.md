---
title: Linux命令行
author: pzc
date: 2023-06-02
cover: /assets/images/jpg/3.jpg
categories: [commandLine]
tags: [Linux,System,Backend]
---
Linux 是一个非常强大的操作系统，提供了丰富的命令行工具来帮助用户管理和操作文件系统、进程、网络等。以下是一些常用的 Linux 命令，按功能分类，可以帮助你更好地使用 Linux 系统。

### 文件和目录操作

- **查看当前目录**
  - `pwd`：显示当前工作目录的完整路径。

- **列出目录内容**
  - `ls`：列出当前目录下的文件和子目录。
  - `ls -l`：以长格式列出文件和目录的详细信息。
  - `ls -a`：列出所有文件，包括隐藏文件（以 `.` 开头的文件）。
  - `ls -la`：结合 `-l` 和 `-a` 选项。

- **切换目录**
  - `cd [directory]`：切换到指定的目录。
  - `cd ..`：切换到上一级目录。
  - `cd ~` 或 `cd`：切换到用户的主目录。

- **创建目录**
  - `mkdir [directory]`：创建一个新目录。
  - `mkdir -p [directory1/directory2]`：递归创建多层目录。

- **删除文件和目录**
  - `rm [file]`：删除文件。
  - `rm -r [directory]`：递归删除目录及其内容。
  - `rm -rf [directory]`：强制删除目录及其内容，不提示确认。

- **复制文件和目录**
  - `cp [source] [destination]`：复制文件。
  - `cp -r [source-directory] [destination-directory]`：递归复制目录。

- **移动或重命名文件和目录**
  - `mv [source] [destination]`：移动文件或目录。
  - `mv [old-name] [new-name]`：重命名文件或目录。

- **查看文件内容**
  - `cat [file]`：显示文件内容。
  - `less [file]`：分页显示文件内容。
  - `head [file]`：显示文件的前几行。
  - `tail [file]`：显示文件的最后几行。
  - `tail -f [file]`：实时查看文件的新增内容。

- **查找文件**
  - `find [path] -name [pattern]`：在指定路径下查找符合模式的文件。
  - `locate [filename]`：快速查找文件（需要先运行 `updatedb` 更新数据库）。

### 文件权限和所有权

- **查看文件权限**
  - `ls -l`：以长格式列出文件和目录的详细信息，包括权限。

- **修改文件权限**
  - `chmod [mode] [file]`：修改文件权限。
    - 例如：`chmod 755 file.txt` 将文件权限设置为 `rwxr-xr-x`。
  - `chmod u+x [file]`：给文件所有者增加执行权限。

- **修改文件所有权**
  - `chown [user:group] [file]`：修改文件的所有者和组。
    - 例如：`chown user:group file.txt` 将文件的所有者设置为 `user`，组设置为 `group`。

### 进程管理

- **查看进程**
  - `ps`：显示当前终端的进程。
  - `ps aux`：显示系统中所有进程的详细信息。
  - `top`：动态显示系统中各个进程的资源占用情况。

- **杀死进程**
  - `kill [pid]`：发送终止信号给指定的进程。
  - `kill -9 [pid]`：强制终止指定的进程。
  - `pkill [process-name]`：通过进程名杀死进程。

### 网络相关

- **查看网络接口**
  - `ifconfig`：显示网络接口的配置信息（某些系统可能需要安装 `net-tools` 包）。
  - `ip addr show`：显示网络接口的配置信息。

- **测试网络连接**
  - `ping [host]`：向目标主机发送 ICMP 请求，测试网络连通性。
  - `traceroute [host]`：显示数据包到达目标主机所经过的路由。

- **查看网络服务**
  - `netstat -tuln`：显示所有监听的 TCP 和 UDP 端口。
  - `ss -tuln`：类似于 `netstat`，显示网络连接和服务。

### 系统信息

- **查看系统信息**
  - `uname -a`：显示系统的内核版本和其他信息。
  - `hostname`：显示主机名。
  - `df -h`：显示磁盘空间使用情况。
  - `du -sh [directory]`：显示指定目录的磁盘使用情况。
  - `free -m`：显示内存使用情况。

### 文本处理

- **文本搜索**
  - `grep [pattern] [file]`：在文件中搜索符合模式的行。
  - `grep -r [pattern] [directory]`：递归搜索目录中的文件。

- **文本替换**
  - `sed 's/old-text/new-text/g' [file]`：在文件中替换文本。

- **文本排序**
  - `sort [file]`：对文件中的行进行排序。
  - `sort -r [file]`：逆序排序。

- **文本统计**
  - `wc [file]`：统计文件中的行数、单词数和字节数。
  - `wc -l [file]`：仅统计行数。

### 压缩和解压

- **压缩文件**
  - `tar -czvf archive.tar.gz [directory]`：将目录压缩为 `.tar.gz` 文件。
  - `zip -r archive.zip [directory]`：将目录压缩为 `.zip` 文件。

- **解压文件**
  - `tar -xzvf archive.tar.gz`：解压 `.tar.gz` 文件。
  - `unzip archive.zip`：解压 `.zip` 文件。

### 用户和组管理

- **查看用户和组**
  - `whoami`：显示当前用户名。
  - `groups`：显示当前用户所属的组。
  - `id [username]`：显示用户的 UID 和 GID 以及所属的组。

- **添加用户和组**
  - `useradd [username]`：添加新用户。
  - `groupadd [groupname]`：添加新组。

- **删除用户和组**
  - `userdel [username]`：删除用户。
  - `groupdel [groupname]`：删除组。

- **修改用户密码**
  - `passwd [username]`：修改用户密码。

### 系统维护

- **关机和重启**
  - `shutdown -h now`：立即关机。
  - `shutdown -r now`：立即重启。
  - `reboot`：重启系统。

- **更新系统**
  - `sudo apt update && sudo apt upgrade`：在 Debian/Ubuntu 系统上更新软件包列表并升级已安装的软件包。
  - `sudo yum update`：在 Red Hat/CentOS 系统上更新软件包。

这些命令涵盖了 Linux 系统管理中的大部分常见任务。