# Django 환경설정

> 1. 프로젝트 기획 / 개발 환경 / 프로젝트 설계
> 2. 개발 환경 구축



## 1. 프로젝트 기획 / 개발 환경 / 프로젝트 설계

### 1) 프로젝트 기획

> 기획 의도, 배경



### 2) 개발 환경

> 시스템 아키텍처, 개발환경

	* 사업 기획발표에서 가장 중요한 단계이다.



### 3) 프로젝트 설계

> 화면 설계, ERD



## 2. 개발 환경 구축

> 1) Web Server
>
> 2) Python Project
>
>  - Web application 추가
>  - django Server
>
> 3) 개발 순서



### 1) Web Server

* pip install django를 파이참 터미널에 입력하면 작업하고 있는 프로젝트는 Web Server가 된다.



### 2) Python project 생성



### 3) Web Application 환경으로 변환

* django-admin startproject confi .을 터미널에 입력하면 Web Application 환경으로 변환된다.






### 4) Project 안에 Web Application 생성

* python manage.py startapp hello를 터미널에 입력하면 프로젝트 안에 hello 폴더를 추가로 생성된다.
* hello라는 이름의 Web App이 만들어진다.



### 5) html 폴더 설정

 * (1) hello 폴더에서 templates 폴더를 만든다.
* (2) config에서 settings.py를 수정한다.

```python
INSTALLED_APPS = [

'django.contrib.admin',

'django.contrib.auth',

'django.contrib.contenttypes',

'django.contrib.sessions',

'django.contrib.messages',

'django.contrib.staticfiles',

'hello' # 웹애플리케이션 이름 

]

​

TEMPLATES = [

{

'BACKEND': 'django.template.backends.django.DjangoTemplates',

'DIRS': [],

'DIRS': [os.path.join(BASE_DIR, 'templates')], # os를 import로 호출한다.
												# 어떠한 디렉토리를 templates로
'APP_DIRS': True,

'OPTIONS': {

'context_processors': [

'django.template.context_processors.debug',

'django.template.context_processors.request',

'django.contrib.auth.context_processors.auth',

'django.contrib.messages.context_processors.messages',

],

},

},

]
```



* (3) config에서 urls.py를 수정한다.

```python
urlpatterns = [

path('admin/', admin.site.urls),

path('', include('hello.urls')), # django.ruls.include() 함수를 호출한다.
    							 # 아무 것도 없으면 Wep App의 urls로 이동한다.
]
```



	* (4) config / urls.py 파일을 hello 폴더에 복사한다.

```python
urlpatterns = [

path('admin/', admin.site.urls),

path('', views.home, name='home'), # hello.views 함수를 호출한다.
									# views에서 home 함수를 이용한다.
]
```



	* (5) views.py 파일에 home 함수 추가

```python
def home(request):
    return render(request,'home.html')
```



	* (6) templates 폴더에 home.html에 생성하고 문구를 추가한다.

```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<h1>Hello Django World !!!</h1>
</body>
</html>
```



 * (7) 서버 실행를 실행하고 Browser에서 127.0.01로 접속한다.
   	* python manage.py runserver 80 : 80포트로 웹 서버를 설정한다는 것을 뜻하며 기본 포트는 80포트이다.
    	* ctrl + c를 누르면 서버 동작을 그만둔다.



# 이미지 넣기

> 1. config 폴더에서 settings.py 파일에 아래 내용 추가
> 2. 실행할 Wep Application의 html 파일에 내용을 추가한다.



## 1. config 폴더에서 settings.py 파일에 아래 내용 추가



```python
STATICFILES_DIRS = [
    os.path.join(BASE_DIR,'static')
]
```

 * 다른 프로젝트에서 같이 사용하기 위해 따로 디렉토리를 설정한다.
   	* project 밑에 static 파일을 만들고 다시 안에 img파일 생성한다.
    * img 파일에 이미지 넣는다.



## 2. 실행할 Wep Application의 html 파일에 내용을 추가



```
{% load static %} **#추가**
# static 파일을 불러와서 사용하겠다!

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>Shop Test</h1> **#추가**
    <img src="{%static 'img/logo.png' %}"> #logo.png 사용 명령어 **#추가**
</body>
</html>
```



# 이동경로 설정

> 1. 경로를 추가할 Web application html파일 설정
> 2. Web application의 urls 파일에서 경로 설정
> 3. Web application의 views 파일에서 함수 정의



## 1. 경로를 추가할 Web application html파일 설정



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>Main Page</h1>
    <br>
    <h2><a href="table">Table</a></h2>
    <h2><a href="resume">Resume</a></h2>
    <h2><a href="multi">Multimedia</a></h2>
</body>
</html>
```

 * '<h2>'는 제목 태그이다.
   	* '<h1>, <h2>, <h3>, <h4>, <h5>, <h6>' 순으로 글자 크기가 작아진다.
   	* 문서의 구조와 밀접한 관련이 었으므로 순서에 맞게 사용하는 것이 바람직하다.
 * '<a></a>'는 하이퍼링크를 걸어주는 태그이다.
    * href는 '<a>'태그를 통해 연결한 주소를 지정한다.
      	* Templates 폴더의 다른 html 파일로 이동하므로 해당 파일의 실제 이름을 쓴다.
   	* target은 링크를 클릭할 때 창을 어떻게 열지 설정한다.
   	* title은 해당 링크에 마우스 커서를 올릴 때 도움말 설명을 설정한다.
   	* '<a></a>' 사이에는 하이퍼링크의 이름을 설정한다.



## 2. Web application의 urls 파일에서 설정



```python
from django.contrib import admin
from django.urls import path, include

from wstest import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('',views.main,name='main'),
    path('table',views.table,name='table'),
    path('resume',views.resume,name='resume'),
    path('multi',views.multi,name='multi'),
    path('bpage',views.bpage,name='bpage'),
]
```

 * Wep Application의 특정 html 파일에서 설정한 하이퍼링크를 통해 입력한 명령을 urls 파일에서 어떻게 처리할 것인가를 설정한다.
   	* views 파일에서 명령 수행에 대한 함수 이름을 지정한다.



## 3. Web application의 views 파일에서 함수 정의



```python
from django.shortcuts import render

# Create your views here.
def main(request):
    return render(request,'main.html')

def table(request):
    return render(request,'table.html')

def resume(request):
    return render(request,'resume.html')

def multi(request):
    return render(request,'multi.html')

def bpage(request):
    return render(request,'main.html')
```

 * 실제로 수락한 요청에 대해 어떻게 처리할 것인가를 함수로 설정한다.
   	* 하이퍼링크를 통해 이동하려는 html 파일을 지정한다.
	* 경로를 지정한 이후에는 해당 html 파일에서 추가 작업을 수행한다.

