---
title: "Sass(Extra)"
date: "2019.10.21"
template: "post"
draft: false
slug: "/posts/sass(extra)/"
category: "SASS"
tags:
  - "SASS"
description: "Introductino to Sass"
socialImage: ""
---

## **SASS**

Sass란 무엇일까?  
Sass는 css와 같은 stylesheet 언어로, css로 해석 및 컴파일되는 스크립트 언어이다. scss는 sass의 새로운 버전으로 css와 비슷한 블록 형식을 사용한다. 또한 변수, 네스팅, mixin, 셀렉터 상속 등을 사용할 수 있어 마치 프로그래밍 언어처럼 사용할 수 있어 편리하게 css를 작성할 수 있다. 테마 컬러나 border등, 디자인의 통일성이 필요한 것에 사용할 때 유용하게 사용할 수 있다.

```
$deFont: 12px;
$smlFont: 8px;
$btnColor: #3897f0;
$border: 1px solid rgb(199, 199, 199);
```

위와 같이 변수 설정이 가능해서 `@import [name]`와 같이 재사용이 가능하다.

```
@function sum($numbers...) {
  $sum: 0;
  @each $number in $numbers {
    $sum: $sum + $number;
  }
  @return $sum;
}

.micro {
  width: sum(50px, 30px, 100px);
}
```

이처럼 함수 선언도 가능하다. border같은 경우 유용하게 사용할 수 있다.

```
%input-style {
  font-size: 14px;
}

.input-black {
  @extend %input-style;

  color: black;
}

.input-red {
  @extend %input-style;

  color: red;
}
```

%는 extend 전용 selector로 자신은 컴파일되지 않고 상속만을 위해 존재한다.

```
@mixin circle($size) {
  width: $size;
  height: $size;
  border-radius: 50%;
}

.box {
  @include circle(100px);

  background: #f00;
}
```

mixin은 extend와 별 차이가 없어보이지만, argument를 사용할 수 있다는 점이 다르다. 사용 빈도가 높은 마크업을 사전에 정의하여 사용할 때 유용하다. 오히려 function과 더 유사해보이기도 한다. 그러나 function은 값을 return하는데 반해, mixin은 style markup자체를 return한다.
