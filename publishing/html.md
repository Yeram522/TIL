---
icon: html5
---

# HTML

## 🔲HTML 기본 틀

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

## 🅰️글자 관련 태그

### - 글꼴 크기

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

<figure><img src="../.gitbook/assets/image (11) (1).png" alt=""><figcaption></figcaption></figure>

### - 줄 바꿈

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

<figure><img src="../.gitbook/assets/image (12) (1).png" alt=""><figcaption></figcaption></figure>

### - 그 밖에 텍스트를 다루는 태그들

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

<figure><img src="../.gitbook/assets/image (13) (1).png" alt=""><figcaption></figcaption></figure>



## 🧾목록 관련 태그들

### - 순서 없는 목록 태그

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

<figure><img src="../.gitbook/assets/image (14) (1).png" alt=""><figcaption></figcaption></figure>

### - 순서 있는 목록 태그

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

<figure><img src="../.gitbook/assets/image (15) (1).png" alt=""><figcaption></figcaption></figure>



### - 설명 목록 태그

```

<h1>설명 목록 태그</h1>
<dl>
        <dt>이곳은 목록의 제목을 적는 곳입니다.</dt>
        <dd>이곳은 목록에 대한 설명을 적는 곳 입니다.</dd>
        <dd>또 다른 줄을 작성할 수도 있습니다.</dd>
        <dt>다른 제목을 적어 새로운 목록을 만들 수 있습니다.</dt>
</dl>
```

<figure><img src="../.gitbook/assets/image (16) (1).png" alt=""><figcaption></figcaption></figure>



## 🥅표 관련 태그

### - 기본적인 표 만들기

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

<figure><img src="../.gitbook/assets/image (17) (1).png" alt=""><figcaption></figcaption></figure>



{% hint style="success" %}
example

![](<../.gitbook/assets/image (20) (1).png>)

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

<figure><img src="../.gitbook/assets/image (19) (1).png" alt=""><figcaption></figcaption></figure>

### - 테이블 태그의 구조 설정

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

<figure><img src="../.gitbook/assets/image (18) (1).png" alt=""><figcaption></figcaption></figure>



{% hint style="success" %}
목록, 표 모두 수식을 이용해 쉽게 구조를 만들 수 있다.
{% endhint %}

<figure><img src="../.gitbook/assets/image (21) (1).png" alt=""><figcaption></figcaption></figure>



## 🪧영역 관련 태그

### - 영역을 구분하는 태그

```html
<div> : 줄 바꿈이 적용되어 이미 존재하는 태그의 다음 줄에 영역이 설정됨 (블럭요소)
<span> : 줄 바꿈이 적용되지 않아 옆으로 영역이 붙음 (인라인 요소)
<p> : 문단 영역을 지정하는 태그(블럭 요소)
<pre> : 입력란대로 문단 영역을 저장하는 태그(블럭 요소)
```



### - div 태그와 span 태그의 영역

#### div 영역

```html
<div style="background-color: yellow;">새가 봄바람을 인생을 듣기만 우리 힘있다. 같이, 지혜는 우리는 속에 것은 가슴에 오아이스도 끓는 피어나는 약동하다. 위하여 그들은 일월과 인도하겠다는 방지하는 주며, 
        쓸쓸한 사막이다. 살았으며, 위하여 싶이 천지는 피어나기 끓는 있는 지혜는 뿐이다. 이것을 인생에 어디 품었기 철환하였는가? 꽃 미인을 가지에 쓸쓸한 것이다. 거친 방황하여도, 있는 위하여, 
        철환하였는가? 작고 우리 우리 원대하고, 어디 위하여서. 청춘의 황금시대를 오아이스도 끝까지 장식하는 두손을 철환하였는가? 동력은 현저하게 따뜻한 사랑의 이것은 듣는다. 새가 하였으며, 끓는 되는 철환하였는가?</div>

```

#### span 영역

```html
<span style="background-color: cyan;">새가 봄바람을 인생을 듣기만 우리 힘있다. 같이, 지혜는 우리는 속에 것은 가슴에 오아이스도 끓는 피어나는 약동하다. 위하여 그들은 일월과 인도하겠다는 방지하는 주며, 
        쓸쓸한 사막이다. 살았으며, 위하여 싶이 천지는 피어나기 끓는 있는 지혜는 뿐이다. 이것을 인생에 어디 품었기 철환하였는가? 꽃 미인을 가지에 쓸쓸한 것이다. 거친 방황하여도, 있는 위하여, 
        철환하였는가? 작고 우리 우리 원대하고, 어디 위하여서. 청춘의 황금시대를 오아이스도 끝까지 장식하는 두손을 철환하였는가? 동력은 현저하게 따뜻한 사랑의 이것은 듣는다. 새가 하였으며, 끓는 되는 철환하였는가?</span>
```

<figure><img src="../.gitbook/assets/image (10) (1).png" alt=""><figcaption></figcaption></figure>

## 🖼️이미지 관련 태그

```html
<img src="sample/image/flower3.PNG">
```

### 🔖<mark style="color:red;">자주 사용하는 속성들</mark>

#### <mark style="background-color:blue;">alt 속성</mark>

```html
<img src="sample/image/river1.PNG" alt="river1의 사진">
```

{% hint style="success" %}
사진의 경로가 잘못되거나 이미지를 제대로 표현할 수 없을 경우 대체 텍스트의 용도로 사용 가능하다.
{% endhint %}

#### <mark style="background-color:blue;">width와  height의 속성</mark>

&#x20;사진의 높이와 너비를 지정할 수있다.

&#x20;✅고정 크기 단위 : 화면 사이즈가 줄어도 크기 변화 X

```html
<img src="sample/image/flower1.PNG" width="200px" height="150px">
```

<figure><img src="../.gitbook/assets/image (1) (1) (1) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

&#x20;✅가변 크기 단위 : 화면 사이즈 혹은 기준이 사이즈에 따라 크기 변경

```html
<img src="sample/image/flower1.PNG" width="15%" height="150px">
```

<figure><img src="../.gitbook/assets/image (2) (1) (1) (1) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>



## 🎬 미디어 관련 태그

### - 🔊오디오 관련 태그

```html
<audio src="sample/audio/major.mp3" controls="controls" loop="loop"></audio>
```

<figure><img src="../.gitbook/assets/image (3) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### - 📼 비디오 관련 태그

```html
<video src="sample/video/video1.mp4" controls="controls"></video>
```

<figure><img src="../.gitbook/assets/image (4) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>



## 🔗하이퍼링크 관련 태그

{% hint style="info" %}
링크 기능은 웹 문서가 다른 문서와 구분되는 가장 핵심적인 기능!

클릭을 통해 연결된 곳으로 이동하여 사용을 편리하게 해주는 기능이다.

텍스트를 클릭해 링크를 이동하는 방법, 이미지를 클릭해 링크를 이동하는 방법이 있다.

페이지 내에서의 링크를 통한 이동도 가능하다.
{% endhint %}

### - <mark style="background-color:red;">a 태그</mark>를 이용한 하이퍼링크

```
<ul>
        <li><a href="1_글자관련태그.html">글자 관련 태그</a></li>
        <li><a href="2_목록관련태그.html">목록 관련 태그</a></li>
        <li><a href="3_표관련태그.html">표 관련 태그</a></li>
        <li><a href="4_영역관련태그.html">영역 관련 태그</a></li>
        <li><a href="5_이미지관련태그.html">이미지 관련 태그</a></li>
    </ul>

    <ul>
        <li><a href="https://www.naver.com" target="_self">네이버</a></li> <!--기존페이지에서 새로고침-->
        <li><a href="https://www.google.com" target="_blank">구글</a></li> <!--새 탭이 열림-->
    </ul>

    <a href="https://www.w3schools.com" target="_blank">
        <img src="sample/image/city1.PNG" width="150px" height="100px">
    </a>
```

<figure><img src="../.gitbook/assets/image (5) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### - 한 페이지 내에서 점프하는 앵커

<pre class="language-html"><code class="lang-html"><strong>&#x3C;h3 id="menu">한 페이지 내에서 점프하는 앵커 만들기&#x3C;/h3>
</strong>    &#x3C;ul>
        &#x3C;li>&#x3C;a href="#content1">본문내용1&#x3C;/a>&#x3C;/li>
        &#x3C;li>&#x3C;a href="#content2">본문내용2&#x3C;/a>&#x3C;/li>
        &#x3C;li>&#x3C;a href="#content3">본문내용3&#x3C;/a>&#x3C;/li>
    &#x3C;/ul>


    &#x3C;h4 id="content1">본문내용1&#x3C;/h4>
    &#x3C;pre> What is Lorem Ipsum?
        Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing software like Aldus PageMaker including versions of Lorem Ipsum.
        
        Why do we use it?
        It is a long established fact that a reader will be distracted by the readable content of a page when looking at its layout. The point of using Lorem Ipsum is that it has a more-or-less normal distribution of letters, as opposed to using 'Content here, content here', making it look like readable English. Many desktop publishing packages and web page editors now use Lorem Ipsum as their default model text, and a search for 'lorem ipsum' will uncover many web sites still in their infancy. Various versions have evolved over the years, sometimes by accident, sometimes on purpose (injected humour and the like).
        
        
        Where does it come from?
        Contrary to popular belief, Lorem Ipsum is not simply random text. It has roots in a piece of classical Latin literature from 45 BC, making it over 2000 years old. Richard McClintock, a Latin professor at Hampden-Sydney College in Virginia, looked up one of the more obscure Latin words, consectetur, from a Lorem Ipsum passage, and going through the cites of the word in classical literature, discovered the undoubtable source. Lorem Ipsum comes from sections 1.10.32 and 1.10.33 of "de Finibus Bonorum et Malorum" (The Extremes of Good and Evil) by Cicero, written in 45 BC. This book is a treatise on the theory of ethics, very popular during the Renaissance. The first line of Lorem Ipsum, "Lorem ipsum dolor sit amet..", comes from a line in section 1.10.32.
        
        The standard chunk of Lorem Ipsum used since the 1500s is reproduced below for those interested. Sections 1.10.32 and 1.10.33 from "de Finibus Bonorum et Malorum" by Cicero are also reproduced in their exact original form, accompanied by English versions from the 1914 translation by H. Rackham.
        
        Where can I get some?
        There are many variations of passages of Lorem Ipsum available, but the majority have suffered alteration in some form, by injected humour, or randomised words which don't look even slightly believable. If you are going to use a passage of Lorem Ipsum, you need to be sure there isn't anything embarrassing hidden in the middle of text. All the Lorem Ipsum generators on the Internet tend to repeat predefined chunks as necessary, making this the first true generator on the Internet. It uses a dictionary of over 200 Latin words, combined with a handful of model sentence structures, to generate Lorem Ipsum which looks reasonable. The generated Lorem Ipsum is therefore always free from repetition, injected humour, or non-characteristic words etc.
    &#x3C;/pre>
    &#x3C;a href="#menu">메뉴로 돌아가기&#x3C;/a>
</code></pre>

<figure><img src="../.gitbook/assets/image (6) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>



## 📦폼 관련 태그

form 태그는 html 사용자가 <mark style="background-color:yellow;">입력할 수 있는 양식을 제공</mark>하는 태그이다.\
form 태그 내의 input 태그들을 통해 **사용자가 입력한 정보를 서버로 넘기는 역할**을 한다

* **action 속성** : 폼의 입력된 값들을 <mark style="background-color:blue;">전송 받을 서버의 클래스명</mark>을 입력한다.-
* **method 속성** : <mark style="background-color:green;">get / post</mark> 방식으로 전송 방식을 지정한다. (get 방식은 url 주소에 form 태그를 통해 넘어가는 데이터가 보임) (post 방식은 url 주소에 form 태그를 통해 넘어가는 데이터가 보이지 않음)

```html
<form action="search" method="post">
        <label>검색할 내용: </label><input type="text" name="search">
        <button type="submit">검색</button>
</form>
```

<figure><img src="../.gitbook/assets/image (7) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

{% hint style="success" %}
submit 버튼을 눌렀을 때, <mark style="color:green;">action에 지정한 경로</mark>로 method를 지정한 방식에 따라 <mark style="color:green;">input 태그에 입력한 값들을 전달</mark>한다.
{% endhint %}



### - fieldset과 legend

```html
<form>
        <fieldset>
            <legend>필드셋의 제목을 작성하는 부분이다.</legend>
            <label>입력1: </label><input type="text" value="사과"><br>
            <label>입력2: </label><input type="text"><br>
            <label>입력3: </label><input type="text"><br>
        </fieldset>
        <fieldset>
            <legend>필드셋으로 묶은 영역별로 구분된다.</legend>
            <label>입력1: </label><input type="text" value="사과"><br>
            <label>입력2: </label><input type="text"><br>
            <label>입력3: </label><input type="text"><br>
        </fieldset>
</form>
```

<figure><img src="../.gitbook/assets/image (9) (1) (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### - 다양한 종류의 input 태그들 type별로 확인하기

#### ✅ text와 관련된 input 태그

<mark style="background-color:green;">**type="text"**</mark>

<figure><img src="../.gitbook/assets/image (22) (1).png" alt=""><figcaption></figcaption></figure>

```html
<p>한 줄짜리 텍스트를 입력할 수 있는 텍스트 상자이다.</p>
        <label for="userid2">아이디: </label>
        <input type="text" id="userid2" name="userid" size="60"
        placeholder="아이디를 입력하세요" value = "user01" autofocus>
```



<mark style="background-color:green;">**type="password"**</mark>

<figure><img src="../.gitbook/assets/image (23) (1).png" alt=""><figcaption></figcaption></figure>

```html
<label for="userpassword2">비밀번호</label>
<input type="password" id="userpassword2" name="userPwD" size="40" placeholder="비밀번호를 입력하세요."><br>
```



<mark style="background-color:green;">**type="search"**</mark>

겉모습은 type="text"와 비슷하지만 각각의 정보에 맞게 분화된 기능을 제공하는 텍스트 상자이다.

<figure><img src="../.gitbook/assets/image (24) (1).png" alt=""><figcaption></figcaption></figure>

```html
<label>검색: </label>
<input type="search" name="searchtext" placeholder="검색할 내용 입력"><br>
<label>홈페이지: </label>
<input type="url" name="homepage" value = "https://"><br>
<label>이메일: </label>
<input type="email" name="email" placeholder="이메일을 입력하세요."><br>
<label>전화번호: </label>
<input type="tel" name="phone" placeholder="전화번호를 입력하세요." >
```



#### ✅ 숫자와 관련된 input 태그

<mark style="background-color:green;">**type="number"**</mark>

<figure><img src="../.gitbook/assets/image (25) (1).png" alt=""><figcaption></figcaption></figure>

```html
<label>수량: </label>
<input type="number" name="amount"min="0" max="100" value="50" step="5"><br>
```



<mark style="background-color:green;">**type="range"**</mark>

슬라이드바를 통해 숫자를 지정할 수 있다.

<figure><img src="../.gitbook/assets/image (26) (1).png" alt=""><figcaption></figcaption></figure>

```html

<label>점수 :</label>
<input type="range" name="point" min="0" max="100" value="0" step="10"><br>

<input type="submit" value="전송">
<input type="reset" value="취소">
```



#### <mark style="background-color:green;">날짜/시간 관련된 input 태그</mark>

#### type="date", type="month", type="week", type="time", type="datetime", type="datetime-local"

<figure><img src="../.gitbook/assets/image (27) (1).png" alt=""><figcaption></figcaption></figure>

<pre class="language-html"><code class="lang-html"><strong>&#x3C;label>date : &#x3C;/label>&#x3C;input type="date" name = "date">&#x3C;br>
</strong>&#x3C;label>month : &#x3C;/label>&#x3C;input type="month" name = "month">&#x3C;br>
&#x3C;label>week : &#x3C;/label>&#x3C;input type="week" name = "week">&#x3C;br>
&#x3C;label>time : &#x3C;/label>&#x3C;input type="time" name = "time">&#x3C;br>
&#x3C;label>datetime-local : &#x3C;/label>&#x3C;input type="datetime-local" name = "datetime-local">&#x3C;br>
</code></pre>



#### ✅ 라디오 버튼(단일선택)과 체크박스(다중선택)

<mark style="background-color:green;">**type="radio"**</mark>

<figure><img src="../.gitbook/assets/image (28) (1).png" alt=""><figcaption></figcaption></figure>

```html
<input id = "male" type="radio" name="gender" value="M" checked>
<label for="male">남자</label>
<input id = "female" type="radio" name="gender" value="F">
<label for="female">여자</label>
```

{% hint style="success" %}
라디오 버튼은 <mark style="background-color:yellow;">name</mark>을 일치시켜서 하나의 그룹으로 만들어 하나만 체크되게 하자!
{% endhint %}

<mark style="background-color:green;">**type="checkbox"**</mark>

<figure><img src="../.gitbook/assets/image (29) (1).png" alt=""><figcaption></figcaption></figure>

```html
<label>취미 :</label>
<input type="checkbox" id="baseball" name="hobby" value="야구">
<label for="baseball">야구</label>

<input type="checkbox" id="football" name="hobby" value="축구">
<label for="football">축구</label>

<input type="checkbox" id="basketball" name="hobby" value="농구">
<label for="baseball">농구</label>
```



#### ✅ 그 밖의 input 태그들

<mark style="background-color:green;">**type="color"**</mark>

<figure><img src="../.gitbook/assets/image (30) (1).png" alt=""><figcaption></figcaption></figure>

```html
<label for="color">색상 선택 :</label>
<input type="color" id="color" name="color">
```



<mark style="background-color:green;">**type="file"**</mark>

<figure><img src="../.gitbook/assets/image (31) (1).png" alt=""><figcaption></figcaption></figure>

```html
<input type="file" name="uploadfile" multiple>
```

{% hint style="success" %}
multiple 옵션을 준 경우에는 파일을 여러개 선택할 수 있다.
{% endhint %}



<mark style="background-color:green;">**type="button", type="submit", type="reset"**</mark>

<figure><img src="../.gitbook/assets/image (32) (1).png" alt=""><figcaption></figcaption></figure>

```html
<input type="button" value="버튼">
<input type="submit" value="전송">
<input type="reset" value="초기화">
<button>버튼2</button>
```



### - select 태그와 option 태그

사용자가 내용을 입력하는 것이 아니라 여러 옵션 중에서 선택하게 하고 싶을 때 사용하는 <mark style="background-color:blue;">드롭다운 목록</mark>이다.

<figure><img src="../.gitbook/assets/image (33) (1).png" alt=""><figcaption></figcaption></figure>

<pre class="language-html"><code class="lang-html">&#x3C;label>국적: &#x3C;/label>
&#x3C;select name="nation">
    &#x3C;option selected>한국&#x3C;/option>
    &#x3C;option>중국&#x3C;/option>
    &#x3C;option>일본&#x3C;/option>
<strong>    &#x3C;option>미국&#x3C;/option>
</strong>    &#x3C;option>베트남&#x3C;/option>
    &#x3C;option>기타&#x3C;/option>
&#x3C;/select>
</code></pre>

#### ✅ select 태그의 속성

**size:** listbox의 크기를 지정한다.

**multiple:** 다중 선택이 가능하다.

<figure><img src="../.gitbook/assets/image (34) (1).png" alt=""><figcaption></figcaption></figure>

<pre class="language-html"><code class="lang-html">&#x3C;select name="nation2" size="5" multiple>
    &#x3C;option selected>한국&#x3C;/option>
    &#x3C;option>중국&#x3C;/option>
    &#x3C;option>일본&#x3C;/option>
    &#x3C;option>미국&#x3C;/option>
    &#x3C;option>베트남&#x3C;/option>
<strong>    &#x3C;option>기타&#x3C;/option>
</strong>&#x3C;/select>
</code></pre>



### - textarea 태그

input type="text"와 비슷하지만 <mark style="background-color:yellow;">여러 줄을 입력할 수 있</mark>고 새로운 input 태그와 달리 크기 조절이 가능하다.

{% hint style="success" %}
css 속성 <mark style="color:blue;">resize</mark>로 크기 조절을 고정할 수도 있고, 범위를 벗어나면 스크롤 바가 생긴다.

**style="resize : none;"**&#xC740; 텍스트 박스 크기를 <mark style="background-color:red;">사용자가 조정할 수 없게</mark> 해준다!
{% endhint %}

```html
<textarea name="content" cols="30" rows="10"
style="resize : none;">텍스트 박스 입니다!
</textarea>
```

<figure><img src="../.gitbook/assets/image (35) (1).png" alt=""><figcaption></figcaption></figure>
