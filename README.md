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

실행 코드에서 필요한 모듈
```python
import sys # 파이썬 인터프리터를 제어
from PyQt5.QtWidgets import * # PyQt5의 Widget을 사용
from PyQt5 import uic # PyQt5 확장자 ui를 python에서 로드
```
