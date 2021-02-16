# CSS 활용(1)

> 1. 기본 설정
> 2. CSS파일 분리
> 3. 구글 폰트 적용



## 1. 기본설정

```python
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'shop1',
    'shop2',
]

TEMPLATES = [
    {
        'BACKEND': 'django.template.backends.django.DjangoTemplates',
        'DIRS': [],
        'DIRS': [os.path.join(BASE_DIR,'templates')],
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

# Static files (CSS, JavaScript, Images)
# https://docs.djangoproject.com/en/3.1/howto/static-files/

STATIC_URL = '/static/'
STATICFILES_DIRS = [
    os.path.join(BASE_DIR,'static')
]
```

	* 새로운 웹 애플리케이션을 추가할 때에는 기본 경로를 지정할 필요가 없다.



```python
from django.contrib import admin
from django.urls import path, include

urlpatterns = [
    path('admin/', admin.site.urls),
    path('shop1/', include('shop1.urls')),
    path('shop2/', include('shop1.urls')),
]
```

 * config 폴더 안에 있는 urls 파일의 path에서 ''로 비어있을 때 127.0.0.1을 주소 창에 입력하면 브라우저는 이를 웹 서버로 보낸다. 웹 서버는 이를 공란으로 인식하고 웹 애플리케이션으로 전달한다.
   	* 'shop1'이나 'shop2'가 있으면 주소 창에 '127.0.0.1/shop1' 또는 '127.0.0.1/shop2'을 입력해야 웹 서버가 이를 'shop1' 또는 'shop2'로 인식한다.



```python
from django.contrib import admin
from django.urls import path, include
from django.views.generic import TemplateView

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', TemplateView.as_view(template_name='shop1/shop1.html'),name='shop1'),
    path('css01', TemplateView.as_view(template_name='shop1/css01.html'),name='css01'),
    path('css02', TemplateView.as_view(template_name='shop1/css02.html'),name='css02'),
    path('css03', TemplateView.as_view(template_name='shop1/css03.html'),name='css03'),
    path('css04', TemplateView.as_view(template_name='shop1/css04.html'),name='css04'),
    path('css05', TemplateView.as_view(template_name='shop1/css05.html'),name='css05'),
    path('css06', TemplateView.as_view(template_name='shop1/css06.html'),name='css06'),
]
```

 * 웹 서버에서 전달받은 urls를 인수로 인식하여 views 파일에서 특정 html을 생성한다. 이때,  단순히 화면만 이동하려면 views 파일에서 함수를 지정하지 않고 외부에서 함수를 호출할 수 있다.
   	* TemplateView : django.views.generic을 호출하고 메서드를 as_view를 선택한다.
    * template_name을 정의하면 장고에서는 자동으로 templates를 참조하여 파일명이 정의한 것과 같은 파일로 연결한다.
      	* templates 폴더 내에 shop1이나 shop2와 같은 특정 웹 애플리케이션에 대한 html 파일을 따로 저장했기 때문에 'shop1/shop1.html'와 같이 정의해야 한다.



## 2. CSS 파일 분리

```python
{% load static %}
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" type="text/css" href="{% static 'css/test01.css' %}">
    <style>
        a{
            text-decoration: none;
            color:black;
        }
        h3 > a{
            background:red;
            color:white;
        }
    </style>
</head>
<body>
    <h1>CSS Test 01</h1>
    <h1 class="cc">CSS Test 01</h1>
    <h2 class="cc">CSS Test 01</h2>
    <h2>CSS Test 01</h2>
    <h2 id="id01">CSS Test 01</h2>

    <h3><a href="">CSS Test 03</h3>
    <h3><a href="">CSS Test 03</h3>
    <h4><a href="">CSS Test 03</h4>
    <h4><a href="">CSS Test 03</h4>
</body>
</html>
-------------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>Shop1 Main Page</h1>
    <h2><a href="{% url 'css01' %}">CSS01</a></h2>
    <h2><a href="{% url 'css02' %}">CSS02</a></h2>
    <h2><a href="{% url 'css03' %}">CSS03</a></h2>
    <h2><a href="{% url 'css04' %}">CSS04</a></h2>
    <h2><a href="{% url 'css05' %}">CSS05</a></h2>
    <h2><a href="{% url 'css06' %}">CSS06</a></h2>
</body>
</html>
------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h2><a href="{% url 'shop1' %}">Main page</a></h2>
    <h2><a href="{% url 'css02' %}">CSS02 page</a></h2>
    <h2><a href="{% url 'css03' %}">CSS03 page</a></h2>
</body>
</html>
```

 * CSS에서 html의 개체에 대한 디자인을 다루기 때문에 CSS 코드가 지나치게 길면 이를 따로 저장한다. 일반적으로 static 폴더에서 CSS 하위 폴더를 만들고 안에 관련 CSS 파일을 저장한다.
   	* 이미지를 html에서 삽입할 때와 마찬가지로 templates 폴더 밖에 있는 static 폴더를 호출한다.
    * html의 '<link rel>'을 이용한다.
      	* stylesheet : 스타일 시트로 사용할 외부 자원(resource)을 불러온다.
 * {% static 'css/test01.css' %} : 장고 템플릿 언어는 html에서 사용할 수 있는 특별한 규칙 또는 문법이다. 템플릿 태그는 {% %}로 구성되어 있다.
   	* static : 웹 서버 내 CSS 파일이 있는 상위 폴더 이름
      	* 'css/test01.css' : 하위 폴더에 있는 CSS 파일의 위치
   	* 위와 같은 방식을 적용하더라도 <style>에서 다시 디자인을 지정할 수 있다.



 * 클래스를 지정하면 다른 개체에서도 동일한 형식을 적용할 수 있다.
    * class="클래스 이름"으로 정의하고 CSS 파일이나 코드에서는 .클래스 이름{ }으로 형식을 지정한다.
 * 특정 태그에 대해서만 특별히 다른 형식을 적용하고 싶을 떄에는 id="id이름"으로 지정한다.
    * CSS 파일이나 코드에서는 # id이름{ }으로 형식을 지정한다.
       * 오직 태그 하나만 적용할 때 사용해야 하며 중복해서 활용하면 오류가 날 수 있다. 
 * 하이퍼링크에 대한 CSS의 기본 설정은 밑줄과 보라색이다.
    * '<sytle>'에서 text-decoration: none;, color:black;으로 다시 설정할 수 있다.
    * 특정 상위 태그에 있는 하위 태그에 대해 형식을 지정하려면 상위 태그 > 하위 태그{ }을 사용한다.



 * <a> 태그에서 하이퍼링크를 정의할 때 {% url %} 템플릿 태그를 이용하면 url 설정에 정의된 특정 url 경로의 의존성을 제거할 수 있다. 즉, {% url 'css01' %}은 css01에 해당하는 url로 연결한다.
    * 특정 웹 애플리케이션의 urls 파일에서 다시 경로를 지정한다.
    * 만약 프로젝트를 확장하면서 웹 애플리케이션마다 urls 파일을 따로 관리를 하기 위해 이름 공간(namespace)으로 연결할 경우에는 앞에 이를 추가한다. 즉, {% url '이름공간:url 이름' %}
    * 이 방식을 사용하지 않는다면 주소 창을 기준으로 '<a href="/shop1/shop1">'과 같이 설정해야 하며 페이지가 많을 때 작업이 복잡해진다.



```python
/* 주석문 : 2010 01 25 */
        h1{
            color: yellow;
            background: black;
        }
        .cc{
            color: white;
            background:blue;
        }
        #id01{
            color: pink;
            background:red;
        }
```



## 3. 구글 폰트 적용

```py
{% load static %}

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="preconnect" href="https://fonts.gstatic.com">
    <link href="https://fonts.googleapis.com/css2?family=Anton&family=Coda+Caption:wght@800&display=swap" rel="stylesheet">

    <style>
        body{
            background:pink;
            background-image: url("{% static 'img/bg.jpg' %}");

        }
        h2{
            text-align:center;
            font-size:2em;
            color:red;
            font-family: Arial, Helvetica, sans-serif;
        }
        h3{
            font-family:'Anton','Coda Caption';
        }
    </style>
</head>
<body>
    <h1>CSS02 Main Page</h1>
    <h2>CSS Font Test</h2>
    <h3>CSS Font Test</h3>
</body>
</html>
```

 * 외부에서 저장한 글꼴을 가져오면 기기에 관계없이 동일한 유형과 크기로 화면을 볼 수 있다.
   	* 기기마다 저장된 글꼴의 종류가 다르기 때문이다.
 * 구글이나 파이어폭스에서 접속을 해야 해당 글꼴이 적용된다.
   	* https://fonts.google.com/에 접속하여 원하는 글꼴를 찾는다.
      	* select this style을 누르면 원하는 글꼴을 추가할 수 있다. 
    * 추가하고자 하는 글꼴을 모두 선택했으면 Use on the web에서 '<link>'에 있는 내용을 복사한 후에 '<head>'의 '<link rel>'에 삽입한다.
      	* preconnect는 브라우저가 대상 리소스의 원본에 미리 연결하도록 명시한다.
    * CSS rules to specify families에서 편하게 웹 글꼴 코드를 넣을 수 있다.
      	* font-family에서 기입한 순서대로 웹 글꼴이 적용된다. 즉, 앞에 있는 글꼴이 적용되지 않으면 다음 번째에 있는 것을 사용하는 것처럼 순차적으로 작업이 이루어진다.
	* '<style>'의 '<body>'는 화면의 전체 뒷배경에 대한 형식을 지정한다.

