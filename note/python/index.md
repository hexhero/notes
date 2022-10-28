# Python

- [venv 虚拟环境的使用](note/python/venv.md)
- [Pyinstaller 打包应用](note/python/pyinstaller.md)
- [Eel 使用html开发桌面程序](note/python/eel.md)
- [OCR 图片文字提取](https://github.com/JaidedAI/EasyOCR)
- [彩色日志输出](#彩色日志输出)


# 彩色日志输出

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