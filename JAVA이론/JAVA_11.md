## try-with-resource (자동 리소스 닫기)

```java
public static void main(String[] args) {
        

//자동으로 br.close();
        String filePath = System.getProperty("user.dir") + "/src/test.txt";
        try(BufferedReader br = new BufferedReader(new FileReader(filePath))){
            System.out.println(br.readLine());
        }catch (IOException e){
            System.out.println("예외처리 로직");
        }
    }
```

- try 조건 안에 들어갈 수 있는 클래스는 close를 구현할 수 있는 클래스여야 함

- 자동 리소스 닫기 기능을 사용하는데는 리로스 객체는 java.lang.AutoCloseable 인터페이스를 구현하고 있어야 함

- 예외가 발생하면 먼저 닫아 준 후 Exception 처리가 됨

(이전 부분 복습)

자바의 특징

- GC(Garbage Collection)로 `자동 메모리 관리 기능`이 있음
- JVM 안에서 GC가 일어남(백그라운드에서 비주기전으로 수행됨)
- JVM 머신으로인해 운영체제에 독립적

변수

- `데이터의 값을 저장하는 메모리 공간`
- primitive type, reference type

객체 지향 언어

- 객체 : 현실 세계를 추상화하여 표현한 것, 데이터와 그 데이터를 조작하는 메서드의 결합으로 구성
- 객체 지향 언어를 사용했을 때는 코드를 재사용 할 수 있음, 이미 작성된 클래스가 있다면 상속, 다형성 등을 이용하여 새로운 기능을 쉽게 개발 가능
- 절차 지향언어는 순차적으로 처리하는 반면, 객체 지향 언어는 다수의 객체를 만들고, 이들끼리 서로 상호작용하도록 함

클래스와 객체

- 클래스는 객체를 만들기 위한 설계도, 데이터와 메서드를 가짐
- 객체는 클래스의 인스턴스, 객체는 클래스에서 정의한 데이터와 메서드를 가짐

<br></br>
## 제네릭

- 데이터의 타입을 일반화 하는 것 (타입의 안정성을 위해)
- 컴파일 시에 미리 타입이 정해지기 때문에, 타입 검사나 변환 같은 번거로운 작업을 생략할 수 있음
- 컴파일 시 강한 타입 체크가 가능

제네릭 표기법

```java
public class 클래스명<T> { ... }
public interface 인터페이스명<T> { ... }
```

타입 파라미터는 변수명과 동일한 규칙에 따라 작성할 수 있지만, 일반적으로 대문자 알파벳 한 글자 T(Type)로 표현

실제 코드에서 제네릭 타입을 사용하려면 타입 파라미터에 구체적인 타입을 지정해야 함

```java
public class Box<Integer> {
	private Integer t;

	public Integer get() {
		return t;
	}

	public void set(Integer t) {
		this.t = t;
	}
}

Box<Integer> box = new Box<Integer>();
box.set(6);             // 자동 Boxing
int value = box.get();  // 자동 Unboxing
```
