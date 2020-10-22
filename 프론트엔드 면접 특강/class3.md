## 1. 프론트엔드 입문 특강 
### 객체
#### # 객체란
- 모든건 객체다. null과 undefined를 빼고는 전부 객체다.

```javascript
let name = '박은재';
console.log(name.length); // 3
```
  - `name`변수의 값은 `박은재`로 객체인데 어떻게 length를 불러오는걸까?
    - `let name = '박은재';`를 선언하는 순간, `let temp = new String('박은재');`가 생긴다고 생각하면 된다. (`랩핑`된다고 한다.)
    - 이렇게 생성 된 `temp`에는 length라는 요소가 들어있는 것이다.
    
    ```javascript
    // 이 순서로 진행되는 것이다.
    
    let name = '박은재';
    let temp = new String('박은재');
    console.log(temp.length); // 3
    temp = null; // temp는 다시 비워진다.
    ```
<br/>

- 객체는 `비순서`적이다. 
- 배열은 [1000, 1001, 1002...]가 있으면 1000부터 순서대로 처리가 된다. 
- 반면 객체는 {가: 10, 나: 20, ...}가 있어도 선택되는 애들(찾아지는 객체)부터 처리가 된다.
- 따라서 재인덱싱되야하는 경우 객체가 유리, 배열은 불리하다. (예를 들면, 배열은 중간 하나가 줄어들면 그 뒤의 모든 내용이 앞으로 옮겨져야 한다.) 

<br/>

#### # 일반 객체는 어떻게 만들어지나?
```javascript
// 1.
let b = new Object()
b.name = 'pej';

// 2.
let a = {name: 'pej'}; 
// new Object()로 생성하는 것을 보다 간편하게 하는 방법.
// 기호적으로 생성한다고 보면 된다. ({,}등의 기호 사용)
```
- 모든 함수는 유산(`toString()`등와 같은 요소들)이 있다. 다만, `new`를 사용하는 함수만 이 유산들을 사용할 수 있다. ( ex) `new Object()` )
-  유산이 연결되는 통로를 `_proto_`라고 한다.(console에서 보임. 코드에 ` __proto__`라고 입력하면 된다.)
- 신텍스 슈거..?
	- [참고](https://jaeyeophan.github.io/2017/04/18/ES6-6-Class-sugar-syntax/)
- 클래스 지향 언어....
	 - [참고](https://poiemaweb.com/js-object-oriented-programming)


<br/>

#### # class를 이용해 작성하면?
- 전통적인 작성법
  ```javascript
  function Transport(창문수, 바퀴수, 엔진수, 엑셀수) {
    this.창문 = 창문수;
    this.바퀴 = 바퀴수;
    this.엔진 = 엔진수;
    this.엑셀 = 엑셀수;
    this.소재  =  '금속';
    console.log(this); // Transport {창문: 4, 바퀴: 4, 엔진: 1, 엑셀: 1, 소재: "금속"}
  }
  Transport.prototype.전진  =  function  () {console.log('가라');}

  let car = new Transport(4, 4, 1, 1);
  let airport = new Transport(3, 3, 2, 2);

  console.log(car); // Transport {창문: 4, 바퀴: 4, 엔진: 1, 엑셀: 1, 소재: "금속"}
  console.log(airport);  // Transport {창문: 3, 바퀴: 3, 엔진: 2, 엑셀: 2, 소재: "금속"}

  console.log(car.전진()); // 가라
  console.log(airport.전진());
  // '전진()'은 _proto_에 속해있다. 즉, Transport의 유산이 생긴 것.

  ```

	- `_proto_`에는 공통으로 필요한 애들을 담아놓는다.
  
<br/>

- ES6의 class를 이용한 작성법
  ```javascript
  class Transport {
    // constructor: function() {}라고 쓰는 것과 같음을 알고있자.
    constructor(창문수, 바퀴수, 엔진수, 엑셀수) {
      this.창문 = 창문수;
      this.바퀴 = 바퀴수;
      this.엔진 = 엔진수;
      this.엑셀 = 엑셀수;
    }
    소재 = '금속'; // 건들여지지 않게하고 싶은 애들은 constructor() 밖으로 빼준다.
    static type = function() {}; // 이렇게 하면 유산에 넣지 않고 부모가 가지고 있는 것이다. 즉, 사용하려면 Transport.type()라고 적어야 사용이 가능하다.
    #sn =  '1234556'; // #을 붙이면 해당 함수 바깥에서는 보여지지 않게 된다.(접근불가)
    세차하기() {console.log('세차했다!')};
    get  basicInfo() {
      return `소재는 ${this.소재}이고, S/N은 ${this.#sn}입니다.`;
    };
    set 탑승객(승객) { // set함수에는 반드시 파라미터가 필요하다.
      if(승객 > 5) {
        this.바퀴 = this.바퀴 + 2;
      }
    }
  }

  let car = new Transport(4, 4, 1, 1);

  console.log(car); // Transport {소재: "금속", 창문: 4, 바퀴: 4, 엔진: 1, 엑셀: 1}
  console.log(car.sn); // undefined
  console.log(car.세차하기()); // 세차했다!
  car.탑승객 = 6;
  console.log(car); // {소재: "금속", 창문: 4, 바퀴: 6, 엔진: 1, #sn: "1234556", …}
  // car.탑승객은 console에서 보이지 않는다. 하지만 5이상으로 줬기 때문에 '바퀴'는 6으로 증가했다.
  // 즉, set자체는 저장공간이 없다. 저장하려면 별도로 저장을 해주는 코드를 작성해야 한다.

  ```
	- `constructor() {}`
		- `new`를 사용할 필요 없이 간단하게 작성 가능하다는 이점이 있다.
		- `static`
		- `#`
			- `static`,`#`는 class 안에서만 일어난다.
		- `get()`, `set()`
			- 생성자함수
<br/>

#### # 클래스의 하위클래스 생성
```javascript
/* ------ 클래스의 하위클래스 생성 ------*/
class 은재 {
	constructor() {
		this.키 = '170cm';
	}
	운동하기() {
		console.log('운동했다!');
	}
}
class 재은 extends 은재 { // '은재'의 하위 클래스로 '재은'을 선언한다.
	constructor() {
		super(); // super()는 상위 클래스의 constructor()를 가져온다.
		this.머리색 = '갈색';
	}
	운동하기() { 
		// 운동하기()를 '재은'에도 두었다. 
		// 하위클래스에 똑같은 항목을 추가하면 상위 항목을 가리는 꼴이 된다. 이것을 'overriding'이라고 한다.
		console.log('재은만 운동했다!');
	}
	소개하기() {
		console.log(`저의 키는 ${this.키}이며, 머리색은 ${this.머리색}입니다.`);
	}
}

var 사람 = new 재은();
사람.운동하기(); // 재은만 운동했다!
```

<br/>

###  프로퍼티
- 프로퍼티에는 2가지가 있다.
	- 1. 데이터 프로퍼티
	- 2. 

<br/>

***

- 프론트엔드 신입 면접본다면 이런 질문 하겠다.
	- isArray()와 indexOf()를 작성해보시겠어요?~~둘의 차이는?~~
	- ~~MDN의 proto와 ....~~


<br/>

***
- 책 추천
	- 더글러스 크락포드, <자바스크립트는 왜 그모양일까?>
