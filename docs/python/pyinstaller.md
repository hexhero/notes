# PyInstaller 打包

Document <https://pyinstaller.org/en/stable/usage.html#options>

`pyinstaller [options] script [script …] | specfile`

## 常用命令

打包单个可执行文件。

`pyinstaller --onefile -n redis_monitor --add-data './icon.png;.'  -w --icon favicon.ico main.py`

## 将资源打包到一个文件的路径问题

py 中获取文件的路径.

```py
import os,sys

def resource_path(relative_path):
    try:
        base_path = sys._MEIPASS
    except Exception:
        base_path = os.path.abspath(".")

    return os.path.join(base_path, relative_path)

icon = QPixmap(resource_path('icon.png'))
```

pyinstaller 附加文件

`--add-data './icon.png;.'` `datas=[('icon.png', '.')]` 

