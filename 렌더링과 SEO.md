렌더링(Rendering)
--------------------------------------------
- 웹 브라우저가 HTML, CSS, JavaScript 등을 처리해서 웹 페이지를 사용자에게 보여주는 과정을 말합니다.
- 크게는 서버에서 클라이언트(브라우저)로 웹 페이지가 전송된 후, 사용자가 볼 수 있는 화면으로 변환되는 과정으로 볼 수 있습니다.
- 한 마디로 표현하자면, 코드를 시각적인 컨텐츠로 바꾸는 과정을 말합니다.
  
참고) 렌더링의 동작 원리
------------------------------------------------
- HTML 파싱 : 브라우저(클라이언트)가 HTML 문서를 받은 후, 이를 DOM 트리로 변환합니다. ( DOM : 페이지의 모든 요소를 계층적인 트리 구조로 표현하는 것을 말합니다. )
- CSS 파싱 : CSS도 해석되어서 CSSOM(CSS Object Model) 트리로 변환됩니다. ( CSSOM : 스타일 규칙을 표현한 트리입니다. )
- 렌더 트리 생성(Render Tree) : DOM과 CSSOM 트리가 결합해서 렌더 트리(Render Tree)가 생성됩니다. ( 렌더 트리(Render Tree) : 페이지의 시각적인 요소들을 포함하는 트리입니다. )
- 레이아웃 계산 : 렌더 트리를 기반으로 해서 각 요소의 위치와 크기가 계산됩니다. -> 이 과정에서 각 요소가 화면에 배치될 위치와 그 크기가 결정됩니다.
- 페인팅(Painting) : 계산된 레이아웃을 바탕으로 실제 화면에 그리는 작업이 이루어집니다.

자바스크립트의 렌더링 시점
----------------------------------------------
- 자바스크립트는 페이지가 그려지는 과정에서 스크립트의 위치나 실행 방식에 따라 렌더링 시점이 다릅니다.
- 즉, 자바스크립트의 렌더링 시점은 정해져 있지 않다고 볼 수 있습니다.

렌더링(Rendering)을 알면 도움이 되는 이유
-----------------------------------------
- 렌더링 과정을 이해하면, 웹 페이지의 로딩 속도나 디자인을 최적화하는 데 도움이 됩니다.
- 이는 사용자 경험의 향상으로 이어질 수 있습니다.

렌더링 성능에 있어서 고려할 사항
---------------------------------------
- DOM의 크기 : DOM의 크기나 요소 수가 많아지면 브라우저가 이를 렌더링하기 위해 소모되는 시간과 자원이 증가합니다. -> 불필요한 DOM은 최소화하고, 자주 변하지 않는 부분은 캐싱합니다.
- CSS의 복잡성 : CSS 스타일 규칙이 많거나 복잡하면 브라우저가 렌더링 시 스타일 적용 시간이 더 걸립니다. -> CSS 규칙은 최대한 간단하게, 복잡한 레이아웃 사용은 지양합니다.
- Javascript의 비효율적인 동작 : 자바스크립트가 DOM인 CSSOM을 수정할 수 있어서, 동기적인 DOM 수정은 성능 저하를 유발합니다. -> DOM 변경은 최소화하고, 비동기 작업을 사용해서 렌더링 방해를 줄입니다.

렌더링 성능 최적화 예시
-------------------------------
```html
<!-- 불필요한 요소는 제거 -->
<div>불필요한 요소</div>
<div>사용되는 요소</div>
```

```css
/* 복잡한 CSS 애니메이션 */
div {
  transition: all 0.5s ease;
}

/* 간단한 CSS 적용 */
div {
  background-color: lightblue;
}
```

```javascript
// 비효율적인 방법: DOM을 자주 수정
for (let i = 0; i < 1000; i++) {
  document.body.appendChild(document.createElement('div'));
}

// 효율적인 방법: 한 번에 여러 요소를 추가
const fragment = document.createDocumentFragment();
for (let i = 0; i < 1000; i++) {
  fragment.appendChild(document.createElement('div'));
}
document.body.appendChild(fragment);
```

사용자의 DOM 캐싱
--------------------------------------
- 자주 사용하는 DOM 요소는 캐시해서 재사용하는 방식을 택하는 것이 렌더링 성능을 향상 시킬 수 있습니다.
- 자주 사용하는 DOM 요소를 변수에 저장해두고, 재사용시에는 이 변수를 사용해서 DOM에 접근하는 방식을 DOM 캐싱이라고 합니다.
- DOM은 트리 구조로 되어 있어서, 특정 요소를 찾으려면 노드를 따라 내려가야 하므로 시간 소모가 큰 작업입니다.

```javascript
// 매번 DOM을 탐색하여 버튼에 접근
document.querySelector('.my-button').addEventListener('click', function() {
  alert('버튼 클릭!');
});

document.querySelector('.my-button').style.backgroundColor = 'blue';
```
- DOM 캐싱을 사용하지 않으면 한 번 접근한 DOM 요소를 또다시 querySelector로 탐색합니다.

```javascript
// DOM을 한 번만 탐색하여 변수에 캐시
const myButton = document.querySelector('.my-button');

// 캐시된 요소를 여러 번 사용할 수 있음
myButton.addEventListener('click', function() {
  alert('버튼 클릭!');
});

myButton.style.backgroundColor = 'blue';
```
- DOM 캐싱을 사용하면 DOM은 한 번만 탐색해서 변수에 캐싱한 후, 캐싱된 요소를 여러 번 사용할 수 있습니다.

SEO(Search Engine Optimization)
-------------------------------------------
- SEO는 검색 엔진 최적화로, 웹 페이지가 검색 엔진 결과에서 더 잘 보이도록 최적화하는 방법입니다.
- 본질적으로는 검색 결과에서 더 많은 트래픽을 얻기 위해서 최적화합니다.
- SEO를 통해 웹 사이트의 트래픽을 늘려서 비즈니스 성과를 향상시킬 수 있습니다.

참고) 다양한 SEO 방법
---------------------------------------------
```html
<meta name="description" content="This is an example of SEO best practices.">
// meta 태그를 이용해서 페이지에 대한 설명이나 키워드를 명확히 설정합니다.
<h1>Learn SEO best Practices</h1>
// 제목 태그를 통해 검색엔진이 페이지의 핵심 주제를 이해할 수 있게 합니다.
<a href="https://www.example.com">Visit out SEO Guide</a>
// 내부 링크와 외부 링크를 적절하게 사용해서 검색엔진이 페이지를 더 잘 크롤링 할 수 있게 합니다.
<img src="seo-guide.jpg" alt="SEO guide example">
// 이미지의 alt 속성을 설정해서 검색 엔진이 이미지를 이해하도록 돕습니다.
```

- 과도한 키워드 사용(키워드 스태핑)은 오히려 SEO에 부정적인 영향을 미칠 수 있습니다.

렌더링과 SEO의 관계
-----------------------------------------
- 렌더링이 제대로 이루어지지 않으면, 페이지 내용이 검색엔진에 제대로 표시되지 않아서 SEO 효과를 제대로 볼 수가 없습니다.
- Javascript 렌더링이 필요한 페이지는 검색 엔진이 페이지를 크롤링하기 어려울 수 있습니다. -> 이럴 때는 서버 사이드 렌더링(SSR)이나 프리렌더링을 활용할 수 있습니다.
