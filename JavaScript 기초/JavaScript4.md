# 객체지향 프로그래밍

## 프로토타입

- 메모리상의 이점을 얻기 위해 사용
- `프로토타입은 모든 인스턴스가 공유하는 공간을 가리킨다.`
- 생성자 생성 후 prototype 키워드를 통해 메서드 혹은 값들은 등록 가능

```jsx
function NewFactory2(name){
    this.name = name;
}

NewFactory2.prototype.sayYourName = function(){
    console.log(`삐리비리. 제 이름은 ${this.name}입니다. 주인님.`);
}
```

## 객체의 상속

- 상속은 prototype을 통해 일어남
- `prototype은 함수가 가지고 있음 !`
- `__proto는 객체가 가지고 있음  !`
- `모든 생성자 함수는 Object.prototype과 연결되어 있음`

## class 사용

```jsx
// function Robot(name) {
//     this.name = name;
// }

// Robot.prototype.sayYourName = function () {
//     console.log(`삐리비리. 제 이름은 ${this.name}입니다. 주인님.`);
// }

class Robot {
    // 클래스의 생성자 함수입니다. 하나의 클래스는 하나의 생성자만 정의할 수 있습니다. 
		// 그리고 생성자 함수는 new 키워드가 호출될때 자동으로 실행됩니다.
    constructor(name) {
        this.name = name;
    }

    // 메소드를 정의합니다. 메소드는 클래스가 생성한 인스턴스를 통해 사용할 수 있습니다.
    sayYourName() {
        console.log(`삐리비리. 제 이름은 ${this.name}입니다. 주인님.`);
    }
}
```

⇒ 내부적인 동작은 동일하지만 보기 좋고 편리하게 개선된 문법 (슈가신텍스)

```jsx
class BabyRobot extends Robot {
    constructor(name) {
        super(name);
        this.ownName = '아이크';
    }

    sayBabyName() {
				// 또한 상속을 받게되면 부모 클래스의 메소드를 사용할 수 있게 됩니다. 때문에 this로 접근 할 수 있습니다.
        this.sayYourName();
        console.log('Suceeding you, Father!');
    }
}
```

<br></br>
# DOM

- innerHTML은 요소 내에 포함된 HTML 마크업을 가져오거나 설정

`myP.innerHTML = "<strong>I'm Strong!!</strong>";`

- 요소 제거하고싶을 경우 ⇒ `myP.innerHTML = "”`

## 속성 제어하기

```jsx
const target = document.querySelector("p");
const txtColor = target.style.color; // 현재 스타일 정보를 가져옵니다.
```

⇒ 인라인 스타일로 적용됨

## 이벤트 객체

- 이벤트에서 호출되는 핸들러에는 이벤트와 관련된 모든 정보를 가지고 있는 매개변수가 전송
- 가장 상위의 window 객체부터 document, body 순으로 DOM 트리를 따라 내려갑니다. 이를 **캡처링 단계**
- 다시 DOM 트리를 따라 올라가며 만나는 모든 버블링 이벤트 리스너를 실행합니다.  이를 이벤트 **버블링 단계**

### 이벤트의 this

```jsx
<script>
    const parent = document.querySelector('.parent');
    parent.addEventListener('click', function (event) {
        console.log(this);
    });

		const myObj = {
        name: 'jaehyun',
        walk() {
            parent.addEventListener('click', () => {
                console.log(this.name + ' is walking');
            })
        }
    }
</script>
```

- 만약 이벤트 리스너 함수를 화살표 함수로 쓴다면 this 가 가리키는 대상이 달라진다는 점

**stopPropagation() 연습**

```jsx
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
<!DOCTYPE html>
<html lang="ko">

<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <link rel="stylesheet" href="../reset.css">
    <style>
    </style>
</head>

<body>
    <!-- submit 의 기본 동작을 중지 -->
    <h1>나의 todo list</h1>
    <p>1. 오늘 저녁에는 부대찌게를 끓여 먹겠다.<button type="button">삭제</button></p>
    <p>2. 후식으로 슈팅스타를 먹겠다.<button type="button">삭제</button></p>
    <p>3. 자기 전에 반드시 내일 아침 메뉴를 생각해두겠다.<button type="button">삭제</button></p>
    <script>
        const txts = document.querySelectorAll('p');
        txts.forEach((item)=>{
            item.addEventListener('click', (event)=>{
                alert(event.target.childNodes[0].data);
            });
        });

        const btns = document.querySelectorAll('button');
        btns.forEach((item)=>{
            item.addEventListener('click', (event)=>{
                const reselt = confirm('삭제하시겠습니까?');
                event.stopPropagation();
                if(reselt){
                    event.target.parentElement.remove();
                }
            });
        })
    </script>
</body>

</html>
</body>
</html>
```

<br></br>
# Ajax

- 비동기 [코드 순서는 따로 있고, 순서와는 별도로 동시에 코드에 대한 처리가 진행되는 것]
- 언제 일어날지 모르는 일에 대응할 때 ⇒ 비동기 코드 사용

```jsx
console.log(1);
// setTimeout으로 콜백함수가 일정시간 뒤에 실행하도록 코드를 작성합니다. 
순서대로 실행되지 않습니다.(비동기적으로 실행). 이러한 비동기 실행 코드는 setInterval, addEventListener[언제 실행되어야할지 알 수 없는 경우]와 같은 함수들이 있습니다.
setTimeout(() => console.log(2), 100);
[3, 4, 5].forEach(i => console.log(i));
console.log(6); 

//1
//3
//4
//5
//2
```

calback ⇒ 함수의 인자로 함수가 들어오는 것

<br></br>
## fetch API

- XMLHttpRequest 를 대체할 새로운 API

```jsx
let result = fetch('https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json');
console.log(result);
```

- fetch는 promise 반환

비동기를 어떻게 동기적으로 쓸 수 있을까 🤔 ⇒ async await

```jsx
async function fetchTest() {
try {
const response = await fetch('https://mdn.github.io/learning-area/javascript/oojs/json/superheroes.json');

      if (!response.ok) throw new Error('error');
    } catch (e) {
        console.error('error', e);
    }
}

fetchTest();

```
