#### 모던 자바스크립트 Deep Dive와 모던 자바스크립트 핵심 가이드의 내용을 가져온 것입니다!

<br/>

# let / const / var + TDZ + 호이스팅

ES6부터 let과 const가 도입되었다.

const = 상수 = 값을 덮어 쓸 수 없다.

let, var = 변수 = 값 재할당 가능.

var 대신 let을 사용해야 한다.

변수명은 숫자로 시작할 수 없다. 공백, 기호, 마침표가 들어갈 수 없다. 예약어를 사용할 수 없다.

- 스테이크 케이스 ex) last_logged_in
- 캐멀 케이스 ex) lastLoggedIn

# var

var로 선언된 변수는 **함수 스코프에 종속**된다. ( 함수의 코드 블록만을 지역 스코프로 인정한다. )

반면 for 루프(블록 스코프) 내에서 var로 변수를 선언하면 이 변수는 for 루프 밖에서도 사용할 수 있다.

```jsx
for(var i=0; i<10; i++){
	var leak = "I love you";
}
console.log(leak); // I love you

function myFunc(){
	var scoped = "I love you";
	console.log(scoped);
}

myFunc(); // I love you
console.log(scoped); // ReferenceError: scoped is not defined;
```

**블록 스코프를 벗어나도 변수에 접근할 수 있는 반면, 함수 내에 선언된 var 변수는 함수 외부에서 접근할 수 없다.**

### var는 변수를 중복 선언할 수 있다. ( 기존 값이 의도치 않게 변경 되서 부작용 발생 가능! )

```jsx
var x = 1;
var y = 1;
var x = 100;
var y;

console.log(x); // 100
console.log(y); // 1
```

- var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용한다.
- 초기화문이 있는 변수 선언문은 자바스크립트 엔진에 의해서 var 키워드가 없는 것처럼 동작한다.
- 초기화문이 없는 변수 선언문은 무시된다. 에러는 발생하지 않는다.

# let

let(및 const) 키워드로 선언된 변수는 **블록 스코프에 종속**된다.

변수가 선언된 블록과 그 하위 블록 내에서만 사용할 수 있다.

```jsx
let x = "global";

if(x === "global"){
	let x = "block-scoped";
	console.log(x); // block-scoped
}

console.log(x); // global

var y = "global";

if(y === "global"){
	// y는 전역변수이다. 이미 선언된 전역 변수 y가 있으므로 중복 선언된다.
	var y = "block-scoped";
	console.log(y); // block-scoped
}

console.log(y); // block-scpoed
```

블록 스코프 내에서 let으로 선언한 변수에 새 값을 할당했을 때 블록 바깥에서는 그 값이 변경되지 않는다.

var로 선언된 변수는 블록 스코프 외부에서 접근이 가능하므로 블록 바깥에서도 값이 변경된다.

### let은 변수를 중복 선언 할 수 없다!

```jsx
// var 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용한다.
// 아래 var foo = 456; 변수 선언문은 자바스크립트 엔진에 의해 var 키워드가 없는 것처럼 동작한다.
var foo = 123;
var foo = 456;

let bar = 123;
let bar = 456; // SyntaxError: Identifier 'bar' has already been declared
// let이나 const 키워드로 선언된 변수는 같은 스코프 내에서 중복 선언을 허용하지 않는다.
```

### let은 변수 호이스팅이 발생하지 않는 것처럼 동작한다.

```jsx
console.log(foo); // ReferenceError: foo is not defined
let foo;
```

위와 같이 let 키워드로 선언된 변수를 변수 선언문 이전에 참조하면 참조 에러가 발생한다.

var 키워드로 선언한 변수는 런타임 이전에 자바스크립트 엔진에 의해 암묵적으로 “선언 단계"와 “초기화 단계"가 한번에 진행된다. 즉, 선언 단계에서 스코프에 변수 식별자를 등록해 자바스크립트 엔진에 변수의 존재를 알린다. 그리고 즉시 초기화 단계에서 undefined로 변수를 초기화한다. 따라서 변수 선언문 이전에 변수에 접근해도 스코프에 변수가 존재하기 때문에 에러가 발생하지 않는다. 다만 undefined를 반환한다. 이후 변수 할당문에 도달하면 비로소 값이 할당된다.

```jsx
// var 키워드로 선언한 변수는 런타임 이전에 선언 단계와 초기화 단계가 실행된다.
// 따라서 변수 선언문 이전에 변수를 참조할 수 있다.
console.log(foo); // undefined

var foo;
console.log(foo); // undefined

foo = 1; // 할당문에서 할당 단계가 실행된다.
console.log(foo); // 1
```

![Untitled](let%20const%20var%20+%20TDZ%20+%20%E1%84%92%E1%85%A9%E1%84%8B%E1%85%B5%E1%84%89%E1%85%B3%E1%84%90%E1%85%B5%E1%86%BC%20904d97c55971472db9e15f16a11f2565/Untitled.png)

let 키워드로 선언된 변수는 “선언 단계"와 “초기화 단계”가 분리되어 진행된다.

즉, 런타임 이전에 자바스크립트 엔진에 의해 암묵적으로 선언 단계가 먼저 실행되지만(호이스팅) 초기화 단계는 변수 선언문에 도달했을 때 실행된다. 

초기화 단계가 실행되기 전에 변수에 접근하려고 하면 참조 에러가 발생한다.

let 키워드로 선언된 변수는 스코프의 시작 지점부터 초기화 단계 시작 지점(변수 선언문)까지 변수를 참조할 수 없다. 

**스코프의 시작 지점부터 초기화 시작 지점까지 변수를 참조할 수 없는 구간을 일시적 사각지대(temporal dead zone) TDZ라고 부른다.**

```jsx
// 런타임 이전에 선언 단계가 실행된다. 아직 변수가 초기화되지 않았다.
// 초기화 이전의 일시적 사각지대에서는 변수를 참조할 수 없다.
console.log(foo); // ReferenceError: foo is not defined

let foo; // 변수 선언문에서 초기화 단계가 실행된다.
console.log(foo); // undefined

foo = 1; // 할당문에서 할당 단계가 실행된다.
console.log(foo); // 1
```

![Untitled](let%20const%20var%20+%20TDZ%20+%20%E1%84%92%E1%85%A9%E1%84%8B%E1%85%B5%E1%84%89%E1%85%B3%E1%84%90%E1%85%B5%E1%86%BC%20904d97c55971472db9e15f16a11f2565/Untitled%201.png)

### let 변수는 호이스팅이 발생하지 않는 것처럼 보이는 것이지 호이스팅이 발생한다!

```jsx
let foo = 1; // 전역 변수
{
	console.log(foo); // ReferenceError: Cannot access 'foo' before initialization
	let foo = 2; // 지역 변수
}
```

let 키워드로 선언한 변수의 경우 변수 호이스팅이 발생하지 않는다면 위 예제는 전역 변수 foo의 값을 출력해야 한다. 하지만 let 키워드로 선언한 변수도 여전히 호이스팅이 발생하기 때문에 참조 에러가 발생한다!!

### 전역 객체와 let

- var 키워드로 선언한 전역 변수와 전역 함수, 그리고 선언하지 않은 변수에 값을 할당한 암묵적 전역은 전역 객체 window의 프로퍼티가 된다. 전역 객체의 프로퍼티를 참조할 때 window를 생략할 수 있다.

```jsx
// 브라우저 환경에서 실행해야 한다!!!!!

// 전역 변수
var x = 1;
// 암묵적 전역
y = 2;
// 전역 함수
function foo(){}

// var 키워드로 선언한 전역 변수는 전역 객체 window의 프로퍼티이다.
console.log(window.x); // 1
// 전역 객체 window의 프로퍼티는 전역 변수처럼 사용할 수 있다.
console.log(x); // 1

// 암묵적 전역은 전역 객체 window의 프로퍼티다.
console.log(window.y); // 2
console.log(y); // 2

// 함수 선언문으로 정의한 전역 함수는 전역 객체 window의 프로퍼티다.
console.log(window.foo); // foo() {}
// 전역 객체 window의 프로퍼티는 전역 변수처럼 사용할 수 있다.
console.log(foo); // foo() {}

let hi = 1;
// let, const 키워드로 선언한 전역 변수는 전역 객체 window의 프로퍼티가 아니다.
console.log(window.hi); // undefined
console.log(hi); // 1
```

- let 키워드로 선언한 전역 변수는 전역 객체의 프로퍼티가 아니다. 즉, window.foo와 같이 접근할 수 없다.
- let 전역 변수는 보이지 않는 개념적인 블록(전역 렉시컬 환경의 선언적 환경 레코드) 내에 존재하게 된다.
    
    (실행 컨텍스트에 대해 공부하면 이해하면 알 수 있다.)
    

# const

let과 마찬가지로 const로 선언된 변수도 블록 스코프에 종속된다.

const 키워드로 선언한 변수에 원시 값을 할당한 경우 변수 값을 변경할 수 없다. 원시 값은 변경 불가능한 값이므로 재할당 없이 값을 변경할 수 있는 방법이 없기 때문이다.

변수의 상대 개념인 상수는 재할당이 금지된 변수를 말한다. 상수도 값을 저장하기 위한 메모리 공간이 필요하므로 변수라고 할 수 있다. 단 변수는 언제든지 재할당을 통해 값을 변경할 수 있지만, 상수는 재할당이 금지된다.

**재할당을 통해 값을 변경할 수 없다. → const로 선언된 변수가 불변이라는 의미는 아니다!!!!**

→ 새로운 값을 재할당하는 것은 불가능하지만 프로퍼티 동적 생성, 삭제, 프로퍼티 값의 변경을 통해서 객체를 변경하는 것은 가능하다. 이때 객체가 변경되더라도 변수에 할당된 참조 값은 변경되지 않는다.

```jsx
const constant = "I am a constant";
constant = "I can't be reassigned";
// Uncaught TypeError: Assignment to constant variable
```

### const에 객체가 담겼다면???

```jsx
const person = {
	name: 'BTS',
	age: 10,
};

person.age = 25;
console.log(person.age); // 25
```

위의 예시는 변수 전체를 재할당하는 것이 아니라 그 속성 중 하나만 재할당하는 것이므로, 문제가 없다.

+) Object.freeze()를 통해서 객체의 내용을 변경할 수 없게 설정할 수는 있지만, 값을 변경하려고 시도할 때 자바스크립트는 오류를 던지지 않는다.

### const 키워드로 선언한 변수는 반드시 선언과 동시에 초기화해야 한다!!!

그렇지 않으면 문법 에러가 발생한다.

```jsx
const foo; // SyntaxError: Missing initializer in const declaration
```

# TDZ

```jsx
console.log(i); // undefined
var i = "I am a variable";

console.log(j); 
// ReferenceError: can't access lexical declaration 'j' before initialization
let j = "I am a let";
```

var는 정의되기 전에 접근할 수 있지만, 그 값에는 접근할 수 없다.

let과 const는 정의하기 전에 접근할 수 없다.

var, let, const 모두 다른 소스에서 읽을 수 있는 내용임에도 불구하고 **호이스팅**의 대상이 된다.

코드가 실행되기 전에 처리되고 해당 스코프(글로벌 이든 블록이든) 상단으로 올라간다.

var가 가지는 가장 큰 차이점은 정의되기 전에도 접근할 수 있다는 점에 있다.

= 즉, 정의되기 전에 undefined 값을 가지게 된다.

let은 변수가 선언될 때까지 일시적으로 비활성 구역, 즉 TDZ에 있게 된다. 따라서 초기화 전에 변수에 접근하면 오류가 발생한다. undefined 값을 얻는 것보다는 오류가 발생하는 편이 코드 디버깅이 더 쉽다.

# 변수 호이스팅

```jsx
console.log(score); // undefined

var score; // 변수 선언문
```

자바스크립트 코드는 인터프리터에 의해 한 줄씩 순차적으로 실행되므로 console.log(score); 가 가장 먼저 실행되고 순차적으로 다음 줄에 있는 코드를 실행한다.

console.log(score);가 실행되는 시점에는 아직 score 변수의 선언이 실행되지 않았으므로 참조 에러가 발생할 것처럼 보이지만 실제로는 에러가 발생하지 않고 undefined가 출력된다!!!!!!!

그 이유는 변수 선언이 소스코드가 한 줄씩 순차적으로 실행되는 시점, 즉 런타임이 아니라 그 이전 단계에서 먼저 실행되기 때문이다.

자바스크립트 엔진은 소스코드를 한 줄씩 순차적으로 실행하기에 앞서 먼저 소스코드의 평가 과정을 거치면서 소스코드를 실행하기 위한 준비를 한다. 이때 소스코드 실행을 위한 준비 단계인 소스코드의 평가 과정에서 자바스크립트 엔진은 변수 선언을 포함한 모든 선언문(변수 선언문, 함수 선언문 등)을 소스코드에서 찾아내 먼저 실행한다.

그리고 소스코드의 평가 과정이 끝나면 비로소 변수 선언을 포함한 모든 선언문을 제외하고 소스코드를 한 줄씩 순차적으로 실행한다.

즉, 자바스크립트 엔진은 변수 선언이 소스코드의 어디에 있든 상관없이 다른 코드보다 먼저 실행한다. 따라서 변수 선언이 소스코드의 어디에 위치하는지와 상관없이 어디서든지 변수를 참조할 수 있다.

만약, 코드가 순차적으로 실행되는 런타임에 변수 선언이 실행된다면 console.log(socre);가 실행되는 시점에는 아직 변수가 선언되지 이전이므로 위 코드를 실행하면 참조 에러가 발생해야 한다. 하지만 undefined가 출력된다.

이는 변수 선언(선언과 초기화 단계)이 소스코드가 순차적으로 실행되는 런타임 이전 단계에서 먼저 실행된다는 증거이다!!!!

**이처럼 변수 선언문이 코드의 선두로 끌어 올려진 것처럼 동작하는 자바스크립트 고유의 특징을 변수 호이스팅이라한다.** 

사실 변수 선언뿐 아니라 var, let, const, function, function*, class 키워드를 사용해서 선언하는 모든 식별자(변수, 함수, 클래스 등)는 호이스팅된다. 모든 선언문은 런타임 이전 단계에서 먼저 실행되기 때문이다.

+) let, const, class를 사용한 선언문은 호이스팅이 발생하지 않는 것처럼 동작한다.

# 어떤걸 사용하는 것이 더 좋을까???

기본적으로 const를 사용한다. 

→ 의도치 않은 재할당을 방지할 수 있다.

변경이 발생하지 않고 읽기 전용으로 사용하는 원시 값과 객체에는 const 키워드를 사용한다. const 키워드는 재할당을 금지하므로 var, let 키워드보다 안전하다.

재할당이 필요한 경우에 한정해 let을 사용한다.
