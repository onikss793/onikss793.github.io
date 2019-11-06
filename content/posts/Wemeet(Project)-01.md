---
title: "Wemeet(Project)-01"
date: "2019.11.01"
template: "post"
draft: false
slug: "/posts/til_191101/"
category: "TIL"
tags:
  - "Scrum"
  - "Project"
description: "Things I've learned through project"
socialImage: ""
---

## Sticky(css)

```js
<div className="main-right-wrapper">
  <div className="main-right">
    <Card
      startDate={data.startDate}
      endDate={data.endDate}
      address={data.address}
      findGroup={data.findGroup}
      geo={{ lat: data.lat, lng: data.lng }}
    />
    <GoogleMap geo={{ lat: data.lat, lng: data.lng }} />
  </div>
</div>
<style>
  .main-right-wrapper {
    .main-right {
      position: sticky;
      top: 120px;
    }
  }
</style>
```

스크롤 할 때, 일정 부분 이상 내려오면 화면에 붙어서 같이 움직이고 싶은 Element가 있다면 sticky를 쓰면 매우 유용하다. sticky는 top, bottom, right, left 중 하나를 필수로 작성해야 한다. 그러면 해당 값에 위치했을 때를 무조건 유지하게 된다. 하지만 주의해야 하는 것은 sticky의 이름 뜻처럼 해당 element가 붙을 wrapper를 만들어주어야 한다는 것이다. 위의 코드에서 stick되는 부분은 `.main-right`이다.  
`.main-right-wrapper`가 없이 적용했을 경우 아예 stick되지 않는다. 하지만 main-right-wrapper로 해당 element가 붙을 수 있도록 해주면 그때부터 정상적으로 작동한다.

## React Router Querystring

React는 Router라는 써드 파티 라이브러리를 사용할 수 있다. 이것을 잘 쓰면 매우 유용하게 화면 전환이 가능하다.  
Wemeet 프로젝트에서 다양한 이벤트 리스트들이 존재하는데 특정한 이벤트를 클릭할 경우 해당 이벤트에 대한 api 호출을 해야 한다. 결국 이벤트 페이지는 하나이지만 어떠한 데이터를 받아오느냐에 따라 다양한 텍스트가 보여져야 하는 것이다. 같은 페이지이지만 다른 url을 사용하려고 할 때 쓸 수 있는 것이 바로 querystring이다.

```js
<Route exact path="/event?eventId=id" component={Event} />
```

먼저 `<Route>`에 어떠한 기준으로 url을 다르게 할 것인지를 위처럼 `:querystring`으로 구분해야 한다. 위의 경우에는 각각의 이벤트의 아이디를 기준으로 하였다.

```js
getData = () => {
  const { eventId } = this.props.match.params;
  fetch(`http://localhost:8000/event/${eventId}`)
    .then(res => res.json())
    .then(res => console.log(res));
};
```

그럼 이제 event list가 있는 페이지에서 특정 이벤트를 클릭할 경우, 그 이벤트의 아이디를 기준으로 예를 들면, `https://localhost:8000/event/${특정아이디}` 페이지로 넘어가게 된다.

그 이벤트 페이지가 mount 되는 순간 `const { eventId } = this.props.match.params;` 를 통해 그 이벤트 아이디를 사용해 GET 요청을 보내 해당 데이터를 받을 수 있다.
