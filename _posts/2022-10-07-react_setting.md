---
title:  "SETTING"
excerpt: "REACT 초기 실행및 설정"

categories:
  - Server
tags:
  - [REACT]

toc: true
toc_sticky: true
 
date: 2022-10-07
last_modified_at: 2022-10-14


---


### 프로젝트생성
$ npm install -g create-react-app
터미널 창 이동 후
$ create-react-app  프로젝트명

### 프로젝트 시작
npm run start
### 프로젝트 구조
node_modules : CRA를 구성하는 패키지 소스 코드가 존재하는 폴더
package.json : CRA 기본 패키지 외 추가로 설치된라이브러리/ 패키지 정보(종류,버전)가 기록되는 파일 
public : static자원 폴더 , 정적파일들을 위한 폴더
src: 리액트를 작업할 폴더  
package-lock.json :프로그래머가 관리할 필요가 없고 npm 이나 yarn이 알아서 관리해주는 파일들
lock파일은 해당 프로젝트에 설치한 패키지 , 그패키지와 관련된 모든 패키지의 버전정보를 포함한다.
## package.json
- dependencies : 리액트를사용하기위한 모든 패키지 리스트, 버전확인 가능 , 실제코드는 node.modules 폴더에 존재한다
- script : start : 프로젝트 development mode(개발 모드) 실행을 위한 명령어. npm run start
build : 프로젝트 production mode(배포 모드) 실행을 위한 명령어. 서비스 상용화.
## public 폴더
- index.html
  메인프로그램인 index.js에 대응되는 것으로 , HTML 템플릿 파일
  이파일이 직접 표시되는서이 아니라 index.js에 의해 랜더링 된 경과가표시됨


## src 폴더
- index.js
index.js을 포함하고 있다.
React의 시작
ReactDOM.render(<App />, document.getElementById('root'))
ReactDOM.render 함수의 인자는 두개이다. 첫 번째 인자는 화면에 보여주고 싶은 컴포넌트,
두 번째 인자는 화면에 보여주고 싶은 컴포넌트의 위치

## App.js
현재 화면에 보여지고 있는 초기 컴포넌트
React Router를 설치하면 컴포넌트가 최상위 컴포넌트로 App.js 컴포넌트 자리에 위치하게 된다.


### 프로젝트 기본 custom
## src 폴더
1. assets 
* 프로젝트에서 사용할 이미지,비디오,json 파일등 미디어 파일들을 모아두어 저장하는곳
2. components 
* 공통 컴포넌트 관리(ex-Header , Footer , Nav등)
3. pages 
* 페이지 단위로 컴포넌트 폴더로 구성 
* ex)Login-Login.js , Login.scss / Main - Main.js , Main.scss

### 프로젝트 배포
npm run start


component 경로관리
https://velog.io/@rimo09/React%EC%97%90%EC%84%9C-%EC%BB%B4%ED%8F%AC%EB%84%8C%ED%8A%B8-%EA%B2%BD%EB%A1%9C-%EA%B9%94%EB%81%94%ED%9E%88-%EA%B4%80%EB%A6%AC%ED%95%98%EA%B8%B0