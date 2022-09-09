# Linux

- [创建Root权限用户](#CREATEROOTUSER)


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