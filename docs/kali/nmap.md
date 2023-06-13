# Nmap 常用命令

* 快速扫描主机的详细信息
```sh
nmap -sT -sV -Pn -v xxx.xxx.xxx.xxx
```

* 扫描所有的端口开放情况
```sh
nmap -sS -p 1-65535 -v 192.168.1.254
```

* 扫描网段主机(ping扫描)
```sh
nmap -sn 192.168.16.100-150
```

* 深度扫描网络主机信息
```sh
nmap -A -T4 192.168.10.1
```

* 半开扫描(TCP SYN扫描) - 隐秘且速度快，比较常用
```sh
nmap -sS host
```

## 参数说明 
```sh
-sn Tcp ping扫描
-Pn 跳过主机发现
-PS/PA/PU/PY[portlist]: SYN/ACK/UDP/SCTP
-n: 不做反向DNS查询
--dns-servers 8.8.8.8 : 指定dns服务器
-p-: 扫描所有端口
```


TCP 三次握手

1. client: SYN→ :server
2. client: ←ACK+SYN :server
3. client: ACK→ :server

* SYN: synchronous 同步
* ACK: acknowledgement 确认