---
title: YOU DON'T KNOW JS - 타입과 문법, 스코프와 클로저 (카일 심슨) &#35;24
author: PajaritoMoyqi
date: 2020-11-27 10:51:22 +0900
categories: [Review, Javascript]
tags: [javascript, basic]
---

3-4 달 전에 봤을 때는 진짜 너무 어려워서 잠시 접어두었다가, 최근에 하는 스터디 모임에서 자바스크립트를 기초부터 공부하게 돼서 다시 꺼내서 참고하면서 보았다. 다행히 그동한 깜냥이 쌓였는지 저번보다는 볼만했다.

자바스크립트가 수박이라고 하면 수박을 허연 부분까지 박박 긁어 먹으려고 노력하는 책이다. '노력한다'? 그렇다면 그리 깊지 않은 책인가? 그건 아니다. 종종 저자가 '책의 지면상 여기서는 생략하고 더 궁금하다면 명세를 살펴보라'고 이야기하는데 그제서야 '아 이 책이 자바스크립트 엔진의 모든 것을 다루는 게 아니구나'할 정도로 깊이가 깊다. 매쪽 정신을 차리지 않으면 이해가 안 가서 다시 그 절을 읽고 있는 나 자신을 발견할 수 있다.

시중에 보면 간혹 자바스크립트의 정수를 다루고 있는 책들을 볼 수 있다. 그런 책들 중 일부는 초보자가 원리부터 이해할 수 있는 책이고 일부는 숙련자만이 그 내용을 자기 것으로 만들 수 있는 책이다. 이 책은 후자에 가깝다. 두 번째 도전만에 성공했지만, 여전히 이해가 가지 않는 부분들이 남아 있다. 몇 달 뒤에 다시 봐야 이해가 되지 싶다.

그러니 부디 초보자가 공부하기 위해 이 책을 보거나 당장의 문제를 해결하기 위해서 이 책을 보지는 않았으면 좋겠다. 이 책을 보다보면 내가 자바스크립트로 학문을 한다는 느낌을 받는다. 이런 어거지 에러를 볼 일이 있을까? 하는 예시들이 많이 나온다. 반대로 이런 고급진 스킬로 코드를 짜면 내 코드를 다음 사람이(혹은 협업자가) 이해할 수 있을까 하는 생각을 불러일으키는 코드도 많이 나온다. 하지만 코딩을 하다보면 나도 모르게 이런 짓을 할 수도 있고 프로젝트가 커지면 어떤 일이 벌어질지 모르다보니 평소 나 자신의 내공을 쌓기 위해서 공부하면 좋은 책이라는 생각이 든다. 그런 의미에서 책의 내용을 다시 훑어보고 정리하면서 글을 마무리하려고 한다. 처음에는 글만 보고 이해가 되도록 요약하려고 했는데 그러다보니 책을 한 권 쓰겠더라. 그래서 보고 찾아볼 수 있도록 볼만한 키워드들을 정리하는 느낌으로 정리했다.

## (1) 타입과 문법

### 1) 타입

####  1. typeof

  ``` javascript
  typeof function a() {}
  ```

####  1. 선언하지 않은 변수는 typeof가 undefined

  ``` javascript
  (typeof someVar === undefined)
  (typeof someVar !== undefined)
  ```

<br>

### 2) 값

####  1. array length

  ``` javascript
  arr["foobar"] = 2; // possible but no length added.
  ```

####  1. array 슬롯 건너뛰기

  - length 적용, 가운데 값 undefined.

####  1. arr["13"] => arr[13]

####  2. number가 유일한 Number type

####  2. 부동소수점과 머신입실론

  ``` javascript
  0.1+0.2 === 0.3 // false
  ```

  Number.EPSILON, Number.MIN_VALUE, Number.MAX_VALUE, Number.MAX_SAFE_INTEGER, Number.MIN_SAFE_INTEGER, Math.pow(-2, 31), Math.pow(2, 31)-1

####  3. void __ ; 모든 값을 무효화하여 undefined화.

####  3. isNaN()

####  3. -0과 0

  변수 값의 이동 방향(0이 되었을 때 잠재적으로 소실될 수 있는 정보)을 보존하기 위한 장치.

####  3. Object.is()

####  4. 값 복사 / 레퍼런스 복사

  전적으로 값의 타입으로 결정된다. 이를 바꾸고 싶다면

  ``` javascript
  a.slice() // for ref type
  wrapper.a // for val type
  ```

<br>

### 3) 네이티브

####  1. 원시값에 프로퍼티나 메서드를 쓰면 자바스크립트가 알아서 래퍼 객체로 박싱하고 프로퍼티나 메서드를 호출한다.

####  2. 구멍난 배열

  ``` javascript
  new Array(3) // [undefined x 3]
  ```

####  3. 리터럴 형식이 있지만 유용한 네이티브 -> new RegExp() // 동적으로 정의할 때

####  3. Error()와 Array()는 앞에 new가 있든 없든 같은 결과를 만들어낸다.

####  3. Symbol()은 유일하게 앞에 new가 오면 에러가 나는 네이티브다. 주로 ES6의 특수한 내장 로직에 쓰기 위해 고안되었다. 전용/특수/내부 프로퍼티라는 것을 알리기 위해 써왔던 언더스코어(_)가 Symbol에 의해 대체될 가능성이 있다.

####  4. 문서화 관례에 따르면 String.prototype.XYZ는 String#XYZ로 줄여서 쓴다.

<br>

### 4) 강제변환

####  1. ToString

  객체를 변환하는 경우 toString()을 통해 내부 [[Class]]를 반환한다.

####  1. JSON 문자열의 경우 toJSON()이 '문자열화하기 적당한 JSON 안전 값으로 바꾸고' JSON.stringify()가 문자열화 처리를 한다.

####  1. ToNumber

  객체를 변환하는 경우 valueOf(), valueOf()가 구현되어 있지 않으면 toString()을 사용한다.

####  1. ToBoolean

  falsy 값 : 불리언 값으로 강제변환하면 false를 return하는 값들

  명세가 정의한 falsy 값 : undefined, null, false, +0, -0, NaN, "", 0n

  falsy 값 이외의 값이 전부 truthy 값.

####  1. To Primitive

####  2. ~ (틸드)

  기본적으로는 2의 보수(complement)를 구하는 연산이다.

  연산을 할 경우 입력 값이 -1이면 falsy한 0을 return하고 나머지의 경우 truthy한 값이 산출되는 것이다.

  -1은 흔히 경계 값이라고 일컬어진다(e.g. indexOf의 산출값). 그럴 때 유용하게 쓰일 수 있다.

  혹은 연산자 우선순위를 가진채로 ToInt32 강제변환을 하고 싶을 때 쓰인다.

  ``` javascript
  if(~a.indexOf('letter'){})
  if(!~a.indexOf('letter'){})
  ```

  ``` javascript
  ~~1E20 / 10
  1E20 | 0 / 10
  (1E20 | 0) / 10
  ```

####  3. Boolean type으로의 암시변환이 일어나는 경우

  if()문의 조건 표현식

  for( ; ; )에서 두 번째 조건 표현식

  while() 및 do ... while() 루프의 조건 표현식

  ? : 삼항 연산 시 첫 번째 조건 표현식

  &#124;&#124; 및 && 의 좌측 피연산자

####  3. 이 중 &#124;&#124; 와 &&는 결과값으로 피연산자들 중 하나를 return한다는 것을 알아야 한다.

  둘 중 연산에 결정적인 역할을 한 값을 return한다.

  이 특성은 가드 연산자에도 쓰인다. 다음 코드를 보자.

  ``` javascript
  function foo(){
    console.log(a);
  }
  const a = 42;
  a && foo();
  ```

  코드의 마지막 연산에서 a가 truthy 값인 경우 결정적인 역할을 한 것은 foo()이다(둘 다 true이므로). 그러므로 a를 console.log한다.

  반면 a가 falsy인 경우 더 연산이 필요 없기 때문에 a만 return하는데 이러면 foo()는 조용히 실행되지 않는다.

####  4. symbol 값은 문자열로 강제변환은 되며 암시변환은 안 된다. 숫자는 그냥 다 안 된다. 불리언 값으로는 다 되고 항상 true다. 근데 이걸 언제?

####  5. ==과 ===의 정확한 차이는 동등함 비교 시 강제변환을 허용하느냐 아니냐의 차이다.

  그리고 ===가 ==보다 몇 마이크로초 정도 차이가 난다.

  == 비교시 String, Number, Boolean 사이에서는 Number로 변환이 일어나 비교를 한다. // ToNumber()

####  5. 변덕스러워 '보이는' == 변환의 복잡한 이면을 알고 싶지 않다면 다음 두 가지 원칙만 지키면 된다.

  피연산자 중 하나가 true/false일 가능성이 있으면 절대로 == 연산자를 쓰지 말자.

  피연산자 중 하나가 [], "", 0이 될 가능성이 있으면 가급적 == 연산자를 쓰지 말자.

####  6. <와 >의 연산의 비교에 있어서 어느 한쪽이라도 문자열이 아니면 ToNumber 강제변환이 일어나서 숫자값으로 만들어 비교한다.

  하지만 양쪽 다 문자열이면 각 문자를 단순 어휘(알파벳 순서)로 비교한다.

<br>

### 5) 문법

####  1. 문의 완료값

  var 문 자체의 완료값은 undefined다.

  { } 블록의 완료값은 내부 마지막 문/표현식의 완료 값이다.

  문의 완료 값을 포착해서 변수에 할당할 수 있을까?

  ``` javascript
  var a, b;
  a = eval("if(true){b=4+38}");
  a; // 42
  ```

  ES7에는 절대 사용하지 않아야 할 eval()을 대신해 이런 것이 제안되었다.

  ``` javascript
  var a, b;
  a = do {
    if(true){
      b = 4 + 38;
    }
  };
  a; //42
  ```

####  1. 표현식

  ``` javascript
  var a = 42;
  var b = a++;
  a; // 43
  b; // 42
  ```

  delete 연산자의 결과값은 유효한/허용된 연산인 경우 true 아닌 경우 false다.

####  1. 위의 문과 표현식을 잘 이용하면 if문을 줄일 수 있다.

  ``` javascript
  function vowels(str){
    var matches;
    if(str && (matches = str.match(/[aeiou]/g))){
      return matches;
    }
  }
  ```

####  2. 레이블문

  코드 블록에 이름을 붙여 그 블록을 break로 빠져나갈 수 있다.

  ``` javascript
  foo: for (var i=0; i<4; i++){
    for (var j=0; j<4> j++;){
      if((i*j)>=3){
        console.log('stop!', i, j);
        break foo;
      }
      console.log(i, j);
    }
  }

  function a(){
    b: {
      console.log('hi');
      break b;
      console.log('절대 실행 안 됨');
    }
    console.log('world');
  }
  ```

####  2. ES6부터는 분해 할당 시 { }를 사용한다.

  ``` javascript
  function getData(){
    return {
      a: 42,
      b: "foo"
    }
  }
  var {a, b} = getData();
  ```

####  2. else if는 없다.

  ``` javascript
  if(a){

  }else if(b){
    
  }else{

  }
  ```

  위의 구문은 아래와 같이 파싱된다.

  ``` javascript
  if(a){

  }
  else{
    if(b){

    }
    else{

    }
  }
  ```

####  3. 연산자 우선순위

  &&, &#124;&#124;, ? : 순으로 논리 연산이 이루어진다.

####  3. 결합

  &&와 &#124;&#124;는 좌측 결합 연산자다.

  ? : 와 = 는 우측 결합 연산자다

####  4. 세미콜론

  자바스크립트 엔진은 단 하나의 ;라도 누락되면 프로그램을 돌리지 않는다.

  하지만 ASI(자동 세미콜론 삽입)이 새 줄(line break) 단위로 파싱을 하다가 에러가 나면 ;를 넣어보고 타당한 것 같으면 ;를 삽입하는 식으로 이런 에러를 방지해준다.

####  5. try ... finally

  try 문에 return 값이 있으면 finally 문이 실행된 다음에야 return 값이 반환된다.

  그런데 finally에도 return 값이 있으면 finally에 있는 return 값만 반환된다.

  finally 문에서 의도치 않은 에러가 발생하면 그 전 try 문은 다 무시된다.

<br>

## (2) 스코프와 클로저

  1) 스코프란 무엇인가

####  1. 컴파일러 이론

  토크나이징/렉싱(문자열을 나누어 토큰이라는 의미 있는 조각으로 나누는 과정) - 파싱(문법 구조를 반영하여 트리 형태로 바꾸는 과정) - 코드 생성(실행코드로 바꿈)

  자바스크립트 엔진이 기존 컴파일러와 다른 점은 자바스크립트 컴파일레이션을 미리 수행하지 않아서 최적화할 시간이 많지 않다.

  엔진 : 컴파일레이션의 시작부터 끝까지 전 과정과 자바스크립트 프로그램 실행을 책임진다.

  컴파일러 : 엔진의 친구로 파싱과 코드 생성의 모든 잡일을 도맡아 한다.

  스코프 : 엔진의 또 다른 친구로 선언된 모든 변수 검색 목록을 작성하고 유지한다. 엄격한 규칙을 강제해 현재 실행 코드에서 변수 적용 방식을 결정한다.

  LHS : 값을 넣기 위해 변수 컨테이너 자체를 찾는다. 대입할 대상, RHS : 특정 변수의 값을 찾는 것과 다름이 없다. 대입한 값.

  b에 대한 RHS 검색이 실패하면 b를 찾을 수 없다. 이렇게 스코프에서 찾지 못한 변수는 선언되지 않은 변수라고 한다. 이 경우 엔진은 'ReferenceError'를 발생시킨다. 반면 엔진이 LHS 검색을 하다 최상위 층에 도착해서도 실패하면 프로그램이 Strict Mode가 아니라면 글로벌 스코프는 엔진이 검색하는 이름을 가진 새로운 변수를 생성해서 엔진에게 넘겨준다. 또한 RHS 검색에 성공했으나 그 값으로 불가능한 일을 하려고 하면 TypeError가 발생한다.

####  2. 렉시컬 스코프

  렉시컬 스코프란 렉싱 타임(렉싱 처리 과정은 소스 코드 문자열을 분석해 상태 유지 파싱의 결과로 생성된 토큰에 의미를 부여한다)에 정의되는 스코프다. 바꿔 말하면 렉시컬 스코프는 개발자가 코드를 짤 때 변수와 스코프 블록을 어디서 작성하는가에 기초해서 렉서가 코드를 처리할 때 확장된다.

  렉시컬 스코프는 함수가 선언된 위치에 따라서 정의된다.

  - 렉시컬 속이기

  eval() 함수는 문자열을 인자로 받아 실행 시점에 문자열의 내용을 코드의 일부분처럼 처리한다.

  ``` javascript
  function foo(str, a){
    eval(str);
    console.log(a, b);
  }
  var b = 2;
  foo("var b = 3;", 1); // 1, 3
  // strict mode에서 실행하면 eval은 자체적인 렉시컬 스코프를 이용한다.
  ```

  with문도 렉시컬 스코프를 속일 수 있는 방법 중 하나다.

####  3. 스코프 안에 숨기는 것의 이점

  - 노출 최소화

  - 충돌 회피

####  3. 스코프 역할을 하는 함수 / 즉시 실행 함수

  ``` javascript
  var a = 2;

  (function IIFE(){
    var a = 3;
    console.log(a);
  })();

  console.log(a);
  ```

  이렇게 적으면 IIFE라는 이름으로 전역 스코프를 오염시킬 일도 없고 좋다.

####  3. 익명 vs 기명

  ``` javascript
  setTimeout(function timeoutHandler(){
    console.log( 'I wanted 1 sec ');
  }, 1000)
  ```

  기명으로 쓰는 것의 장점

  - 스택 추적시 표시할 이름이 생겨 디버깅이 쉬워진다.

  - 이름 없이 함수 스스로 재귀 호출을 하려면 폐기 예쩡인 arguments.callee 참조가 필요하다.

  - 코드 이해도를 높인다.

####  3. 자바스크립트에서 블록 스코프 사용하기.

  - with

  - try/catch에서 catch 블록

  - let

  - const

####  3. 가비지컬렉션

  ``` javascript
  function process(data){
    // do something
  }

  //anything declared inside this block can go away after.
  {
    let someReallyBigData = { ... };

    process(someReallyBigData);
  }

  var btn = document.getElementById('my_button');

  btn.addEventListener('click', function click(evt){
    console.log('button clicked');
  }, false);
  ```

  click함수가 해당 스코프 전체의 클로저를 가지고 있으므로 someReallyBigData가 전역에 있었으면 가비지 컬렉션의 대상이 될 수 없지만, 여기서는 블록 처리를 함으로써 성능을 향상시켰다.

####  4. 호이스팅

  호이스팅 과정에서 함수가 먼저 끌어올려지고 그 다음에 변수가 끌어올려진다.

  함수 선언문은 끌어올려지지만, 함수 표현식은 var foo; 부분만 끌어올려진다.

  함수 표현식이 이름을 가져도 그 이름 확인자는 해당 스코프에서 찾을 수 없다.

####  5. 클로저

  예시1

  ``` javascript
  var fn;
  
  function foo(){
    var a = 2;
    function baz(){
      console.log(a);
    }
    fn = baz;
  }

  function bar(){
    fn();
  }

  foo();

  bar(); //2
  ```

  예시2

  ``` javascript
  for(var i=1; i<=5; i++){
    (function(j){ // var j = i의 역할을 하면서 1000ms 동안 i가 가비지 컬렉션으로 사라지지 않도록 한다.
      setTimeout(function timer(){
        console.log(j);
      }, 1000)
    })(i);
  }
  ```

  물론 예시2는 간단하게 let 키워드를 사용하면 해결이 가능하다.