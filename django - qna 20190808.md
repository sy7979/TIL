# django - qna 20190808

기사에 질문을 달 수 있는 사이트를 만들어보자.

일단, 꾸미지 않고 틀부터 완성해보자.

### 1. 시작설정

```bash
1. $ python -m venv venv
2. $ pip install django
```

3. gitingore 파일 만들기
4. f1 -->  python select interpreter --> venv

```bash
3. $ django-admin startproject qna .
4. $ django-admin startapp articles
```



### 2. aricles

##### 1. class 생성하기

models.py

```python
from django.db import models

# Create your models here.
class Question(models.Model):
    title = models.CharField(max_length=50)
    content = models.CharField(max_length=100)
    user = models.CharField(max_length=20)
    # 작성 시간을 (자동으로) 기록
    created_at = models.DateTimeField(auto_now_add=True)
```



##### 2. migration :

모델을 만들었으니 migration을 해준다

```bash
$ python manage.py makemigrations
$ python manage.py migrate
```

```bash
# 내가 설정한 title, content, user, created_at 외에도 장고에서 기본 정보들을 알아서 저장해준다.
Applying contenttypes.0001_initial... OK
Applying auth.0001_initial... OK
Applying admin.0001_initial... OK
Applying admin.0002_logentry_remove_auto_add... OK
Applying admin.0003_logentry_add_action_flag_choices... OK
Applying articles.0001_initial... OK
Applying contenttypes.0002_remove_content_type_name... OK
Applying auth.0002_alter_permission_name_max_length... OK
Applying auth.0003_alter_user_email_max_length... OK
Applying auth.0004_alter_user_username_opts... OK
Applying auth.0005_alter_user_last_login_null... OK
Applying auth.0006_require_contenttypes_0002... OK
Applying auth.0007_alter_validators_add_error_messages... OK
Applying auth.0008_alter_user_username_max_length... OK
Applying auth.0009_alter_user_last_name_max_length... OK
Applying auth.0010_alter_group_name_max_length... OK
Applying auth.0011_update_proxy_permissions... OK
Applying sessions.0001_initial... OK
```

##### 3. admin.py

```python
from django.contrib import admin
from .models import Question
# Register your models here.
admin.site.register(Question)
```



##### 4. ulrs.py < qna(master)

```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('questions/', include('articles.urls'))
]

```



### 3. articles

#### #Create_1 : 질문 등록하기

##### 1. new basic

사용자 데이터 입력창(form)

```python
1. urls.py
from django.urls import path
from . import views

urlpatterns = [
    # Create
    path('new/', views.new),    
]
```

```python
2. views.py
from django.shortcuts import render

# Create your views here.
def new(request):
    return render(request, 'new.html')
```

```html
3. new.html
{% extends 'base.html'%}
{% block body%}
  <form action="/questions/create/">
    <input type="text" name="user">
    <input type="text" name="title">
    <input type="text"name="content">
    <input type="submit">
  </form>

{% endblock %}
```



##### 2. create : 

저장하는 역할

```
1. urls.py
path('create/', views.create)
```

```python
2. views.py
from django.shortcuts import render, redirect
from .models import Question

def create(request):
    user = request.GET.get('user')
    title = request.GET.get('title')
    content = request.GET.get('content')

    question = Question()
    question.user = user
    question.title = title
    question.content = content

    question.save()

    return redirect('/questions/')
	#아직 /questions/페이지가 만들어지지 않았기 때문에 불러올 수 없다. 읽어오는 페이지를 만들자!
```



#### #Read

/questions/ 페이지 만들기: 저장된 정보 읽어오기

##### 1. index basic

```python
1.urls.py
path('', views.index),
```

```python
2.views.py
def index(request):
    questions = Question.objects.all()
    context = {
        'questions': questions,
    }
    return render(request, 'index.html', context)
```

```html
3.index.html
{% extends 'base.html'%}
{% block body%}
  {{questions}}
{% endblock %}

Q. 페이지에 어떤 형식으로 출력될까??
A. <QuerySet [<Question: Question object (1)>, <Question: Question object (2)>]>
```

##### 2. index.html :

반복문으로 정보 불러오기

```html
{% extends 'base.html'%}
{% block body%}
{% for question in questions %}
  <h1>{{question.title}}</h1>
  <p>{{question.user}}</p>
  <p>{{question.content}}</p>
  <hr>
{% endfor %}
{% endblock %}
```



하나의 질문에 여러개의 댓글이 달린다(1 : n 모델)

question : answer = 1 : n

질문과 댓글의 table을 완전 분리, 댓글에는 질문의 id(ForeignKey=내가 어디에 속해있는지를 담고있는 정보)를 같이 저장함

==>  question이외에 answer class를 생성한다.''



#### #Create_2: 댓글 달기

##### 1. 댓글 저장

###### 1. models.py :

answer class 생성

```python
class Answer(models.Model):
    content = models.CharField(max_length=100)
    # 어떤 question(id)에 속해있는지 담고 있는 정보 필요
    # question = models.ForeignKey(상속받을 클래스명, on_delete=models.CASCADE)
    # cascade: 폭포
    question = models.ForeignKey(Question, on_delete=models.CASCADE)

```

사용자의 입력을 받기 위해 form 생성

```python
{% extends 'base.html'%}
{% block body%}
{% for question in questions %}
  <h1>{{question.title}}</h1>
  <p>{{question.user}}</p>
  <p>{{question.content}}</p>
  <form action="/questions/{{quesiton.id}}/answers/create/">
    <!-- form을 입력받아 내용을 저장하는 페이지로 넘겨야한다. -->
    <input type="text" name="content">
    <input type="submit">
  </form>
  <hr>
{% endfor %}
{% endblock %}
```

###### 2. urls.py

```python
urls.py
path('<int:question_id>/answers/create/', views.answer_create)
```

###### 3. views.py

```python
def answer_create(request, question_id):
    content = request.GET.get('content')

    question = Question.objects.get(id = question_id)

    answer = Answer()
    answer.content = content
    answer.question = question
    # question에 Question object를 넘겨주어야한다.
    # class Question 안에서 나온 id를 넘겨주어야한다. object와 object의 연결
    answer.save()
```

###### 4. admin에 등록

```python
from .models import Question, Answer
admin.site.register(Answer)
```



##### 2. 댓글 보기

###### 1. views.

```
def index(request):
    questions = Question.objects.all()
    answers = Answer.objects.all()

    context = {
        'questions': questions,
        'answers': answers
    }
    return render(request, 'index.html', context)
```

###### 2. index.html

```html
{% for answer in question.answer_set.all %}
	<p>{{answer.content}}</p>
{% endfor %}
```

### 4. 꾸미기

bootstrap이용해서 꾸며주자!

##### 1. index.html 원본

```html
1. index.html 원본
{% extends 'base.html'%}
{% block body%}
{% for question in questions %}
  <h1>{{question.title}}</h1>
  <p>{{question.user}}</p>
  <p>{{question.content}}</p>
  <form action="/questions/{{question.id}}/answers/create/">
    <!-- form을 입력받아 내용을 저장하는 페이지로 넘겨야한다. -->
    <input type="text" name="content">
    <input type="submit">
  </form>
  
  <!-- question 하나가 가지고 있는 answer들의 set을 전부 가지고 온다. -->
  <!-- 해당 게시물에 해당되는 댓글들만 그 아래 출력될 수 있다. -->
  <!-- 인스턴스변수명_set : 자동으로 set를 가져온다.-->
  {% for answer in question.answer_set.all %}
    <p>{{answer.content}}</p>
  {% endfor %}
  <hr>
{% endfor %}
{% endblock %}
```

##### 2. new.html 원본

```html
2.new.html원본
{% extends 'base.html'%}
{% block body%}
  <form action="/questions/create/">
    <input type="text" name="user">
    <input type="text" name="title">
    <input type="text"name="content">
    <input type="submit">
  </form>

{% endblock %}
```



