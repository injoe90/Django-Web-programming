# JavaScript 이해

> 1. JavaScript의 특성
> 2. JavaScript의 특징



## 1. JavaScript의 특성

	* 한번 화면에 출력되면 언제나 모습이 그대로인 정적 HTML과 달리 사용자의 조작에 반응해서 프로그램이 움직이게 하는 기술이 JavaScript이다.
	* HTML 내부 태그와 속성 값을 자유롭게 변경하거나 추가할 수 있다.
	* HTML 태크에서 다양한 CSS를 바꿀 수 있다.
	* JavaScript를 통해 화면에 입력한 데이터의 검정 작업을 할 수 있다.
	* 화면 이벤트 처리 및 행위를 제어할 수 있다.
 * 다양한 API를 제공하며 웹 페이지에서 프로그램 부분을 담당한다.
   	* API(Application Programming Interface)는 응용 프로그램에서 사용할 수 있도록 운영 체제나 프로그래밍 언어가 제공하는 기능을 제어할 수 있게 만든 인터페이스를 뜻한다.



## 2. JavaScript의 특징

```python
from django.contrib import admin
from django.urls import path, include
from django.views.generic import TemplateView

urlpatterns = [
    path('admin/', admin.site.urls),
    path('', TemplateView.as_view(template_name='home.html'),name='home'),
    path('js1', TemplateView.as_view(template_name='js1.html'),name='js1'),
    path('js2', TemplateView.as_view(template_name='js2.html'),name='js2'),
    path('js3', TemplateView.as_view(template_name='js3.html'),name='js3'),
    path('js4', TemplateView.as_view(template_name='js4.html'),name='js4'),
    path('js5', TemplateView.as_view(template_name='js5.html'),name='js5'),
    path('js6', TemplateView.as_view(template_name='js6.html'),name='js6'),
    path('js7', TemplateView.as_view(template_name='js7.html'), name='js7'),
    path('js8', TemplateView.as_view(template_name='js8.html'), name='js8'),
    path('js9', TemplateView.as_view(template_name='js9.html'), name='js9'),
    path('js10', TemplateView.as_view(template_name='js10.html'), name='js10'),
]

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
    window.onload = function(){
        document.querySelector('h1').innerHTML = '<a href="">Click1</a>';
        document.querySelector('h1').innerHTML = '<a href="">Click2</a>';
        console.log('Start Web Page....')
    };
    function clickh3(){
        alert('clicked h3....');
    };
    </script>
</head>
<body>
    <h1>Header1</h1>
    <h2>Header2</h2>
    <h3 onclick="clickh3();">Header3</h3>
</body>
</html>
```

 * (1) '<head>' : '<script>', (2) '<body>', (3) 프로젝트 내 외부 폴더에 저장된 JavaScript 파일('파일이름.js')
    
    	* '<script src="myScript.js"></script>'
    
    
    
* JavaScript DOM(Document Object Model)은 문서에 접근하기 위한 표준을 정의한다.

    * HTML DOM은 웹 브라우저를 위한 문서 표준이며 HTML을 위한 프로그램 인터페이스이다.
    * JavaScript를 통해 HTML DOM을 접근하고 위의 모든 작업을 진행하며 동적 HTML을 만들 수 있다.



* Fiding HTML Element는 HTML을 조작하기 위해 모든 요소에 접근하는 방법을 제공한다.
  * document.getElementById() : id를 통해 element를 찾는다.
  * document.getElementByTagName() : name을 통해 element를 찾는다.
  * document.getElementByClassName() : class를 통해 element를 찾는다.
  * document.querySelector() : id, name, class 등 다양한 형태로 element를 찾는다.
    * document.querySelector(element).value == '#???#'
  * document.querySelectorAll() : 복수로 element를 찾는다.
    * document.querySelectorAll('a') : 웹 페이지에 있는 모든 <a> 태그를 가져오기
    * 출력결과는 리스트 형태로 나타난다.
* Changing HTML Element는 HTML Element를 변경하기 위한 방법을 제공한다.
  * element.innerHTML : element 내부의 내용을 변경한다.
  * element.style.property: style을 변경한다.
  * element.attribute / element.setAttribute(attribute, value) : 속성 값을 변경한다.



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        var n1 = 10.1;  // 10
        var n2 = 'abc'; //"abc"
        var n3 = true;
        var n4 = [1,2,3,4,5];
        var n5 = {'id':'id01','name':'james','age':30} //JSON//
        var n6; //undefined
        var n7 = function(){    //변수에 함수를 넣을 수 있음
        };
        //alert(typeof(n7));
        var a = '100';
        var b = 200;
        //alert(Number(a)+b);

        var str = 'jmlee@naver.com';
        var id = str.substring(0,str.indexOf('@'));
        var domain = str.substring(str.indexOf('@')+1, str.indexOf('.'));
        alert(id);
        alert(domain);
    </script>
</head>
<body>
    <h1>Header1</h1>
    <h2>Header2</h2>
    <h3 onclick="clickh3();">Header3</h3>
</body>
</html>
```

* JavaScript에서는 모든 변수 선언을 var로 선언한다.
* 변수, 함수, 객체 생성할 때 문자, 숫자, _, $를 포함할 수 있다.
  * 공백은 포함할 수 없다.
  * 반드시 문자 또는 _, $로 시작해야 하며 숫자로 시작할 수 없다.
  * 문자는 대소를 구분한다.
  * 예약어는 사용할 수 없다.
* string 변환을 위한 다양한 함수가 있다.
  * substring(start, end) : start에서 end-1까지 위치한 하위 문자열을 반환한다.
  * indexOf(number) : 특정 위치의 문자열을 반환한다.
  * trim() : 문자열 양 옆의 공백을 없애고 반환한다.



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
    function a(d1){
        var result = d1 * 1000;
        alert('a...'+result);

    };
    function c(d1){
        var result = d1 * 1000;
        return result;
    };
    var b = function(d2){
        alert('b...'+d2);
    };
    //a(100);
    //b('abc');
    //rs = c(200);
    //alert(rs);
    var f1 = function(){
        return 10;
    };
    function f2(f){
        result = 100 * f();
        return result;
    };
    rs = f2(f1);
    alert(rs);

    var f3 = function(){
        return function(){
            return 10;
        };
    };

    rsf = f3();
    alert(rsf());

    str1 = 'alert("abc");';
    eval(str1);

    // JSON 이 아닌 단순 스트링 형태
    //str2 = '{"id":"id01","age":30. "score":[90,80,90,100]}';
    // eval()함수를 통해 JSON 형식으로 바꾸어줌
    //obj1 = eval(str2);
    //alert(obj1.id);
    </script>
</head>
<body>
    <h1>Header1</h1>
    <h2>Header2</h2>
    <h3 onclick="clickh3();">Header3</h3>
</body>
</html>
```

 * JavaScript에서는 함수 선언을 함수 이름과 변수 이름으로 할 수 있다.
   * (1) function funcA(){alert('Function A')};
   * (2) var funcB = function(){alert('Function B')};
* JSON(JavaScript Object Notation)은 경량 형식으로 데이터를 시스템 간 전송에서 사용된다. JavaScript에서 해석과 데이터 추출에 편리하다.



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        var a = 10;
        if(a > 100){
            alert('big number');
        }else{
            alert('small number');
        };
        var nums = [1,2,3,4,5];
        var sum = 0;
        for(i in nums){
            sum += eval(i);
        };
        alert(sum);
    </script>
</head>
<body>
    <h1>Header1</h1>
    <h2>Header2</h2>
    <h3 onclick="clickh3();">Header3</h3>
</body>
</html>
-------------------------------------------------------------------------------
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        div{
            width:100px;
            border:2px solid red;
        }
    </style>
    <script>
    function display(data){
        var result = '';
        for(u in data){
            result += '<h1>';
            result += data[u].id+' '+data[u].name+' '+data[u].age;
            result += '</h1>';
        };
        document.querySelector('div').innerHTML = result;
    };
    function getData(){
        var users = [
            {'id':'id01','name':'james','age':10},
            {'id':'id02','name':'james','age':20},
            {'id':'id03','name':'james','age':30},
            {'id':'id04','name':'james','age':40},
            {'id':'id05','name':'james','age':50},
            {'id':'id06','name':'james','age':60},
        ];
        display(users);
    };
    </script>
</head>
<body>
    <button onclick="getData();">GET DATA</button>
    <div>


    </div>
</body>
</html>
```

	* if (조건 1) { }else if (조건 2) { } else { }
	* for ( 변수 in 배열) { 반복 형식 }



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        function gonaver(){
            var c = confirm('Go Naver.....?');
            if(c == true){
                location.href='http://www.naver.com';
            }else {
                return;
            };
        };
        function godaum(){
            var c = confirm('Go Daum.....?');
            if(c == true){
                location.href='http://www.daum.net';
            }else {
                return;
            };
        };

    </script>
</head>
<body>
    <a href="#" onclick="gonaver();">NAVER</a>
    <button onclick="godaum();">DAUM</button>
</body>
</html>
```

 * onclick은 마우스로 개체를 클릭 할 때 발생하는 이벤트를 지정한다. 
    * "함수();"를 작성하여 이 함수의 실행을 설정할 수 있다.
    * this는 일반적으로 메서드를 호출한 객체가 저장되어 있는 속성이다.
       * 일반 함수와 중첩 함수, 메서드 내부의 중첩 함수에서는 window가 된다.
       * 이벤트에서는 이벤트 객체가 된다.
       * 메서드에서는 메서드 객체가 된다.



```python
<script>
    setTimeout(function(){
        location.href='http://127.0.0.1:8000/js7';
    }, 3000);
</script>

<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script>
        window.onload = function(){
            // 주기적으로 서버에 요청해서 변화된 내용을 화면에 뿌러줄 수 있는 함수
            setInterval(function(){
                date = new Date();
                str = date.getHours()+':'+date.getMinutes()+':'+date.getSeconds();
                document.querySelector('h1').innerHTML = str;
            }, 1000);
        };

    </script>
</head>
<body>
<h1></h1>
</body>
</html>
```

 * BOM(Browser Object Model)은 JavaScript를 통해 Brwoser에서 제공하는 기능을 제어하는 방법을 제공한다.
   	* window : 현재 동작하는 브라우저의 window 정보를 사용할 수 있다.
      	* screen : 현재 시스템의 화면 정보를 사용할 수 있다.
   	* location : url 정보를 사용할 수 있다.
   	* navigator : 웹 브라우저 정보를 사용할 수 있다.
   	* popup : 다양한 popup box를 제공한다.
   	* timing : 다양한 timer를 사용할 수 있다.



 * window.onload는 JavaScript에서 페이지가 불러오면 자동으로 실행하는 전역 함수이다.
   	* 페이지의 모든 요소가 불러와야만 호출할 수 있으며 한 페이지 당 한 개만 적용할 수 있다.
    * window.onload = function(){시작할 때 실행할 내용}
      	* location.href='url 주소' : 현재 페이지의 href (url)을 반환한다.
       * setinterval(function, milliseconds) : 반복적인 이벤트 타이밍을 제공한다.
         	* milliseconds : 천 분의 1초를 의미한다.



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <script src="https://code.highcharts.com/highcharts.js"></script>
    <script src="https://code.highcharts.com/modules/exporting.js"></script>
    <script src="https://code.highcharts.com/modules/export-data.js"></script>
    <script src="https://code.highcharts.com/modules/accessibility.js"></script>
    <script>
        function display(datas){
            Highcharts.chart('container', {
                chart: {
                    type: 'column'
                },
                title: {
                    text: 'World\'s largest cities per 2017'
                },
                subtitle: {
                    text: 'Source: <a href="http://en.wikipedia.org/wiki/List_of_cities_proper_by_population">Wikipedia</a>'
                },
                xAxis: {
                    type: 'category',
                    labels: {
                        rotation: -45,
                        style: {
                            fontSize: '13px',
                            fontFamily: 'Verdana, sans-serif'
                        }
                    }
                },
                yAxis: {
                    min: 0,
                    title: {
                        text: 'Population (millions)'
                    }
                },
                legend: {
                    enabled: false
                },
                tooltip: {
                    pointFormat: 'Population in 2017: <b>{point.y:.1f} millions</b>'
                },
                series: [{
                    name: 'Population',
                    data: datas,
                    dataLabels: {
                        enabled: true,
                        rotation: -90,
                        color: '#FFFFFF',
                        align: 'right',
                        format: '{point.y:.1f}', // one decimal
                        y: 10, // 10 pixels down from the top
                        style: {
                            fontSize: '13px',
                            fontFamily: 'Verdana, sans-serif'
                        }
                    }
                }]
            });
        };
        function getdata(){
            // 서버에서 데이터 가져온다
            var datas = [
                        ['Shanghai', 24.2],
                        ['Beijing', 20.8],
                        ['Karachi', 14.9],
                        ['Shenzhen', 13.7],
                        ['Guangzhou', 13.1],
                        ['Istanbul', 12.7],
                        ['Mumbai', 12.4],
                        ['Moscow', 12.2],
                        ['São Paulo', 12.0],
                        ['Delhi', 11.7],
                        ['Kinshasa', 11.5],
                        ['Tianjin', 11.2],
                        ['Lahore', 11.1],
                        ['Jakarta', 10.6],
                        ['Dongguan', 10.6],
                        ['Lagos', 10.6],
                        ['Bengaluru', 10.3],
                        ['Seoul', 9.8],
                        ['Foshan', 9.3],
                        ['Tokyo', 9.3]
                    ];
            // 가져온 데이터를 화면에 뿌린다
            display(datas);
        };
    </script>
</head>
<body>
    <button onclick="getdata();">Graph1</button>

    <figure class="highcharts-figure">
    <div id="container"></div>
    <p class="highcharts-description">
        Chart showing use of rotated axis labels and data labels. This can be a
        way to include more labels in the chart, but note that more labels can
        sometimes make charts harder to read.
    </p>
    </figure>
</body>
</html>
```

