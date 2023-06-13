# PyInstaller 打包

Document <https://pyinstaller.org/en/stable/usage.html#options>

`pyinstaller [options] script [script …] | specfile`

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

pyinstaller 打包

`--add-data './icon.png;.'` `datas=[('icon.png', '.')]` 

## options

`--add-data <SRC;DEST or SRC:DEST>`

windows 用 ; linux 用 : 

`-F, --onefile`

打包成一个文件

`-D, --onedir`

打包成一个文件夹

`-c, --console, --nowindowed`

只有命令行

`-w, --windowed, --noconsole`

只有窗口