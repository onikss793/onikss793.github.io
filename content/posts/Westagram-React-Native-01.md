---
title: "Westagram React Native"
date: "2019.10.18"
template: "post"
draft: false
slug: "/posts/westagram_react_native01/"
category: "React Native"
tags:
  - "React Native"
description: "Glimpse of React Native"
socialImage: ""
---

## **React Native**

`expo init {project name}`를 사용해서 쉽게 project를 시작할 수 있다. react-create-app과 거의 같은 기능을 한다고 볼 수 있다. expo가 편리한 점은 실제 휴대전화 앱으로 다운 받아 같은 로컬에서 현재 내가 작업하고 있는 프로젝트를 실시간으로 확인할 수 있다는 점이다. 또 한가지는 hot render를 통해 내가 변화시킨 부분만 매우 빠르게 확인할 수 있다는 점이다. 마치 web에서 localhost를 통해 바로 바로 확인하며 작업하는 것과 같은 효과를 낼 수 있다.

expo로 시작할 때, template의 기본 설정을 선택할 수 있다. expo를 사용하는 경우의 대부분, blank로 시작한다. 하지만 처음에는 너무 어렵기 때문에 tab으로 시작했다.  
tab을 선택하게되면 기본적으로 주어지는 template들이 많이 있다. 가장 먼저 눈으로 볼 수 있는 것은 Homescreen이다. westagram 중에서 1개의 페이지만 만들기로 했으므로, Homescreen에 기본적인 틀을 잡아 작업하기 시작했다. reaact native는 별도의 css 대신 styles라는 변수를 활용한다. 객체 형태를 이용해 일종의 props처럼 받아서 쓸 수가 있다.
