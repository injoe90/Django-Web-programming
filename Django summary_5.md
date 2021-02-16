# CSS 활용(2)



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        *{
            margin:0;
            padding:0;
        }
        div{
            float:left;
        }
        #div1{
            width:300px;
            height:200px;
            border: 2px solid red;
            margin:50px 0 0 0;
            overflow: auto;
        }
        #div1 > p {
            display:inline;
        }

        #div1 > span{
            display:block
        }
        #div2{
            width:300px;
            height:200px;
            border: 2px solid blue;
        }
        #div3{
            width:300px;
            height:200px;
            border: 2px solid black;
        }
    </style>
</head>
<body>
    <h1>CSS03 Main Page</h1>
    <div id="div1"></div>
        <p>Paragraph1</p>
        <p>Paragraph1</p>
        <p>Paragraph1</p>
    <div id="div2"></div>
    <div id="div3"></div>
</body>
</html>
```

 * 일반적으로 화면의 크기를 1000px로 상정한다.
 * margin은 바깥쪽 여백을, padding은 안쪽 여백을 조정한다. 
    * margin에 대해 auto를 조건으로 지정하면 화면 크기에 따라 자동으로 가운데 정렬을 한다. 이때, width가 항상 0보다 커야 한다.
      	* CSS에서는 크기가 0일 때 px를 쓰지 않아도 된다.
    * overflow는 내용이 요소의 크기를 벗어났을 떄 처리 방법을 정하는 속성이다.
      	* 속성을 auto로 지정하면 상자를 넘어가면 스크롤바가 나오고 그렇지 않으면 스크롤바도 표시하지 않는다.
      	* 속성을 scroll로 지정하면 상자를 넘어가는 여부에 관계없이 스크롤바가 나타난다. 



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        *{
            margin:0;
            padding:0;
        }
        a{
            text-decoration:none;
            color:black;
        }
        ul, ol{
            list-style:none;
        }
        header{
            width: 900px;
            height: 150px;
            background:black;
            color:white;
            text-align:center;
            margin:0 auto;
            line-height: 150px;
            font-weight: 1.5em;
        }
        nav{
            width: 900px;
            height: 50px;
            line-height: 50px;
            margin: 0 auto;
            border-bottom:1px solid black;
        }

        nav > ul{
            width:600px;
            margin:0 auto;
        }

        nav > ul >li{
            float:left
        }

        nav > ul > li > a{
            display: block;
            width:150px;
            font-size:1.5em;
            text-align:;center;
        }

        nav > ul > li > a:hover{
            color:yellow;
            background:black;
        }
        section{
            width:900px;
            height:400px;
            background:blue;
            margin:0 auto;
        }
        footer{
            width:900px;
            height:30px;
            background:black;
            margin:0 auto;
        }
    </style>
</head>
<body>
    <h1>CSS 04 Page</h1>
    <header>
        <h1>Naningu.com</h1>
    </header>
    <nav>
        <ul>
            <li><a href="">HTML5</a></li>
            <li><a href="">CSS3</a></li>
            <li><a href="">jQuery</a></li>
            <li><a href="">AJAX</a></li>
        </ul>
    </nav>

    <section>

    </section>

    <footer>

    </footer>
</body>
</html>
```

 * float은 '<div>'로 구분한 영역을 1줄로 나란히 정렬하며 블록 속성인 모든 태그에 적용할 수 있다.
   	* 오른쪽 혹은 왼쪽 정렬만 가능하다.
    * 블록 속성 : '<div>', '<p>', '<ul>', '<li>'
      	* '<header>', '<nav>', '<section>', '<footer>', '<aside>'는 모두 '<div>'의 일종으로 HTML5에서 제공하는 편의 기능이다.
   	* 인라인 속성 : '<span>'
    * display는 블록 속성을 인라인 속성으로 혹은 이와 반대로 바꾸는 기능을 한다.
      	* display : none으로 하면 화면에서 해당 태그와 이 태그가 차지한 영역을 사라지게 할 수 있다. 반면에, visibility : hidden으로 하면 태그만 사라지고 영역은 그대로 남는다.



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        *{
            margin:0;
            padding:0;
        }
        a{
            text-decoration:none;
            color:black;
        }
        ul, ol{
            list-style:none;
        }
        header{
            width: 900px;
            height: 150px;
            background:black;
            color:white;
            text-align:center;
            margin:0 auto;
            line-height: 150px;
            font-weight: 1.5em;
        }
        nav{
            width: 900px;
            height: 50px;
            line-height: 50px;
            margin: 0 auto;
            border-bottom:1px solid black;
        }

        nav > ul{
            width:600px;
            margin:0 auto;
        }

        nav > ul >li{
            float:left
        }

        nav > ul > li > a{
            display: block;
            width:150px;
            font-size:1.5em;
            text-align:;center;
        }

        nav > ul > li > a:hover{
            color:yellow;
            background:black;
        }
        section{
            width:900px;
            height:600px;
            background:blue;
            margin:0 auto;
        }

        footer{
            width:900px;
            height:30px;
            background:black;
            margin:0 auto;
        }
        aside{
            float: left;
        }
        #left_aside{
            width:200px;
            height:600px;
            background:gray;
        }

        #center_aside{
            width:600px;
            height:600px;
            background:cyan;
        }

        #right_aside{
            width:100px;
            height:600px;
            background:pink;
        }
    </style>
</head>
<body>
    <h1>CSS 04 Page</h1>
    <header>
        <h1>Naningu.com</h1>
    </header>
    <nav>
        <ul>
            <li><a href="">HTML5</a></li>
            <li><a href="">CSS3</a></li>
            <li><a href="">jQuery</a></li>
            <li><a href="">AJAX</a></li>
        </ul>
    </nav>

    <section>
        <aside id="left_aside"></aside>
        <aside id="center_aside"></aside>
        <aside id="right_aside"></aside>
    </section>

    <footer>

    </footer>
</body>
</html>
```

	* '<aside>' 요소는 문서의 주요 내용과 간접적으로만 연관된 부분을 나타낸다. 주로 사이드바 혹은 콜아웃 박스로 표현한다.
	* list-style:none을 하면 '<ul>', '<ol>'에 적용되는 기본 속성을 배제할 수 있다.
	* '*'은 전체 화면 영역에 대한 속성을 지정한다.
	* 특정 태그 : hover { }는 링크 가상 클래스이다. 사용자의 커서가 요소에 올라있을 때 적용된다.



```python
 *{
            margin:0;
            padding:0;
        }
        a{
            text-decoration:none;
            color:black;
        }
        ul, ol{
            list-style:none;
        }
```



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name = "viewport" content="width=device-width, initial-scale=1.0">
    <title>Title</title>
    <style>
    @media screen and (max-width:767px){
        div{
            width:200px;
            height:200px;
            background:red; } }
    @media screen and (min-width:768px) and (max-width:959px){
        div{
            width:400px;
            height:400px;
            background:blue; } }
    @media screen and (min-width:960px){
        div{
            width:600px;
            height:600px;
            background:cyan; } }
    </style>
</head>
<body>
    <h1>CSS 06 Page</h1>
    <div></div>
</body>
</html>
```

 *  미디어 쿼리(@media)는 미디어 타입(media type: screen, tv, print)와 적어도 하나 이상의 표현식으로 구성된다.
    	*  표현식은 미디어 특성(media feature)을 이용하여 상태에 따라 다른 형식을 적용할 수 있다.
    	*  따라서 반응형 웹에서 주로 사용된다.

