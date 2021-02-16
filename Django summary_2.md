# HTML 테이블 만들기

> 1. 테이블 구성 및 디자인
> 2. 폼



## 1. 테이블 구성 및 디자인



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        table{
        width:300px;
        background:yellow;
        }
        table > thead > tr{
            text-align: center;
            background: black;
            color: white;
        }
        table > tbody > tr > td{
            border: 1px solid black;
        }
    </style>
</head>
<body>
    <h1>Table Test</h1>
    <table>
        <thead>
            <tr><td>ID</td><td>PWD</td><td>NAME</td></tr>
        </thead>
        <tbody>
            <tr><td>id01</td><td>pwd01</td><td>james</td></tr>
        </tbody>
    </table>
    <!-- Table 2 -->

    <h1>Table Test</h1>
    <table>
        <caption>Caption Test</caption>
        <thead>
            <tr><td>ID</td><td>ID</td><td>ID</td></tr>
        </thead>
        <tbody>
            <tr><td>1</td><td>2</td><td>3</td></tr>
            <tr><td colspan="2">1</td><td>3</td></tr>
            <tr><td>1</td><td rowspan="2">2</td><td>3</td></tr>
            <tr><td>1</td><td>3</td></tr>
        </tbody>
    </table>
</body>
</html>
```

 * 표 뿐만 아니라 갤러리를 만들 수 있다.
   	* '<table>' : 테이블을 만든다.
   	* '<caption>' : 테이블의 이름을 표시한다.
   	* '<thead>' : 테이블의 헤더 영역(머릿말, 첫 행)을 지정한다.
    * '<hbody>' : 테이블의 바디 영역(내용)을 지정한다.
      	* '<th>' : 테이블의 헤더 부분을 만든다. 테이블의 첫 행에 대해 자동으로 가운데 정렬을 하고 글씨를 굵게 적용한다.
      	* '<tr>' : 테이블의 행을 만든다.
      	* '<td>' : 테이블의 열을 만든다.



 * 표 디자인 뿐만 아니라 브라우저 화면에 표시하는 내용의 스타일을 조정할 때에는 '<head>' 에서 '<style>' 안에 태그를 쓴다.
 * 표 안에 다시 표를 그릴 수 있다.
   	* '<algin>' : 정렬을 지정한다. [left, center, right]
   	* '<border>' : 테두리 선의 두꼐를 "숫자"로 지정한다. 숫자가 높을수록 테두리가 두꺼워진다. 선의 종류에는 solid, dashed, dotted, double 등이 있다.
   	* '<bordercolor>' : 테두리 선 색을 지정한다. "색상" 또는 rgb 형식의 #dddddd와 같이 설정한다. 기본 값은 검정색이다.
   	* '<bgcolor>' / '<background>' : 배경색을 지정하며 '<bordercolor>' 와 방식이 동일하다.
   	* '<cellspacing>' : 셀 간격을 지정한다.
   	* '<width>' : 가로 길이를 지정한다. 상수 값이나 % 단위를 입력할 수 있다. 이때, 후자에 대해선 웹브라우저 크기에 대한 기준을 뜻한다.
   	* '<height>' : 세로 길이를 지정하며 방식은 가로 길이와 똑같다.
   	* '<rawspan>' : 지정한 값만큼 행을 위아래로 병합한다. ['<td rowspan="2">']
   	* '<colspan>' : 지정한 값만큼 열을 좌우로 병합한다. ['<td colspan="2">']



	* table { border-collapse : collapse } td { border: 1px solid red; } : 선이 겹치지 않게 한다.
 * table { border-collapse : collapse } td { border-bottom: 1px solid red; } : 칸의 밑줄만 표시된다. 만약 tr { border-bottom: 1px solid red; }을 입력하면 데이터 사이에 공백이 생긴다. 
   	* border : 전체 / border-top : 윗줄만 / border-bottom : 아랫줄만 / 
   	* border-left : 왼쪽 / border-right : 오른쪽



	* td/tr : nth-child(k) { width: 100px; background: #dddddd;} : k 번째 요소에만 조건을 적용한다. k 대신에 even을 넣으면 짝수 번째에만 조건을 적용한다. odd를 넣으면 홀수 번째에만 조건을 적용한다.
	* tr: not(nth-child(k)) { background : lightgray; } : k 번째 요소에만 조건을 적용하지 않으려면 not 조건을 지정한다.
	* td{padding : 15px 5px 10px 5px;} : 위쪽, 오른쪽, 밑쪽, 왼쪽 순(시계 방향)으로 간격을 준다.



	* '<p>' : 문단을 만드는 태그이다. 문단과 문단 사이의 간격은 크고 문단 내에서 줄바꿈을 하고 싶으면 '<'br>'을 이용한다.



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
    <style>
        table{
            border-collapse: collapse;
            width: 100%;
        }

        table > thead > tr{
            text-align: center;
            background: gray;
            color: white;
        }

        table > tbody > tr > td{
            text-align: center;
        }

        tr:nth-child(even){
            background-color: #dddddd;
        }

    </style>
</head>
<body>
    <h1>Financial statement(1)</h1>
    <table>
        <thead>
            <tr>
                <th>법인 이름</th>
                <th>매출액</th>
                <th>매출총이익</th>
                <th>영업이익</th>
                <th>당기순이익</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>A전자</td>
                <td>1000000</td>
                <td>900000</td>
                <td>450000</td>
                <td>350000</td>
            </tr>
            <tr>
                <td>B통신</td>
                <td>6000000</td>
                <td>5400000</td>
                <td>3500000</td>
                <td>2500000</td>
            </tr>
            <tr>
                <td>C자동차</td>
                <td>100000000</td>
                <td>90000000</td>
                <td>55000000</td>
                <td>45000000</td>
            </tr>
        </tbody>
    </table>

    <h1>Financial statement(2)</h1>
    <table>
        <thead>
            <tr>
                <th>법인 이름</th>
                <th>PER</th>
                <th>PBR</th>
                <th>산업평균 PER</th>
                <th>산업평균 PBR</th>
            </tr>
        </thead>
        <tbody>
            <tr>
                <td>A전자</td>
                <td>7.25</td>
                <td>2.65</td>
                <td>5.58</td>
                <td>2.35</td>
            </tr>
            <tr>
                <td>B통신</td>
                <td>3.25</td>
                <td>1.65</td>
                <td>2.58</td>
                <td>1.35</td>
            </tr>
            <tr>
                <td>C자동차</td>
                <td>3.25</td>
                <td>1.35</td>
                <td>5.58</td>
                <td>2.35</td>
            </tr>
        </tbody>
    </table>
    <h2><a href="bpage">Back to the main page</a> </h2>
</body>
</html>
```



## 2. 폼



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>Form Test</h1>
    <form action="registerapp" method="get">
        ID<input type="text" name="id">
        NAME<input type="text" name="name">
        AGE<input type="number" name="age">
        <input type="submit" value="REGISTER">
    </form>
</body>
</html>
```

 * 폼은 웹 페이지에서 입력 양식을 의미한다 로그인 창, 회원가입 폼 등이 이에 해당한다.
    * 폼을 이용하여 서버에 데이터를 전송한다.
      	* '<form action = "register" method = "get">' : action은 폼 데이터가 전송되는 백엔드 url을, method는 전송 방식(get / post)을 지정한다.
       * 위의 방식을 통해 쿼리 문자열(Query string)을 만들어 백엔드 서버 측에 전달한다.
   	* 테이블과 달리 폼 안에서 다시 폼을 만들 수 없다.



|                              |                get                |           post           |
| :--------------------------: | :-------------------------------: | :----------------------: |
|             보안             |      상대적으로 보완에 취약       |  상대적으로 보안에 강함  |
|         데이터 제한          |      url 허용 길이에서 제한       |        제한 없음         |
|       데이터 유형 제한       |      오직 ASCII 문자만 가능       |        제한 없음         |
| 뒤로 가기 버튼 / 재전송 버튼 |     사용자가 다시 작성해야 함     |     사용자에게 경고      |
|            인코딩            | application/x-www-form-urlencoded | multipart/form-data 또는 |



 * 폼 태그는 전체 양식을 의미하며 화면에 보이지 않는다. 따라서 실제로 사용자가 양식을 입력하기 위한 태그는 '<input>'이다.
   	* 폼 내부에 '<input>' 요소가 많으면 '<fieldset>'을 사용하여 내부 요소를 비슷한 내용끼리 묶는다.
   	* '<fieldset>' 내부에 '<legent>' 요소를 사용하여 식별할 수 있다.



 * '<input>'에서 type 속성을 통해 종류를 나타내고 name을 통해 데이터의 이름을, value를 통해 기본 값을 지정한다.
   	* 폼에 작성한 내용을 스크립트를 통해 서버로 보내려면 식별 이름이 필요하다. 따라서 '<input>'에 name(이름) 속성을 작성한다.
   	* '<input>'에서는 반드시 속성에 값을 명시해야 한다.
   	* '<label>' 요소의 for 속성은 관련 '<input>' 요소의 id 값과 연결된다. 이를 통해 사용자는 접근성 및 사용성을 높일 수 있다.
    * '<select>' 요소 내부에 '<option>' 요소가 많으면 '<optgroup>' 요소를 사용하여 군집화하는 것이 바람직하다.
      	* text : 일반 문자 / password : 비밀번호
      	* number : 숫자(쿼리 문자열에서는 여전히 문자로 입력된다.)
      	* radio : 한 개만 선택할 수 있다. / checkbox : 다수를 선택할 수 있다.
      	* file : 파일을 올릴 수 있다.
      	* hidden : 사용자에게 보이지 않는 숨은 요소이지만 쿼리 문자열에서는 나타난다. 단순히 화면에서 해당 정보를 숨길 때 사용한다.
      	* '<select>' 및 '<option>'은 드롭다운 리스트를 만드는 태그이다.



 * 사용자 데이터를 단순히 서버에 보낼 수 있게 하려면 '<button>' 요소를 사용한다.
   	* submit : 폼 테이터를 action 속성에서 정의된 폼 데이터가 전송되는 백엔드 url에 전송된다.
   	* reset : 모든 폼 위젯을 기본 값으로 바꾼다.

(참고 : https://teilar.tistory.com/entry/%ED%8E%8C-%ED%8F%BCForm-%EB%94%94%EC%9E%90%EC%9D%B8-%EC%9E%98%ED%96%88%EB%8B%A4%EB%8A%94-%EC%86%8C%EB%A6%AC%EB%A5%BC-%EB%93%A3%EA%B8%B0-%EC%9C%84%ED%95%9C-%EB%B0%A9%EB%B2%95%EB%A1%A0)



```python
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    <h1>Register</h1>
    <form action="register" method="get">
        <fieldset>
            <legend>Register Page</legend>

            <input type="color" name="favcolor"><br>
            <input type=“date" name=“regdate"><br>
            <input type="range" name="points" min="0" max="10"><br>


            <label for="id">ID</label>
            <input type="text" name="rid" id="id"><br>
            <label for="pwd">PWD</label>
            <input type="password" name="rpwd" id="pwd"><br>
            <label for="age">AGE</label>
            <input type="number" name="rage" id="age"><br>

            <p>직업</p>
            <label for="job1">선생</label>
            <input type="radio" name="r1" value="cr1" id="job1">
            <label for="job2">교장</label>
            <input type="radio" name="r1" value="cr1" id="job2">
            <label for="job3">학생</label>
            <input type="radio" name="r1" value="cr1" id="job3">

            <p>취미</p>
            <label for="h1">공부</label>
            <input type="checkbox" name="c1" value="ch1" id="h1">
            <label for="h2">운동</label>
            <input type="checkbox" name="c1" value="ch1" id="h2">
            <label for="h3">독서</label>
            <input type="checkbox" name="c1" value="ch1" id="h3">

            <p>자기소개</p>
            <textarea rows="10" cols="50" name="tt"></textarea>

            <p>전화번호</p>
            <select name="p">
                <option value="skt">SKT</option>
                <option value="kt">KT</option>
                <option value="lgt">LGT</option>
            </select>
            <br>
            <input type="hidden" name="loginid" value="user01">
            <input type="submit" value="Register">
            <input type="reset" value="Reset">
        </fieldset>
    </form>
</body>
</html>
```

