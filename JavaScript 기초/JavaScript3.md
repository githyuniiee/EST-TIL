# 배열의 여러가지 메소드

1. push()와 pop()

```jsx
const arr = [1, 2, 3];
arr.push(4);
console.log(arr); // [1, 2, 3, 4]
arr.pop();
console.log(arr); // [1, 2, 3]
```

1. shift()와 unshift()
- shift() → 배열에서 첫 번째 요소를 꺼내고 반환
- unshift() → 배열의 첫 번째 요소로 새로운 요소를 추가

```jsx
const myArray = ["사과", "바나나", "수박"]; 
myArray.shift();
console.log(myArray);  //['바나나', '수박']
myArray.unshift("오이", "배");
console.log(myArray); //['오이', '배', '바나나', '수박']
```

const 상수인데 왜 값이 바뀌나 ? 🤔

⇒ 배열의 주소를 저장한 것임 const는 !! 그래서 그 내부의 값이 변경하더라고 한들 주소는 변하지 않음 !

1. splice()
- 배열의 요소를 추가, 제거, 교체
- splice(삭제나 추가할 인덱스, 삭제할 요소의 개수, 추가할 요소들)

```jsx
const arr = [1, 2, 3];
arr.splice(1, 0, 4); 
console.log(arr); // [1, 4, 2, 3]
arr.splice(2, 1, 5);
console.log(arr); // [1, 4, 5, 3]
```

splice 연습 문제

```jsx
const fish = ['정어리', '고등어', '돌고래', '참치', '고래상어', '코끼리'];
    fish.splice(5, 1);
    console.log(fish);
    fish.splice(4, 0,'다금바리');
    console.log(fish);
    fish.splice(2, 1, '옥돔', '갈치');
    console.log(fish);
```

1. slice()
- 요소들을 추출하여 새로운 배열로 반환하는 메서드

```jsx
const myArray = ["apple", "banana", "cherry", "durian", "elderberry"];
console.log(myArray.slice(1, 4)); //['banana', 'cherry', 'durian']
console.log(myArray.slice()); //['apple', 'banana', 'cherry', 'durian', 'elderberry']
console.log(myArray.slice(0, 10)); //['apple', 'banana', 'cherry', 'durian', 'elderberry']
```

1. sort()
- 배열의 요소를 정렬하는데 사용

```jsx
const avengers = ['아이언맨', '스파이더맨', '헐크', '토르'];
console.log(avengers.sort()); //['스파이더맨', '아이언맨', '토르', '헐크']
```

```jsx
const nums = [3, 1, 8, 6];
console.log(nums.sort()); //[1, 3, 6, 8]

const nums2 = [23, 5, 1000, 42];
console.log(nums2.sort()); //[1000, 23, 42, 5]
```

⇒ 원소를 문자열로 전환한 후에 유니코드 포인트의 순서대로 변환하기에 의도와 다르게 정렬될 수 있음

→ 비교함수 사용 가능!

비교 함수의 두 인자 a, b를 비교해서(즉, 빼서) 0보다 작은 수 즉, 음수가 나오면 a를 앞으로 위치하고, 두 인자를 뺐는데 0보다 큰 양수가 나오면  b를 앞으로 위치

```jsx
const num3 = [13, 9, 10];

num3.sort(function (a, b) {
  console.log('a: ' + a, 'b: ' + b);
  return a - b;
});
```

1. forEach()
- 배열의 각 요소에 대해 주어진 함수를 실행

```jsx
const arr = ['참외', '키위', '감귤'];
arr.forEach(function(item, index) {
  console.log(item, index);
	arr[index] = index; 
}); //콜백함수

// 결과
// 참외 0
// 키위 1
// 감귤 2
```

1. map()
- 배열의 각 요소에 대해 주어진 함수를 실행하고, 새로운 배열로 반환

```jsx
const arr = [1, 2, 3];
const newArr = arr.map(function(item, index) {
  return item * index;
});

console.log(newArr);
```

`forEach 메소드의 경우 반환값이 없지만 map 메소드는 새로운 배열을 반환한다는 차이`

1. filter()
- 기조의 배열에서 특정 조건을 만족하는 요소들만 추출하여 새로운 배열을 만듦

```jsx
const arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const newArr = arr.filter(function(el) {
  return el % 2 === 0;
});

console.log(newArr);
```

1. includes ⇒ 요소가 포함되어 있으면 true 아니면 false 반환

<br></br>
## 객체

- 키와 값으로 이루어져 있음
- 배열은 값에 접근하기 위해서는 인덱스 번호를 이용해야 했음

배열의 리터럴 표현 → []

객체의 리터럴 표현 → {}

접근 방법

```jsx
console.log(`${babaYaga.name} from ${babaYaga.from}`);
console.log(`${babaYaga['name']} from ${babaYaga['from']}`); //문자열로서 접근해야함
```

### 객체의 메소드

- hasOwnProperty()

hasOwnProperty() 메소드는 객체가 특정 프로퍼티를 가지고 있는지를 나타내는 불리언 값을 반환

- for … in

```jsx
const person = {
  name: '재현',
  age: 20,
  gender: 'male'
};

for (let key in person) {
  console.log(`${key}: ${person[key]}`);
}
```

- keys(), values()

<br></br>
# this

- this는 객체를 가리키는 참조 변수
- `주소만 가리킴 !`

window 객체

⇒ 브라우저 환경의 전역 공간

Node.js 환경에서의 전역공간은 global이란 이름을 가진다

- this는 실행되는 객체에 따라 위치가 달라짐

```jsx
function sayName(){
  console.log(this.name);
}
var name = 'Hero';

let peter = {
  name : 'Peter Parker',
  sayName : sayName
};

let bruce = {
  name : 'Bruce Wayne',
  sayName : peter.sayName
};

bruce.sayName(); //Bruce Wayne
```
<br></br>
# 객체지향 프로그래밍

## 객체지향 프로그래밍이란 ?

- 객체들을 만들어 서로 소통하도록하는 방법
- 객체란 ?
    - 자바스크립트의 객체는 키, 값 쌍으로 이루어진 데이터의 묶음
    - 객체 지향의 객체는 표현하고자 하는 구체적인 사물을 추상적으로 표현한 것

## 생성자

- 객체를 만들 때 new 연산자와 함께 사용하는 함수

```jsx
let myArr = new Array(1,2,3);
```

이러한 생성자를 내장 생성자

⇒ 객체를 빠르게 대량 생산 가능 !

## 커스텀 생성자 만들어보기

생성자 함수는 암묵적으로 대문자로 시작하는 이름을 가짐

```jsx
function Factory(){}
let a = new Factory();
```

따로 return 값을 가지지 않지만 new 키워드가 앞에 붙으면 자동적으로 객체를 생성하고 반환한다. 이 때의 객체를 다른 말로 `인스턴스`

```jsx
a instanceof Factory //true
```

`instanceof` 를 통해 객체 관계 확인 가능

생성자 함수에서 사용되는 this는 생성자를 통해 만들어진 인스턴스를 가리킴

## 프로토타입

```jsx
NewFactory2.prototype.sayYourName = function(){
    console.log(`삐리비리. 제 이름은 ${this.name}입니다. 주인님.`);
}
```

⇒ 모든 인스턴스들이 해당 함수를 바라보고 있음

⇒ 메모리를 효율적으로 사용할 수 있음 !

⇒ 모든 인스턴스가 공유하는 공간을 가리킴

생성자 함수가 인스턴스를 생성하게 되면 그 안에는 숨겨진 프로퍼티인 [[Prototype]] 이 존재하게 됩니다. 코드상에서는 `__proto__`로 표현

```jsx
function Test(){};

const obj = new Test();

obj.__proto__ === Test.prototype
```

`__proto__`  는 객체 안에 존재하는 숨겨진 프로퍼티

<br></br>
# DOM

- 브라우저의 기능을 사용할 수 있게 해주는 API
- DOM 은 HTML 문서의 내용을 트리형태로 구조화하여 웹페이지와 프로그래밍 언어를 연결시켜주는 역할을 합니다. 이때 각각의 요소와 속성, 콘텐츠를 표현하는 단위를 **'노드(node)'**

DMO 트리에 접근하기

```jsx
// css 선택자로 단일 요소에 접근하기
document.querySelector("selector");

// css 선택자로 여러 요소에 접근하기
document.querySelectorAll("selector");
```

## DOM 제어 명령어

이벤트 삽입

```jsx
const myBtn = document.querySelector("button");

myBtn.addEventListener('click' //[이벤트 타입], function() //[콜백함수]{
	console.log("hello world");
})
```

클래스 제어

```jsx
const myBtn = document.querySelector("button");

myBtn.addEventListener('click', function(){

// blue 라는 클래스의 속성 값을 지정 할 수 있습니다.
	myBtn.classList.add("blue"); //스타일 제어할 때 가장 많이 사용

	// myBtn.classList.remove("blue");     클래스를 제거합니다.
	// myBtn.classList.toggle("blue");     클래스를 토글합니다. 없으면 넣어주고, 있으면 제거합니다.
	// myBtn.classList.contains("blue");   해당하는 클래스가 있는지 확인합니다.
})
```

```jsx
myP.innerHTML = "<strong>I'm Strong!!</strong>";

// innerHTML 은 요소(element) 내에 포함된 HTML 마크업을 가져오거나 설정합니다. 중요한 기능은 innerHTML로 값을 할당할 때, 마크업으로 변환할 수 있는 문자열이 있다면 마크업으로 만들어 보여준다는 것 입니다. 
// 만약 그런 문자열이 없다면 그냥 문자열만 컨텐츠로 설정합니다.
// 요소 생성,수정,제거 가능
```
