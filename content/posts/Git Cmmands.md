---
title: Git commands
date: "2019.10.04"
template: "post"
draft: false
slug: "/posts/git_commands/"
category: "Git terminal"
tags:
  - "Git"
  - "Terminal"
description: "Basic Commands of terminal for git"
socialImage: ""
---

#### **github.io 블로그 만들며서 썻던 git commend들 정리**

- 기본적인 터미널 단축키
  cd: change directory 디렉토리로 이동할 수 있다.  
  ls: listing directory 디렉토리에 있는 콘텐츠를 확인할 수 있다.  
  open: file을 열 수 있다.  
  mv: move file을 이동시킬 수 있다  
  mkdir: make directory 새로운 디렉토리를 만들 수 있다.  
  rmdir: 디렉토리를 제거할 수 있다 .  
  rm -R: 현재 경로 안에 있는 디렉토리를 제거한다.  
  sudo: 관리자로서 접근하여 명령할 수 있다. 매우 신중히 사용할 것.

1. 우선 Gatsby를 사용할 수 있도록 전역에 설치  
   `npm install -g gatsby-cli`  
   npm은 node.js package manager의 약자로 자바스크립트 언어를 위한 패키지 관리자이다. node를 다운받으면 같이 받을 수 있다.
2. Gatsby의 theme 중 원하는 것의 source code를 가져온다.
   `gatsby new blog https://github.com/alxshelepenok/gatsby-starter-lumen`  
   추가적으로 facebook이 만든 yarn을 설치했다.  
   yarn은 npm과 같은 자바스크립트 언어를 위한 패키지 관리자이다. npm의 취약한 저장소, 보안의 대안으로 나타났으며 npm보다 속도가 빠르다고 한다.
3. 블로그 설치 완료 후 localhost에서 확인  
   yarn develop 혹은 npm run develop으로 localhost:8000에서 확인 가능하다.  
   추가적으로 서버를 멈추고 싶다면 terminal 창을 끄거나 ctrl-c를 누르면 서버가 닫힌다.
4. github에 repository를 만든다.
   github에서 repository를 만든다. 여기서 주의할 점은 github 사용자 아이디와 같은 이름으로 naming해야 한다는 것이다. 그리고 사용자 이름 뒤에 github.io를 붙인다.  
   `username.github.io`
5. Source Code와 Repository를 연결한다. 설치한 blog파일에서 git을 시작한다.  
   `git init` Repository의 주소와 연결한다.  
   `git remote add origin repository-url`  
   git add와 git commit을 통해 내용을 추가, 수정한 뒤 repository에 저장 가능하다.  
   git add는 commit하기 전 추가할 사항들을 정하는 명령어로 add -p로 세부적인 사항을 하나하나 검토할 수도 있고, add . 으로 일괄적으로 추가할 수도 있다.  
   git commit은 현재 branch로 push하기 전, 그러니까 저장소로 업로드하기 전에 메시지와 함께 작업 내역을 마지막으로 정리할 수 있는 명령어이다. commit -m으로 메시지를 남길 수 있고, commit -v를 이용하면 세부적인 변경사항을 확인할 수 있다.
6. push와 deploy
   branch는 보통 배포용인 master 외에 추가적으로 만들어 관리한다. 블로그이기 때문에 추가적인 branch 한 개를 더 만들어 내용을 업로드한다. 그러나 그 상태로는 아무리 push를 해도 배포에는 반영이 되지 않기 때문에, 자동으로 수행할 수 있는 `"deploy": "yarn run clean && gatsby build && gh-pages -d public -b master` 명령어를 실행한다.  
   이후 배포할 때는 `yarn deploy`를 명령어를 사용하면, 알아서 build, master에 push 그리고 deploy도 실행된다.

​

##### **commands**

- git init: local에 새로운 repository를 만든다.
- git clone: local에 repository를 복사한다.
- git add: 상태에 1개 혹은 그 이상의 파일을 추가한다.
- git commit: 상태를 commit한다. repository에 접근하기 바로 전 단계
- git push { branch }: branch에 commit한 사항을 업로드 한다.
- git status: 현재의 상태
- git remote add origin: local에 있는 repository를 서버에 연결할 때 사용한다.
- git checkout: 해당 repository의 branch 리스트를 보여준다.
- git checkout { branchname }: 해당 branch로 이동한다.
- git log: commit한 기록들을 보여준다.
