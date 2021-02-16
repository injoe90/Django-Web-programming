# HTML 정리

> 1. 영상 올리기
> 2. 기타



## 1. 영상올리기



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>Today's music</h1>
    <iframe width="640" height="360" src="https://www.youtube.com/embed/vWEbx_8BMeY" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
    <h2><a href="bpage">Back to the main page</a> </h2>
</body>
</html>
```

 * 영상을 올려서 이를 재생하려면 '<video>'와 '<iframe>' 태그를 사용한다.
   	*  '<video scr = "">' : 브라우저 호환성을 고려하여 mp4파일을 사용하는 것이 바람직하다.
   	*  '<video scr = "" controls>' : 영상 화면에서 재생 버튼, 위치, 볼륨 등을 조절할 수 있다. 단순히 controls만 지정하면 이 요소를 조절할 수 있는 패털이 추가된다.
   	*  '<video width="" height="" scr = "" control>' : 크기를 조절하는 단위에서는 px(픽셀)만 사용할 수 있다.
   	* '<iframe>' : 유튜브 채널 페이지의 공유에서 퍼가기를 클릭한 후에 동영상 퍼가기의 소스를 복사한다.



```python
<video width="600px" height="400px" src="" controls autoplay muted playsinlie></video>
```

 * playsinline은 전체 화면으로 전환하지 않고 사이트 내에서 재생을 할 수 있게 한다.
   	* [playsinline], [muted], [autoplay]를 모두 사용해야 사이트 내 재생이 가능하며 이 중에 하나라도 빠지면 실행이 이루어지지 않는다.



```python
<video width="600px" height="400" controls>
	<source src="ma.mp4"></source>
    <source src="ma.webm"></source>
    <source src="ma.ogg"></source>
</video>
```

	* 영상 재생에 대한 에러를 대비하기 위해 여러 개의 파일 확장자를 준비할 수 있다. 



## 2. 기타

>1. div
>
>2.



```python
<div style="width:50px; height:50px; border:1px solid black; background-color:yellow">세 번째 영역</div>
<div style="width:100px; height:50px; border:3px solid black; float:right">네 번째 영역</div>
<div style="width:30; height:30px background-color:green; float:left; margin:30px;">다섯 번째 영역</div>
```

	* '<div>'는 웹페이지에서 논리적 구분을 정의하는 태그이다.
 * 각 공간을 알맞게 배치하고 CSS를 활용하여 스타일을 적용할 수 있다.
   	* style : '<div>' 태그의 스타일을 지정하여 다른 속성을 사용할 수 있게 한다.
   	* border : 테두리의 굴기를 정한다.
   	* float : '<div>'의 정렬(좌우)을 하지만 가울데 정렬을 할 수 없다.
    * margin : '<div>'의 정렬 기준 끝에서 여백을 준다.
      	* margin-top, margin-bottom, margin-left, margin-right