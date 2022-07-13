---
title:  "ANGULAR COMPONENT"
excerpt: "angular component의 개념 및 시용"

categories:
  - Angular
tags:
  - [Angular, Component]

toc: true
toc_sticky: true
 
date: 2022-06-29
last_modified_at: 2022-06-29


---

### 개념  
화면과 관련된 데이터의 변화 이벤트발생 등의 일을 수행 

### component 생성
ng generate component <컴포넌트 이름>
(ng g component <컴포넌트 이름>)

접근제어자  
private : 해당 클래스 에서만 사용 가능  
protected : 해당 클래스와 직접 관계된곳만 사용  
public : 어디서든 사용가능  
앵귤러에서는 클래스의 접근제어 기본 값이 protected 이다.  

1. 표현식(양방향 데이터 바인딩)  
표현식 기호 는 대괄호 2개( {{}} )를 사용하고 있다.  
컴포넌트 파일(.ts) 에서 생성한 변수를 표현식에 넣어 사용할수있다.(private 제외)  
2. click  
클릭이벤트는 (click)으로 사용 하며 , 동작할 함수를 명시 해준다.  
3. 구조지시자 (디렉티브)  
컴포넌트에 존재하는 데이터를 html 파일에서 세부적으로 동작
태그 안에 명시하며, *기호 와 대입연산자를 통해 동작할 명령어 입력 한다 (ex *ngFor , *ngIf)

### 모듈 구성방식
모듈은 애플리케이션을 효율적으로 구성하기 위해 마련된 체계이며 , 외부 라이브러리를 효율적으로 사용하기 위한 방법이다.  
NgModule은 컴포넌트와 디렉티브 , 파이프등 기능이 연관된 구성요소를 하나로 묶어 관리하는 단위이며, 기능측면이나 업무흐름 , 공통유틸이 담당하는 부분에만 집중하고록 구성한다.

NgModule의 메타데이터  
- 해당 모듈에 속한 컴포넌트, 디렉티브, 파이프 정의
- 모듈에 속한 컴포넌트, 디렉티브, 파이프 중 모듈 외부로 공개할 요소를 지정, 다른 모듈의 컴포넌트 템플릿에서 이 구성요소를 사용할수 있도록 함.
- 해당 모듈에 필요한 다른 모듈의 컴포넌트, 디렉티브, 파이프를 로드.
- 컴포넌트에 사용할 서비스 프로바이더를 등록.  

### 데이터 바인딩
1. ngModule 디렉티브 사용
ngModule 은 외부 라이브러리 개념의 디렉토리 이기때문에 설정을 필요로 한다.  
app.Modules.ts 에 FormModules 와  ReactiveFormsModule 를 import 에 추가 해준다.
<script src="https://gist.github.com/cocomalco/54883e37ac51f7231f93e1f5fe1ebf2b.js"></script>
사용하고자 하는 곳에 '[(ngModule)]=<아이디값>'을 선언해준다
{% highlight java linenos%}
  <input type="text"  [(ngModel)]="client_ani">
{%endhighlight%}

component에 변수 선언
{% highlight java linenos%}
export class HomeComponent implements OnInit {
  public client_ani: string;

  constructor() {
    this.client_ani = '';

  }
  ngOnInit(): void {
    console.log("client ani : ",this.client_ani);
  }
}
  {%endhighlight%}



##상위 컴포넌트와 하위 컴포넌트간의 데이터 전달  
@INPUT 데코레이터는 '받는' 역활을한다.  
보내고자 하는 부분에 [하위컴포넌트 변수] = '보낼값' 으로 전달 해주며 , 하의 컨포넌트는 input 데코레이터를 통해 값을 받아 사용 한다.
 
 예시

 [상위 컴포넌트 HTML 파일]
 {% highlight java linenos%}
    <app-login [longinPop]='true'></app-login>
  {%endhighlight%}

   [하위 컴포넌트 ts 파일]
 {% highlight java linenos%}
    @Input() longinPop :boolean = false;
  {%endhighlight%}

@OUTPUT 데코레이터는 '주는' 역활을 한다.
보내고자 하는 부분에 EventEmitter 를 통해서 이벤트나 값을 전달 하며 ,  (sendEvent) 을 이용하여 OUTPUT 데코레이터 값을 받는다.

예시 
상황 : 하위 컴포넌트에서 상위 컴포넌트로 데이터 전달.
EventEmitter import , OUTPUT 뎈토레이터 선언 , 이벤트 emit
[하위 컴포넌트 ts 파일]
<script src="https://gist.github.com/cocomalco/7f40726640cdbf187b5c6903826f052d.js"></script>

[상위 컴포넌트 ts 파일]

{% highlight java linenos%}
  <app-login (sendEvent)="getEvent($event)"></app-login>
{%endhighlight%}

데이터 바인딩 심화  
여러 데이터 전달 및 받기  
[보내는 데이터 선언]  
{% highlight java linenos%}
  data = {'login':false, 'popClose':false};
  this.sendEvent.emit(this.data);
{%endhighlight%}


[데이터 받는 부분]  
{% highlight java linenos%}
  getEvent(event :any){
    console.log("get event popClose :"+event.popClose);
    console.log("get event login :"+event.login);
    }
{%endhighlight%}


