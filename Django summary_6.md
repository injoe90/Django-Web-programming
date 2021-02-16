# CSS 활용(3) : 템플릿 확장하기

> 1. 부모 템플릿 작성
> 2. 자식 템플릿 작성



## 1. 부모 템플릿 작성

```python
{% load static %}

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <link rel="stylesheet" type="text/css" href="{% static 'css/shop2.css' %}">
    <style>
    </style>
</head>
<body>
    {% block content %}
    {% endblock %}
</body>>
</html>>
```

 * 'base.html'은 부모 템플릿 기능을 수행하며 서로 다른 페이지에서 동일하게 다시 사용된다. 이떄, Templates 폴더에 따로 저장한다.
    *  화면을 이동할 때 내용이 바뀌는 부분은 자식 템플릿 기능을 한다. 부모 템플릿에서 상속을 받기 때문에 자식 템플릿에 해당하는 부분을 삭제하고 {% block content %} ~ {% endblock %}을 지정한다.
      	* {% block content %} ~ {% endblock %}에 해당하는 부분은 따로 자식 템플릿으로 저장되며 base.html을 상속받는다.



## 2. 자식 템플릿 작성

```python
{% extends "base.html" %}

{% load static %}
{% block content %}
    <style>
        header > h1 > a{
            color: white;
        }
    </style>
    <header>
        <h1><a href="{% url 'shop2' %}">Naningu.com</a></h1>
    </header>
    <nav>
        <ul>
            <li><a href="{% url 'userlist' %}">User List</a></li>
            <li><a href="{% url 'useradd' %}">User Add</a></li>
            <li><a href="{% url 'itemlist' %}">Item List</a></li>
            <li><a href="{% url 'itemadd' %}">Item Add</a></li>
        </ul>
    </nav>
    {% if section == 'userlist' %}
        {% include "shop2/userlist.html" %}
    {% elif section == 'useradd' %}
        {% include "shop2/useradd.html" %}
    {% elif section == 'itemlist' %}
        {% include "shop2/itemlist.html" %}
    {% elif section == 'itemadd' %}
        {% include "shop2/itemadd.html" %}
    {% elif section == 'userdetail' %}
        {% include "shop2/userdetail.html" %}
    {% else %}
        {% include "shop2/mainsection.html" %}
    {% endif %}
    <footer>
    </footer>
{% endblock %}
```

	* 자식 템플릿에 {% extends "base.html" %}을 추가하면 부모 템플릿을 상속받는다.
 * {% block content %} ~ {% endblock %} 사이에 수정할 부분을 작성한다.
   	* 장고에서 템플릿 태그를 이용하여 if문을 작성할 때에는 반드시 {% endif %}를 마지막에 삽입해야 한다.



```python
{% load static %}

<section>
    <h1>User List</h1>
    {% for u in rsusers %}
    <h3><a href="{% url 'userdetail' %}?id={{ u.id }}">{{ u.id }}</a>,{{ u.name }}</h3>
    {% endfor %}
</section>
-------------------------------------------------------------------------------
{% load static %}

<section>
    <h1>User Add</h1>
    <form action="{% url 'useraddimpl' %}" method="post">
        {% csrf_token %}
        ID<input type="text" name="id"><br>
        PWD<input type="text" name="pwd"><br>
        NAME<input type="text" name="name"><br>
        <input type="submit" value="REGISTER">
    </form>
</section>
```

 * {% url 'userdetail' %}?id={{ u.id }} : 쿼리 문자열(Query string)로써 물음표 앞에 있는 것은 서버의 웹 프로그램을, 뒤에 있는 것은 데이터를 뜻한다. GET방식으로 데이터를 전송한다.
   	* 장고에서는 서버에서 받는 자료를 저장할 때에는 {{ 자료 }}로 나타낸다.



```python
{% load static %}

<section>
    <h1>User Detail</h1>
    <h2>ID: {{rsuser.id}}</h2>
    <h2>PWD: {{rsuser.pwd}}</h2>
    <h2>NAME: {{rsuser.name}}</h2>
</section>
-----------------------------------------------
from django.contrib import admin
from django.urls import path, include
from django.views.generic import TemplateView

from shop2 import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', TemplateView.as_view(template_name='shop2/shop2.html'),name='shop2'),
    path('userlist',views.userlist, name='userlist'),
    path('useradd',views.useradd, name='useradd'),
    path('useraddimpl',views.useraddimpl, name='useraddimpl'),
    path('itemlist',views.itemlist, name='itemlist'),
    path('itemadd',views.itemadd, name='itemadd'),
    path('userdetail',views.userdetail, name='userdetail'),
]
-------------------------------------------------------------------------------
from django.shortcuts import render

# Create your views here.
def userlist(request):
    rsuserlist = [
        {'id': 'id01', 'pwd': 'pwd01', 'name': 'james01'},
        {'id': 'id02', 'pwd': 'pwd02', 'name': 'james02'},
        {'id': 'id03', 'pwd': 'pwd03', 'name': 'james03'},
        {'id': 'id04', 'pwd': 'pwd04', 'name': 'james04'},
        {'id': 'id05', 'pwd': 'pwd05', 'name': 'james05'}
    ];
    context = {
        'section':'userlist',
        'rsusers':rsuserlist
    };
    return render(request,'shop2/shop2.html',context)

def userdetail(request):
    id = request.POST['id'];
    rsuser = {'id':id,'pwd':'pwd99','name':'이말숙'};
    context = {
        'section': 'userdetail',
        'rsuser': rsuser
    };
    return render(request, 'shop2/shop2.html',context)

def useradd(request):
    context = {
        'section': 'useradd'
    };
    return render(request,'shop2/shop2.html',context)

def useraddimpl(request):
    id = request.POST['id'];
    pwd = request.POST['pwd'];
    name = request.POST['name'];
    ruser = {};
    ruser['id'] = id;
    ruser['pwd'] = pwd;
    ruser['name'] = name;
    context = {
        'section':'userdetal',
        'rsuser':ruser
    };
    return render(request,'shop2/shop2.html',context)

def itemlist(request):
    context = {
        'section': 'itemlist'
    };
    return render(request,'shop2/shop2.html',context)
def itemadd(request):
    context = {
        'section': 'itemadd'
    };
    return render(request,'shop2/shop2.html',context)
```



