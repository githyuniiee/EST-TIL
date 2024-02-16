## Hashtable

HashMap과 동일한 내부 구조를 지님

 HashMap과의 가장 큰 차이는 Hashtable은 동기화된(synchronized) 메소드로 구성되어 있기 때문에 멀티 스레드가 동시에 이 메소드를 실행할 수 없고, 하나의 스레드가 실행을 완료해야 다른 스레드를 실행할 수 있음

⇒ `thread safe하다 : 앞선 처리를 하던 스레드가 처리될 때 까지 뒤에 있던 스레드가 대기 상태인 것`

⇒ 실제로는 HashMap을 더 많이 사용

<br></br>

## Stack과 Queue

`후입선출 (LIFO: Last In First Out)은 나중에 넣은 객체가 먼저 빠져나가는 자료구조`

`선입선출(First In First Out)은 먼저 넣은 객체가 먼저 빠져나가는 구조`

`컬렉션 프레임워크 에서는 후입선출(LIFO) 자료구조를 제공해주는 Stack`

`선입선출(FIFO) 자료구조를 제공해주는 Queue 인터페이스`

- Stack

| 리턴 타입 | 메소드 | 설명 |
| --- | --- | --- |
| E | push(E item) | 주어진 객체를 스택에 넣는다 |
| E | peek() | 스택의 맨 위 객체를 가져온다. 객체를 스택에서 제거하지 않는다. |
| E | pop() | 스택의 맨 위 객체를 가져오고, 객체를 스택에서 제거한다. |
- Queue

| 리턴 타입 | 메소드 | 설명 |
| --- | --- | --- |
| boolean | offer(E e) | 주어진 객체를 넣는다. |
| E | peek() | 객체 하나를 가져온다. 객체를 큐에서 제거하지 않는다. |
| E | poll() | 객체 하나를 가져온다. 객체를 큐에서 제거한다. |

<br></br>
## 람다식

- 랃다식은 함수(메서드)를 간단한 식으로 표현하는 방법 ⇒ 익명함수를 생성하기 위한 식
- 컬렉션 요소를 필터링 하거나 매핑해서 원하는 결과를 쉽게 집계할 수 있음

```java
int max(int v1, int v2) {
		return v1 > v2 ? v1 : v2;
}

//랃다식
(int v1, int v2) -> {
		return v1 > v2 ? v1 : v2;
}

//반환 값이 있는 경우에는 식이나 값만 적고 return문도 생략 가능
(int v1, int v2) **->** v1 > v2 ? v1 : v2
```

함수형 인터페이스 : 단 하나의 추상 메소드만 선언된 인터페이스

람다식 변경해보기

```java
//1번
int max(int v1, int v2) {
		return v1 > v2 ? v1 : v2;
}

(v1,v2) -> v1 > v2 ? v1 : v2;

//2번
int print(String name, int i) {
System.out.println(name + "=" +i);
}

(name, i) -> System.out.println(name + "=" +i);

//3번
int square(int x) {
   return x*x;
}

(x) -> x*x;
```

<br></br>
## 함수형 인터페이스

`함수형 인터페이스 : 단 하나의 추상 메소드만 선언된 인터페이스`

- 매개 변수와 리턴값이 없는 람다식
    
    ```java
    @FunctionalInterface
    public interface MyFunctionalInterface {
        void method();
    }
    
    public class MyFunctionalInterfaceExample {
    
        public static void main(String[] args) {
            MyFunctionalInterface finter;
    
            finter = () -> {
                String str = "method call 1";
                System.out.println(str);
            };
            finter.method();
    
            finter = () -> {
                System.out.println("method call 2");
            };
            finter.method();
    
            finter = () -> System.out.println("method call 3");
            finter.method();
        }
    }
    ```
    
- 매개 변수와 리턴값이 있는 람다식
    
    ```java
    @FunctionalInterface
    public interface MyFunctionalInterface2 {
        void method(int x);
    }
    
    public class MyFunctionalInterfaceExample2 {
    
        public static void main(String[] args) {
            MyFunctionalInterface2 finter2;
    
            finter2 = (x) -> {
                int result = x * 5;
                System.out.println(result);
            };
            finter2.method(2);
    
            finter2 = (x) -> {
                System.out.println(x * 5);
            };
            finter2.method(2);
    
            finter2 = x -> System.out.println(x * 5);
            finter2.method(2);
        }
    }
    ```
    
- 리턴값이 있는 람다식
    
    ```java
    @FunctionalInterface
    public interface MyFunctionalInterface3 {
        int method(int x, int y);
    }
    
    public class MyFunctionalInterfaceExample4 {
        public static void main(String[] args) {
            MyFunctionalInterface3 finter3;
    
            finter3 = (x, y) -> {
                int result = x + y;
                return result;
            };
            System.out.println(finter3.method(2, 5));
            
            finter3 = (x, y) -> {
                return x + y;
            };
            System.out.println(finter3.method(2, 5));
            
            finter3 = (x, y) -> x + y;
            System.out.println(finter3.method(2, 5));
        }
    }
    ```
