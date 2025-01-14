---
layout: post
categories: blog
title: 자바스크립트 변수 및 자료형
tags: [JavaScript, JS, 자바스크립트, 자스, Web, 프론트엔드]
date: 2025-01-14
toc: true
---

## 변수란?

<b>var</b> : 블록 밖과 안 선언 차이가 없음 <br>
<b>let</b> : 블록 안에서 사용하면 안에서만 사용 가능하다.

```js
// 사용 방법
var 변수명; 또는 var 변수명 = 값;
```

변수에 저장할 수 있는 자료형은 <b>문자형(string), 숫자형(num), 논리형(boolean), 빈 데이터(Undefined)</b>이 있다.

<h3>typeof</h3>
지정한 데이터 또는 변수의 자료형에 대해 알고 싶을 때 사용합니다. 기본형은 다음과 같다.

```js
  typeof 변수 또는 데이터
  //사용법
  var num = 100;
  var str = "자바스크립트";
  document.write(typeof num, "<br>");
  document.write(typeof str);
```