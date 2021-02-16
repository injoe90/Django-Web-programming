# jQuery 이해

> 1. jQuery의 특징
> 2. 함수
> 3. Ajax



## 1. jQuery의 특징



```python
# views.py
from django.contrib import admin
from django.urls import path, include
from django.views.generic import TemplateView

from jq import views

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', TemplateView.as_view(template_name='jq1.html'),name='jq1'),
    path('/jq2', TemplateView.as_view(template_name='jq2.html'),name='jq2'),
    path('/jq3', TemplateView.as_view(template_name='jq3.html'),name='jq3'),
    path('/jq4', TemplateView.as_view(template_name='jq4.html'),name='jq4'),
    path('/jq5', TemplateView.as_view(template_name='jq5.html'),name='jq5'),
    path('/login', views.login, name='login'),
]

# jq1.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
    <script>
        $(document).ready(function(){
            $('h1').html('<a href="">abc</a>');
            $('#hh2').html('<a href="">id test</a>');
            $('.c1').html('<a href="">class test</a>');
            $('h3').css('color','red');
            $('h4').css({'color':'red','background':'black'});
        });
    </script>
</head>
<body>
    <h1>jquery test 1</h1>
    <h1>jquery test1</h1>
    <h2 id="hh2">jquery test1</h2>
    <h2 class="c1">jquery test2</h2>
    <h4>hahaha</h4>
</body>
</html>
```

 * jQuery는 자바스크립트 라이브러리 중 하나이다.
   	* JavaScript Programming을 아주 쉽고 빠르게 할 수 있다.
   	* jQuery는 배우기 쉽다.
    * jQuery는 오픈소스 라이브러리이다.
      	* 이벤트 처리가 쉽다.
      	* HTML DOM 관련 처리가 쉽다.
      	* CSS 관련 처리가 쉽다.
      	* AJAX 관련 처리가 쉽다.
      	* 모든 브라우저에서 동일하게 동작한다.
      	* 다양한 함수와 플러그인을 제공한다.



	* jQuery.org에서 라이브러리를 받고 서비스를 하려는 서버에 이를 설치한다.
 * CDN(Content Delivery Network) 방식을 이용하면 특정 서버에서 실시작으로 동작할 때 받아서 라이브러리를 웹 페이지에 설치하여 사용한다. 다만, 외부 인터넷 망이 막힌 사이트에서는 사용할 수 없다.
   	* '<script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"> </script>'



## 2. 함수



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
    <style>
        div{
            width:300px;
            height:300px;
            background:yellow;
            border: 2px solid red;
        }
    </style>
    <script>
        $(document).ready(function(){
            $('h1').click(function(){
                alert('h1');
            });
            $('a').click(function(){
                $('div').hide();
            });
            $('button').click(function(){
                 $('div').show();
            });
        });
    </script>
</head>
<body>
    <h1>Click1</h1>
    <a href="#">Click2</a>
    <button>Click3</button>
    <div></div>
</body>
</html>
```

 * jQuery 문법은 다음과 같다.
    * $(selector).action()
      	* '<script> window.onload = function(){ }; </script>'
      	* '<script> $(document).ready(function(){ }); </script>'
   	* jQuery selector는 HTML element를 자유롭게 선택할 수 있도록 다양한 형식을 제공한다.
    * jQuery 이벤트 함수 중 click()은 클릭 이벤트를 처리한다.
      	* hide() : 해당 element와 영역을 사라지게 한다.
      	* show() : 해당 element를 다시 나타나게 한다.



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
    <script>
        $(document).ready(function(){
            $('input[name="id"]').focus();
            $('#login_form > button').click(function(){
                id = $('input[name="id"]').val();
                pwd = $('input[name="pwd"]').val();
                if(id == '' || id == null){
                    alert('ID is mandatory field...');
                    $('input[name="id"]').focus();
                    // return하면 더 이상 진행하지 말라는 의미
                    return;
                };
                if(pwd == '' || pwd == null){
                    alert('PWD is mandatory field...');
                    $('input[name="pwd"]').focus();
                     // return하면 더 이상 진행하지 말라는 의미
                    return;
                };
                // 입력이 끝났으면 서버로 전송
                $('#login_form').attr({
                    'action':'login',
                    'method':'get'
                });
                $('#login_form').submit();
            });
        });
    </script>
</head>
<body>
    <h1>LOGIN</h1>
    <form id="login_form">
        ID<input type="text" name="id"><br>
        PWD<input type="password" name="pwd"><br>
        <button>LOGIN</button>
    </form>
</body>
</html>
```

 * focus() ; 커서 강제 이동을 지정한다. 이를 해제하려면 blru()를 사용한다.
    * val() : 폼에서 입력된 값을 받아온다.
    * arrt() : 해당 element의 속성 값을 가지고 온다.



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.11.3/jquery.min.js"></script>
    <style>
        div{
            width:400px;
            border:3px solid red;
        }
        .mycss {
            color:yellow;
            background:black;
        }
    </style>
    <script>
        $(document).ready(function(){
            $('button:eq(0)').click(function(){
                $('div').append('<h2>Append</h2>');
            });
            $('button:eq(1)').click(function(){
                $('div').prepend('<h2>prepend</h2>');
            });
            $('button:eq(2)').click(function(){
                $('div').after('<h2>after</h2>');
            });
            $('button:eq(3)').click(function(){
                $('div').before('<h2>before</h2>');
            });
            // 태크를 아예 지워버림
            $('button:eq(4)').click(function(){
                $('div').remove();
            });
            // 안의 내용만 지움
            $('button:eq(5)').click(function(){
                $('div').empty();
            });
            //css를 적용한다
            $('button:eq(6)').click(function(){
                $('h1').addClass('mycss');
            });
            //css를 제거한다
            $('button:eq(7)').click(function(){
                $('h1').removeClass('mycss');
            });
        });
    </script>
</head>
<body>
    <button>Append</button>
    <button>Prepend</button>
    <button>After</button>
    <button>Before</button>
    <button>Remove</button>
    <button>Empty</button>
    <button>CSS ON</button>
    <button>CSS OFF</button>
    <h1>Header1</h1>
    <div></div>
</body>
</html>
```

	* append() : element 영역의 가장 뒷 부분에 HTML을 추가할 수 있다.
	* prepend() : element 영역의 가장 앞 부분에 HTML을 추가할 수 있다.
	* after() : 특정 element의 앞에 HTML을 추가한다.
	* before() : 특정 element의 뒤에 HTML을 추가한다.



	* remove() : 선택한 element의 내부 정보와 영역을 모두 삭제한다.
	* empty() : 선택한 element의 내부 정보만 삭제하고 영역은 유지한다.
	* addClass() : 특정 element에 선언한 class를 삽입할 수 있다.
	* removeClass() : 특정 element에 선언한 class를 제거할 수 있다.



## 3. AJAX

	* AJAX는 JavaScript에 추가된 통신 방식으로 화면 전체를 다시 불러오지 않고도 서버에서 특정 데이터를 송수신할 수 있다.
 * AJAX는 빠르고 동적인 웹 페이지를 만들기 위한 기술이다.
   	* 웹 페이지가 서버와 데이터를 교환하여 비동기적으로 갱신할 수 있다.
   	* 전체 페이지를 다시 불러오지 않고 일부만을 갱신할 수 있다.
	* jQuery에서 기본적으로 $.ajax({name:value, name:value, ...})를 제공한다.