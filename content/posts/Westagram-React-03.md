---
title: "Westagram React-03"
date: "2019.10.19"
template: "post"
draft: false
slug: "/posts/westagram_react_03/"
category: "React"
tags:
  - "React"
description: "What I learned from Instagram-React Clone Coding"
socialImage: ""
---

## **Westagram React**

### class? constructor?

React에서는 class 혹은 function으로 component를 생성할 수 있다. 각각의 component는 기능과 가독성을 기준으로 분리되며 생성한 component는 HTML 태그처럼 사용할 수 있다. Instagram 클론 코딩에서는 class만을 이용해 component를 만들었다. component는 아래와 같이 만들 수 있다.

```js
class MyClass extends React.Component {
  constructor() {
    super();
  }
}
```

constructor를 사용한다면 항상 super()를 써줘야한다.

```js
class MyClass extends React.Component {
  constructor() {
    console.log(this); //Error: 'this' is not allowed before super()
  }
}
```

super() 전에 this가 허용되지 않는 이유는, super()가 불리지 않으면 this가 초기화되지 않기 때문이다.  
ES6 class constructor는 subclasses가 있다면 무조건 super()를 불러야 한다(하지만 constructor가 아예 필요없을 때도 있다).  
constructor 안에서 this.props에 접근하고 싶을 때는 super(props)를 쓰면 된다. 이외에는 자동으로 설정해준다.

```js
class MyClass extends React.Component {
  constructor(props) {
    super(props);
    console.log(this.props); // prints out whatever is inside props
  }
}
```

### **props와 state로 주고 받기**

Component로 나눌 때, 마치 HTML의 tree 구조로 이루어져 있는 태그를 직접 나누고 있는 것과 같은 느낌이 든다. 각각의 태그를 class 혹은 function으로 만들어 배치할 수 있다는 점이 Front-End의 기능과 흥미를 한층 더 해준다.

Instagram 클론 코딩을 하며 총 2개의 페이지를 만들었다. 먼저 Login 페이지에서 데이터 세트에 미리 지정해둔 아이디와 비밀번호를 입력하면 main 페이지로 넘어갈 수 있도록 만들었다.

```js
class IdPwForm extends Component {
  constructor() {
    super();
    this.state = {
      placeholder: { id: "전화번호, 사용자 이름 또는 이메일", pw: "비밀번호" },
      type: { id: "text", pw: "password" },
      idActive: false,
      pwActive: false,
      warning: false,
      idValue: "",
      pwValue: ""
    };
  }
```

class 내에서 state는 다음과 같이 관리할 수 있다. state는 component 내에서 보관할 수 있는 일종의 상태 값이며 수정이 가능하다. 예를 들어, 위의 `placeholder, type` 이라는 key는 특별한 경우가 아닌 이상 변동 사항이 거의 없다. 그러나 `idActive, pwActive, warning, idValue, pwValue`와 같은 상태 값들은 변동이 필요한 것들이다.

```js
idActivate = state => {
  state
    ? this.setState({ idActive: true }, () => {
        const { makeWarning } = this;
        makeWarning();
      })
    : this.setState({ idActive: false }, () => {
        const { makeWarning } = this;
        makeWarning();
      });
};
```

idActivate는 id를 입력한 뒤 다시 지웠을 경우, id를 입력해야한다는 경고를 밑에 생성하는 메서드이다. 위처럼 `Boolean ? ifTrue : ifFalse` 와 같은 삼항 연산을 이용하면 간결하게 표현할 수 있다.

```js
updateInputVal = (name, textValue) => {
  this.setState({
    [name]: textValue
  });
};
```

input의 value는 항상 조심스럽게 다뤄야 한다.  
왜냐하면 사용자는 정확한 값을 입력했는데 네트워크나 기타 오류로 인해 백엔드 서버에 제대로 전달되지 않을 경우, 서버는 부정확한 값이라고 인식하게 되고, 서비스에 큰 차질로 이어질 수 있기 때문이다.  
그래서 local storage와 같은 브라우저의 데이터 베이스에 업데이트한 뒤, 그 값을 사용자에게 보여주는 방식으로 input의 value를 관리해야 한다.

이번 Instagram 클론 코딩에서는 local storage를 이용하지는 않았고, 미리 import 해둔 데이터 파일의 값과 id, pw가 일치할 경우 main 페이지로 넘어갈 수 있도록 했다.

```js
goToMain = () => {
  const { idValue, pwValue } = this.state;
  const { history } = this.props;
  LoginData.forEach(user => {
    Object.values(user).includes(idValue) &&
    Object.values(user).includes(pwValue)
      ? history.push("/main")
      : window.location.reload();
  });
};
```

##### **Destructuring Assignment**

비구조화 할당을 이용하면 이미 구조화되어 있는 객체나 배열 등을 해체하여 간결하게 다룰 수 있다. 아래와 같이 계속해서 반복되는 선언들을 모아 한꺼번에 할당할 때 유용하게 사용할 수 있다.

```js
render() {
    const { placeholder, type, warning, idActive, pwActive } = this.state;
    const {
      idActivate,
      pwActivate,
      handleSubmit,
      goToMain,
      updateInputVal
    } = this;
  }
```
