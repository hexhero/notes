# PyQt5

## 显示空背景的文字
```py
from PyQt5.QtWidgets import QApplication, QWidget, QLabel
from PyQt5 import QtCore
import sys

class UI(QWidget):
    def __init__(self):
        super().__init__()
        self.initUI()
        
    def initUI(self):
        self.setWindowFlags(self.windowFlags() | QtCore.Qt.FramelessWindowHint | QtCore.Qt.WindowStaysOnTopHint)
        self.setAttribute(QtCore.Qt.WA_TranslucentBackground)
        self.setGeometry(120, 120, 300, 200)
        self.label = QLabel('Hello World!', self, styleSheet='color: green; font-size: 36px; font-weight: bold;')
        self.label.setFixedWidth(self.width() - 20)
        self.label.move(10, 10)

if __name__ == '__main__':
    app = QApplication(sys.argv)
    ui = UI(query=query)
    ui.show()
    sys.exit(app.exec_())        
```
