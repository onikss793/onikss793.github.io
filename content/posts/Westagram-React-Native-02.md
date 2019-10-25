---
title: "Westagram React Native Navigation"
date: "2019.10.24"
template: "post"
draft: false
slug: "/posts/westagram_react_native02/"
category: "React Native"
tags:
  - "React Native"
description: "React Native Navigation"
socialImage: ""
---

모바일 앱은 대부분 여러 개의 스크린으로 이루어져 있다. 다수의 스크린을 다룰 때는 navigator를 사용하면 된다. 네비게이터를 만들기 위해서는 다양한 Navigation component를 사용할 수 있지만, navigation을 처음 사용하는 입장에서는 React Navigation을 사용하는 것이 좋다. React Navigation은 iOS와 Android에서 모두 사용가능하며 stack navigation과 tabbed navigation을 제공한다.

```js
npm install --save react-navigation
npm install --save react-native-gesture-handler
npm install --save react-navigation-stack
```

위 명령어로 react navigation을 설치할 수 있다. 하지만 expo tab으로 작업할 경우, 자동적으로 설치가 된다.

createStackNavigator는 stack이 되는 component를 return한다.
createAppcontainer는 stack인 component를 인자로 받는다.

```js
const AppNavigator = createStackNavigator({
  Home: {
    screen: HomeScreen
  }
});
```

위와 같은 방식으로 작성하면 되는데 주의할 점은

```js
import { createAppContainer } from "react-navigation";
import { createStackNavigator } from "react-navigation-stack";

import Main from "./Main";

const MainNavigator = createStackNavigator(
  {
    Home: { screen: Main },
    Sample: { screen: Sample }
  },
  {
    initialRouteName: "Home"
  }
);

const Index = createAppContainer(MainNavigator);

export default Index;
```

반드시 위와 같은 방식으로 import를 해줘야 한다는 것이다.  
`Home: { screen: Main },` 밑에 screen을 추가할 수 있다. screen으로 넘어가려면 아래와 같이 작성하면 된다.

```js
// Sample.js
<View style={{ flex: 1, alignItems: "center", justifyContent: "center" }}>
  <Button
    onPress={() => this.props.navigation.navigate("Home")}
    title={"Home"}
  ></Button>
</View>
```

위와 같이 `this.props.navigation.navigate(name)`를 쓰면 해당 name이 있는 screen의 stack이 덮어 쓰게 된다. 자동으로 뒤로 가기 버튼이 생성되고 아이폰의 경우 화면의 끝을 슬라이드하면 뒤로 갈 수 있다.  
이제 여러 screen을 Appcontainer에 적용시켰다면 실제로 이동하도록 만들어주면 된다. 어떠한 button을 눌렀을 때 이동하게 하려면 아래처럼 하면 된다.

```js
goToSample = () => {
    const { navigate } = this.props.navigation;
    navigate("Sample");
  };

  render() {
    const { userInfo } = this.props;
    const { userImage, user, userName } = styles;
    const { goToSample } = this;

    return (
      <TouchableOpacity onPress={goToSample}>
        <View style={user}>
          <Image source={userInfo.img} style={userImage} />
          <Text style={userName}>{userInfo.userId}</Text>
        </View>
      </TouchableOpacity>
    );
  }
```

여기서 가장 중요한 것은 `this.props.navigation.navigate`이다.  
만약 이 코드만 작성할 경우, `this.props.navigation`이 undefined로 나오게 된다.

React에서 Router를 할 때도 잘 생각해보면 넘어가고자하는 Route를 설정하는 component에는 반드시 withRouter를 import하고 HOC해주어야 했다.

React Native에서는 그 작업이 없는 대신 screen을 지정해 놓은 component에서 `navigation={this.props.navigation}`을 해당 component까지 이어주어야 한다.

다시 말해, screen component에서 해당 component까지의 사이에 있는 모든 부모 comonent에 `navigation={this.props.navigation}`를 작성해주어야 한다.

expo tab으로 어플리케이션을 시작하게 되면, Navigation에 대한 구조가 비교적 잘 나와 있다. 먼저 Navigation 폴더에는 navigation 구조를 담은 파일을 담아야 한다.

```js
const MainStack = createStackNavigator(
  {
    Main: { screen: Main },
    Profile: { screen: Profile }
  },
  {
    initialRouteName: "Main"
  }
);
MainStack.navigationOptions = {
  tabBarLabel: "Main"
};
MainStack.path = "";
const ProfileStack = createStackNavigator({
  Profile: { screen: Profile }
});
const tabNavigator = createBottomTabNavigator({
  MainStack,
  ProfileStack
});
tabNavigator.path = "";
export default tabNavigator;
```

위와 같이 각각의 screen을 stack으로 만들고, 어떤 구조로 stack을 쌓을 것인지를 설정해준다. 그리고 `createBottomTabNavigator()`를 사용하면 화면의 하단에 위치할 navigation을 만들 수 있다. 위의 경우에는 메인 페이지와 프로필 페이지로 이동할 수 있는 네비게이터를 만들었다.

```js
export default createAppContainer(
  createSwitchNavigator({
    Main: MainTabNavigator
  })
);
```
