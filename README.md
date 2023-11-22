# PyQt5-memo
# PyQt5를 사용하여 윈도우 프로그램 메모장 만들기
## 만드는 절차
- 레이아웃
- 메뉴바
- 열기, 저장 기능
- 다른 이름으로 저장
- 클로즈 이벤트
- 메시지 박스 띄우기
### 1. PyQt5 메모장 - 레이아웃 만들기 
- QT 디자이너
QT 디자이너에서 Main Window 폼을 생성한다.

![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/01ceb015-6b17-4f56-86bc-654b513bf7d7)

여기에 Layout에 있는 Grid Layout를 생성한다.

![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/774a76db-d652-4e8f-99c8-fa3636a4ef6d)

그리고 centralwidget을 클릭 후 격자형 배치로 바꾸고 Layout에 margin의 크기를 전부 0으로 맞춰준다.

![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/4f158248-cb81-4ff5-8e28-c20f7baf294c)

![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/b9c6c642-1a3a-4c47-90cc-97c3d7905641)

마지막으로 Input Widgets에 있는 Plain Box를 배치하면 레이아웃이 완성된다.

![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/1400a01c-82d2-4e4a-a5fd-7fedbd233f8d)

- 파이썬
```python
import sys
from PyQt5.QtWidgets import *
from PyQt5 import uic
// 디자이너에 사용되는 위젯에 모든 라이브러리를 가져온다.
// ui파일을 클래스 파일로 사용할 수 있게 해주는 라이브러를 uic도 가져온다.


form_class = uic.loadUiType("C:\\Users\\MOA\\Desktop\\QtDesigner\\파이큐티\\파이큐티 두번째 - 메모장\\memo.ui")[0]
// ui 파일 경로를 가져와서 uic.loadUiType 함수에 넣게 되면 ui파일을 클래스 파일로 사용할 수 있게된다.
class WindowClass(QMainWindow, form_class):
    def __init__(self):
// init에 self에는 인스턴스 자체가 전달되어 있어 메소드 내에 인스턴스 변수 작성, 참고가 가능해진다.
        super().__init__()
// 부모클래스를 상속시킨다.
        self.setupUi(self)
// 연결한 ui파일을 준비한다.
        
app = QApplication(sys.argv)
// pyqt를 실행한다.
mainWindow = WindowClass()
mainWindow.show()
app.exec_()
```
### 2. PyQt5 메모장 - 메뉴바 만들기
### 3. PyQt5 메모장 - 열기, 저장 기능 만들기 
### 4. PyQt5 메모장 - 다른 이름으로 저장 기능 만들기
### 5. PyQt5 메모장 - 클로즈 이벤트 만들기
### 6. PyQt5 메모장 - 메시지 박스 띄우기 만들기
