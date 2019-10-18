---
title: "Westagram React-02"
date: "2019.10.18"
template: "post"
draft: false
slug: "/posts/westagram_react_02/"
category: "React"
tags:
  - "React"
description: "What I learned from Westagram-React Clone Coding"
socialImage: ""
---

## **Westagram React**

westagram을 react로 재구성하면서 새롭게 알게 된 것들을 정리해보려 한다.

1. Component를 나눌 때, 기능적으로 나누는 것도 있지만 가독성을 위해 나눌 때도 있다는 것을 알게 되었다. 최대한 간결하게 나타내어 알아 보기 쉽게 하는 것도 React를 사용하는 이유 중에 하나라고 생각한다. 그렇기 때문에 과하지 않은 선에서 하위 component에는 최대한 간결한 내용만이 들어가도록 한다.

2. component 단위에서 state로 상태 및 데이터를 관리하고 업데이트할 수 있어 효율적인 유지, 보수가 가능하다. 하지만 주의해야하는 것은 this.setState()를 이용해 state를 변경하고, 그 변경된 값을 이용해 어떠한 작업을 하기 원하는 경우, 반드시 call-back 함수를 이용해야 한다. 왜냐하면 javascript는 비동기로 작동하기 때문에 this.setState() 바로 다음에 있는 함수에 state가 변경된 이후의 값이 반영되지 않기 떼문이다.

3. Package Manager 개발할 때 필요한 Library를 관리해주는 프로그램이다. 원래는 Node-Package-Manager만 존재했다. 그러나 속도가 느리고, 보안에 취약하다는 이슈가 부각되면서 yarn이 등장했다. yarn과 npm이 저장하는 곳은 동일하다.

4. input에 카드 번호와 같은 것을 넣을 때, form 태그에 타입 card 를 사용해서 크롬에서 지원하는 기능을 사용한다. install i save --s
