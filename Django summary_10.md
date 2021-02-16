# HTML에서 작동하기 위한 기능 설정하기(1)

> 1. 데이터베이스에 새로운 정보 저장하기
> 2. 데이터베이스에 저장된 정보 출력하기



```python
{% extends "base.html" %}

{% load static %}
{% block content %}

    <style>
        header > h1 > a{
            color: white;
        }
        section > h3 >a> img{
            width:50px;
        }
    </style>
    <header>
        <h1><a href="{% url 'shop2' %}">Naningu.com</a></h1>
    </header>
    <nav id="login_nav">
        {% if request.session.suser == None %}
        <ul>
            <li><a href="{% url 'login' %}">LOGIN</a></li>
            <li><a href="{% url 'useradd' %}">REGISTER</a></li>
            <li><a href="{% url 'itemlist' %}">ABOUT US</a></li>
        </ul>
        {% else %}
        <ul>
            <li><a href="{% url 'login' %}">{{request.session.suser.id}}</a></li>
            <li><a href="{% url 'logout' %}">LOGOUT</a></li>
            <li><a href="{% url 'itemlist' %}">ABOUT US</a></li>
        </ul>
        {% endif %}
    </nav>
    <nav id="main_nav">
        <ul>
            <li><a href="{% url 'userlist' %}">User List</a></li>
            <li><a href="{% url 'useradd' %}">User Add</a></li>
            <li><a href="{% url 'itemlist' %}">Item List</a></li>
            <li><a href="{% url 'itemadd' %}">Item Add</a></li>
        </ul>
    </nav>
    {% if  section != None  %}
        {% include  section %}
    {% else %}
        {% include  "shop2/mainsection.html" %}
    {% endif%}

    <footer></footer>
{% endblock %}

```



## 1. 데이터베이스에 새로운 정보 저장하기

```python
def useradd(request):
    context = {
        'section': 'shop2/useradd.html'
    };
    return render(request, 'shop2/shop2.html',context)

{% load static  %}

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

def useraddimpl(request):
    id = request.POST['id'];
    pwd = request.POST['pwd'];
    name = request.POST['name'];
    try:
        UserDb().insert(id,pwd,name);
    except:
        context = {
            'section': 'shop2/error.html',
            'error': ErrorCode.e0001
        };
        return render(request,'shop2/shop2.html',context);
    return redirect('userlist');
-------------------------------------------------------------------------------
class ItemView:
        def itemadd(request):
        context = {
            'section': 'shop2/itemadd.html'
        };
        return render(request, 'shop2/shop2.html',context)

{% load static  %}

<section>
      <h1>Item Add</h1>
      <form action="{% url 'itemaddimpl' %}" method="post"
      enctype="multipart/form-data">
            {% csrf_token %}
            NAME<input type="text" name="name"><br>
            PRICE<input type="number" name="price"><br>
            IMG<input type="file" name="img"><br>
            <input type="submit" value="REGISTER">
      </form>
</section>

class ItemView:
	def itemaddimpl(request):
        name = request.POST['name'];
        price = request.POST['price'];
        imgname = '';
        if 'img' in request.FILES:
            img = request.FILES['img']
            imgname = img._name

            fp = open('%s/%s' % (UPLOAD_DIR, imgname), 'wb')
            for chunk in img.chunks():
                fp.write(chunk);
                fp.close();

        ItemDb().insert(name,int(price),imgname);
        return redirect('itemlist');
```

	* 폼 데이터를 POST방식으로 전송하려면 반드시 {% csrf_token %}을 입력해야 한다.
 * '<form>' 태그의 enctype 속성은 폼 데이터가 서버로 제출될 때 해당 데이터가 인코딩되는 방법을 명시한다. 
   	* method의 속성 값이 POST인 경우에만 사용할 수 있다.
      	* "multipart/form-data" : 모든 문자를 인코딩하지 않음을 명시하며 폼 요소가 파일이나 이미지를 서버로 전송할 때 주로 사용한다.
 * 바이너리 파일을 쓰기 위해선 open 함수에 'wb'로 지정한다.
   	* 바이너리 파일에는 텍스트를 제외한 이미지, 음성, 영상 등의 파일이 포함된다.





## 2. 데이터베이스에 저장된 정보 출력하기

```python
# views.py
def userlist(request):
    #logger.debug('GET access User List....')
    rsuserlist = UserDb().select();
    context = {
        'section':'shop2/userlist.html',
        'rsusers':rsuserlist
    };
    return render(request, 'shop2/shop2.html',context)

{% load static  %}

<section>
    <h1>User List</h1>
    {% for u in rsusers %}
    <h3><a href="{% url 'userdetail' %}?id={{ u.id }}">{{ u.id }}</a>,{{ u.name }}</h3>
    {% endfor %}
</section>
-------------------------------------------------------------------------------
# views.py
class ItemView:
        def itemlist(request):
        items = ItemDb().select();
        context = {
            'section': 'shop2/itemlist.html',
            'itemlist':items,
        };
        return render(request, 'shop2/shop2.html',context)

{% load static  %}

<section>
      <h1>Item List</h1>
      {% for i in itemlist %}
      <h3>
            <a href="{% url 'itemdetail' %}?id={{i.id}}"><img src="static/img/{{i.imgname}}">
            {{i.name}},{{i.price}},{{i.regdate}}</a>
      </h3>
      {% endfor %}
</section>
```

 * (1) 장고 템플릿 태그를 이용하여 userlist.html, itemlist.html에 for문을 작성한다.
   	* for문에서 적용할 리스트는 shop2에서 userlist/itemlist를 눌렀을 때 전송되는 url 주소에 관한 함수에서 저장된 것이다.
      	* 장고에서 변수를 나타낼 때에는 {{ 변수 }} 또는 {{ 리스트.변수 }}로 나타낸다. 
   	* 장고에서 for문을 작성할 때에는 반드시 {% endfor %}로 마무리해야 한다.
 * (2) userlist.html, itemlist.html에서 데이터가 저장된 개체의 특정 변수(예: 아이디)를 누르면 상세 정보로 이동하는 기능을 구현하려면 쿼리 문자열을 통해 ulr 주소와 변수를 함께 전송할 수 있게 해야 한다.
   	* "{% url 'url 이름' %}"?={{ 변수 }}



```python
def userdetail(request):
    id  = request.GET['id'];
    #logger.debug('user id:'+id)
    rsuser = UserDb().selectone(id);
    context = {
        'section': 'shop2/userdetail.html',
        'rsuser': rsuser
    };
    return render(request, 'shop2/shop2.html',context)
{% load static  %}

<section>
      <h1>User Detail</h1>
      <h2>ID: {{rsuser.id}}</h2>
      <h2>PWD: {{rsuser.pwd}}</h2>
      <h2>NAME: {{rsuser.name}}</h2>
      <a href="{% url 'userdelete' %}?id={{rsuser.id}}">DELETE</a>
      <a href="{% url 'userupdate' %}?id={{rsuser.id}}">UPDATE</a>
</section>
-------------------------------------------------------------------------------
class ItemView:
        def itemdetail(request):
        id = request.GET['id'];
        item = ItemDb().selectone(int(id));
        context = {
            'section': 'shop2/itemdetail.html',
            'item':item,
        };
        return render(request, 'shop2/shop2.html', context)
{% load static  %}

<section>
      <h1>Item Detail</h1>
      <img src="static/img/{{item.imgname}}">
      <h2>ID: {{item.id}}</h2>
      <h2>NAME: {{item.name}}</h2>
      <h2>price: {{item.price}}</h2>
      <h2>regdate: {{item.regdate}}</h2>
      <a href="{% url 'itemupdate' %}?id={{item.id}}">UPDATE</a>
</section>
```

	* 폼 형식으로 전송할 때에는 GET과 POST 방식이 모두 가능하지만 이 외에는 전부 GET 방식만 유효하다.



