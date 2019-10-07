---
title: "Python"
date: "2019.10.05"
template: "post"
draft: false
slug: "/posts/python/"
category: "Python"
tags:
  - "python"
description: "Basics of Python"
socialImage: ""
---

#### **Hello World**

파이썬에서 화면에 출력을 하고 싶을 때는 `print()`명령어를 사용하면 된다.  
python은 indentation이 매우 중요하다. 그것을 통해 종속 관계를 설정하기 때문이다.  
 주로 `[space bar] X 4`를 사용한다.

## **Data Types**

파이썬에는 5개의 data types가 있다.

1. Integer 정수
2. Float 소수
3. Complex Numbers 실수와 허수를 포함하는 복소수
4. String 문자열
5. Boolean True / False

## **Math Expressions**

Javascript와 유사하지만 다른 점이 있다면, 몫을 구하는 `//`가 있다는 것이다. 예를 들어,

```py
num1 = 7
num2 = 2
num3 = num1 // num2
print(num3)
3
```

더불어 Integer끼리의 나눗셈의 결과값이 항상 Float의 형태가 된다. 예를 들어,

```py
num1 = 6
num2 = 3
num3 = num1 / num2
print(num3)
2.0
print(type(num3) == float)
True
```

## **literal string interpolation**

매우 python다운? String Concatenation 방법이 있다. 대략 3가지 정도가 있는데, 가장 편리한 방법 중 하나는 아래의 예시와 같다.

```py
name = "python"
pring(f"Hello, {name}")
"Hello, python
```

## **If Statement**

if는 javascript와 매우 유사한 방식으로 작동하는데, 몇 가지 문법이 조금 다르다. 그 차이는 직관적으로 python이 조금 더 쉽고, 편리한 방법을 지향한다는 점에 기인하는 듯 하다.

기본적인 문법은 다음과 같다.

```py
name = "python"
if name == "python":
    print(f"Hello, {name}")
"Hello, python"
```

또한, python은 else if와 else의 기능도 지원한다.(else if 는 elif로 줄여 사용한다)

```py
name = "python"
if name == "javascript":
    print(f"Hello, Javascript")
elif name == "java":
    print(f"Hello, Java")
else:
    print(f"Hello, python")
```

## **Logical Operators**

python은 javascript보다 직관적인 논리 연산자를 제공하는 듯 하다. 말 그대로 `and`는 `그리고`의 의미를, `or`은 `또는`의 의미를 가지고 있다. 아울러 `>, <, =>, =<, ==, !=`를 통한 비교 연산도 가능하다.

## **Data Structure**

- list: 서로 다른 type의 값들을 `[]`안에 저장할 수 있으며, 순서가 존재한다. 그렇기에 index를 통해 list의 요소들을 조회할 수 있다.

  - 기본적인 추가, 제거는 `append() / del / remove()`로 구현할 수 있다.
  - slicing은 `list[start:end]`로 가능하다.

- tuple: tuple은 list와 유사하게 요소들을 한데 모아 저장할 때 쓰이지만, 약간의 차이를 가지고 있다. tuple은 한번 선언하게된 이후에는 수정이 불가능하다. 그럼에도 tuple을 쓰는 이유는 list보다 차지하는 메모리 용량이 적기 때문에, 수정이 필요없고 간단한 형태의 데이터는 tuple로 사용하는 것이 효과적이다.  
  tuple은 list와 같이 쓰이는 경우가 많다. 예를 들어,

  ```py
  my_list = [1, 2, 3, 4, 5, 6]
  print(tuple(my_list))
  [(1, 2), (3, 4), (5, 6)]
  ```

- set: List는 순차적으로 여러가지 요소들이 들어갈 수 있다. 하지만 set은 순차적으로 저장되지 않으며 중복되는 요소들이 없다. 예를 들어,

  ```py
  my_list = [1, 2, 1, 2, 3, 2, 4, 5]
  print(set(my_list))
  {1, 2, 3, 4, 5}
  ```

- 기본적인 추가, 제거는 add()와 remove()로 구현할 수 있다.
- set은 어떠한 요소가 있는지 찾거나 조회하는데 유용하다.
  in 키워드를 사용해 포함 여부를 확인할 수 있다.  
   `&` 와 `|` 를 이용해 교집합과 합집합을 구할 수도 있다.

  ```py
  set1 = {1, 2, 3, 4, 5, 6}
  set2 = {4, 5, 6, 7, 8, 9}
  print(set1 & set2)
  > {4, 5, 6}
  print(set1.intersection(set2))
  > {4, 5, 6}
  ```

- Dictionary: key와 value의 값으로 이루어져 있다. Javascript의 객체와 매우 유사하다. 하지만 dot notation으로는 접근할 수 없고, 오직 [key]를 이용해 접근할 수 있다.

## **Loops**

- for
  - Javascript와 대부분 유사한 방식으로 작동한다. 그러나 변수를 통한 접근이 아닌
    `py for element in list: do_something_with_element`
    element에 직접적인 접근이 가능하다.
    list, tuple, set 등 다른 data structure에도 사용이 가능하다.
  - break: 반복문이 도중에 break를 만나게 되면, 반복문을 종료하고 빠져나온다.
  - continue: 반복문이 도중에 continue를 만나게 되면, 다음 반복으로 넘어가게 된다.
- while
  - else: Javascript의 while과 거의 유사하다. 그러나 Python의 while문은 else문을 추가할 수 있다. while의 조건이 성립되지 않을 때 실행된다는 것인데, 쉽게 말하면 while이 종료될 때 실행된다는 것이다.

## **Keyorded variable length of arguments**

- 그 수가 정해지지 않고, 유동적으로 변화할 수 있는 arguments를 받기 위해 "kwargs"라는 기능이 있다. 대부분 "\*\*kwargs"라고 parameter 이름을 정한다.
- 이와 비슷하지만, keyword를 사용하지 않고, 순서대로 값을 전달하며, 그저 다양한 수의 arguments를 받기 위한 "args"라는 기능이 있다. 주로 "\*args"라고 parameter 이름을 정한다. 이 arguments는 tuple로 변환되어 함수로 전달된다.

## **Nested Function(Decorator)**

- closure를 이용해 부모 함수에서 선언된 변수나 정보를 외부로부터 격리한 채, 중첩 함수에서 그 값을 참조해 사용하기 위해 Nested Function을 사용한다.
- 중첩 함수의 유지, 보수, 재사용의 효율을 최대화하기 위해 Decorator를 사용한다.
  ```py
  @decorator
  def function():
      return 'Hello'
  function()
  ```
  위와 같이 function을 실행했을 때, "@decorator"를 자동을 먼저 실행하게 되고,
  "function"이라는 함수를 인자로 받아 사용할 수 있다.
  가장 쉽게 이해할 수 있는 방법은 실행 순서를 생각하며 코드를 짜는 것 같다. 인자에 집중하게 되는 순간 헷갈릴 여지가 생긴다.

## **Class**

- Python의 클래스는 Javascript와 다르게 this대신 self라는 키워드를 사용한다.
  또한 클래스 안에서 정의할 수 있는 special method가 있다. 앞, 뒤에 더블 언더스코어(**)를 붙여 사용하는데, 대표적으로 **init\_\_이라는 magic method가 있다. 인스턴스가 선언됨과 동시에 호출된다.

## **Module & Packages**

- 다른 파일에서 재사용이 가능하고, 여러 파일로 나누어 정리하고 관리할 때 사용하는 것이 module이다. import, import as로 모듈을 호출할 수 있다. 특정 함수나 변수를 호출하기 위해서는 from import 키워드를 사용하면 된다. Package는 Module의 모음이라고 생각하면 되며, dot notation과 위의 import와 같은 키워드로 활용하면 된다. Package 안에 **init**.py이라는 라는 파일이 있으면 해당 Package가 import될 때 자동으로 해당 파일의 코드들이 실행되기 때문에 package의 초기 설정이 가능하다.
- Sys Module
  Sys 모듈은 파이썬 런타임 환경의 다양한 부분을 조작하기 위해 사용되는 함수와 변수를 제공한다.  
   먼저 런타임 환경이란 무엇일까. 런타임 환경을 알기 위해서는 런타임을 알아야 할 것 같다. 런타임은 프로그램이 실행되고 있는 그 순간을 말한다. 예를 들어, 컴퓨터에서 어떤 프로그램이 가동되면 그 순간이 그 프로그램의 런타임이다. 말그대로, "runtime 작동하는 순간"을 말한다. 여기서의 순간은 단순 시간적인 것만 이야기하는 것이 아닌, 환경 전체를 의미한다고 보는 것이 명확하다. Javascript => Browser, Node.js 그렇기에 런타임 환경이라는 말을 쓴다고 생각한다.

  이 시점에서 맨 첫 문장을 다시보자. Sys 모듈은 파이썬을 구동하는 동안 특정 부분을 조작하기 위해 함수와 변수를 제공한다는 의미이다.

  Sys 모듈 빌트인 모듈이다. 파이썬을 설치할 때 이미 포함되어 있으므로 쉽게 찾을 수 있다.

  sys.modules는 현재 로딩되어 있는 모듈들을 dictionary 형태로 나타낸다. 수정, 삭제와 같은 조작이 가능하다.

  sys.path는 파이썬이 모듈을 찾을 때 참조하는 경로를 나타낸다. 여기에 없다면 파이썬이 찾을 수 없을 것이다.
