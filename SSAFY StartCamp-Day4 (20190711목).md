#### SSAFY StartCamp-Day4 (20190711목)



#### Activity 1 

##### Flask

플라스크를 이용하여 서버 돌려보기

1.

![1562803405389](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562803405389.png)

​		@@ code. : vscode 여는 명령어



2. http://flask.pocoo.org/

![1562803479640](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562803479640.png)

​		복사 --> vs code에 붙이기

```python
@app.route("/")
```

/ 는 최상단(루트)을 의미한다. 서버주소 그 자체를 의미한다

url에 /가 붙어있다는 것은

주소(url)는 서버컴퓨터의 위치를 의미한다(내 집주소랑 똑같이)

210.89.164.90. ==> 정확한 주소(-구-동-번지-호수) , 컴퓨터의 주소는 숫자로만 표현 가능

이 주소는 어디게?? https://www.naver.com/

naver.com은 도메인 네임 서비스

이 숫자는 이 이름으로 대체 가능하다.



3. ![1562803781712](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562803781712.png)

   터미널에

   ```python
   student@DESKTOP MINGW64 ~/startcamp/04.first_app (master)
   $ pip install flask
   ```

   

```python
$ FLASK_APP=app.py flask run
```

​	hello.py를 app.py로 수정해서 실행한다.

​	저장 하고 실행 	
​	ctrl하고 link를 누른다.





4. ![1562804156387](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562804156387.png)

127.0.0.1은 내 자신을 의미하는 주소. 외부에서는 접속이 안된다? 나만 들어갈 수 있는 주소이다?? 

/ 뒤는 서버에 있는  resource 의미

라우트 = 경로를 받아주는 것

서버를 끄기 위해서는 ctrl + c



```python
from flask import Flask
app = Flask(__name__)

@app.route("/")
def hello():
    return "Hello World!"

@app.route("/hi")
def hi():
    return "안녕하세요!!!"
```

![1562804843984](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562804843984.png)

![1562804866009](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562804866009.png)

/hi를 추가하면 안녕하세요가 나온다.



@@

터미널에 보면,,,

```python
 Debug mode: off
```

test, 개발, 제품화 단계

debug 모드는 개발단계 :  error가 표시된다

debug 모드 off 는 제품화 단계 :  error가 표시되지 않는다.

```python
if __name__== '__main__':
    app.run(debug=True)
```

```python
student@DESKTOP MINGW64 ~/startcamp/04.first_app (master)
$ python app.py
```

Flask대신 python으로도 실행 가능

이렇게 하면 debug모드가 on으로 뜬다.

```python
 Debug mode: on
```



5. html으로 좀 더 구조화된 웹을 만들어보자

   새로운 라우트를 열어줄거에요

   ```
   @app.route("/html_tag")
   def html_tag():
       return "<h1>안녕하세요</h1>"
       
   ```

   

   %% 중간점검

   ![1562805462715](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562805462715.png)



![1562805684652](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562805684652.png)

return은 한 번 하면 끝난다.

첫번째 return에서 끝난 줄 안다. 결과적으로 안녕하세요만 나오고, 반갑습니다는 실행되지 않음. 이렇게 하면 안됨!!!!



![1562805818267](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562805818267.png)

'""" """ 안에 입력하면 모두 하나의 스트링으로 인식해서 내가 쓴 값이 다 나오게 할 수 있다.



6.

D day 세기 ==> 연산이 가능한 명령을 삽입할 수 있다.

```python
import datetime
@app.route("/dday")
def dday():
    today = datetime.datetime.now()
    endday = datetime.datetime(2019,11,29)
    d = endday-today
    return f"1학기 종료까지 {d.days}일 남음!!"
```









#### Ativity 2 

##### :이제  html를 분리해서 입력하자.

(html을 flask?py?안에 같이 입력하는건 비효율적이다.)



@@ !+tab : html 기본 바디 구조를 입력해준다.

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    # 여기에다가 내용 입력
</body>
</html>
```



variable : 변수

url에 변수를 넣을 거에요

Flask는 html과 다르게 동적인 웹이에요

url이 달라질 때 마다 다르게 작동한다.



##### 1. url에 따라 달라지는 내용

```python
@app.route("/greeting/<string:name>")
def greeting(name):
    return f"안녕하세요 {name}님!!"
```



![1562808161715](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562808161715.png)

![1562808190854](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562808190854.png)

url이 달라지면 웹 상에 나타나는 내용도 달라진다.



```python
@app.route("/cube/<int:num>")
def cube(num):
    R = num **3
    return f"{num}의 세제곱은 {R}입니다."
# num의 세제곱은 num^3입니다.
```

@@html에서 {}안에서는 python 문법을 적용할 수 있다.





![1562808809317](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562808809317.png)



2. ##### 여러가지 변수가 들어갈 수 있을까?!

html과 합작

python

```python
@app.route("/cube_html/<int:num>")
def cube_html(num):
    cube_num = num**3
    return render_template("cube.html", num_html=num, cube_num_html=cube_num)
```

num_html=num

오른쪽을 왼쪽에 대입한다. 는 의미

왼쪽은 새로운 이름, 오른쪽은 원래 있던 이름

관례상 이 둘이 같은 이름을 사용하는게 좋다.



html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
  <strong>{{num_html}}</strong>의 세제곱은 <i>{{cube_num_html}}</i>입니다.
</body>
</html>
```



@@파이썬 변수를  html에서 사용하는 법: 중괄호 두개! {{}}입력

엄밀히말하면 {{}}도 html의 언어가 아닌데, render_template 함수가 있기 때문에 가능. 더 엄밀히 말하면 우리가 작성한 html도 완전한 html 문서가 아니다;;; {{}}은 진자에서의 문법;;; 

render : 완전하지 않은것을 완전하게 도와주는 것

![1562809729892](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562809729892.png)

@@ 코세라: 미국 서부 대학 강의를 온라인으로 업로드한 서비스

https://www.coursera.org/

@@ edx : 미국 명문 대학 강의 온라인 서비스

강좌 : cs50 : 컴퓨터 기초 강의, 유튜브에도 있습니다. 강추강추



3. ##### 이미지 불러오기

   점심메뉴 추천

   random하게 이미지 불러 오기

```python
import random
@app.route("/lunch")
def lunch():
    menu = {
        "짜장면":"https://upload.wikimedia.org/wikipedia/commons/thumb/6/6f/Jajangmyeon_by_stu_spivack.jpg/240px-Jajangmyeon_by_stu_spivack.jpg",
        "짬뽕":"http://recipe1.ezmember.co.kr/cache/recipe/2017/02/18/42ec50c7c281289367d1e7e4d06f4fcc1.jpg",
        "스파게티":"http://ko.sukpasta.wikidok.net/api/File/Real/578c682d5e1a20ee46f0264e"
    }

    menu_list = list(menu.keys()) #['짜장면'."짬뽕","스파게티"]
    pick = random.choice(menu_list)
    img = menu[pick]

    return render_template("lunch.html", pick=pick, img=img)
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <h3>오늘의 점심은 {{pick}} 어떠세요?</h3>
    <img src="{{img}}" alt="">
</body>
</html>
```



4. ##### 영화 list 보여주기

   ```python
   @app.route("/movies")
   def movies():
       movie_list = ['스파이더맨','토이스토리','존윅3','알라딘']
       return render_template("movies.html", movie_list = movie_list)
   ```

   

   ```html
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <meta name="viewport" content="width=device-width, initial-scale=1.0">
       <meta http-equiv="X-UA-Compatible" content="ie=edge">
       <title>Document</title>
   </head>
   <body>
       <ol>
           {% for movie in movie_list %}
               <li>{{movie}}</li>
           {% endfor %}
       </ol> 
   </body>
   </html>
   ```

   @@  <ol></ol>은 목록을 숫자 리스트로 불러오게 해준다.

   @@ html에서 for문을 사용할려면 꼭 endfor로 닫아줘야 한다.

   ​	for 문 시작할 때 닫는 문장도 같이 쓰면서 시작하는 습관을 들이세요.

   

   

   

5. ##### ping pong 

​     @@ 네이버에 iu 검색햐면 url이 이렇게 표시 된다.

   ![1562819223816](C:\Users\student\AppData\Roaming\Typora\typora-user-images\1562819223816.png)

   url 구조를 보면,   물음표 뒤쪽은 파라메터를 의미, 검색 내용은  query= 다음에 표시 된다는 걸 알 수 있다.

py

```python
@app.route("/ping")
def ping():
    return render_template("ping.html")

@app.route("/pong")
def pong():
    user_input = request.args.get("test")
    return render_template("pong.html", user_input= user_input)

```



ping 과 pong 각각 총 2개의 html 필요

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <h1>여기는 핑입니다.</h1>
    <form action="/pong">
        <input type="text" name="test">
        <input type="submit">
    </form>
</body>
</html>
```



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <meta http-equiv="X-UA-Compatible" content="ie=edge">
    <title>Document</title>
</head>
<body>
    <h1>여기는 퐁입니다.</h1>
    사용자가 방금 입력한 데이터는
    <p>{{user_input}}</p>
    입니다
</body>
</html>
```

1. ping의 html에서 name="test"

     		2.	화면 구동하면 pong의 url에  test=(검색사항)이 뜬다
     		3.	py의 route의 request.args.get()에 "test"를 입력한다.





6. ##### naver. google 검색창 만들기







