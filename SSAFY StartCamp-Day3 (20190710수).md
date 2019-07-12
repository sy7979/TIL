### SSAFY StartCamp-Day3 (20190710수)



git.bash에서

초록색 U : untrackted 아직 깃에 업로드 되지 않았다.

w = write



#### 파일 만들기

```python
f = open('student.txt', 'w')

f.write("안녕하세요")

f.close()


```

```python
student@DESKTOP MINGW64 ~/startcamp/file (master)
$ python make_file.py
```

@@ ctrl + / 하면 주석처리 되서 실행이 되지 않는다



#### with open(A) as f : 오픈으로 열린 A파일을 f라고 부르겠다.


#### csv 
comma seperated values

각 라인의 컬럼들이 콤마로 분리된 텍스트 파일 포맷

엑셀처럼 데이터 표로 정리해주는 기능



lunch 는 딕셔너리. 정의데이터 만들때 사용



확장자와 프로그램은 다르다.

확장자: hwp, doc 등등



*text보다 csv 형식으로 데이터를 저장하는게, 다루기가 더 쉽다.*



#### csv_file.py

```python
import csv

lunch = {
    "BBQ":"123456",
    "중국집":"456789",
    '한식':"7411852"
}

with open("lunch.csv", 'w', encoding="utf-8", newline="") as f:
    csw_writer = csv.writer(f)

    for item in lunch.items():
        csw_writer.writerow(item)
```

결과

![1562727410191](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562727410191.png)

엑셀처럼 표로 정리하려면 확장에서 excel viewer다운로드 

![1562727640843](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562727640843.png)

![1562727545414](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562727545414.png)

가게, 전화번호 입력하면 아래와 같이 

![1562727606898](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562727606898.png)

예쁘게 정리 가능!



### crawling + csv

크롤링한 정보를 csv로 보기 편하게 구성해보자



##### 1. exchange_csv.py

환율 csv형식으로 가져오기

웹에서 크롤링을 할 때 html을 이해하는것이 우선이에요!

```python
import csv
import requests
from bs4 import BeautifulSoup


url = "https://finance.naver.com/marketindex/exchangeList.nhn"
res = requests.get(url).text
soup = BeautifulSoup(res, "html.parser")

tr =  soup.select('tbody > tr')
with open("naver_exchange.csv", 'w', encoding='utf-8', newline="") as f:
    csv_writer = csv.writer(f)
    for r in tr:
        print(r.select_one('.tit').text.strip())
        print(r.select_one('.sale').text)
        row = [r.select_one('.tit').text.strip(), r.select_one('.sale').text]
        csv_writer.writerow(row)
```



##### 2. csv_bittumb.py

코인 이름 현 가격 csv 형식으로 가져오기

```python
import csv
import requests
from bs4 import BeautifulSoup


url = "https://www.bithumb.com/"
res = requests.get(url).text
soup = BeautifulSoup(res, "html.parser")

tr =  soup.select('tbody > tr')
with open("bithumb.csv", 'w', encoding='utf-8', newline="") as f:
    csv_writer = csv.writer(f)
    for r in tr:
        print(r.select_one('.sort_coin').text.strip())
        print(r.select_one('.sort_real').text)
        row = [r.select_one('.sort_coin').text.strip(), r.select_one('.sort_real').text]
        csv_writer.writerow(row)

```

코인의 종류를 나타내는 정보의 class가 안떠서 r.select_one()에 입력할 수 없었음,

html의 구성을 이해해야 이 문제를 해결할 수 있다는데,, 어떻게 해야할까???



##### 3. csv_flightticket.py

실행 안 됌ㅜㅜㅜㅜ

..  세 가지 정보가 동시에 뜨게 하고 싶었는데,, 머가 문제일까??

```python
import csv
import requests
from bs4 import BeautifulSoup

# 에러도 안뜨고 실행도 안되고!!

url = "https://flyairseoul.com/I/KO/viewAvail.do"
res = requests.get(url).text
soup = BeautifulSoup(res, "html.parser")

tr =  soup.select('tbody > td')
with open("airseoul.csv", 'w', encoding='utf-8', newline="") as f:
    csv_writer = csv.writer(f)
    for r in tr:
        print(r.select_one('.tb1-start-time').text.strip())
       # print(r.select_one('.point-color02').text)
        print(r.select_one('.bookint-airlineticket-minimum-date').text)
        
        row = [r.select_one('.tb1-start-time').text.strip(),r.select_one('.bookint-airlineticket-minimum-date').text] # r.select_one('.point-color02').text] #r.select_one('.bookint-airlineticket-minimum-date').text]
        csv_writer.writerow(row)
```



#### HTML

공통 형식

``` python
<태그이동 속성명="속성값"></태그이동>
```

속성명 추가

```python
<태그이동 속성명="속성값" 속성명2="속성값2"></태그이동> 
```

@@ 띄어쓰기 잊지마유

@@ ctlr / : 모든 프로그램에서 주석 의미



HTML이란? 어떤 글자를 적기위한 문서

​	(HTML을 사람들이 보기 좋게 하는 것이 웹브라우져)

​	파일을 실행시키면 연결프로그램으로 크롬 등을 연결 시킬 수 있다

​	Hypertext를 만드는 언어, 일반 text보다 한 단계 위의 기능을 포함한 text.

​	문서를 표기하기 위한 언어, 글의 순서와는 상관 없이, 단어를 클릭하면  **link**로 문서와 문서가 바로 연결 되게끔 	한다.



html은 여는태그(<h1>)와 닫는 태그(</h1>)로 구성이 된다.

h1 : 대제목 

href :hypertext reference 

a : anchor (닻)링크를 연결시켜준다. 



ol : ordered list



html 의 필수 요소

```python
<!DOCTYPE html>
<html>
    <head></head>
    <body>
      # 이 사이에 코드 입력  
    </body>
</html>
```

@@ alt +방향키 : 이동

@@ body보다 한 단계 안쪽으로 이동해서 코드 작성을 시작해야한다. 

파일 정리하듯이 같은 위치에 있는 폴더는 같은 선상에, 상하 관계 폴더는 한단계 위 아래로!

예를 들면 폴더 정리할 때

![1562733711223](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562733711223.png)



html도 마찬가지로 이런식으로 정리하는 습관 꼭 들이세요! 상위 하위 level을 구분하기 위해서!



#### W3

www을 만드는 국제 표준화 기구

https://www.w3schools.com/html/ : html 공부할 수 있는 튜토리얼 사이트

html reference에 html tag list 활용하세요, attribute에 활용할 수 있는 것이 같이 나타남



![1562735252024](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562735252024.png)





@@ .과 #의 의미

.(마침표) : class 의미

#(샵) : id 의미



#### background-color

h1은 빨간색 class는 파란색 충돌이 일어났을 떄 class가 우선순위가 우위

우선순위

id>class>h

id는 중복 되면 안된다. 클래스는 중복되도 상관 없음.



#### html + css 

css는 <sytle></style> 안에 표시해서 html과 분리한다.

```html
<!DOCTYPE html>
<html>
    <head>
        <style>
            h1 {
                background-color:red;
            }
            a {
                color:brown;
            }
            .blue {
                background-color:blue;
            }
            #git {
                background-color:black;
            }
        </style>
    </head>
    <body>
        <h1>HTML</h1>
        <h1 class="blue">CSS</h1>
        <h2 class="blue">HyperText Markup Language</h2>
        <a href="https://naver.com">네이버</a>
        
        <!-- <태그이동 속성명="속성값" 속성명2="속성값2"></태그이동>  -->
        
        <h3 class="blue">우리가 공부한것<strong>ssafy</strong></h3>
        <ol>
            <li><strong><i>파이썬</i></strong></li>
            <li id="git">HTML</li>
            <li id="git" class="blue">Git</li>
        
        </ol>
        
    </body>
</html>
```



#### html과 css를 다른 파일 상으로 분리하기

1. html 파일

html에서 쓴 style기능을 css 의 파일로 따로 분리할건데,  분리된 파일을 연결하는데 link 사용가 사용된다. (link tab하면 자동으로 뒷부분 입력 됨) 

link는 닫는 태그가 없다.(필요 없으니까)

```html
<!DOCTYPE html>
<html>
    <head>
        <link rel="stylesheet" href="./intro.css">  
        <!-- link를 추가한 부분. href 사이에 "./"를 입력하면 현재 폴더가 뜬다. 여기 뜨는 폴더로 link를 추가할 수 있다.-->
    </head>
    <body>
        <h1>HTML</h1>
        <h1 class="blue">CSS</h1>
        <h2 class="blue">HyperText Markup Language</h2>
        <a href="https://naver.com">네이버</a>
        
        <!-- <태그이동 속성명="속성값" 속성명2="속성값2"></태그이동>  -->
        
        <h3 class="blue">우리가 공부한것<strong>ssafy</strong></h3>
        <ol>
            <li><strong><i>파이썬</i></strong></li>
            <li id=>HTML</li>
            <li id="git" class="blue">Git</li>
        
        </ol>
        
    </body>
</html>
```



2. css 파일

```css
/* 여기는 css 파일입니다/ */
h1 {
    background-color:red;
}
a {
    color:brown;
}
.blue {
    background-color:blue;
}
#git {
    background-color:black;
}
```

@@ html과 css의 주석표시도 서로 다름 <!-- -->  /* */ 



#### Start Bootstrap

html계의 탬플릿이라고 생각하면 됩니다.

![1562738970846](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562738970846.png)

위에서부터 순서대로 입력하고 따라하기

주의 폴더 위치 잘 지정해서 그 폴더로 들어가세용





https://fontawesome.com/

![1562739611697](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562739611697.png)

![1562739623839](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562739623839.png)



https://sy7979.github.io/index.html

https://sy7979.github.io



http://tech.kakao.com/

https://spoqa.github.io/



https://jekyllrb-ko.github.io/ : 마크다운 문서를 게시물 형식으로 바꿔주는 기능



https://awesome-devblog.netlify.com/ 국내 개발자 블로그

http://woowabros.github.io/ 우아한 형제들 기술 블로그

=======
### SSAFY StartCamp-Day3 (20190710수)



초록색 u : untrackted 아직 깃에 업로드 되지 않았다.

w = write



#### 파일 만들기

f = open('student.txt', 'w')

f.write("안녕하세요")

f.close()

student@DESKTOP MINGW64 ~/startcamp/file (master)
$ python make_file.py



@@ ctrl + / 하면 주석처리 되서 실행이 되지 않는다



#### with open(A) as f : 오픈으로 열린 A파일을 f라고 부르겠다.



#### csv comma seperated values

각 라인의 컬럼들이 콤마로 분리된 텍스트 파일 포맷

엑셀처럼 데이터 표로 정리해주는//



lunch 는 딕셔너리. 정의데이터 만들떄 사용



확장자와 프로그램은 다르다.

확장자: hwp, doc 등등





text보다 csv 형식으로 데이터를 저장하는게, 다루기가 더 쉽다.



#### csv_file.py

```python
import csv

lunch = {
    "BBQ":"123456",
    "중국집":"456789",
    '한식':"7411852"
}

with open("lunch.csv", 'w', encoding="utf-8", newline="") as f:
    csw_writer = csv.writer(f)

    for item in lunch.items():
        csw_writer.writerow(item)
```

결과

![1562727410191](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562727410191.png)

엑셀처럼 표로 정리하려면 확장에서 excel viewer다운로드 

![1562727640843](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562727640843.png)

![1562727545414](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562727545414.png)

가게, 전화번호 입력하면 아래와 같이 

![1562727606898](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562727606898.png)



#### exchange_csv.py

코인 이름 현 가격 csv 형식으로 가져오기

웹에서 크롤링을 할 때 html을 이해하는것이 우선이에요!

```python
import csv
import requests
from bs4 import BeautifulSoup


url = "https://finance.naver.com/marketindex/exchangeList.nhn"
res = requests.get(url).text
soup = BeautifulSoup(res, "html.parser")

tr =  soup.select('tbody > tr')
with open("naver_exchange.csv", 'w', encoding='utf-8', newline="") as f:
    csv_writer = csv.writer(f)
    for r in tr:
        print(r.select_one('.tit').text.strip())
        print(r.select_one('.sale').text)
        row = [r.select_one('.tit').text.strip(), r.select_one('.sale').text]
        csv_writer.writerow(row)
```



#### csv_bittumb.py

```python
import csv
import requests
from bs4 import BeautifulSoup


url = "https://www.bithumb.com/"
res = requests.get(url).text
soup = BeautifulSoup(res, "html.parser")

tr =  soup.select('tbody > tr')
with open("bithumb.csv", 'w', encoding='utf-8', newline="") as f:
    csv_writer = csv.writer(f)
    for r in tr:
        print(r.select_one('.sort_coin').text.strip())
        print(r.select_one('.sort_real').text)
        row = [r.select_one('.sort_coin').text.strip(), r.select_one('.sort_real').text]
        csv_writer.writerow(row)

```



#### csv_flightticket.py

실행 안 됌

..  세 가지 정보가 동시에 뜨게 하고 싶었는데,,

```python
import csv
import requests
from bs4 import BeautifulSoup

# 에러도 안뜨고 실행도 안되고!!

url = "https://flyairseoul.com/I/KO/viewAvail.do"
res = requests.get(url).text
soup = BeautifulSoup(res, "html.parser")

tr =  soup.select('tbody > td')
with open("airseoul.csv", 'w', encoding='utf-8', newline="") as f:
    csv_writer = csv.writer(f)
    for r in tr:
        print(r.select_one('.tb1-start-time').text.strip())
       # print(r.select_one('.point-color02').text)
        print(r.select_one('.bookint-airlineticket-minimum-date').text)
        
        row = [r.select_one('.tb1-start-time').text.strip(),r.select_one('.bookint-airlineticket-minimum-date').text] # r.select_one('.point-color02').text] #r.select_one('.bookint-airlineticket-minimum-date').text]
        csv_writer.writerow(row)
```



#### HTML

공통 형식

``` python
<태그이동 속성명="속성값"></태그이동>
```

속성명 추가

```python
<태그이동 속성명="속성값" 속성명2="속성값2"></태그이동> 
```

@@ 띄어쓰기 잊지마유

@@ ctlr / : 모든 프로그램에서 주석 의미





어떤 글자를 적기위한 문서

(이걸 사람들이 보기 좋게 하는 것이 웹브라우져)

파일을 실행시키면 연결프로그램으로 크롬 등을 연결 시킬 수 있다

hypertext를 만드는 언어, 일반 text보다 한 단계 위의 기능을 포함한 text.

문서를 표기하기 위한 언어, 순서와는 상관 없이, 단어를 클릭하면  link로 문서와 문서가 바로 연결 되게끔

html은 여는태그(<h1>)와 닫는 태그(</h1>)로 구성이 된다.

href :hypertext reference

a : 닻

h1 : 대제목 

a : 링크를 연결시켜준다. 



ol : ordered list



html 의 필수 요소

```python
<!DOCTYPE html>
<html>
    <head></head>
    <body>
      # 이 사이에 코드 입력  
    </body>
</html>
```

@@ alt +방향키 : 이동

@@ body보다 한 단계 안쪽으로 이동해서 코드 작성을 시작해야한다. 

파일 정리하듯이 같은 위치에 있는 폴더는 같은 선상에, 상하 관계 폴더는 한단계 위 아래로!

예를 들면 폴더 정리할 때

![1562733711223](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562733711223.png)



html도 마찬가지로 이런식으로 정리하는 습관 꼭 들이세요! 상위 하위 level을 구분하기 위해서!



#### W3

www을 만드는 국제 표준화 기구

https://www.w3schools.com/html/ : html 공부할 수 있는 튜토리얼 사이트

html reference에 html tag list 활용하세요, attribute에 활용할 수 있는 것이 같이 나타남



![1562735252024](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562735252024.png)





@@ .과 #의 의미

.(마침표) : class 의미

#(샵) : id 의미



#### background-color

h1은 빨간색 class는 파란색 충돌이 일어났을 떄 class가 우선순위가 우위

우선순위

id>class>h

id는 중복 되면 안된다. 클래스는 중복되도 상관 없음.



#### html + css 

css는 <sytle></style> 안에 표시해서 html과 분리한다.

```html
<!DOCTYPE html>
<html>
    <head>
        <style>
            h1 {
                background-color:red;
            }
            a {
                color:brown;
            }
            .blue {
                background-color:blue;
            }
            #git {
                background-color:black;
            }
        </style>
    </head>
    <body>
        <h1>HTML</h1>
        <h1 class="blue">CSS</h1>
        <h2 class="blue">HyperText Markup Language</h2>
        <a href="https://naver.com">네이버</a>
        
        <!-- <태그이동 속성명="속성값" 속성명2="속성값2"></태그이동>  -->
        
        <h3 class="blue">우리가 공부한것<strong>ssafy</strong></h3>
        <ol>
            <li><strong><i>파이썬</i></strong></li>
            <li id="git">HTML</li>
            <li id="git" class="blue">Git</li>
        
        </ol>
        
    </body>
</html>
```



#### html과 css를 다른 파일 상으로 분리하기

1. html 파일

html에서 쓴 style기능을 css 의 파일로 따로 분리할건데,  분리된 파일을 연결하는데 link 사용가 사용된다. (link tab하면 자동으로 뒷부분 입력 됨) 

link는 닫는 태그가 없다.(필요 없으니까)

```html
<!DOCTYPE html>
<html>
    <head>
        <link rel="stylesheet" href="./intro.css">  
        <!-- link를 추가한 부분. href 사이에 "./"를 입력하면 현재 폴더가 뜬다. 여기 뜨는 폴더로 link를 추가할 수 있다.-->
    </head>
    <body>
        <h1>HTML</h1>
        <h1 class="blue">CSS</h1>
        <h2 class="blue">HyperText Markup Language</h2>
        <a href="https://naver.com">네이버</a>
        
        <!-- <태그이동 속성명="속성값" 속성명2="속성값2"></태그이동>  -->
        
        <h3 class="blue">우리가 공부한것<strong>ssafy</strong></h3>
        <ol>
            <li><strong><i>파이썬</i></strong></li>
            <li id=>HTML</li>
            <li id="git" class="blue">Git</li>
        
        </ol>
        
    </body>
</html>
```



2. css 파일

```css
/* 여기는 css 파일입니다/ */
h1 {
    background-color:red;
}
a {
    color:brown;
}
.blue {
    background-color:blue;
}
#git {
    background-color:black;
}
```

@@ html과 css의 주석표시도 서로 다름 <!-- -->  /* */ 



#### Start Bootstrap

html계의 탬플릿이라고 생각하면 됩니다.

![1562738970846](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562738970846.png)

위에서부터 순서대로 입력하고 따라하기

주의 폴더 위치 잘 지정해서 그 폴더로 들어가세용





https://fontawesome.com/

![1562739611697](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562739611697.png)

![1562739623839](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562739623839.png)



https://sy7979.github.io/index.html

https://sy7979.github.io



http://tech.kakao.com/

https://spoqa.github.io/



https://jekyllrb-ko.github.io/ : 마크다운 문서를 게시물 형식으로 바꿔주는 기능



https://awesome-devblog.netlify.com/ 국내 개발자 블로그

http://woowabros.github.io/ 우아한 형제들 기술 블로그

유튜부 우아한  tech