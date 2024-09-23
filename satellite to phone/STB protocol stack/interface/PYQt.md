### 代码框架

```python
import sys
from PyQt5.QtWidgets import QApplication, QMainWindow, QVBoxLayout, QHBoxLayout, QPushButton, QLabel, QWidget, QSlider

class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()
		
		''' your code '''

        central_widget = QWidget()
        central_widget.setLayout(HBox_Layout)
        self.setCentralWidget(central_widget)

if __name__ == "__main__":
    app = QApplication(sys.argv)
    window = MainWindow()
    window.show()
    sys.exit(app.exec_())
```

### 布局管理器
自动/手动布局，根据容器的大小和月航速排列和调整组建的位置和大小
#### 使用方法

```python
"""###################################
（1）管理子部件
（2）将子部件给到主部件
（3）窗口显示主部件
###################################"""

layout = QVBoxLayout()  				# 创建一个垂直布局管理器对象（用于管理垂直排列的子部件）
layout.addWidget(container_widget)  	# 将名为container_widget的部件添加到垂直布局中

central_widget = QWidget()  			# 创建一个QWidget对象（用作主窗口的中央部件）
central_widget.setLayout(layout)  		# 将布局设置为central_widget的布局管理器，使布局成为central_widget的主要布局
self.setCentralWidget(central_widget)  	# 将central_widget设置为主窗口（通常是QMainWindow）的中央部件，以便显示在窗口中
```

#### 组件类型与控制

1. layout.addStretch(int weight):控制组件间的间距
2. QVBoxLayout:垂直布局管理器
3. QHBoxLayout:水平布局管理器
4. QGridLayout:网格布局管理器，QGridLayout.addWidget(widget, row, column)
5. QFormLayout:QLabel配合QLineEdit()使用，应用QFormLayout.addRow(label, QLine)加入每行表单
6. QStackedLayout:堆叠布局管理器，在一个窗口中管理多个窗口，同时刻只能显示一个

```python
import sys
from PyQt5.QtWidgets import QApplication, QMainWindow, QWidget, QPushButton, QLabel, QVBoxLayout, QStackedLayout

class MainWindow(QMainWindow):
    def __init__(self):
        super().__init__()
        self.setWindowTitle("Stacked Layout Example")
        
        self.stacked_layout = QStackedLayout()
        page1 = self.create_page("Page 1 Content", "Switch to Page 2")
        page2 = self.create_page("Page 2 Content", "Switch to Page 1")
        self.stacked_layout.addWidget(page1)
        self.stacked_layout.addWidget(page2)

        central_widget = QWidget()
        central_widget.setLayout(self.stacked_layout)
        self.setCentralWidget(central_widget)

    def create_page(self, content_text, switch_button_text):
        layout = QVBoxLayout()
        content_label = QLabel(content_text)
        switch_button = QPushButton(switch_button_text)
        switch_button.clicked.connect(self.switch_page)
        layout.addWidget(content_label)
        layout.addWidget(switch_button)

        page = QWidget()
        page.setLayout(layout)
        return page

    def switch_page(self):
        # 切换页面
        current_index = self.stacked_layout.currentIndex()
        next_index = (current_index + 1) % 2  # 切换到下一页（循环切换）
        self.stacked_layout.setCurrentIndex(next_index)

if __name__ == "__main__":
    app = QApplication(sys.argv)
    window = MainWindow()
    window.show()
    sys.exit(app.exec_())
```

### 常用组件

**窗口组件**
	QWidget	所有用户界面对象的基类，用于创建窗口和部件。
	QMainWindow	主窗口的类，通常用作应用程序的主界面。
**基础组件**
	QLabel	显示文本或图像。
	QLineEdit	输入单行文本。
	QTextEdit	输入多行文本。
	QSpinBox	（数字）整数输入框。
	QDoubleSpinBox	（数字）浮点数输入框。
	QPushButton	按钮。
	QRadioButton	单选按钮。在多个选项中进行单选。
	QCheckBox	复选框。在多个选项中进行多选
	QGroupBox	分组框。将其他小部件放置在其中
	QSlider	滑动条。
	QTabWidget	选项卡界面。
	QComboBox	下拉列表框。
**对话框类 - 组件**
	QDialog	自定义对话框
	QInputDialog	获取用户输入对话框
	QFontDialog	字体对话框。
	QColorDialog	颜色对话框。
	QProgressDialog	进度对话框。
	QFileDialog	打开文件/文件夹对话框。
	QMessageBox	消息提示框。
**菜单类 - 组件**	
	QMenu	菜单。
	QMenuBar	菜单栏。
	QToolBar	工具栏。
	QStatusBar	状态栏。
	QProgressBar	进度条。
**绘图类 - 组件**
	QGraphicsScene	管理2D图形项的场景。
	QGraphicsView	显示二维图形和图像。
	QGraphicsItem	在QGraphicsScene中显示图形项。
	QTableView	显示表格数据。
	QTreeWidget	显示树形数据。
	QListWidget	显示列表数据。
	QCalendarWidget	显示日历。
	QDockWidget	创建可停靠的面板。
	QSplitter	在界面中创建可调整大小的分割区域。
	QScrollArea	显示超过容器尺寸的内容，并支持滚动查看。