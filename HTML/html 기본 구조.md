HTML(HyperText Markup Language)
-----------------------------------
- HTML은 웹 문서를 작성할 때 사용되는 언어입니다.
- HyperText는 링크를 통해 텍스트를 뛰어넘는다는 의미를, Markup은 문서의 구조를 표현한다는 의미를 가지고 있습니다.
- 즉 HTML은 텍스트를 뛰어넘는 기능과 문서를 구조화하는 기능을 갖춘 언어라고 할 수 있습니다.

HTML의 구성요소
--------------------------
- HTML을 구성하는 구성 요소에는 태그와 속성이 있습니다.

태그(Tag)
-------------------------
- <와 >를 이용해서 만드는 것이 태그입니다.
- 태그명은 소문자로 쓰고, 여는 태그와 닫는 태그 짝을 맞추어서 써야 합니다. 

```html
<h1>html 태그</h1>
```

자식 태그와 부모 태그
----------------------------
- 태그들도 부모, 자식 관계를 갖는 태그가 있습니다.
- 자식 태그는 부모 태그 안에서만 사용할 수 있고, 반드시 자식 태그를 쓸 때는 부모 태그 내에서 들여쓰기를 해야합니다.

```html
<ul>
  <li>자식 태그</li>
</ul>
```

빈 태그(self-closing tag)
----------------------------
HTML에서 닫는 태그 없이 자체적으로 종료되는 태그를 빈 태그(self-closing tag)라고 합니다.

```html
<img src="image.jpg" alt="A beautiful image">
<p>첫 번째 줄<br>두 번째 줄</p>
<hr>수평선 그리기
<input type="text" name="username">
<meta charset="UTF-8">
<link rel="stylesheet" href="style.css">
```
HTML5 스타일과 XHTML 스타일의 닫는 태그 비교
--------------------------------------
```html
<!-- XHTML 스타일 (슬래시를 사용) -->
<img src="image.jpg" alt="A beautiful image" />

<!-- HTML5 스타일 (슬래시 없이) -->
<img src="image.jpg" alt="A beautiful image">
```

속성
-------------------------------------------------
- HTML 태그에 추가적인 정보를 제공하는 요소를 속성이라고 합니다. 
- 태그 내에 작성하며, 속성명과 속성값은 붙여서 적습니다.

```html
<img src="images/logo.png" width="160" height="70">
```

미리 정해진 속성 vs data-로 시작하는 속성
--------------------------------------------------
```html
<a href="https://www.naver.com">사이트로 가기</a>
<img src="image.jpg" alt="beuatiful image">
<div id="header">
```
- 위에서 보듯 href, src, id, alt와 같은 속성은 HTML에서 미리 정해진 속성입니다.

```html
<body>
    <div id="test" data-user-id="12345" data-product-name="Laptop">
        <p>id 12345의 노트북입니다.</p>
    </div>
<script>
    const dom = document.getElementById('test');
    console.log(dom.dataset.userId);
    console.log(dom.dataset.productName);
</script>
```
- 위에서 보듯 data-로 시작하는 속성은 사용자가 정의한 데이터를 HTML 요소에 저장할 수 있게 해주는 속성입니다.
- HTML5에서 사용자 정의 데이터를 저장하면 JavaScript를 통해서 이를 읽고 사용할 수 있습니다.

HTML 문서의 기본 구조
-----------------------------------------------
```html
<!doctype html>
<html lang="ko"> <!-- 문서의 언어를 한국어로 설정 -->
<head>
    <meta charset="utf-8"> <!-- 문자 인코딩 방식 -->
    <title>문서의 제목</title> <!-- 웹페이지의 제목 -->
    <link rel="stylesheet" href="style.css"> <!-- 스타일시트 링크 -->
    <!-- 여기에 자바스크립트 파일을 추가할 수 있습니다. 예시: <script src="script.js"></script> -->
</head>
<body>
    <h1>웹페이지 제목</h1>
    <p>이것은 본문 내용입니다.</p>
    <a href="https://www.example.com">Example 웹사이트</a> <!-- 링크 예시 -->
</body>
</html>
```
- !doctype html : 해당 문서가 HTML5 규칙을 준수하는 HTML 문서임을 나타냅니다.
- html ~ /html : html 문서의 루트 태그입니다. ( 즉, HTML 문서 내에 하나만 가질 수 있으며 모든 태그는 해당 태그사이에 위치해야 합니다. ) 
- head ~ /head : 웹 브라우저에게 문서에 대한 정보(메타 데이터)를 제공하는 태그입니다. ( 화면 구성을 위한 메타데이터이지, 화면에는 안 보입니다. )
- body ~ /body : 웹 브라우저에 실제로 표시될 컨텐츠를 포함하는 태그입니다. ( 화면에 보일 내용입니다. )
