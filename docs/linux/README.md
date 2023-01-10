# Linux

- [创建Root权限用户](#create-root-user)
- [SCP 传输文件](#SCP)
- 查找端口 `lsof -i:端口号`

## CREATE ROOT USER

```sh
# 创建用户
adduser tomcat
# 设置密码
passwd tomcat
# 赋予root权限

# 文件中添加如下内容
vim /etc/sudoers

# 使用sudo的权限
root    ALL=(ALL:ALL) ALL
tomcat  ALL=(ALL:ALL) ALL

# 提权root
usermod -g root ftpapl
```


## SCP

从本地复制到远程

```sh
scp /home/space/music/1.mp3 root@www.runoob.com:/home/root/others/music 
scp /home/space/music/1.mp3 root@www.runoob.com:/home/root/others/music/001.mp3 
```

复制目录

```
scp -r /home/space/music/ root@www.runoob.com:/home/root/others/ 
scp -r /home/space/music/ www.runoob.com:/home/root/others/ 
```

从远程复制到本地

从远程复制到本地，只要将从本地复制到远程的命令的后2个参数调换顺序即可，如下实例

```
scp root@www.runoob.com:/home/root/others/music /home/space/music/1.mp3 
scp -r www.runoob.com:/home/root/others/ /home/space/music/
```