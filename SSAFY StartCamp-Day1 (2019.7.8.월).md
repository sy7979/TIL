# SSAFY StartCamp-Day1 (2019.7.8.월)
#### Computational 이란?
How to Program과 같은 뜻.
Program은 컴퓨터에 의해 실행되는 지시사항의 모음, 명령의 집합을 의미한다. 쉽게 말해 무언가를 시키는 작업을 의미한다고 할 수 있다.



#### 상식 --> 논리

어려운 논리 문제이더라도 내가 가지고 있는 상식과 관련된 문제라면 더 쉽게 풀 수 있다. 알고리즘도 이런식으로 생각하면 좀 더 쉽게 이해할 수 있을 것이다.



#### 프로그래밍 언어 : 3형식

##### 1. 저장 

1. 의미: 저장한 값을 변수로 활용하겠다.

2. 저장할 수 있는 값

   1. 현실세계의 모든 숫자(글자제외)
   2. 큰 따옴표, 또는 작은 따옴표로 둘러싼 글자나 숫자
   3. 참/거짓 (True/False)

3. 여러가지 저장 form (저장하는법/불러오는법/출력법)

   1. 변수 : (`dust = 40`/`dust`/`40`)

   2.  리스트 : (`dus t= [40,50,80,]`/`dust[0]`/`40`) 

      <!----> 파이썬에서 숫자는 0부터 시작한다.

   3. 딕셔너리 : (`dust = {'영등포구':40,'강남구':50}`/`dust['영등포구']`/`40`) 

      <!---->'영등포구':40의 관계는 key:value 의 관계이다.

4. 예시

   `dust = 60` : dust 라는 박스에 60이라는 값을 저장했다.

5. 주의 사항

   1. 같다는 의미를 표현하고 싶다면 --> `dust == 60` 으로 표현!

   2. 같은 이름으로는 여러개의 정보 저장 불가
      만약, 
      ```
      dust = 60
      dust = 58
      ```
      
      이라면 dust는 최종적으로 58이 저장 되고, `print(dust)` 결과값으로 58이 나온다.

##### 2. 조건 (if)

1. 의미: 조건문 판단

2. 표기
	```python
	if(True) :
			print('조건문입니다.')
	```
	
	​	만약  True가 성립된디면 '조건문입니다.'가 출력된다.



##### 3. 반복(while, for)

1. 의미 

   1. while True : 조건이 True일 때 까지 반복적으로 실행하여라. (종료 조건이 반드시 필요)

   2. for i in dust : 정해진 범위를 반복 하여라. (종료조건 필요 없음)

      <!----> while문보다 for문을 더 많이 사용한다.



#### 예시(파이썬 챗봇)

1. 날씨 

```python
import requests

url = "https://api.openweathermap.org/data/2.5/weather?q=Gwangju,KR&lang=kr&APPID="+key
data = requests.get(url).json()
weather = data['weather'][0]['main']
temp = float(data['main']['temp'])-273.15
temp_min = float(data['main']['temp_min'])-273.15
temp_max = float(data['main']['temp_max'])-273.15

print(f'''광주의 오늘 날씨는 {weather}이며, {temp}도 입니다.
최저/최고 온도는 {temp_min}/{temp_max}입니다.''')

```

2. 환율

```python
import requests
from bs4 import BeautifulSoup
url = "https://finance.naver.com/marketindex/?tabSel=exchange#tab_section"

html = requests.get(url).text
soup = BeautifulSoup(html, 'html.parser')
select = soup.select_one('#exchangeList > li.on > a.head.usd > div > span.value')

print(f'지금 1$는 {select.text}원 입니다.')
```

3. 코스피

```python
import requests
from bs4 import BeautifulSoup
url = "https://finance.naver.com/sise/"

html = requests.get(url).text
soup = BeautifulSoup(html, 'html.parser')
select = soup.select_one('#KOSPI_now')

print(f"코스피 지수 : {select.text}")
```

4. 안녕

```
greeting = 'hi'

print(greeting)
print(greeting)
print(greeting)
print(greeting)
print(greeting)
```

5. 점심메뉴

```python
import random

# 원하는 메뉴를 []안에 넣어주세요
menu = ['','']

choice = random.choice(menu)
print(f"오늘 점심은 {choice} 어떤가요?")
```

6.배달

```
import random

# 원하는 식당과 전화번호를 {}안에 넣어주세요
phonebook = {
    '영암매력한우수완점':'062-383-8118',
    '신전떡볶이 광주수완점':'062-956-2334',
    '양동통닭':'062-471-9277',
    'ㅇㅅㅇ':'123-456-7891'
            }
choice = random.choice(list(phonebook.keys()))
print(f"{choice} : {phonebook[choice]}")
 

```

7. 미세먼지

```python
import requests
from bs4 import BeautifulSoup

url = f'http://openapi.airkorea.or.kr/openapi/services/rest/ArpltnInforInqireSvc/getCtprvnRltmMesureDnsty?serviceKey={key}&numOfRows=10&pageSize=10&pageNo=1&startPage=1&sidoName=%EA%B4%91%EC%A3%BC&ver=1.6'
request = requests.get(url).text
soup = BeautifulSoup(request,'xml')
dong = soup('item')[7]
location = dong.stationName.text
time = dong.dataTime.text
dust = int(dong.pm10Value.text)
dust = 100

print(f"{time} 기준 {location}의 미세먼지 농도는 {dust}입니다.")

# 아래에 코드를 작성해주세요
if dust>150:
    print('매우나쁨')
elif 80<dust<=150:
    print('나쁨')
elif 30<dust<=80:
    print('보통')
else:
    print('좋음')
```

8. 로또

```python
import random
numbers = list(range(1,46))

pick = random.sample(numbers,6)
print(pick)
```

9.가위

```python
import random
play = ['가위','바위','보']
pick = random.choice(play)
print(pick)

if pick == '가위':
    print('비겼습니다.')
elif pick == '바위':
    print('졌습니다')
else:
    print('이겼습니다')
```

