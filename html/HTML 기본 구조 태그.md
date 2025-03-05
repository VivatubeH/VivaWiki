HTML 기본 구조 태그
=========================================
HTML의 기본 구조 태그는 웹 페이지의 정상 작동, 다른 사용자들과의 호환성, 검색엔진 최적화(SEO)에 있어 중요한 역할을 합니다.


DOCTYPE html
--------------------------------------
- 해당 문서가 HTML5 문서임을 웹브라우저에 알려주어야 -> 브라우저가 페이지를 제대로 렌더링 할 수 있습니다.
- 문서 유형을 선언하는 태그이며, 필수 태그입니다.

```html
<!DOCTYPE html> 
```
- 문서의 첫 번째 줄에 위치하며, 그 앞에 다른 코드나 공백이 들어가면 안됩니다.

html
-------------------------------------------------------
- HTML 문서의 최상위 요소이자, 문서의 모든 내용을 감싸는 최상위의 컨테이너 역할을 합니다. ( 모든 HTML 코드를 하나의 블록으로 묶습니다. )
- HTML 문서는 반드시 html 태그 내에 작성되어야 하기 때문에, 문서 구성요소들이 어디서부터 어디까지 포함되는지를 정의합니다.

```html
<html lang="en">
  <head>
    <meta charset="UTF-8">
    <title>My Web Page</title>
  </head>
  <body>
    <h1>Hello, World!</h1>
  </body>
</html>
```
- html 태그는 반드시 하나만 사용해야 하며, 중첩되거나 복수로 존재해서는 안 됩니다.

head
--------------------------------------------------------
- 문서의 메타 정보(메타데이터), 스타일 시트, 스크립트 등 페이지의 내용과는 직접적으로 관련되지 않은 정보를 포함하는 역할을 합니다.
- head 태그를 통해서 웹 페이지의 정보 설정이 가능하며, 사용자에게 직접 보이지 않는 요소들을 설정합니다. -> 이를 통해 SEO 최적화 및 웹페이지 효율성이 증대됩니다.

```html
<head>
  <meta charset="UTF-8">
  <meta name="description" content="This is a sample web page.">
  <title>My Web Page</title>
</head>
```
- meta chartset="UTF-8" : 해당 문서의 문자 인코딩을 UTF-8로 설정합니다.
- title : 브라우저 탭에 표시될 제목을 설정합니다.
- 주의점으로는 head 태그에는 페이지의 내용이 포함되어서는 안 됩니다.

body 
----------------------------------------------------------------
- 웹 페이지의 본문 컨텐츠를 담고 있는 태그입니다. ( 사용자가 실제로 볼 수 있는 텍스트, 이미지, 비디오 등의 모든 내용이 포함됩니다. )
- 웹 페이지에서 사용자에게 실제로 보여지는 컨텐츠를 포함하는 가장 중요한 영역입니다.

```html
<body>
  <h1>Welcome to My Web Page!</h1>
  <p>This is a paragraph.</p>
</body>
```
- body 태그 내에도 javascript나 동적 컨텐츠도 넣을 수 있지만, 너무 많은 스크립트를 넣으면 페이지 성능에 영향을 미칠 수 있습니다.

meta
-------------------------------------------------------------
- 문서의 메타 정보를 제공하는 태그입니다. ( 브라우저나 검색엔진이 웹 페이지 처리 시 필요한 정보를 제공합니다. )
- 검색 최적화(SEO), 언어 설정, 인코딩 등 다양한 정보를 설정할 수 있습니다. -> 이를 통해 올바른 렌더링을 돕습니다.

```html
<meta charset="UTF-8">
<meta name="author" content="John Doe">
<meta name="description" content="This is a sample web page for learning HTML.">
```
- name=description : 페이지의 간단한 설명을 제공해서 검색 엔진의 이해를 돕습니다.
- meta 태그는 head 태그 내에 위치해야 하며, 적절한 정보가 포함되지 않으면 검색엔진 최적화(SEO)에 부정적인 영향을 미칠 수 있습니다.

```html
<!DOCTYPE html>
<html lang="en">  <!-- HTML5 문서의 시작, 'en'은 페이지 언어를 영어로 설정 -->
  <head>
    <meta charset="UTF-8">  <!-- 문자 인코딩을 UTF-8로 설정 (다국어 지원) -->
    <meta name="description" content="This is a sample web page for learning HTML.">  <!-- 페이지 설명 (SEO 최적화) -->
    <meta name="author" content="John Doe">  <!-- 작성자 정보 -->
    <meta name="viewport" content="width=device-width, initial-scale=1.0">  <!-- 반응형 웹을 위한 뷰포트 설정 -->
    <title>My Sample Web Page</title>  <!-- 브라우저 탭에 표시될 페이지 제목 -->
  </head>
  <body>
    // 내용
  </body>
</html>
```
