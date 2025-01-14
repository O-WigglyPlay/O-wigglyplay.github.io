---
layout: post
categories: blog
title: 자바스크립트 기초 문법
tags: [JavaScript, JS, 자바스크립트, 자스, Web, 프론트엔드]
date: 2025-01-14
toc: true
---

### JS 선언문

```js
<script>자바스크립트 코드</script>

실제 사용법
<script>
  document.write("안녕하세요");
</script>
```

script 태그의 위치는 상관이 없다. <br>
head, body 둘 다 가능하다. <br>

### JS 주석 방법

```js
// 한 줄 주석
/* 여러 줄 주석 */

<!-- HTML 주석 -->
```

JS 상에서 주석 방식과 html 상 주석 방식이 다르니 구분에 주의해야한다.

### 내부 스크립트 외부로 분리

```js
<script src="JS 파일 경로"></script>
```

가독성과 유지 보수를 위해 분리해서 작성하는 것이 좋다.