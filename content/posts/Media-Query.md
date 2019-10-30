---
title: "Media-Query"
date: "2019.10.28"
template: "post"
draft: false
slug: "/posts/media-query/"
category: "media-query"
tags:
  - "Media Query"
description: "Introductino to Media Query"
socialImage: ""
---

## **Media Query**

media query는 css 내부에 삽입하는 방법, 링크로 연결하는 방법이 있다. css 내부에 삽입하는 방법은 아래와 같다.

```js
<style>
@media(max-width: 700px) {
  .container {
    margin: 0px;
    padding: -px;
  }
}
</style>
```

링크로 연결할 때는 아래처럼 하면 된다.

```js
<link red="stylesheet" media="(max-width: 700px)" href="test.css" />
```

media query는 4개의 연산자가 있다.

1. **and**: 여러 미디어 특징들을 하나로 결합
2. **, (or)**: 쉼표로 분리된 각 목록은 개별 미디어 퀴리
3. **not**: 전체 미디어 쿼리를 부정하기 위해 사용
4. **only**: 미디어 쿼리를 지원하지 않는 브라우저가 주어진 스타일을 적용하는 것을 방지
   _not이나 only를 사용하려면 미디어 타입을 규정해야 한다_
   _미디어 쿼리는 대소문자 구별하지 않는다_

**기본적인 media query**
`@media (min-width: 700px) {background-color:yellow;}`
최소 너비 700px일 때 스타일을 적용한다. 즉, 700px 이상일 때만 적용한다는 뜻

**and 연산자**
`media (min-width: 700px) and (orientation: portrait) {...}`
최소 너비 700px 이상일 때 그리고 방향이 세로 모드일 때만 적용한다는 뜻
