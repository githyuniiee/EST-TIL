# 조건문과 반복문

prompt(”뭔가 입력해보세요”); ⇒ 브라우저로부터 입력받는 자바스크립트 명령어(사용자로부터 받은 데이터를 모두 문자열로 받음)

parseInt(); ⇒ 해당 명령어로 숫자형 데이터로 변경해줌

## if 문 연습 코드

```jsx
const age = prompt("나이를 입력해주세요!");

    if(age >= 18){
        console.log("안녕하세요!");
    }else if(age >= 10){
        console.log("안녕! 반가워 꼬마친구!")
    }else{
        console.log("부럽다...")
    }
```

왜 `const age = parseInt(prompt("나이를 입력해주세요!"));` 가 아닐까!

그렇다면 parseInt를 사용하지 않았는데 어떻게 문자열과 숫자가 비교되는걸까?🤔 ⇒ `암묵적형변환!` [자바스크립트는 문자를 숫자로 바꿔서 비교]

자바도 var 타입으로 → var 변수 명 이렇게 하면 문자열이던 숫자던 자동적으로 판단

## 삼항연산자 연습

```jsx
<script>
    const score = prompt("성적 입력해주세요!");

    if(score >= 90){
        console.log("A");
    }else if(score >= 80){
        console.log("B");
    }else if(score >= 70){
        console.log("C");
    }else if(score >= 60){ 
        console.log("D");
    }else{
        console.log("강해져서 돌아와라");
    }

//if문과 동일
    score >= 90 ? console.log("A") 
    : score >=80 ? console.log("B") 
    : score >= 70 ? console.log("C") 
    : score >= 60 ? console.log("D") 
    : console.log("강해져서 돌아와라");
</script>
```
<br></br>
## Switch문 연습

```jsx
<script>
    const score = prompt("성적 입력해주세요!");

    switch (score){
        case score >= 90 :
            console.log("A");
            break;
        case score >= 80 :
            console.log("B");
            break;
        case score >= 70 :
            console.log("C");
            break;
        case score >= 60 :
            console.log("D");
            break;
        default :
            console.log("강해져서 돌아와라");

    }
</script>
```

✔️switch문에서는 암묵적형변환이 되지 않음
<br></br>
## for문 연습

```jsx
for(let i=1; i<10; i++){    
    ***document***.write(`5 X ${i} = ${i*5} <br>`);
}
```

- NaN의 타입 → 숫자

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/2425584b-39b4-4203-8d95-8f8ec2274189)

- template literal 사용할 경우 아래와 같이 대체 가능 !


![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/77e3237f-b6ae-4a7b-b932-6cb5e4e03440)


## While문 연습

```jsx
let num = 0;

    while(num < 10){
        num += 1;
        if(num === 4 || num === 7){
            continue;
        }
        console.log(num);
    }
```
<br></br>
# Type

- 데이터를 용도에 맞게 쓰기 위해 사용
- 자바 스크립트의 타입 → 원시타입, 참조타입(객체타입)

## 원시타입

- 값이 변경 불가능
- 값이 복사되어 저장 (원본은 건드리지 않음) ⇒ 실제 메모리에 저장된 주소가 복사되어 저장

## 객체타입

- 프로퍼티(객체 안에 들어있는 데이터)로 값과 메서드(함수)를 가지며, 이 둘은 각각 객체의 상태와 동작을 나타냄
- 값을 변수에 저장할 때 값 자체가 아닌 값의 위치가 저장됨
