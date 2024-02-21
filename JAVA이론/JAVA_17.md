## Optional

- NullPointerException을 예방하기 위해 등장
<br></br>
### Optional 객체 반환

기본적으로 Optional 클래스의 get()메서드를 사용하여 Optional 객체에 저장된 값을 반환하지만, 만약 Optional 객체가 null일 경우에는 예외가 발생

안전하게 객체를 꺼내오기 위해서는 null일 경우 사용할 default 값을 정할 수 있음

이때 사용하는 메소드가 `orElse(), orElseGet(`) 메소드

orElseGet() 메소드는 인수로 람다 표현식을 사용할 수 있음

<br></br>
### Optional을 이용한 Null 처리 방법

```java
List<Integer> list = new ArrayList<>();

OptionalDouble optional = list.stream()
						.mapToInt(Integer::intValue)
						.average();

// 값이 실제로 존재하는지 체크
if (optional.isPresent()) {
	System.out.println(optional.getAsDouble());
}
```

 ifPresent 메소드를 사용

Optional의 **ifPresent**에는 값이 실제로 존재할 경우에만 동작하는 코드를 작성

```java
List<Integer> list = new ArrayList<>();

list.stream()
	.mapToInt(Integer::intValue)
	.average()
	.ifPresent(avg -> System.out.println(avg));  // 평균 값이 있을 경우에만 출력
```

<br></br>
## 스레드 (운영체제에서의 프로세스와 스레드)

`프로그램 ⇒ “아직 실행되지 않은 소스코드 덩어리”`

`프로세스 ⇒ “실행 중인 프로그램”` (운영체제에서 자원을 할당받는 단위)

`스레드 ⇒ “하나의 프로세스 안에서 진행되는 작업들”`

프로세스 내부 구조

`프로그램을 실행하면 운영체제가 메모리에 프로세스를 할당`

메모리 ⇒ `stack, Heap, Data, Code 4개의 영역`으로 나눠짐

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/4da42108-090d-47c3-821e-1397ea36df65)

<br></br>

- Code 영역
    - 프로그래머가 작성한 소스코드가 저장 ⇒ 컴퓨터가 이해할 수 있는 기계어 형태로 저장
- Data 영역
    - 코드가 실행되면서 사용하는 전역변수나 static 변수들이 저장
- Stack 영역
    - 함수가 호출되면 Stack 영역에 할당되며 함수가 종료되면 소멸, 함수에서 사용하는 지역 변수도 함께 저장
    - 만약 프로세스가 할당된 메모리보다 Stack 영역을 많이 사용하면 stack overflow 에러가 발생
- Heap 영역
    - 생성자, 인스턴스와 같은 동적으로 할당되는 데이터들을 저장
    
<br></br>
### 스레드 내부 구조

- 스레드는 프로세스가 할당받은 자원을 이용
- 여러 개의 스레드가 있다면 스레드끼리 자원을 공유하기 때문에 동시 작업이 불가능
- `스레드는 Stack 영역만 별도로 사용하고 Code, Data, Heap은 다른 스레드들과 공유`

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/89e9f563-4fa1-4135-a8de-0c2139367be6)


<br></br>
## 자바에서 스레드 생성

1. `Thread 클래스 상속`
2. `Runnable 인터페이스 구현`

```java
class MyRunnable implements Runnable {
    public void run() {
        // 스레드가 수행할 작업 정의
    }
}

public class RunnableExample {
    public static void main(String[] args) {
        Thread thread = new Thread(new MyRunnable());
        thread.start(); // 스레드 시작
    }
}

```
