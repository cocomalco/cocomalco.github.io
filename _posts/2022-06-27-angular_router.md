---
title:  "ANGULAR ROUTER"
excerpt: "angular 라우터 개념및 사용"

categories:
  - Angular
tags:
  - [Angular, Router]

toc: true
toc_sticky: true
 
date: 2022-06-27
last_modified_at: 2022-06-27


---

### 개념  
SPA
단일 페이지 어플리케이션 (Single page Application)의약자.

### SPA의 장점
기존 서버의 사이드렌더링 방식은 요청에 응하는 새로눔 페이지릉 다시 그려 제공 하여 비용과 속도에 문제가 있다. 이문제를 해결하기 위해 처음에 모든리소스를 다 내려받고  그안에서 동작하게 하게한다.
초반 구동 속도는 상대적으로 느리지만 구동후의 속도는 압도적으로 빠르다.
그이후 필요한 데이터는 부분적으로 요청후 업데이트.

### SPA의 단점
초기구동 속도가 느림  
SEO(검색 엔진 최적화)
우리 웹사이트가 검색 엔진에 노출되는 방식은 아래와 같은 순서로 색인된다.
1) 검색엔진 로봇이 사이트를 돌아다닌다.
2) 사이트의 웹문서 파일을 읽는다. (주로 HTML 코드 파일)
3) 읽은 파일 내용을 토대로 검색 엔진에 노출시켜준다.

웹페이지가 각각 100개씩 있는 페이지는 검색 봇이 페이지를 읽을 수 있다.
하지만, 페이지는 1개이고 필요한 부분만 JavaScript로 바꿔진 경우 검색봇이 페이지를 읽을 수 없게 된다.

### ROUTING
출발지에서 목적지까지의 경로를 결정하는 기능 , SPA(single page Application)를 위한 클라이언트 사이드 네비게이션으로, URL과 컴포넌트의 쌍으로 라우트 설정을 참고 하여 , 뷰를 렌더링 한다.
본래 라우팅시 URL 을 변경하여 다른 페이지로 넘어가는 방식과 다르게 AJAX 요청에 의해 서버로부터 받은 데이터를 반다 화면을 생성 하는 경우에는  URL이 변경되지 않아, SEO 문제가 야기된다.
라우터를 사용하여 화면 전환을 하려면 component가 2개 이상 존재해야 한다.

### 위치정책
SPA 이기 때문에 새로고침시 첫페이지가 로드되며 , URL이 변경되지않아 SEO 문제를 해결하기 위해 2가지 정책을 제시한다.

pathLocationStrategy
HTML5 History API pushState 메서드 를 사용하는 정책으로 Angular 라우터의 기본 정책.

HashLocationStraregy
해시 URL 스타일을 사용.

### 기본 라우팅 규칙 
AppModule 이 정의된 파일에 AppRoutingModule을 로드하고 , 이 라우팅 모듈을 AppModule import에 추가.
Angular CLI로 앱을 생성했다면 , 해당 과정이 처리 완료, 앱을 직정 작성하거나,이미 있는앱기반으로 작업 한다면 규칙을 확인 해야 한다.



### 라우터 설정



1. 라우트 구성및 등록
Route 인터페이스 배열을 이용하여 path와 전환될 component를 설정  
  [app-routing.modules.ts]  
  <script src="https://gist.github.com/cocomalco/54b65e8ccf6a364db84d84d8e3df53e8.js"></script>

  | 요청한 URL 경로 | URL | 활성화될 컴포넌트 |
  |:--------:|:--------:|:--------:|
  | HOME |localhost:4200/HOME|HomeComponent|
  | CUST |localhost:4200/CUST|CustComponent|
  |  |localhost:4200/|HomeComponent|
  | unkown |localhost:4200/~ |NotFoundComponent|

2. 뷰의 렌더링 위치 지정
라우트될 뷰의 위치를 지정 하여 RouterOutlet 추가, RouterOutlet은 라우터가 컴포넌트를 렌더링 하여 뷰를 표시할 영역인 router-outlet을 구현한 디렉티브로 컴포엉트의 뷰를 렌더링할 위치를 설정  

{% highlight java linenos%}
<router-outlet></router-outlet>
{%endhighlight%}

3. 네비게이션 작설
- Router Link 디렉티브를 사용하는 방법
{% highlight java linenos%}
 <a routerLink="HOME">HOME</a>
 <a routerLink="CUST">CUST</a>
{%endhighlight%}
RouterLink 디렉티브는 자신의 값을 라우터에게 전달하고 , 라우터는 이를 전달 받아 해당 컴포넌트를 활성화하여 뷰를 렌더링.

-RouterLinkActive를 사용하는 방법
RouterLinkActive는 현제 브라우저의 경로가 RoutrLink 디렉티브에서 지정한 URL 경로의 '트리'에 포함되는 경우 RouterLinkActive 클래스명을 DOM에 자동 추가한다.
즉, router 활성화시 RouterLinkActive에 저의 되어있는 클래스 속성을 DOM엑추가 해주는 디렉티브 

- native 메서드를 이용하는 방법
[component.ts]
<script src="https://gist.github.com/cocomalco/1fdefa93b9ecaf96bbc4479309abb8d3.js"></script>

### 중첩라우터
특정 컴포넌트 안에서 동작하는 라우팅이며 ,자식 라우팅(child routing) 이라고 한다.

중첩라우터  설정  
1. 부모 html에 자식 페이지가 렌더링 될 자리에 router-outlet 태그 추가, 자식 페이지가 렌더링 될수있도록 routerLink 태그 추가
[예시]
{% highlight java linenos%}
<p>HOME TEST</p>
<ul>
  <li>
    <a routerLink="CHILD-A">CHILD-A</a>
  </li>
  <li>
    <a routerLink="CHILD-B">CHILD-B</a>
  </li>
  <li>
    <a routerLink="CHILD-C">CHILD-C</a>
  </li>
</ul>
<router-outlet></router-outlet>
{%endhighlight%}
2.  app-routing-modules.ts 파일에 부모 router 하위에 자식 router를 설정
{% highlight java linenos%}
const routes: Routes = [
  {path:'HOME',component:HomeComponent 
    , children:[
     {path:'CHILD-A',component:ChildAComponent} //자식 라우팅과 연결되는 주소
    ,{path:'CHILD-B',component:ChildBComponent}
    ,{path:'CHILD-C',component:ChildCComponent}]
  }
,{path:'CUST',component:CustComponent}
,{path:'', redirectTo:'/HOME',pathMatch:'full'}
,{path:'**',component:NotFoundComponent}
];
{% highlight java linenos%}
### Router를 통한 파라미터 참조
 1. 파라미터 전달
- 브라우저 URL을 통해 파라미터 전달하는 방법
  - 브라우저 URL 에 파라미타를 추가해 전달  
  URL - http://localhost:4200/CUST?id=test 
- routerLink 를 통해 전달하는 방법  
(routerLink 를 통해 값을 전달 하고자 한다면 , router  생성시 (기본 파일 :app-routing.modules.app) path 설정부분에 파라미터 값취득 설정 필요)
  -  routerLink 에 호출 주소와 파라미터를 넣어 컴포넌트에 전달 , UR은 http://localhost:4200/CUST/test/test_id 이다.
{% highlight java linenos%}
      <a routerLink=“/CUST/test/test_id”>parameterTest</a> 
{% highlight java linenos%}
 
  - component에 생성한 값을 사용하여 파라미터값 사용 하며 실제 사용되는 URL 은 http://localhost:4200/CUST/test/test_id 이다.
{% highlight java linenos%}
    <a routerLink="/CUST/{{user_idx}}/{{menu_temp_idx}}">parameterTest</a>
{%endhighlight%}
  - routerLink의 state를 통해 전달하는 방법
    .ts 파일
{% highlight java linenos%}
    import { Component, OnInit} from '@angular/core';
    import { Router } from '@angular/router';


    @Component({
      selector: 'app-home'
      ,templateUrl: './home.component.html'
      ,styleUrls: ['./home.component.css']
      })

      export class HomeComponent implements OnInit {
        title="CUST_TEST";
        title02="CUST_TEST02";
        user_idx ="test";
        menu_temp_idx ="depth02";
        constructor(private router:Router) {}
        ngOnInit(): void {}
        }
  {%endhighlight%}
    HTML
{% highlight java linenos%}
    <a [title]="title02" [routerLink]="['/CUST',user_idx ,menu_temp_idx]">{{title}}</a>
  {%endhighlight%}
- router.navigateByUrl를 통해 전달하는 방법
{% highlight java linenos%}
    this.router.navigateByUrl('/CUST/{$user_idx}/{$menu_temp_idx}');
  {%endhighlight%}


 2. 파라미터 취득  
 routerLink 영역에 렌더링 된 컴포넌트는 ActivatedRouter 객체를 통해 라우터 상태(router state)에 접근하여, 옵저버블로 취득한다.  
 Activited Route property  
 
    | 프로퍼티 | 설명 |
    |:--------:|:----|
    | URL |라우팅경로를 Observable 타입으로 표현, 이 프로퍼티를 참조하면 라우팅 경로를 구성하는 각 문자열을 배열 형태로 확인 가능|
    |Data|라우팅 규칙에 data 객체가 지정이 되었을떄 이  데이터를 Observable 타입으로 표현, 이 객체에는 라우터 가드에서 처리된 내용 포함|
    |paramMap|라우팅 규칙에 정의된 라우팅 변수를 map 타입의 Observable로 표현, 맵을 사용하면 라우팅 규칙에 포함된 라우팅 인자 전부를 취득 가능| 
    |queryParamMap|라우팅 규칙에서 접근할수있는 모든 쿼리변수를 map 타입의 Observable로 표현 , 맵을 사용하면 라우팅 규칙에 포함된 쿼리 변수전부를 취득 가능
    |fragment|모든 라우팅 규칙에 포함된 URL조각을 Observable 형태로 표현.| 
    |outlet|라우팅 영역으로 사용되는 RouterOutlet을 지정할떄 사용, 라우팅영역에 이름을 지정하지않으면 primary가 기본 이름으로 지정됨.|
    |routeConfig|현재 라우팅된 규칙의 설정을 표현, 이 객체에는  URL 주소에 대한 정보포함.|
    |parent|현재 러우탕 된것이 자식 라우팅 규칙이라면 , 이 라우팅 규칙의 부모 ActivitedRoute를 표현.| 
    |firstChild|현재 라우팅된 규칙의 자식 라우팅 규칙중 첫번쨰 ActivitedRoute를 표현| 
    |children|현재 활성된 라우팅 규칙에 있는 모든 자식 라우팅 규칙을 표현.|

  <script src="https://gist.github.com/cocomalco/19db4b869dd4885962ff76ecf73e8913.js"></script>
  