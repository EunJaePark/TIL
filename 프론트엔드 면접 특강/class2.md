##### 🗓 2020. 10. 20(화)

### # (10.19일 수업) 실행 컨텍스트 복습
#### console.log에 어떻게 찍힐지 예상해보자.
1.
```javascript
// 표현형 - 즉시 실행
function () {} 

// 선언형 - a()로 실행해줘야 실행됨.
var a = function() {} 
```
<br/>

2.
```javascript
var a = 10; 
  
(function () { 
  var b = 20; 
})();

console.log(a) // 10
consoe.log(b) // undefined
```

<br/>

3.
```javascript
console.log(x); // function x() {} 
var x = 10; 
console.log(x); // 10 
x = 20; 
function x() {}  // 선언형 함수이기 때문에 끌어올려지는 것이다(호이스팅). 따라서 처음 호출한 콘솔에서 불러진다.
console.log(x); // 20
```
<br/>

4.
```javascript
if  (true)  {  
	var a =  1;  
}  else  {  
	var b =  2;  
} 
console.log(a);  // 1 
console.log(b);  // undefined

// 이미 a와 b는 선언되어있다. if문과 상관없이!
// 따라서 console.log로 찍어보았을 때 a는 당연히 값이 나오고, b역시 메모리 주소는 저장되어있기 때문에 undefined라고 나오는 것이다.
```
<br/>

####  Q1. 아래를 보고 콜스택 층을 예상해보자.
```javascript
var a = 10; 
  
function test(x) { 
  var b = 20; 
};
  
test(30);

console.log(b); // 얘는 아무리 찾아도 notdefine이다. test()함수는 실행되고 나면 스코프에서 사라지기 때문에 test()함수 속에서 선언된 b는 해당 함수 바깥에서는 찾을 수가 없는 것이다.

callStack = {
    1 : { // test()함수를 실행하기 위한 준비물 데이터들
        AO : {}, // 내용을 적어보세요
        Scope : [], // 내용을 적어보세요
        this: ''
    },
    0 : { // 모든 함수에서 사용하기 위한 글로벌(전역)의 준비물 데이터들
        VO : {}, // 내용을 적어보세요
        Scope : [], // 내용을 적어보세요
        this: callStack.0.VO 
    }
}
```
  - A1.
```javascript
callStack = {
    1 : { // test()함수를 실행하기 위한 준비물 데이터들
        AO : {
	        x: 30,
	        b: 20,
        }, // 내용을 적어보세요
        Scope : [AO, VO], // 1의 AO와 0의 VO.
        this: ''
    },
    0 : { // 모든 함수에서 사용하기 위한 글로벌(전역)의 준비물 데이터들
        VO : {
	        // *** 1단계 ***
	        // a: , // a에 10이 들어오기 전 a의 이름만 먼저 메모리되어있던 것임.
	        // test: function test(x) { 
		    //     var b = 20;
	        // }
	        // *** 2단계 ***
	        a: 10, 
	        test: function test(x) { 
		        var b = 20;
	        }
		}, // 내용을 적어보세요
        Scope : [VO], // 0의 VO
        // scope는 이 함수가 가지고 있는 건 얘야 라고 알려준다고 생각하면 편하다.
        this: callStack.0.VO 
    }
```

<br/>

#### Q2. 아래 코드를 보고 콜스택을 예상해보자.
```javascript
function test(a, b) { 
  var c = 10; 
  function d() {} 
  var e = function _e() {}; 
  (function x() {}); 
}
   
test(10); // call
```
  - A2.
```javascript
// 진입(준비단계)
callStack = {
    1 : { // test() 용
        AO : {
	        // *** 1. 준비단계 ***
	        a: undefined,
	        b: undefined,
	        c: undefined,
	        d: function() {}, // 선언형이기 때문에 준비단계에서도 이미 함수가 준비되어 있는 것.
	        e: undefined, // 표현형. 따라서 준비단계에서는 아직 할당되지 않았기 때문에 undefined인 것이다.			
	        // x는 생기지 않는다. 그냥 실행만 될뿐, 메모리되지 않는다.(메모리주소 할당x) 이런 함수는 주로 굳이 메모리주소를 할당할 필요가 없는 일회성으로 실행할 함수일 때 사용하면 된다.
	              	        
        }, // 내용을 적어보세요
        Scope : [AO, VO], 
        this: ''
    },
    0 : {
        VO : {
	        test: function () {...},
        },
        Scope : [VO], 
        this: callStack.0.VO 
    }
}

// 실행단계
callStack = {
    1 : {
        AO : {
	        // *** 2. test(10) 실행단계 ***
	        a: 10,
	        b: undefined,
	        c: 10,
	        d: function() {},
	        e: function _e() {},
        }, // 내용을 적어보세요
        Scope : [], 
        this: ''
    },
    0 : { // 위의 준비 단계와 동일.
        VO : {},
        Scope : [], 
        this: callStack.0.VO 
    }
}
```

<br/>

### # arguments = 파라미터
```javascript
functin test(a,b) {
	console.log(arguments[0], arguments[1]);
	// test(a,b)함수에 a,b가 인자로 들어왔기 때문에 arguments가 자동으로 생성된다.
	// a를 찾으려면 arguments[0], b를 찾으려면 arguments[1] 객체에 접근하면 된다.
	// 진입될 때는 arguments가 없다가 함수가 실행되면 arguments가 딱 준비되는 것이다.
}

test(10);
// 10이라는 인자를 하나만 줘서 test()함수를 실행시키면 
// arguments[0]은 10, arguments[1]은 undefined가 나온다.
```

<br/>

### # closure(클로져)
- 함수의 층 간에 연결된 통로를 `스코프체인`, 이렇게 연결 된 상태를 용도에 맞게 더 적극적, 공격적으로 사용하는 것을 `클로저`라고 한다. 즉, 클로저는 지워지지 않는 공간이 생긴 것을 뜻한다.
```javascript
var  data  =  [];

// data[0] = function() { console.log(k) }
// data[1] = function() { console.log(k) }
// data[2] = function() { console.log(k) }

for (var  k  =  0; k  <  3; k++) {
	data[k] =  function() { // 선언형 함수.
		console.log(k);
	}
}

data[0]();  // 3
data[1]();  // 3
data[2]();  // 3

// [0],[1],[2]모두 console에 3이 찍힘. 왜?

// 스코프로 생각하면 된다. 스코프가 0단계 VO에서는 'k'가 3까지 저장되어 있다. 
// for문에서 3미만일 때까지라는 범위를 주었기 때문에 k는 3까지 저장되어 있는 상태인 것이다.

// data[0]()함수를 실행했을 때 스코프가 1층으로 늘어난 상태이다. 
// 1단계 AO에서는 k의 값을 찾을 수없다. 빈 값이다. for문의 조건을 만족하지 못해 k의 값이 undefined되어있는 것이다. 
// 그렇기 때문에 스코프체인을 따라 내려와 0단계에서 3이라고 메모리에 저장되고 있는 k의 값을 불러오게 되는 것이다.

// 따라서 data[0](), data[1](), data[2]()에서 모두 k = 3을 가져오는 것이다.
```
<br/>

```javascript
/* -- 3이 아닌 다른 수가 나오도록 해보자. -- */
for (var  k  =  0; k  <  3; k++) {
	data[k] = (function(h) { // 선언형 함수.
		function  진짜할일() {
			console.log(h);
		}
		return  진짜할일
	})(k)
}

data[0]();  // 0
data[1]();  // 1
data[2]();  // 2
```

<br/>

- 함수 안에서 함수가 실행되면 반드시 클로저가 생성된다. 
- 이 클로저를 사라지지 않고 남아있도록 하는 것을 현업에서 주로 '클로저 했다'라고 한다고 한다...

#### 클로저 예시 1
```javascript
function  foo() {
	const  a  =  10;
	function  bar() {
		debugger;
		const  sum  =  a  +  a;
	}
	bar();
}
foo();


/* 예시1 콜스택 */
callStack  = {
	2: { // bar()가 foo() 속에서 실행되었기 때문에 1층 스택(foo)이 사라지지않고 2층이 생긴 것이다.
		AO: { sum:20 },
		Scope: [2.AO, 1.AO, 0.VO],
		this:
	},
	1: {
		AO: {
			a: 10, // 준비단계가 끝난 후 a에 10이 할당 됨.
			bar: function() {},
		},
		Scope: [AO, VO],
		this: ''
	},
	0: {
		VO: {
		foo: function() {}
		},
		Scope: [],
		this: callStack.0.VO
	}
}
```

<br/>

#### 클로저 예시2
```javascript
/* closure 예시 2 */
function  foo() {
	const  a  =  10;
	const  b  =  20;
	function  bar() {
		debugger;
		const  sum  =  a  +  a;
	}
	return  bar();
}
foo();


/* 예시2 콜스택 */
callStack  = {
	1: { // 원래라면 foo()함수가 끝난 뒤 지워져야하지만, return bar()를 해줬기 때문에 사라지지 않는다.(a를 foo()함수 밖에서 참조 가능하게 된 것.)
		AO: {
			a: 10, // 준비단계가 끝난 후 a에 10이 할당 됨.
			b: 20,
			bar: function() {},
		},
		Scope: [AO, VO],
		this: ''
	},
	0: {
		VO: {
			foo: function() {},
			bar: function() {} // a + a 내용이 들어있음. 아직 실행은 안 된 상태.
		},
		Scope: [],
		this: callStack.0.VO
	}
}
```

<br/>

#### 클로저 예시 3
```javascript
function foo() {
	const a = 10;
	const b = 20;
	function bar() {
		const sum = a + a + b;
		return sum;
	}
	return bar;
}
const bar = foo();
bar()

/* 콜스택 */
callStack  = {
	1: { 
		AO: {
			a: 10, 
			b: 20,
			bar: function() {
				[[call]]: 'const sum = a + a'
			},
		},
		Scope: [AO, VO],
		this: ''
	},
	0: {
		VO: {
			bar: function() { // 1층의 스택을 참조하고 있는 것. 따라서 foo()함수가 끝나도 1층의 스택이 사라지지 않는다.
				[[call]]: 'const sum = a + a'
			}, 
			foo: function() {
				[[call]: '....'
			}
		},
		Scope: [VO],
		this: callStack.0.VO
	}
}
```
<br/>

#### 클로저 예시4
```javascript
function foo(e) { //2. 인자 5를 e로 받았다.
	const a = 10;
	const b = 20;
	function bar(e) { // 3. e를 foo()함수 안의 bar()안에 적용하면
		const sum = a + a + b;
		console.log(e); // 4. undefined가 나오게 된다.
		return sum;
	}
	return bar;
}
const bar = foo(5); // 1. foo()함수 실행 시 인자로 5를 주고,
bar();

// 1~4의 이유: bar()함수가 foo()함수 안에 있긴하지만, bar()함수를 foo()함수 바깥에서 별도로 실행시켰기 때문에 foo(e)함수의 e인자를 받지 못하는 것이다.
// 바깥에서 bar()함수 실행시킬 때 별도의 인자를 주지 않았기 때문에 foo()함수 속의 bar(e)함수에 아무리 e를 적어준다한들 e는 찾을 수 없는 값인 것.

// 파라미터는 함수 실행시에만 넘겨줄 수 있다는 것.
```
<br/>

#### 클로저 예시5
```javascript
let 증가 = function () {
	let num = 0;
	return num++;
}
console.log(증가()); // 0
console.log(증가()); // 0
console.log(증가()); // 0

// ===> num이 증가한 상태를 저장시키지 않아서 증가()함수를 여러번 실행해도 모두 0이 산출되는 것.


// 이럴 때 보통 해당 함수 바깥에 num을 선언했었는데, 이번에는 '클로저'를 사용해서 해보자.

// let 증가 = ()(); // 즉시실행 함수
let  증가  =  (function()  {
	let  num  =  0;
	function  알짜()  {
		return ++num;
	}
	return 알짜;
})();
console.log(증가()); // 1
console.log(증가()); // 2
console.log(증가()); // 3

// 위의 클로저 이용한 함수를 실제로는 이렇게 사용하지 보통..
let 증가 = (function() {
	let num = 0;
	return function() {
		return ++num;
	}
})();
```
<br/>

#### 클로저 예시6
```javascript
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport"  content="width=device-width, initial-scale=1.0">
	<title>Document</title>
</head>
<body>
	<ul class="buttons">
		<li>학교</li>
		<li>집</li>
		<li>공원</li>
	</ul>
	<div class="targets">
		<div>학교에서 놀았습니다.</div>
		<div>집에서 놀았습니다.</div>
		<div>공원에서 놀았습니다.</div>
	</div>

<script>
const buttons = document.querySelectorAll('.buttons > li');
const targets = document.querySelectorAll('.targets > div');

// 평소 for문에 let으로 i를 설정해서 작성했던 방식의 코드.
for(let i = 0; i < buttons.length; i++) {
	buttons[i].onclick = function() {
		targets[i].style.backgroundColor = 'orange';
	}
}

// (plus 내용) for문에서 var로 i를 선언하면 안된다. buttons의 최대개수만큼의 값만 i에 적용되게 됨.

// 클로저를 이용해 해보자.
for(var i = 0; i < buttons.length; i++) { // for문 돌 때 실행
	buttons[i].onclick = (function(j) { // 클릭 될 때 실행
		return function 알짜() {
			console.log(j);
			targets[j].style.backgroundColor = 'pink';
		}
	})(i); // (i)가 function(j){}의 j로 들어가진 것.
}
</script>
</body>
</html>
```

<br/>

### # debugger
- debugger를 입력 후 크롬의 콘솔-sources를 보면 해당 단계의 콜스택을 볼 수 있다.
```javascript
for (var  k  =  0; k  <  3; k++) {
	data[k] =  function() { // 선언형 함수.
		var  a  =  1;
		debugger; // debugger를 입력 후 크롬의 콘솔-sources를 보면 해당 단계의 콜스택을 볼 수 있다.
		console.log(k);
	}
}
```
![디버거 실행 이미지](./src/디버거.png)

