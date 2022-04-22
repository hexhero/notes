# PyInstaller 打包

Document <https://pyinstaller.org/en/stable/usage.html#options>

`pyinstaller [options] script [script …] | specfile`

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