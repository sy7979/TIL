### SSAFY StartCamp-Day2 (2019.07.09)

### 프로그램 다운로드

![1562659947461](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562659947461.png)



1. python

   python.org --> PATH에도 체크하기

2. git.bash

   Adjusting your PATH environment에서 use git and optional **Unix** tool 체크.(unix os에 익숙해지기 위해?!)

   터미널에 접근하기 위해서 이제부터  git.bash사용할게요.

3. vscode

   Visual Studio Code, 앞으로 여기서 코드작성할거에요. 바탕화면 바로가기 만들기 기타 사항 4가지 모두 체크



#### 들어가기 전에: CLI를 알아보자 (명령 줄 인터페이스)

CLI = Command Line Interface (조작, 구동하는 역할)

Interface란? 조작, 구동하는 역할, 예를 들면 키보드, 마우스!!

키보드와 마우스 이전의 인터페이스가 CLI입니다. 키보드와 마우스보다 좀 더 개발자스러운 인터페이스라고 말할 수 있습니다. 예를 들면 git.bash의 까만 화면!!



1. CLI 종류 

   유닉스 쉘(bash, sh, zsh 등)
   CP/M

   

2. bash 명령어 기초

   1. ls (list의 약자) : 내 폴더에 있는 파일들을 나타내는 명령어

   2. pwd (present work ): 나의 폴더 위치가 어디있는지 알려주는 것 항상 내 위치가 어디있는지 확인해야한다!! 중요!

      왜 중요할까? 탐색기 안에서 처럼 직관적으로 볼 수 없다. 내가   pwd 로 검색하여 지금 위치가 어딘지 직접 확인해야암

   3. cd(change directory): 내가 있는 폴더를 변경한다.

      cd 폴더명 을 입력하면 ~ 뒤에 내가 있는 폴더(폴더명)가 뜬다.

      .하나는 현재 폴더 

      ..두 개는 상위 폴더

      cd ..  하면 폴더 한 단계 밖(상위 폴더)으로 나오게 된다.

      cd ~  하면 홈 폴더로 나올 수 있다.

      cd 입력 후 Tab을 누르면 폴더 명이 나온다

      폴더가 여러 개일 경우 Tab 을 두 번 누르면 폴더명을 나열하여 보여준다.

      폴더 뒤에는 / 표시가 뜬다 

      예   StartCamp/

      

   4. mkdir (make directory): 새로운 폴더를 만드는 일 = 새폴더 만들기와 똑같은 일

      mkdir 폴더명 입력하면 내가 입력한 폴더명의 폴더가 만들어짐

      예) mkdir startcamp  --> startcamp폴더가 생성된다.

      만약 폴더명이 너무 길면?

      cd하고 0적고 tab을 누르면 내가 입력한 폴더를 자동으로 찾아준다.

   5. toucht :  파일을 만들어준다.

      touch day1.md라고 하면 ~뒤 폴더에 이파일을 만드렁준다

   6. rm (remove)

      rm day1.md

      rm -r 폴더명 : 폴더를 지우리는 명령어

      code .  code를 현재 파일에서 열어줘

      하면 vscod가 뜨는데

      ctrl+Shift+p 누르고 Terminal: Select default Shell 누르면 CLI에서 bash로 바뀐다.

   7. mw (move) : 저장 위치 옮기기

      mw 내위치 옮길위치

      mw 내위치 ..    --> 상위 폴더로 옮긴다.

      파일 이름을 바꿀떄도   mv 사용!

      $ mv 99_장정식.txt 99_오창희.txt  --> 이름을 99 장정식에서 99 오창희로 바꾼다/

      

#### VSCODE 이용하기 (윗창: 코드작성, 아래창: 실행명령)

1.

-윗창에


```python
import webbrowser



webbrowser.open('naver.com')

webbrowser.open_new_tab('goole.com')

# **저장!!**(ctrl s 꼭 눌러야한다.)
```



-아래창(bash)에

```python
student@DESKTOP MINGW64 ~/startcamp
$ python browser.py
```
실행 결과 : naver.com 브라우져가 뜬다!



2.

-윗창에

```python
import webbrowser

url = "https://search.naver.com/search.naver?sm=top_hty&fbm=1&ie=utf8&query="
my_keywords = ["iu", "bts", "winner", "샤이니"]
for my_keyword in my_keywords:
    webbrowser.open(url + my_keyword)
```


url = "https://search.naver.com/search.naver?sm=top_hty&fbm=1&ie=utf8&query="   --> 뒤 url은 네이버에 직접 검색해 보고 뜬 url 복사해서  query  뒤에 검색한 값만 지워준것!

**저장!!**

-아래창에

```python
student@DESKTOP MINGW64 ~/startcamp
$ python browser.py
```
실행 결과: "iu", "bts", "winner", "샤이니"에 대한 검색결과가 뜬다!



#### 정보 스크랩하기

1. naver에 들어간다.
2. 정보를 검색한다.
3. 원하는 정보만 복사한다.
4. 내컴퓨터에 저장한다.



-아래창 
```
$ pip install requests   
```
-->  request라는 툴이 없기 때문에 외부로부터 다운로드 설치를 하는 과정이 필요하다.

-위 창
```python
import requests
```
-아래창 
```python
python requests
```

-윗 창

```python
import requests


res = requests.get("https://naver.com")

print(res)
```

-아래 창

```python
student@DESKTOP MINGW64 ~/startcamp
$ python kospy.py
<Response [200]>
```


-윗 창
```python
import requests



res = requests.get("https://naver.com")

print(res.text) -->text만 뽑아달라는 의미
```


-아래 창
```python
student@DESKTOP MINGW64 ~/startcamp
$ python kospy.py
```

~~ 참고 ctlr l 지우기, ctrl f 찾기~~ 


```python
student@DESKTOP MINGW64 ~/startcamp
$ pip install bs4
```
```python
import requests 
```
from bs4 import BeautifulSoup -->bs4라는 공구상자 안에서 BeautifulSoup(text정보를 예쁘게 정리해주는 툴)을 꺼내줘





최종적으로

-윗 창
```python
import requests

from bs4 import BeautifulSoup



res = requests.get("https://finance.naver.com/sise/").text

soup = BeautifulSoup(res)

print(soup)
```


-아래 창
```python
student@DESKTOP MINGW64 ~/startcamp
$ python kospy.py
```


사람눈에는 똑같아보이는데 python입장에서 잘 정리된 결과로 나타난다.



#### 문서안에 있는 특정 내용을 뽑기

#### . select(selector)

:정보(들)을 가져온다

-윗 창

```python

import requests

from bs4 import BeautifulSoup



res = requests.get("https://finance.naver.com/sise/").text

soup = BeautifulSoup(res, 'html.parser')

kospi = soup.select('#KOSPI_now') 

#[^#KOSPI_now]: #KOSPI_now 이 정보는 네이버 주식 웹 상에서 가져오고 싶은 정보 마우스 오른쪽, 검사 까지 누르면 F12로 뜬 창에 파란 줄로 표시가 된다/ 거기서 마우스 오른쪽,Copy, Copy Selector 누르면 복사가 된다! 꼭 따옴표 안에 작성!! 그리고 저장 꾹!!

print(kospi)
```


-아래창 
```python
student@DESKTOP MINGW64 ~/startcamp
$ python kospy.py
```
결과는?!  [<span class="num num2" id="KOSPI_now">2,062.09</span>

코스피는 계속 변동이 일어나는 데이터이기 때문에 다시 실행하면 값이 바뀐다.

대괄호[] = 리스트 표시, 리스트 안에 잇는 데이터 중 하나의 데이터

id는 혼자 선점 unique한 값 --> #으로 표시

#KOSPI_now : id가 KOSPI_now 인 값을 의미



@@안되는 것 : 네이버 실시간 검색순위 1위

![1562645701253](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562645701253.png)

==> 수정 사항 : elect_one 뒤를 (".ah_k")로 수정하면 값이 나온다.

==> 실행이 안됐던 이유: select_one 뒤의  입력이 잘못 된 것! 동적인 화면은 이런 현상이 일어날 수 있다,,,, 왜인지는 이해가 안 됌..ㅜㅜ





#### .select_one(selector)

: 하나의 정보만 가저온다.

import requests

from bs4 import BeautifulSoup



res = requests.get("https://finance.naver.com/sise/").text

soup = BeautifulSoup(res, 'html.parser')

kospi = soup.select_one('#KOSPI_now')



print(kospi.text)



text는 >와 <사이 있는 값 ==> 

 student@DESKTOP MINGW64 ~/startcamp
$ python kospy.py
2,065.12

==> 결과가 숫자로만 나옴

why? 웹 상 개발자 화면에서 <span id="KOSPI_now" class="num">2,065.31</span>



크롤링 스크랩핑 ==> 웹페이지 검사해서 나오는 결과를 복사해 가져오는것. 하지만 완전 동적인 정보들은 못가져오는 페이지들은..  문제가 생길 수 있어요

@ 실시간 검색 순위 
for 구문을 

![1562661973041](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562661973041.png)

#### Faker

랜덤의 값들을 불러오는 함수

-윗 창

from faker import Faker

f = Faker('ko_KR')

-->한국어 지원 가능(KR)

print(f.name())



-아래 창

student@DESKTOP MINGW64 ~/startcamp/students
$ python files.py
윤영진



![1562639797838](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562639797838.png)

주의 사항 f = Faker('ko_KR')이 for 문의 위에 있어야 한다. 그래야 불러올 수 있다.



![1562639970813](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562639970813.png)



랜덤한 이름으로 100개의 file이 만들어 진다.



#### os 모듈 사용

os = operating system

![1562641084608](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562641084608.png)

파일 새로 생성 ==> os.chdir



![1562641227308](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562641227308.png)

파일 이름 앞에 SAMSUGN 붙이기 ==> os.listdir / os.rename(원래 이름, 바꿀 이름)

r의 의미? 아직 몰라도 됌



![1562646361467](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562646361467.png)

SAMSUNG_을 SSAFY 로 바꾸기





#### +

문자열끼리 +는 연결하라는 의미



#### 환율

-환율정보 불러오는 법

![1562649297762](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562649297762.png)



tbody > tr   --> tbody 안에 있는 tr 을 불러온다



-환율정보에 나라 이름까지 불러오기

![1562649417623](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562649417623.png)

strip() --> 여백이 너무 커서 날려주는 함수





#### Git

##### git 이전에는 수정을 반복할 때 자료간 뭐가 바뀌었는지 알 수 없다

버전관리 시스템

코드의  history 를 관리하는 도구

개발된 과정과 역사를 볼 수 있으며, 프로젝트의 이전 버전을 복원하고 변경 사항을 비교, 분석 및 병합도 가능



작업한 파일(Working directory)--> add -->커밋할 목록(Index, staging area)--> commit --> 쌓인 커밋들(HEAD)--> push-->  GitHub



![1562656386041](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562656386041.png)





-상대방이 올린거 가져오기

![1562658800467](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562658800467.png)

링크 복사



![1562656962548](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562656962548.png)



-상대방이 수정한거 가져오기(pull)

![1562657884933](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562657884933.png)

-내가 수정한거 올리기(push)

![1562657979771](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562657979771.png)

```

```