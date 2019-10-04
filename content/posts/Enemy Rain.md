---
title: Enemy Rain
date: "2019.10.04"
template: "post"
draft: false
slug: "/posts/enemy_rain"
category: "HTML css javascript"
tags:
  - "HTML"
  - "css"
  - "javascript"
description: "What I Learnded From Making Vanila Javascript Game"
socialImage: ""
---

#### **개요**

1. 배경화면을 띄운다.
2. 주인공이 배경 맨 아래에 위치하며 오른쪽, 왼쪽으로 이동할 수 있다.
3. 주인공이 왼쪽, 오른쪽으로 이동할 때마다 각각에 맞는 이미지로 변하며, 배경의 끝에 도달하면 더 이상 못 움직인다.
4. 귀신이 위에서 무작위로 내려온다.
5. 주인공이 귀신을 잡으면 귀신이 죽고 약 2초 뒤에 사라진다.

#### css

- 선수 지식: image-sprite - 여러 개의 이미지를 한 개의 파일에 모두 담아 관리하는 이미지를 말한다. 이렇게 하면 서버에서 각각의 이미지를 다운 받으면서 생기는 로딩 시간을 단축할 수 있고, 한 개의 파일만 관리하면 되기 때문에 유용하다.  
  image-sprite를 사용하려면 background-postition을 사용해야 하는데 x축과 y축, width와 height를 이용해 하나의 이미지 파일에서 원하는 만큼만 보여지게 할 수 있다.

#### Javascript

- 가장 먼저 애를 먹었던 부분은 주인공과 귀신 모두 class를 사용해 생성해야 한다는 것이었다. 얼추 흉내는 냈지만 많은 부분을 그냥 function으로 실행했기 때문에 추후에 리팩토링하며 class로 변환하는 것을 연습해보아야겠다.

  먼저 주인공 class에는 `this.hero`라는 div를 만들었다. 그리고 `createHero, heroLeft, heroRight`라는 method를 만들었다.

  createHero(x)를 이용해 x축 값을 받아 배경 상에서 주인공이 어디에 위치할지를 정해주었고, 기본값으로 정면을 바라보고 있는 이미지를 주었다. `` this.hero.style.left = `${x}px` ``를 사용했는데, javascript내에서 style을 적용할 때, 저런 식으로 px을 따로 입력하는 것을 잊지 말자.
  heroLeft()를 이용해 왼쪽을 바라보고 있는 이미지를, heroRight()를 이용해 오른쪽을 바라보고 있는 이미지를 정해주었다.

  귀신 class에는 `createEnemy(x, y), killEnemy(), removeEnemy()`를 사용했는데, 주인공 class와 유사한 기능을 가지고 있으며, 추가 사항으로는 귀신이 떨어지기 위한 y값과 죽었을 때의 이미지를 위한 killEnemy(), 사라질 때를 위한 removeEnemy()가 있다. 사라지는 것을 단순하게 display:none으로 구현했는데 이외에 분명 더 좋은 방법이 있을 것 같다.

- 게임을 실행하는 것을 크게 3 가지로 구분해보면,  
  **1. 첫째로 주인공을 만든 뒤 좌우로 이동시키는 것**  
  **2. 둘째로 귀신을 만든 뒤 아래로 내려오게 만드는 것**  
  **3. 셋째로 주인공과 귀신이 만났을 때 효과를 주는 것**  
  이렇게 나눌 수 있을 것이다.

우선 Hero라는 인스턴스를 한개 생성한다. 인스턴스의 갯수가 곧 개체 수의 갯수가 되는데, 주인공은 한 명이므로 한개만 생성한다.  
기존의 Hero class로 만들어 두었던 주인공 생성 method를 사용해 주인공을 화면에 띄운다. 이때의 x값은 default인 배경의 한 가운데이다.  
keyUp, keyDown event를 사용해 키보드 좌, 우 키를 눌렀을 때 주인공의 이미지를 좌, 우에 맞게 바꾸어준다(background-position-x를 사용한다). 이때 주의해야할 것은 게임이 진행되는 과정에서 애니매이션처럼 보이게 만들어주는 setInterval과의 관계이다. 키보드를 눌렀을 때 바라보는 이미지가 주어진 초에 맞추어 소위 reset되기 때문에 키가 눌려졌는지 여부를 알 수 있는 변수를 만들어 마치 on/off 같은 기능을 만드는 것이 중요하다.  
주인공이 한번의 key event에 움직일 px을 정해준 뒤, 각각의 key가 on/off일 때 맞추어 움직이는 함수를 생성한다.

귀신을 생성하기에 앞서서 귀신이 생성될 random한 x축 값을 만드는 것이 우선이었다.  
최솟값, 최댓값의 범위 안에서 random한 상수를 생성하는 공식은 다음과 같다. `Math.random() * (max - min) + min` 만약 정수가 필요하다면 floor를 사용하면 된다.  
귀신을 생성할 때 의문이었던 것은, 귀신의 인스턴스가 많아질 경우, 어떻게 관리해야하나 하는 문제였다. 이를 해결하기 위해 배열을 만든 뒤 인스턴스 각각을 객체로 설정해 집어넣었다.  
귀신을 만들 때는 귀신의 y점이 배경의 높이보다 커질 경우, y는 0, x는 다시 randomise하게 설정했다.  
귀신이 떨어질 때 일괄적으로 떨어지는 속도가 재미가 없어보여, 곱하기를 통해 각각 속도가 다르도록 설정했다.

```js
function fallEnemy() {
  let fallingSpeed = 4;

  const adding = 1.2;

  for (let i = 0; i < enemyList.length; i++) {
    const enemy = enemyList[i];

    enemy.y += fallingSpeed;

    fallingSpeed *= adding;
  }
}
```

귀신과 부딫혔을 때를 계산하는 것이 제일 번거로웠는데, x축과 길이, y축과 높이를 계산하여 부딫혔을 때를 알 수 있다.

가장 찝찝한 부분은 귀신과 주인공이 부딫히고 나서, 귀신이 죽은 이미지로 바뀐 후, 사라지는 과정이다. setInterval로 실행하는 전체 실행 함수인 init에 같이 넣게되면 이미지가 바뀜과 동시에 사라지는 문제가 생긴다. 그렇다고 따로 setInterval을 정하게 되면 순전히 타이밍에 따라서 2초를 꽉 채운 후, 사라지는 경우가 있고, 2초를 채우지 못하고 사라질 때도 있다. 분명 다른 방법이 있을 것 같다.
