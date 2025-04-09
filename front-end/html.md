---
icon: html5
---

# HTML

## HTML 기본 틀

```html
<!DOCTYPE html>
<html lang="ko">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>글자관련태그입니다</title>
</head>
<body>
    <!-- 웹 페이지의 컨텐츠 내용을 이곳에 작성 -->
</body>
</html>
```

## 글자 관련 태그

### 글꼴 크기

```html
<h1></h1>
<h1>h1 태그입니다!</h1>
<h2>h1 태그입니다!</h2>
<h3>h1 태그입니다!</h3>
<h4>h1 태그입니다!</h4>
<h5>h1 태그입니다!</h5>
<h6>h1 태그 &nbsp; 입니다!</h6>
<h6>h1 태그 &nbsp; &nbsp; &nbsp;입니다!</h6>
```

<figure><img src="../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

### 줄 바꿈

```html
<!--줄 바꿈 태그-->
<br>

<h1>줄 바뀌었나?</h1>

<!--줄 바꾸면서 수평선 넣는 태그-->
<hr>  

<!--문단을 나누는 태그-->
<p>문단 영역을 나누는 태그로는 p태그와 pre태그가 있다. 
    p태그는 문단영역을 나누는 태그이지만 한 개의 공백만         표시하며 줄 바꿈 입력을 별도의
    태그로 지정해 주며 pre태그는 여러 칸 띄우기 혹은 줄 바꿈 등을 포함하여 내용 그대로 표현하는
    태그이다.</p>
<pre>문단 영역을 나누는 태그로는 p태그와 pre태그가 있다. 
    p태그는 문단영역을 나누는 태그이지만 한 개의 공백만         표시하며 줄 바꿈 입력을 별도의
    태그로 지정해 주며 pre태그는 여러 칸 띄우기 혹은 줄 바꿈 등을 포함하여 내용 그대로 표현하는
    태그이다.</pre>

<hr>
```

<figure><img src="../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

### 그 밖에 텍스트를 다루는 태그들

<pre class="language-html"><code class="lang-html"><strong>&#x3C;!--기타 관련 글자 태그-->
</strong>&#x3C;h3> 그 밖에 텍스트를 다루는 태그들&#x3C;/h3>
일반글꼴
&#x3C;br>
&#x3C;strong>글자를 굵게 표시하는 태그&#x3C;/strong>
&#x3C;br>
&#x3C;b>글자를 굵게 표시하는 태그&#x3C;/b>
&#x3C;em>글자를 기울이는 태그&#x3C;/em>
&#x3C;br>
&#x3C;i>글자를 기울이는 태그&#x3C;/i>
&#x3C;mark>형광펜 효과를 나타내는 태그&#x3C;/mark>
&#x3C;br>
&#x3C;u>글자에 밑줄을 긋는 태그&#x3C;/u>
&#x3C;br>
&#x3C;small>글자를 작게 표시하는 태그&#x3C;/small>
&#x3C;br>
기본 글자에 &#x3C;sub>아래첨자&#x3C;/sub>를 나타내는 태그와 &#x3C;sup>윗첨자&#x3C;/sup>를 나타내는 태그이다.
&#x3C;s>글자에 취소선을 넣는 태그&#x3C;/s>
&#x3C;blockquote cite = "http://www.naver.com">인용 문구를 나타내는 태그&#x3C;/blockquote>

&#x3C;!--글자 태그 응용-->
&#x3C;br>
&#x3C;p>태그들은 해당 태그 내에서 중첩으로 사용 가능하다. &#x3C;br>
&#x3C;strong>굵은&#x3C;/strong>글자를 사용할 수도 있고, &#x3C;em>기울기거나&#x3C;/em>,&#x3C;s>취소선&#x3C;/s>을 넣는 등
다양하게 사용할 수 있다.
&#x3C;/p>
</code></pre>

<figure><img src="../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>



## 목록 관련 태그들

### 순서 없는 목록 태그

```html

<h1>순서 없는 목록 태그</h1>
<h3>화면 구현 수업 내용</h3>
<ul>
<li>html</li>
<li>css</li>
<li>javascript</li>
<li>react</li>
</ul>
```

<figure><img src="../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

### 순서 있는 목록 태그

```html
<h1>순서 있는 목록 태그</h1>
<h3>화면 구현 수업 내용</h3>
<ol>
    <li>html</li>
    <li>css</li>
    <li>javascript</li>
    <li>react</li>
</ol>
<br>
<ol type="A">
    <li>html</li>
    <li>css</li>
    <li>javascript</li>
    <li>react</li>
</ol>
<ol type="a">
    <li>html</li>
    <li>css</li>
    <li>javascript</li>
    <li>react</li>
</ol>
<!--로마 소문자로 표기-->
<ol type="i">
    <li>html</li>
    <li>css</li>
    <li>javascript</li>
    <li>react</li>
</ol>
<!--로마 대문자로 표기-->
<ol type="I">
    <li>html</li>
    <li>css</li>
    <li>javascript</li>
    <li>react</li>
</ol>
<!--시작 값 변경하기-->
<ol type="1" start="5">
    <li>html</li>
     <li>css</li>
     <li>javascript</li>
     <li>react</li>
</ol>
<h3>역순으로 항목 표시하기</h3>
<ol reversed="reversed">
    <li>html</li>
    <li>css</li>
    <li>javascript</li>
    <li>react</li>
</ol>
```

<figure><img src="../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>



### 설명 목록 태그

```

<h1>설명 목록 태그</h1>
<dl>
        <dt>이곳은 목록의 제목을 적는 곳입니다.</dt>
        <dd>이곳은 목록에 대한 설명을 적는 곳 입니다.</dd>
        <dd>또 다른 줄을 작성할 수도 있습니다.</dd>
        <dt>다른 제목을 적어 새로운 목록을 만들 수 있습니다.</dt>
</dl>
```

<figure><img src="../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>



## 표 관련 태그

### 기본적인 표 만들기

```html
<h1>기본적인 표 만들기</h1>
<table border="1"> <!--1px solid black-->
    <tr>
        <td>1</td>
        <td>2</td>
        <td>3</td>
    </tr>
    <tr>
        <td>4</td>
        <td>5</td>
        <td>6</td>
    </tr>
    <tr>
        <td>7</td>
        <td>8</td>
        <td>9</td>
    </tr>
</table>
```

<figure><img src="../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>



{% hint style="success" %}
example

![](<../.gitbook/assets/image (13).png>)

```html
<table border="1">
    <caption><b>웹 브라우저의 종류</b></caption>
    <tr>
        <th>브라우저명</th>
        <th>제조사</th>
        <th>홈페이지</th>
    </tr>
    <tr>
        <td>크롬</td>
        <td>google</td>
        <td>https://www.google.com</td>
    </tr>
    <tr>
        <td>사파리</td>
        <td>애플</td>
        <td>https://www.apple.com</td>
    </tr>
</table>
```
{% endhint %}

{% hint style="info" %}
`<td>` 태그의 속성을 이용하여 행과 열 합치기를 할 수 있다.

`colspan` : 열 합치기

`rowspan` : 행 합치기

```html

<h1>표의 행과 열 합치기</h1>
<h3>회원 정보</h3>
<table border="1">
    <tr>
        <td width="130px" height="150px" colspan="2" rowspan="2">사진</td>
        <td width="80px">이름</td>
        <td width="200px"></td>
    </tr>
    <tr>
        <td>연락처</td>
        <td></td>
    </tr>
    <tr>
        <td width="70px" height="50px">주소</td>
        <td colspan="3"></td>
    </tr>
    <tr>
        <td height="100px">자기소개</td>
        <td colspan="3"></td>
    </tr>
</table>
```
{% endhint %}

<figure><img src="../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

### 테이블 태그의 구조 설정

```
<h2>테이블 태그의 구조 설정</h2>
<table border="1">
    <thead>
        <tr>
            <th>이름</th>
            <th>나이</th>
            <th>주소</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td>홍길동</td>
            <td>20</td>
            <td>서울시 서초구</td>
        </tr>
        <tr>
            <td>김영희</td>
            <td>24</td>
            <td>서울시 강동구</td>
        </tr>
        <tr>
            <td>이순신</td>
            <td>30</td>
            <td>경기도 남양주</td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td colspan="2">총 인원</td>
            <td>3명</td>
        </tr>
    </tfoot>
</table>
```

<figure><img src="../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>



{% hint style="success" %}
목록, 표 모두 수식을 이용해 쉽게 구조를 만들 수 있다.
{% endhint %}

<figure><img src="../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>
