# HTML에서 작동하기 위한 기능 설정하기(2)

> 3. 데이터베이스에 있는 정보 수정/삭제하기
> 4. 로그인/로그아웃



## 3. 데이터베이스에 있는 정보 수정/삭제하기

```python
def userupdate(request):
    id = request.GET['id'];
    user = UserDb().selectone(id);
    context = {
        'section': 'shop2/userupdate.html',
        'uuser':user,
    };
    return render(request, 'shop2/shop2.html',context)

def userdelete(request):
    id = request.GET['id'];

    try:
        UserDb().delete(id);
    except:
        context = {
            'section': 'shop2/error.html',
            'error': ErrorCode.e0002
        };
        return render(request,'shop2/shop2.html',context);
    return redirect('userlist');

{% load static  %}

<section>
      <h1>User Update</h1>
      <form action="{% url 'userupdateimpl' %}" method="post">
            {% csrf_token %}
            ID<input type="text" name="id" value="{{uuser.id}}" readonly="true"><br>
            PWD<input type="text" name="pwd" value="{{uuser.pwd}}"><br>
            NAME<input type="text" name="name" value="{{uuser.name}}"><br>
            <input type="submit" value="UPDATE">
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
	def itemupdate(request):
        id = request.GET['id'];
        item = ItemDb().selectone(int(id));
        context = {
            'section': 'shop2/itemupdate.html',
            'item':item,
        };
        return render(request, 'shop2/shop2.html', context)
        
{% load static  %}

<section>
      <h1>Item Update</h1>
      <form action="{% url 'itemupdateimpl' %}" method="post"
      enctype="multipart/form-data">
            {% csrf_token %}
            ID:{{item.id}}<br>
            NAME<input type="text" name="name" value="{{item.name}}"><br>
            PRICE<input type="number" name="price" value="{{item.price}}"><br>
            IMG:{{item.imgname}}<br>
            NEWIMG<input type="file" name="newimg"><br>
            <input type="hidden" name="id" value="{{item.id}}">
            <input type="hidden" name="img" value="{{item.imgname}}">
            <input type="submit" value="REGISTER">
      </form>
</section>

class ItemView:
	def itemupdateimpl(request):
        id = request.POST['id'];
        name = request.POST['name'];
        price = request.POST['price'];
        img = request.POST['img'];

        imgname = '';
        if 'newimg' in request.FILES:
            newimg = request.FILES['newimg']
            imgname = newimg._name

            fp = open('%s/%s' % (UPLOAD_DIR, imgname), 'wb')
            for chunk in newimg.chunks():
                fp.write(chunk);
                fp.close();
        else:
            imgname = img;

        ItemDb().update(int(id),name,int(price),imgname);
        qstr = urlencode({'id': id})
        return HttpResponseRedirect('%s?%s' % ('itemdetail', qstr))
```

 * urlencode는 퍼센트 인코딩이라고도 하며 url에 문자를 표현할 수 있게 한다.
   	* GET 방식을 통해 HTTP 요청을 할 때 쿼리 모수가 붙을 수 있다. URL은 ASCII 코드값만 사용하며 쿼리 모수에 한글이 포함될 경우에는 이를 ASCII 코드만으로는 표현할 수 없다.
   	* 따라서 미리 인코딩을 거친 형식으로 전송하는 것이 바람직하다.
 * HttpResponseRedirect는 지정된 url 페이지로 다시 호출할 때 사용한다.
   	* 선형 포멧팅을 통해 만든 쿼리 문자열로 url 페이지를 지정한다.
   	* 쿼리 문자열을 통해 url과 id값을 함께 전송할 수 있다.



## 4. 로그인/로그아웃

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

class MainView:
    def login(request):
        context = {
            'section': 'shop2/login.html'
        };
        return render(request, 'shop2/shop2.html', context)

{% load static %}
<script>
$(document).ready(function(){
    $('#login_form > input[type="button"]').click(function(){
        $('#login_form').attr({
            'action':'{% url "loginimpl" %}',
            'method':'POST'
        });
        $('#login_form').submit();
    });
});
</script>

<section>
    <h1>LOGIN PAGE</h1>
    <form id="login_form">
        {% csrf_token %}
        ID<input type="text" name="id"><br>
        PWD<input type="password" name="pwd"><br>
        <input type="button" value="LOGIN"><br>
    </form>
</section>

class MainView:
     def loginimpl(request):
        id = request.POST['id'];
        pwd = request.POST['pwd'];
        try:
            user = UserDb().selectone(id);
            if pwd == user.pwd:
                request.session['suser'] = id;
                context = {
                    'section': 'shop2/loginok.html',
                    'loginuser': user
                };
            else:
                raise Exception;
        except:
            context = {
                'section': 'shop2/error.html',
                'error': ErrorCode.e0003
            };
        return render(request, 'shop2/shop2.html', context);

{% load static  %}

<section>
      <h1>Login OK</h1>
      <h2>{{loginuser.name}} 님 환영합니다.</h2>
</section>
```

 * {% if %} ~ {% endif %}를 통해 로그인을 하지 않았을 때와 한 경우에 대해 출력될 화면을 구분한다.
   	* request.session.suser은 views.py의 loginimpl 함수에서 장고의 session을 이용한 것이다.
    * 장고에서 session은 클라이언트별 정보를 웹 서버에 저장하는 것을 뜻한다.
      	*  같은 브라우저를 사용하면 링크를 통해서 다른 사이트로 이동할 떄에도 sessionId는 쿠키로 쭉 유지된다. 브라우저를 닫으면 사라진다.
      	* 쿠키는 클라이언트의 정보를 웹 브라우저에 저장하는 기술이다.
       * 장고의 sesstion은 쿠키에 sessionId만을 저장하여 클라이언트와 웹 서버 간 연결성을 확보한 뒤에 sessionId를 통해 커뮤니케이션을 실행한다.
         	* (1) 유저가 웹사이트에 접속한다.
         	* (2) 웹사이트의 서버가 유저에게 sessionId를 부여한다.
         	* (3) 유저의 브라우저가 이 sessionId를 cookie에 보존한다.
         	* (4) 통신할 때마다 sessionId를 웹 서버에 전송한다. 장고는 request 객체에 sessionId가 있다.
         	* (5) sessionId에 의해 웹사이트는 수많은 유저 중 특정 유저를 인식할 수 있다.



	* 

