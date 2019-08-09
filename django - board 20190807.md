# django - board 20190807

CRUD

### 1. 새로운 프로젝트 시작(todos)

빈 폴더 생성 --> open with vscode --> 터미널 창 띄우기

```
1. 환경설정
$ python -m venv venv
```

2. f1 --> python select interpreter --> venv --> 터미널 창 껏다가 키기

3. .gitignore 파일생성, gitignore.io에서 코드 복사

```
4. 장고 설치
$ pip install django

5.프로젝트 시작
$ django-admin startproject board .

6.앱추가
$ django-admin startapp todos
```

7. todos 앱 기본 설정

```python
1. settings.py (in master)
INSTALLED_APPS = [
    'todos',
]

2. urls.py (in master)
from django.urls import path, include
urlpatterns = [
    path('admin/', admin.site.urls),
    path('todos/', include('todos.urls')),
]
```



* base.html 이해하기(과목평가 예상 문제)

  ```python
  <!-- 언어설정(lang): 기본 언어 설정-->
  <html lang="en">
  <head>
    <!-- charset: 인코딩 셋: 문자를 어떻게 세팅할지를 정하는 것 -->
    <meta charset="UTF-8">
    <!-- width=device-width: 디바이스 크기를 기준으로, 크기 단위 viewport로 정하겠다. -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
  ```

* navbar 설정하기

  ```
  1. 링크 걸어주기
  <a class="nav-item nav-link" href="/todos/new/">New</a>
  # 최상단의 url로부터의 모든 경로를 적어주어야한다.(/new/만 하면 안된다.)
  ```

  



### 2. Create 데이터 입력 받음(new&create)

##### 1. new 기본 설정

```python
1. urls.py < todos
from django.urls import path
from . import views

urlpatterns = [
    path('new/', views.new),
]

2. views.py < todos
def new(request):
    return render(request, 'new.html')

3. new.html 
form: bootstrap에서 복사하고 name 넣어주기
    	margin은 form에 m-5 넣어주기
form에 action으로 create로 경로 열어주기
```

##### 2. create 기본 설정

```python
1.urls.py in todos
urlpatterns = [
    path('new/', views.new),
    path('create/', views.create)
]

2. views.py in todos
def create(request):
    return render(request, 'create.html')
    
3. create.html 만들기
```

##### 3. class 설정

```python
1. models.py
# class 변수 생성하기
class Todo(models.Model):
    # modles안의 Model을 상속받음
    title = models.CharField(max_length=50)
    content = models.CharField(max_length=200)
    due_date = models.DateField()

2. bash 창: 데이터베이스에 저장하기 위해 언어를 바꿔주는 과정(python --> SQL)
# models.py에서 class, 혹은 class 내부 내용을 수정할때 마다 계속 다시		 migrationd을 해주어야한다.
$ python manage.py makemigrations
$ python manage.py migrate

```

##### 4. create : new에서 받은 정보 저장하기

```python
1. new.html: create url로 연결해주기
<form action="/todos/create/" class='m-5'>

2. views.py 사용자가 전달한 정보 불러오기
1) class 불러오기 
from .models import Todo

2) 함수 정의하기
def create(request):
    title = request.GET.get('title')
    content = request.GET.get('content')
    due_date = request.GET.get('due-date')

    # 인스턴스화 & 변수 저장
    todo = Todo()
    todo.title = title
    todo.content = content
    todo.due_date = due_date
    # 저장하기
    todo.save()
    
    # 훨씬 간단한 코드: 인스턴스화 하면서 변수 할당
    # todo = Todo(title=title, content=content, due_date=due_date)
    return render(request, 'create.html')
   
```

##### 5. create: return 되는 페이지 바꾸기

```python
1.views.py
# redicrect 함수를 import 한 후
return redirect('/todos/')
# 해당 url 주소로 이동한다.
```



##### 6. 관리자(super user) 페이지

```python
1. 관리자 페이지 만들기
$ python manage.py createsuperuser
Username (leave blank to use 'student'): 아이디
Password: 비밀번호

2.관리자 페이지에 Todo 추가하기
$ admin.py in todos
```





### 3. Read: 사용자에게 결과를 읽어줌(index&detail)

##### 1. index 기본 설정

```python
1.urls.py: path 추가
urlpatterns = [
    # create
    path('new/', views.new),
    path('create/', views.create),

    # read
    path('', views.index)
]

2.views.py
def index(request):
    todos = Todo.objects.all()
    context ={
        'todos': todos,
    }
    return render(request, 'index.html', context)
	
3.index.html 생성
```

##### 2. index.html 설정

```html
1. table형식으로 todos에 있는 정보 보여주기
bootstrap에서 table 복사

2. 각각의 데이터의 내용을 링크를 통해 보여주기
각 데이터의 id값을 이용한다. url에 id값이 들어가서 urls.py의 datail의 path로 정보가 넘어감.
<a href="/todos/{{todo.id}}/" class="btn btn-primary">글보기</a>
```



##### 3. detail 기본설정

```python
1. ulrs.py: variable routing을 통해 여러가지 경로를 하나의 path(url)로 처리할 수 있다
urlpatterns = [
    # Create
    path('new/', views.new),
    path('create/', views.create),

    # Read
    path('', views.index),
    path('<int:todo_id>/', views.detail),
    # 여기서 todo_id는 그냥 변수명이다. int가 들어온다는게 핵심(id는 int형이므로)
]

2. views. py
def detail(request, todo_id):
    pass

3.detail.html 만들기
```

##### 4. detail views.py

```python
def detail(request, todo_id):
    # url에 들어온 변수인 todo_id를 쓸 수 있다.
    # get: 이미 저장된 정보를 가져온다
    todo = Todo.objects.get(id=todo_id)
    context = {
        'todo': todo,
    }
    return render(request, 'detail.html', context)
```

##### 5. detail.html

```html
<!-- 부트스트랩 점보트론 -->
<!-- 클래스 변수를 . 으로 접근이 가능하다! -->
<div class="jumbotron my-3">
    <h1 class="display-4">{{todo.title}}</h1>
    <p class="lead">{{todo.content}}</p>
    <hr class="my-4">
    <p>{{todo.due_date}}</p>
    <a class="btn btn-warning btn-lg" href="#" role="button">수정</a>
    <a class="btn btn-danger btn-lg" href="#" role="button">삭제</a>
</div>
```





### 4. Delete 데이터 삭제하기(delete)

##### 1. 기본구조

```html
1. detail.html: detail.html에서 삭제 버튼을 누르면 delete에 연결되게 한다.
<a class="btn btn-danger btn-lg" href="/todos/{{todo.id}}/delete/" role="button">삭제</a>
```

```python
2. ulrs.py
# Delete
    path('<int:todo_id>/delete/', views.delete), 
```

```python
3. views.py
def delete(request, todo_id):
    todo = Todo.objects.get(id=todo_id)
    # todo를 지우는 함수
    todo.delete()

    return render(request, 'delete.html')
```

```html
4. index.html: 모든게 삭제되어서 데이터가 없으면 안내창이 나오게 한다.
{% empty %}
<tr>
    <th>#</th>
    <td>할일이 비었습니다.</td>
    <td></td>
    <td></td>
</tr>
```

##### 2. views.py return page 수정

```python
5. views.py
# redirect를 import해준 후
return redirect('/todos/')
```



### 5. Update(edit&update)

new와 같은 작성 페이지를 불러온다 --> class 인스턴스변수에 값을 재할당해서 저장한다.

##### 1. edit

```python
1. urls.py
# Update
path('<int:todo_id>/edit/', views.edit)
```

```python
2. views.py
def edit(request, todo_id):
    todo = Todo.objects.get(id=todo_id)
    context = {
        'todo': todo,
    }
    
    return render(request, 'edit.html', context)
```

```html
3. edit.html: new.html과 기본 주고는 같게
<!-- form action이 update page로 넘어가게 해준다.-->
<form action="/todos/{{todo.id}}/update/" class='m-5'>
  <div class="form-group">
    <label for="title">ToDo</label>
    <input type="text" class="form-control" id="title" name="title" value="{{todo.title}}">
  </div>
  <div class="form-group">
    <label for="content">Content</label>
    <input type="text" class="form-control" id="content" name="content" value="{{todo.content}}">
  </div>
  <div class="form-group">
      <label for="due-date">Due Date</label>
      <!-- 장고 템플릿 필터를 사용해서 데이터 형식을 오른쪽의 form으로 바꿔준다. f12를 통해 value값을 확인해 보면 해당 데이터가 어떤 form을 가지고 있는지 확인할 수 있다. -->
      <input type="date" class="form-control" id="due-date" name="due-date" value="{{todo.due_date|date:'Y-m-d'}}">
    </div>
  <button type="submit" class="btn btn-warning">수정</button>
</form>
```

##### 

##### 2. update

```python
1. url.py
# Update
path('<int:todo_id>/update/', views.update)
```

```python
2. views.py : 수정된 정보를 가져오고, 원래있던 인스턴스 변수에 재할당한다.
def update(request, todo_id):
    # 수정된 정보 가져오기
    title = request.GET.get('title')
    content = request.GET.get('content')
    due_date = request.GET.get('due-date')
	
    #인스턴스 변수에 재할당하기
    todo = Todo.objects.get(id=todo_id)
    
    todo.title = title
    todo.content = content
    todo.due_date = due_date

    todo.save()

    # return render(request, 'update.html')
    return redirect(f'/todos/{todo_id}')
```

```html
3. update.html
{% extends 'base.html' %}
{% block body %}
  <h1>수정완료</h1>
{% endblock %}
```



