---
title: "Westagram React-01"
date: "2019.10.15"
template: "post"
draft: false
slug: "/posts/westagram_react_01/"
category: "React"
tags:
  - "React"
description: "A First Step to React"
socialImage: ""
---

## **Basics of React**

#### **React란?**

React는 Javascript의 라이브러리이다. 2세대 개발 process에서 3세대로 넘어오는 과정에서 가장 큰 특징이라고 한다면, SPA(Single Page Application)일 것이다. Single-Page Application, SPA, 스파는 서버로부터 완전한 새로운 페이지를 불러오지 않고 현재의 페이지를 동적으로 다시 작성함으로써 사용자와 소통하는 웹 애플리케이션이나 웹사이트를 말한다. HTML, 자바스크립트, CSS 등 필요한 모든 코드는 하나의 페이지로 불러오거나,적절한 자원들을 동적으로 불러들여서 필요하면 문서에 추가하는데, 보통 사용자의 동작에 응답하게 되는 방식이다. 문서는 프로세스 중 어떠한 지점에서도 다시 불러들이지 않으며 다른 문서로 제어권을 넘기지 않으나, 위치 해시나 HTML5 히스토리 API를 사용하여 애플리케이션 안에서 개개의 논리 문서의 인식 및 탐색을 제공한다.  
React는 SPA를 활용하기에 굉장히 적합한 라이브러리로써, 상호작용이 많은 UI를 만들 때 생기는 어려움을 줄여준다. 그리고 애플리케이션의 각 상태에 대한 간단한 뷰만 설계하여 데이터가 변경됨에 따라 적절한 컴포넌트만 효율적으로 갱신하고 렌더링되도록 한다.

#### **JSX**

React에서는 Javascript와는 약간 다른 문법인 JSX라는 것을 사용한다. 쉽게 말하면 Javascript 안에 HTML 태그를 쓸 수 있게 되는 것을 의미하는데, 예를 들어

```js
const greeting = <div>hello</div>;
```

와 같은 형태를 가진다. 뿐만 아니라, 변수, 연산 등 기본적으로 Javascript에서 작동되는 거의 대부분을 HTML 태그 안에서 직접 활용이 가능하기 때문에 편리하고, 효율적인 코드 작성이 가능하다.

#### **Component**

Component는 일종의 재사용이 가능한 UI 단위이다. 반복 가능한 UI를 Component 단위로 만들어, 쉽게 수정 및 재사용이 가능하다.

```js
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

위와 같이 `class` 형태로 생성이 가능하다. 생성된 Component는

```js
<Welcome>
```

위와 같이, customized tag처럼 활용이 가능하다.

##### state 와 props

- state는 Component 내에 상태 값을 말한다.
  ```js
  constructor() {
  super();
  this.state = {
    count: 0,
  };
  }
  ```
  위처럼 Component 안에서 만들어지며 setState를 사용하면 값을 변경할 수도 있다. state의 값이 변경되면 자동으로 다시 Rendering하게 된다.
- props는 기본적으로 부모에게서 받아오는 값을 이야기한다(defaultProps를 사용하면 Component 내부에서도 설정할 수 있다). 이 값은 변동할 수 없으며, 부모에게서 받는 값을 그대로 사용하게 된다.

#### **Lifecycle**

render, componentDidMount, componentDidUpdate, componentWillUnmount 등의 함수는 React.Component class에서 제공하는 Method이다. 컴포넌트를 만들 때 class로 생성하면 위의 Method를 사용할 수 있고, 컴포넌트가 Lifecycle에 따라 각자의 메서드가 호출된다.
![lifecycle](https://yeri-kim.github.io/media/190417-lifecycle-1.png)

위와 같은 순서대로 작동하며, 효율적인 Rendering을 위해 각각의 순서를 인지하여 적절한 곳에 함수와 Method를 배치하는 것이 중요하다.

componentDidMount() : render() 메서드 다음에 호출된다. this.setState()를 사용할 수 있어 다시 render를 해야 할 때 사용할 수 있다. 그로므로 fetch data를 할 때 사용 가능하며, event listener, setTimeOut 등을 이용하면 유용하게 사용할 수 있다.
