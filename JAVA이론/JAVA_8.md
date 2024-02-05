### 인터페이스의 선언

- 다른 클래스를 작성할 때 기본이 되는 틀
- 구현체 여러 개 둘 수 있음

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/246b5184-0993-4fc8-acbc-89bd52b4092c)

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/c72bc95a-38d9-4d39-92a7-48fcce85ac3d)


⇒ 상속과는 다름 ! `공통된 특징을 모아둔 느낌`

```java
public class Sample {
	public static void main(String[] args) {
		ZooKeeper zooKeeper = new ZooKeeper();
		
		Tiger tiger = new Tiger();
		zooKeeper.feed(tiger);
		
		Lion lion = new Lion();
		zooKeeper.feed(lion);
	}
}

class Animal {
	String name;

	void setName(String name) {
		this.name = name;
	}
}

class Tiger extends Animal {
}

class Lion extends Animal {
}

class ZooKeeper {
	void feed(Tiger tiger) {  // 호랑이가 오면 고기를 던져 준다.
		System.out.println("feed meat");
	}

	void feed(Lion lion) {  // 사자가 오면 생선을 던져준다.
		System.out.println("feed fish");
	}
}
```

위와 같이 메소드 오버로딩 방식으로 구현한다면, 각가의 동물 클래스를 생성할 때 마다 feed 메소드를 추가해야함 ⇒ 이러한 어려움을 극복하기 위한 것이 인터페이스

위의 코드 인터페이스 적용 후

```java
interface Predator {   // 육식동물 인터페이스 생성

}

class Tiger extends Animal implements Predator {
	...
}

class Lion extends Animal implements Predator {
	...
}

// 변경 후
class ZooKeeper {
	void feed(**Predator predator**) {
		System.out.println("feed meat");
	}
}
...
```

인터페이스는 `클래스의 필드`, `생성자 또는 메소드의 매개 변수`, `생성자 또는 메소드의 로컬 변수`로 선언될 수 있음


<br></br>

### 인터페이스 상속

- 인터페이스 상속은 다중 상속이 가능함

```java
public interface 하위인터페이스 **extends 상위인터페이스1, 상위인터페이스2, ...** { 
		...
}
```
<br></br>

### 인터페이스 다형성

```java
public interface ProfileRepository {
    void save();
}

public class ProfileDBRepository implements ProfileRepository {

    @Override
    public void save() {
        System.out.println("DB에 프로필 저장하는 기능");
    }
}

public class ProfileMemoryRepository implements ProfileRepository {
    @Override
    public void save() {
        System.out.println("메모리에 프로필 저장하는 기능");
    }
}
```

인터페이스를 사용하여 메소드 호출을 하도록 코딩했다면 구현 객체를 교체하면서 프로그램의 실행 결과가 다양해짐 ⇒ `인터페이스의 다형성`

<br></br>

### 자동 타입 변환

- 구현 객체가 인터페이스 타입으로 변환되는 것은 자동타입변환에 해당

객치 타입 확인(instanceOf)

```java
if (vehicle instanceof Bus) {
	 ...
}

//결과 ture/false로 리턴
```
<br></br>

### 디폴트 메소드

`자바 8 버전 이후부터는 디폴트 메소드를 사용하여 인터페이스의 실제 구현된 형태의 메소드를 가질 수 있게 됨`

```java
interface Predator {
	String getFood();

	// 디폴트 메소드
	default void printFood() {   
		System.out.printf("my food is %s\n", getFood());
	}
}
```

⇒ 추가 ) 추상메서드와 다르게 인터페이스는 추상메서드만 존재하기 때문에 충돌이 생기지 않아 다중상속에 유리한 장점이 있었으나, default 메서드가 추가됨에 따라 인터페이스의 강점인 충돌 미발생이 깨질 수 있게됨
