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
<link ref="stylesheet" media="(max-width: 700px)" href="test.css" />
```

### **연산자**

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

**쉼표(or) 연산자**  
`media (min-width: 700px), print and (orientation: landscape) {...}`  
최소 너비 700px 이상일 때 적용하거나, 프린트 장치에서는 가로 방향일 때만 적용한다는 뜻

**not 연산자**  
`media not all and (color) {...}`  
not은 전체 미디어 쿼리를 수식한다. 조금 더 알기 쉽게 표현하자면, `media not(all and (color))`와 같은 말이다.  
하지만 쉼표를 사용하면 개별 미디어 쿼리로 인식하므로 not을 끊어서 사용하고 싶다면 쉼표 연산자를 사용하면 된다.

### **media type**

1. **all**: 기본값, 모든 미디어 장치에 사용
2. **print**: 프린터에 사용
3. **screen**: 컴퓨터, 태블릿, 스마트폰 등의 스크린
4. **speech**: 페이지를 읽어주는 화면 낭독기

### **media feature**

1. width | height (min / max)
2. device-width | device-height (min / max)
3. aspect-ratio (min / max)
4. divice-aspect-ratio ( min / max)
5. color, color-index ( min / max)
6. monochrome ( min / max)
7. resolution ( min / max)
8. scan | grid ( min / max)

#### **description**

1. min | max : 최소, 최대를 말한다. **(min)보다 크고, (max)보다 작게**로 생각하면 이해하기 쉽다.
2. width | height : 화면의 너비, 높이
3. device-(height | width) : 출력 장치의 너비, 높이
4. aspect-ratio : 화면 영역의 가로 세로 비율( `/`를 사용해, 앞에는 수평 비율, 뒤에는 수직 비율을 적용할 수 있다)
5. device-aspect-ratio : 출력 장치의 가로, 세로 비율(첫 번째 값이 수평, 두번째 값이 수직)
6. color : 출력 장치의 색상 구성요소 당 비트 수
7. color-index : 장치가 표시할 수 있는 색상 수
8. grid : 출력 장치가 그리드 장치 또는 비트맵 장치냐에 따라 결정(그리드이면 1, 아니면 0)
9. monochrome : 흑백 장치에 색상 당 비트 수
10. orientation : 화면이 가로 모드인지, 세로 모드인지 지정(ex: `@media all and (orientation: portrait) {...} // 오직 세로 방향에서만 적용`)
11. resolution : 출력 장치의 해상도(dpi(dots per inch) 혹은 dpcm(dots per cintimeter))
