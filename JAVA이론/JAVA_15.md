## java.util.function 패키지

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/bc5ef952-129c-4423-be08-ec080dbcf536)


Runnable ⇒ 매개변수와 리턴 값 모두 X

```java
import.java.lang.Runnable;

@FunctionalInterface
public interface Runnable {
   public abstract void run();
}

Runnable r = () -> System.out.println("출력문");
r.run(); //"출력문"
```

Supplier<T> ⇒ 매개변수는 없고, 반환값만 있음

```java
import java.util.function; 
@FunctionalInterface
public interface Supplier<T> {
   T get();
}

Supplier<String> s = () -> "리턴되는 값" //input X, output O
String result = s.get();
System.out.println(result); //"리턴되는 값"
```

Consumer<T> ⇒ 매개변수는 있고, 반환값만 없음

```java
@FunctionalInterface
public interface Consumer<T> { //input만 있음
   void accept(T t);
}

Consumer<String> c = (a) -> System.out.println(a);
c.accept("consumer");
```

Function<T,R> ⇒ 하나의 매개변수를 받아서 하나의 결과를 리턴

⇒첫번째 매개변수는 inputType T, 두번째 매개변수는 outputType R

```java
@FunctionalInterface
public interface Function<T,R> { //input만 있음
   R apply(T t);
}

Function<Integer, String> f = a -> String.valueOf(a);
Function<String, Integer> f2 = b -> { return Integer.valueOf(b) + 100; };
```

`Predicate<T> ⇒ 조건식을 표현하는데 사용`

⇒ 매개변수는 하나, 리턴타입은 boolean을 갖는 함수형 인터페이스

```java
@FunctionalInterface
public interface Predicate<T> { //input만 있음
   boolean test(T t);
}

Predicate<String> isEmptyStr = s -> s.length()==0;
String str = "";
if (isEmptyStr.test(str)) { // if(s.length()==0)
		System.out.println("This is an empty String.")
}

```

```java
// 스트림에서 filter메소드 내부에는 Predicate 타입이 들어감
List<Integer> list = Arrays.asList(1,2,3,4,5);
list.stream()
		.filter(x -> x%2==0)
		.collect(Collectors.toList()); // [2,4]
```

LongSupplier 예제

```java
LongSupplier x = () -> 34l;
System.*out*.println(x.getAsLong());
```

<br></br>
## 메소드 참조

 메소드를 참조해서 매개 변수의 정보 및 리턴 타입을 알아내어, 람다식에서 불필요한 매개 변수를 제거하는 것이 목적

정적 메소드 참조할 경우

`클래스명 :: 메소드명`

| 종류 | 람다 | 메소드 참조 |
| --- | --- | --- |
| 정적(static) 메소드 참조 | (x) → ClassName.method(x) | ClassName::method |
| 인스턴스 메소드 참조 | (obj, x) → obj.method(x) | ClassName::method |

인스턴스 메소드

`참조변수::메소드`

<br></br>
### 매개변수의 생성자 참조

생성자의 매개변수는 함수형 인터페이스를 통해 추론

```java
public class Member {
    private String name;
    private String id;

    public Member() {
    }

    public Member(String id) {
        System.out.println("Member(id) 생성자 실행");
        this.id = id;
    }

    public Member(String name, String id) {
        System.out.println("Member(id, name) 생성자 실행");
        this.name = name;
        this.id = id;
    }

    public String getId() {
        return id;
    }
}

public class ConstructorReferencesExample {
    public static void main(String[] args) {
        Function<String, Member> function1 = Member::new;
        Member member1 = function1.apply("angel");

        BiFunction<String, String, Member> function2 = Member::new;
        Member member2 = function2.apply("angel", "devil");
    }
}
```

```java
List<Integer> list = Arrays.asList(1,2,3,4,5);
list.stream().forEach(System.out::println); //( e → System.out.println(e));
```

<br></br>
## 스트림

- for, while문 사용하지 않음
- 병렬 처리 가능

1. 생성 : 스트림 인스턴스 생성 (배열이나 컬렉션을 스트림 인스턴스로 변환)
2. 가공 : 원하는 결과를 만들어가는 중간 작업
3. 최종 결과를 만들어내는 작업

스트림의 종류

- [java.util.stream](http://java.util.stream) 패키지에 스트림 인터페이스가 정의
- BaseStream을 부모로해서 자식 인터페이스들이 다음과 같이 상속 구조를 이룸

| 이름 | 설명 |
| --- | --- |
| BaseStream | 모든 스트림에서 사용할 수 있는 공통 메소드들이 정의되어 있습니다. 코드에서 직접 사용하지는 않습니다. |
| Stream | 객체 요소를 처리하는 스트림입니다. |
| IntStream | int 형을 처리하는 스트림입니다. |
| LongStream | long 형을 처리하는 스트림입니다. |
| DoubleStream | double 형을 처리하는 스트림입니다. |

1. 컬렉션으로부터 스트림 생성

```java
List<String> list = Arrays.asList("a", "b", "c", "d", "e");

**Stream<String> stream = list.stream();**
stream.forEach(System.out::println);
```

1. 배열로부터 스트림 생성

```java
String[] arr = {"하나", "둘"};
Stream<String> stream = Arrays.*stream*(arr);
stream.forEach(System.*out*::println);
```

1. 숫자 범위로부터 스트림 생성

```java
IntStream intStream = IntStream.range(1,5);
LongStream longStream = LongStream.rangeClosed(1l,5l);
DoubleStream doubleStream = DoubleStream.of(1.1, 2.2);
doubleStream.forEach(System.out::println);
```

1. 파일로부터 스트림 생성

```java
// File 클래스
Stream<String> fileStream = Files.lines(Paths.get("file.txt"), Charset.forName("UTF-8"));
fileStream.forEach(System.out::println);

// BufferedReader 클래스
FileReader fileReader = new FileReader(Paths.get("file.txt").toFile());
BufferedReader br = new BufferedReader(fileReader);
stream = br.lines();
stream.forEach(System.out::println);
```

1. 스트림 연결
    
    `Stream.concat(stream1, stream2);`
    

<br></br>
## 필터링 - distinct, filter

distinct ⇒ 중복제거

```java
List<String> list = Arrays.asList("a", "b", "b", "c");
list.stream()
.distinct()
.forEach(System.out::println);
```

filter ⇒ Predicate가 true인 것만 필터링

```java
List<String> list = Arrays.asList("김밥", "김밥", "김치", "나비");
list.stream()
.filter(str -> str.startsWith("김"))
.forEach(System.out::println);
```
