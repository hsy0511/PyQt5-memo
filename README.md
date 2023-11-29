# PyQt5-memo
# PyQt5를 사용하여 윈도우 프로그램 메모장 만들기
출처 : 재즐보프[유튜브] 
링크 : https://www.youtube.com/playlist?list=PLnIaYcDMsScwsKo1rQ18cLHvBdjou-kb5

## 메모장 파일 저장하기
### 실행화면
![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/dab3d164-16e4-4872-961f-d332af689a41)


https://github.com/hsy0511/PyQt5-memo/assets/104752580/43d5f0ad-c1ac-4d69-b4ea-49d3fe7b76f1


### PyQt 
1. 레이아웃 만들기
- Qt Designer에서 Plain Text Edit를 삽입한다.

![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/a53baa5f-3e70-4ae9-ab60-46a5c261ef32)

- MainWindow를 경자형으로 배치하여 Plain Text Edit를 화면에 맞게 맞춘다. 

![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/de99f3ae-5cf8-4e6f-bca2-8794a46c5ef2)

- centralwidget의 margin을 0으로 맞추어 화면이 꽉차도록 한다.

![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/20c01bfe-929f-44af-97e1-fe58946e897c)

2. 메뉴바 만들기

- 화면 위에있는 "여기에 입력하십시오."라는 문구가 써져있는 곳을 더블 클릭하여 메뉴를 삽입한다.

![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/0529dc27-9538-47f1-94f5-5d57d5feb7dc)

3. 각 메뉴바에 알맞은 기능 넣기

- 메뉴를 클릭하면 "여기에 입역하십시오." 라고 문구가 써져있는 곳에 기능 이름을 삽입한다.
※ 주의사항 : 기능 이름을 삽입하는 곳은 한글이 사용되지 않으므로 메모장에 적어서 복사 붙여넣기를 해야한다.

![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/244b3e99-2c30-44d0-89d6-bd0605d93dd5)

4. 기능 단축키 설정

- 메뉴의 기능을 클릭하고 오른쪽 목록에 shortcut를 이용하여 단축키를 설정한다.

![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/fceba154-b428-4e04-b779-724a195254e5)

5. 폼 완성
- 폼 - 미리보기를 통해 폼을 확인할 수 있다.

![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/9d0b5b30-0861-48e1-942b-e30bec8821b4)
![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/0913bbcf-eeae-4938-b18c-8b9fc39dffc9)
![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/39215a1c-2be4-466e-93f0-36588d0e7b44)
![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/29b934d5-8a55-44ca-ac2a-818c61562ec1)
![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/b59f5527-5d72-44a5-b585-ecdbbdedbc48)
![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/a64f4d94-07f1-4fe7-a570-6ae2ce30de40)

### Python code
- 전체 소스코드 (맨 밑에 코드해석)

```python
import sys
from PyQt5.QtWidgets import *
from PyQt5 import uic



form_class = uic.loadUiType("C:\\Users\\MOA\\Desktop\\QtDesigner\\파이큐티\\파이큐티 두번째 - 메모장\\memo.ui")[0]
        
class WindowClass(QMainWindow, form_class):
    def __init__(self):
        super().__init__()
        self.setupUi(self)
        
        self.action_open.triggered.connect(self.openFunction)
        self.action_save.triggered.connect(self.saveFunction)
        self.action_saveas.triggered.connect(self.saveAsFunction)
        self.action_close.triggered.connect(self.close)
        
        self.opened = False
        self.opened_file_path = '제목 없음'
        
    def ischanged(self): 
        if not self.opened:
            if self.plainTextEdit.toPlainText().strip():
                return True
            return False
        
        current_data = self.plainTextEdit.toPlainText()
         
        
        with open(self.opened_file_path , encoding='UTF8') as f:
            file_data = f.read()
            
        if current_data == file_data:
            return False
        else:
            return True
        
    def save_changed_data(self):        
        msgBox = QMessageBox()
        msgBox.setText("변경 내용을 {}에 저장하시겠습니까?".format(self.opened_file_path))
        msgBox.addButton('저장', QMessageBox.YesRole)
        msgBox.addButton('저장 안 함', QMessageBox.NoRole)
        msgBox.addButton('취소',QMessageBox.RejectRole)
        ret = msgBox.exec_()
        
        if ret == 0:
            self.saveFunction()
        else:
            return ret 
        
    def closeEvent(self, event):
        if self.ischanged():             
            ret = self.save_changed_data()
            
            if ret == 2:
                event.ignore()               
        
    def save_file(self,fname):
        data = self.plainTextEdit.toPlainText()
                        
        with open(fname[0], 'w', encoding='UTF8') as f:
                 f.write(data)
                 
        self.opened = True
        self.opened_file_path = fname
                 
        print("save {}!!".format(fname))  
        
    def open_file(self,fname):
        with open(fname, encoding='UTF8') as f:
            data = f.read()
        self.plainTextEdit.setPlainText(data)
        
        self.opened = True
        self.opened_file_path = fname
        
        print("open {}!!".format(fname))
        
        
    def openFunction(self):
        if self.ischanged():             
            ret = self.save_changed_data()
            
        fname = QFileDialog.getOpenFileName(self)
        if fname[0]:
            self.open_file(fname[0])
    
    def saveFunction(self):
        if self.opened:
            self.save_file(self.opened_file_path)  
        else:
            self.saveAsFunction()    
            
    
    def saveAsFunction(self):    
        fname = QFileDialog.getSaveFileName(self)
        if fname[0]:
            self.save_file(fname[0])     
                      
app = QApplication(sys.argv)
mainWindow = WindowClass()
mainWindow.show()
app.exec_()

```

### python code 해석

- 실행 코드에서 필요한 모듈

```python
import sys # 파이썬 인터프리터를 제어
from PyQt5.QtWidgets import * # PyQt5의 Widget을 사용
from PyQt5 import uic # PyQt5 확장자 ui를 python에서 로드
```

- GUI와 Python에 연동

```python
form_class = uic.loadUiType("C:\\Users\\MOA\\Desktop\\QtDesigner\\파이큐티\\파이큐티 두번째 - 메모장\\memo.ui")[0] 
# uic.loadUiType 메서드를 통해 해당 ui 파일을 class 형태로 변환

class WindowClass(QMainWindow, form_class): # QMainWindow와 form_class를 WindowClass에 다중상속
    def __init__(self): # class가 호출되었을 때 초기값
        super().__init__() # 부모 클래스의 초기값 호출
        self.setupUi(self) # 구성한 UI를 화면에 출력
```

- 메뉴바 기능 연동

```python
self.action_open.triggered.connect(self.openFunction) # GUI에서 action_open을 클릭했을 때 openFunction 함수 기능이 실행된다.
self.action_save.triggered.connect(self.saveFunction) # GUI에서 action_save을 클릭했을 때 saveFunction 함수 기능이 실행된다.
self.action_saveas.triggered.connect(self.saveAsFunction) # GUI에서 action_saveas을 클릭했을 때 saveAsFunction 함수 기능이 실행된다.
self.action_close.triggered.connect(self.close) # GUI에서 action_close을 클릭했을 때 closeEvent 함수 기능이 실행된다.
```

- 기본 메모장 파일명

```python
self.opened = False # 열려져 있는 파일이 아님
self.opened_file_path = '제목 없음' # 열려져있는 파일이 아닐 때 파일명을 제목없음으로 표시해놓는다.
```

![image](https://github.com/hsy0511/PyQt5-memo/assets/104752580/e01a99c2-85cd-46a2-9c1c-3ba3a7c2f72a)

- ischanged 함수 (현재 내용이 변경되었는지 확인)

```python
    def ischanged(self):
        # 만약 현재 파일이 열려 있지 않다면
        if not self.opened:

            # 현재 텍스트 편집기에 텍스트가 있으면 변경된 것으로 간주합니다.
            if self.plainTextEdit.toPlainText().strip():
                return True
            return False

        # 현재 파일이 열려 있다면
        current_data = self.plainTextEdit.toPlainText()
         
        # 파일이 열려 있는 경우 해당 파일의 내용을 읽어옵니다.
        with open(self.opened_file_path , encoding='UTF8') as f:
            file_data = f.read()

        # 파일이 열려 있는 경우 해당 파일의 내용을 읽어옵니다.
        if current_data == file_data:
            return False
        else:
            return True
```

- save_changed_data 함수 (변경된 데이터를 저장할지 물어보는 팝업창)

```python
    def save_changed_data(self):
        # QMessageBox 인스턴스를 생성합니다
        msgBox = QMessageBox()

        # 팝업창에 표시될 메시지를 설정합니다.
        msgBox.setText("변경 내용을 {}에 저장하시겠습니까?".format(self.opened_file_path))

        # 버튼을 추가하고 버튼에 대응하는 역할을 할당합니다.
        msgBox.addButton('저장', QMessageBox.YesRole)
        msgBox.addButton('저장 안 함', QMessageBox.NoRole)
        msgBox.addButton('취소',QMessageBox.RejectRole)

        # 팝업창을 표시하고 사용자의 선택을 반환합니다.
        ret = msgBox.exec_()

        # 사용자가 '저장'을 선택한 경우
        if ret == 0:
            # saveFunction 메서드를 호출하여 데이터를 저장합니다.
            self.saveFunction()
        else:
            # 사용자가 '저장 안 함' 또는 '취소'를 선택한 경우 해당 선택 값을 반환합니다.
            return ret 
```

- closeEvent 함수 (창을 닫을 때 동작)

```python
    def closeEvent(self, event):

        # 만약 현재 편집 중인 내용이 있다면
        if self.ischanged():

            # 변경된 내용을 저장할지 묻는 메시지 다이얼로그를 표시하고 사용자의 선택을 받습니다.
            ret = self.save_changed_data()

            # 사용자가 '취소'를 선택한 경우 창을 닫지 않도록 이벤트를 무시합니다.
            if ret == 2:
                event.ignore()
```

- save_file 함수 (파일 저장)

```python
    def save_file(self,fname):
        # 현재 텍스트 편집기의 내용을 가져옵니다.
        data = self.plainTextEdit.toPlainText()

        # 지정된 파일 경로에 텍스트를 쓰기 모드로 열어 저장합니다.
        with open(fname[0], 'w', encoding='UTF8') as f:
                 f.write(data)

         # 파일이 성공적으로 저장되었음을 표시하기 위해 상태 변수를 업데이트합니다.        
        self.opened = True
        self.opened_file_path = fname

        # 저장 완료 메시지를 출력합니다.
        print("save {}!!".format(fname))
```

- open_file 함수 (파일 열기)

```python
    def open_file(self,fname):

        # 지정된 파일을 읽기 모드로 열어서 내용을 읽어옵니다
        with open(fname, encoding='UTF8') as f:
            data = f.read()

        # 읽어온 내용을 텍스트 편집기에 표시합니다.
        self.plainTextEdit.setPlainText(data)

        # 파일이 성공적으로 열렸음을 나타내기 위해 상태 변수를 업데이트합니다.
        self.opened = True
        self.opened_file_path = fname

        # 열기 완료 메시지를 출력합니다.
        print("open {}!!".format(fname))
```

- openFunction 함수 (파일 열기 팝업를 열고, 변경 여부를 확인하고 처리)

```python
   def openFunction(self):

    # 현재 편집 중인 내용이 있다면
    if self.ischanged():

        # 변경된 내용을 저장할지 물어보는 메시지 다이얼로그를 표시하고 사용자의 선택을 받습니다.
        ret = self.save_changed_data()

    # 파일을 열기 위한 다이얼로그를 표시하고 사용자가 선택한 파일의 경로를 받습니다.
    fname = QFileDialog.getOpenFileName(self)

    # 사용자가 파일을 선택한 경우
    if fname[0]:

        # 선택한 파일을 열어서 내용을 편집기에 표시합니다.
        self.open_file(fname[0])
```

- saveFunction 함수 (저장 메서드)

```python
def saveFunction(self):

    # 만약 현재 파일이 열려 있다면
    if self.opened:

        # 현재 열려 있는 파일에 저장합니다.
        self.save_file(self.opened_file_path)
    else:

        # 현재 열려 있는 파일이 없는 경우 "다른 이름으로 저장" 다이얼로그를 열어 사용자에게 저장할 파일을 지정하도록 합니다.
        self.saveAsFunction()

```

- saveAsFunction 함수 (다른 이름으로 저장 메서드)

```python
def saveAsFunction(self):

    # "다른 이름으로 저장" 다이얼로그를 엽니다.
    fname = QFileDialog.getSaveFileName(self)

    # 사용자가 파일을 선택한 경우
    if fname[0]:

        # 선택한 파일에 현재 편집 중인 내용을 저장합니다.
        self.save_file(fname[0])
```


- GUI 실행

```python
app = QApplication(sys.argv) #  PyQt 애플리케이션 초기화
  mainWindow = WindowClass() # WindowClass 클래스의 인스턴스 생성
mainWindow.show() # GUI를 실행하여 화면에 출력된다.
app.exec_() # PyQt 애플리케이션의 메인 루프 시작
```
