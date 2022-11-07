# Python

- [venv 虚拟环境的使用](note/python/venv.md)
- [Pyinstaller 打包应用](note/python/pyinstaller.md)
- [Eel 使用html开发桌面程序](note/python/eel.md)
- [OCR 图片文字提取](https://github.com/JaidedAI/EasyOCR)
- [彩色日志输出](#彩色日志输出)
- [发送Email](#发送email)


## 彩色日志输出

<https://pypi.org/project/coloredlogs/#usage>

```py
import coloredlogs, logging

# Create a logger object.
logger = logging.getLogger(__name__)

# 显示库日志
coloredlogs.install(level='DEBUG')

# 仅显示当前日志 
coloredlogs.install(level='DEBUG', logger=logger)

# Some examples.
logger.debug("this is a debugging message")
logger.info("this is an informational message")
logger.warning("this is a warning message")
logger.error("this is an error message")
logger.critical("this is a critical message")

```

## 发送Email

```py
from smtplib import SMTP_SSL
from email.mime.text import MIMEText

def sendMail(message,Subject,sender_show,recipient_show,to_addrs,cc_show=''):
    '''
    :param message: str 邮件内容
    :param Subject: str 邮件主题描述
    :param sender_show: str 发件人显示，不起实际作用如："xxx"
    :param recipient_show: str 收件人显示，不起实际作用 多个收件人用','隔开如："xxx,xxxx"
    :param to_addrs: str 实际收件人
    :param cc_show: str 抄送人显示，不起实际作用，多个抄送人用','隔开如："xxx,xxxx"
    '''
    # 填写真实的发邮件服务器用户名、密码
    user = 'leoo.yang@qq.com'
    password = 'nvmadtmddhgleadb'
    # 邮件内容
    msg = MIMEText(message, 'plain', _charset="utf-8")
    # 邮件主题描述
    msg["Subject"] = Subject
    # 发件人显示，不起实际作用
    msg["from"] = sender_show
    # 收件人显示，不起实际作用
    msg["to"] = recipient_show
    # 抄送人显示，不起实际作用
    msg["Cc"] = cc_show
    with SMTP_SSL(host="smtp.qq.com",port=465) as smtp:
        # 登录发邮件服务器
        smtp.login(user = user, password = password)
        # 实际发送、接收邮件配置
        smtp.sendmail(from_addr = user, to_addrs=to_addrs.split(','), msg=msg.as_string())

if __name__ = '__main__':
    sendMail("内容",'主题','发件人','','523084685@qq.com','')
```