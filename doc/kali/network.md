# Kali 网络配置

使用用Kali虚拟机需要开启桥接模式。
修改`/etc/network/interfaces`文件

dhcp 自动获取ip地址
```
auto eth0
iface eth0 dhcp
```

手动IP设置
```
auto eth0
iface eth0 inet static
address 192.168.10.188
netmask 255.255.255.0
gateway 192.168.10.1
```

重启网络服务

```sh
/etc/init.d/networking restart
```
