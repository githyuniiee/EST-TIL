## 메소드 재정의

### 메소드 오버로딩 (method overloading)

- `메소드의 이름은 동일하고 입력 항목이 다른 경우`
    - 동일한 리턴 타입과 메소드명, 다른 매개변수
    
    ```java
    void sleep()
    void sleep(int hour)
    ```
    

```java
public class Animal {
	String name;

	public void setName(String name) {
		this.name = name;
	}
}

public class Dog extends Animal {
	void sleep() {
		System.out.println(this.name + " Zzz...");
	}
}

public class HouseDog extends Dog {
	void sleep(int hour) {   // 메소드 오버로딩
		System.out.println(this.name + " Zzz... for " + hour + " hours");
	}

	public static void main(String[] args) {
		HouseDog houseDog = new HouseDog();
		houseDog.setName("puppy");
		houseDog.sleep();
		houseDog.sleep(3);
	}
}

//결과 값
puppy Zzz...
puppy Zzz... for 3 hours
```

### 메소드 오버라이딩(@Override)

- 상속된 부모의 메소드 내용이 자식 클래스에 맞지 않을 경우, 자식 클래스에서 동일한 메소드를 재정의 하는 것
- 부모의 메소드와 동일한 시그니처(리턴타입, 메소드 이름, 매개변수 리스트)를 가져야 한다.
- 부모 클래스의 메소드보다 접근 제한을 더 강하게 오버라이딩 할 수 없음 ⇒ 부모 메소드가 public 접근 제한을 갖고 있다면 자식 메소드는 default나 private 접근 제한으로 수정할 수 없음
- 새로운 예외를 throws 할 수 없음
- 메소드가 오버라이딩 되었다면 부모 객체의 메소드는 숨겨지기 때문에, 자식 객체에서 메소드를 호출하면 오버라이딩된 자식 메소드가 호출됨

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/06e7cf81-6469-479f-80a6-1b84047da74e)

<br></br>
## 추상 클래스

- 추상 메서드
    - 자식 클래스에서 반드시 오버라이드 해야만 사용할 수 있는 메소드
    - abstract 리턴타입 메소드명();
    - 추상 클래스는 새로운 실체 클래스를 만들기 위해 부모 클래스로만 사용됨
    - 추상 클래스만으로는 객체를 생성할 수 없음

```java
class Ant extends Animal { ... }
```

- 추상 클래스의 오버라이딩
    - 메소드의 선언만 동일하고, 실행 내용은 실체 클래스마다 달라야 하는 경우
    
    ```java
    public abstract class Animal {
    public abstract void sound();  // 추상메소드 - 메소드의 타입과 이름만 정의
    }
    ```
    

```java
public abstract class Animal {    // 추상 클래스
	protected String kind;
	
	public void breathe() {
		System.out.println("숨을 쉽니다.");
	}
	
	public abstract void sound();   // 추상 메소드
}

public class Dog extends Animal {
	public Dog() {
		this.kind = "포유류";
	}

	@Override
	public void sound() {           // 추상 메소드 재정의
		System.out.println("멍멍");
	}
}

public class Cat extends Animal {
	public Cat() {
		this.kind = "포유류";
	}

	@Override
	public void sound() {           // 추상 메소드 재정의
		System.out.println("야옹");
	}
}

```

<br></br>
## 인터페이스

- 다른 클래스를 작성할 때 기본이 되는 틀을 제공하면서, 다른 클래스 사이의 중간 매개 역할을 하는 일종의 추상 클래스를 의미

```java
interface Predator {
    String getFood();
}

class Tiger extends Animal implements Predator {
	@Override
	public String getFood() {
		return "meat";
	}
}

class Lion extends Animal implements Predator {
	@Override
	public String getFood() {
		return "fish";
	}
}
```


- `인터페이스의 모든 메서드는 추상 메서드다 ❌  ⇒ 자바 8부터 default 메서드 사용 가능`

인터페이스와 다르게 추상 클래스는 생성자, 필드, 일반 메소드도 포함 가능한 차이

→ 인터페이스에서도 필드는 선언이 가능하지만 static final인 상수로만 선언가능

<aside>
💡 추상 클래스는 상속을 통해 기능을 확장해나가는 목적으로 자주 사용되고 인터페이스는 기능 확장이라기보다는 뼈대를 클래스로 가져와서 살 붙이는 느낌

</aside>

추상 클래스와 인터페이스의 공통, 차이점 정리

공통점 

- 객체를 생성할 수 없다.
- 추상 메서드를 포함한다.
- 상속받는 클래스에서는 추상 메서드를 반드시 재정의하여 구현하여야 한다

차이점

- 추상 클래스
    - `상속 받아서 기능을 확장`시키는데 목적
    - 클래스이다.
    - 일반 메서드 정의가 가능하다.
    - 멤버 변수는 클래스와 동일하게 변수 선언 및 사용이 가능하다.
    - extends
    - 다중 상속 - 불가능
- 인터페이스
    - 구현 객체의 동일한 실행 기능을 보장하기 위한 목적
    - 클래스가 아니다.
    - 일반 메서드 정의 불가능하였지만 (Java 8 이후 static, default 메서드 정의 가능)
    - 멤버 변수는 상수만 사용 가능하다.
    - implements
    - 다중 상속 가능
