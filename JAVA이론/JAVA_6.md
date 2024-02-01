### final 필드와 상수

- final 필드
    - final 필드가 초기값 지정이 되면 최종적인 값이 되어, 프로그램 실행 도중에 수정할 수 없음
    - 프로그램을 수행하면서 그 값이 바뀌면 안될 때 사용
    
    ```java
    final String nation = "Korea";
    ```
    
    - final 필드의 초기값 줄 수 있는 방법
        - 필드 선언시
        - 생성자에서 초기화
        
- 상수 (static final)
    - 불변의 값을 저장하는 필드
    - final 필드는 한 번만 초기화되면 수정할 수 없는 필드지만, final 필드를 상수라고 부르지는 않음 ! → 불변의 값은 객체마다 저장할 필요가 없는 공용성을 띠고 있으며 여러 가지 값으로 초기화될 수 없음
    
    ```java
    static final 타입 상수 [= 초기값];
    ```
    

⇒ 객체마다 저장할 필요 없이 공용으로 선언하여 사용하기 때문에 static 이면서 final로 선언

- 상수 이름은 모두 대문자로 작성하는게 컨벤션

```java
static final double PI = 3.14159;
static final double EARTH_SURFACE_AREA;
```

<br></br>
### 접근 제어자

- 접근 제어자를 사용하여 변수나 메소드의 사용 권한을 설정할 수 있음

| 접근 제어자 | 같은 클래스 | 같은 패키지 | 자식 클래스 | 전체 |
| --- | --- | --- | --- | --- |
| public | O | O | O | O |
| protected | O | O | O |  |
| default(packege-private) | O | O |  |  |
| private | O |  |  |  |

- private
    - private이 붙은 변수나 메서드는 해당 클레스 안에서만 접근이 가능
- default
    - 접근 제어자를 별도로 설정하지 않는다면 변수나 메소드는 default 접근 제어자가 자동으로 설정됨 → `동일한 패키지 안에서만 접근 가능`
- protected
    - 접근 제어자가 protected로 설정되었다면 protected가 붙은 변수나 메소드는 동일 패키지의 클래스 또는 해당 클래스를 상속받은 클래스에서만 접근이 가능
- public
    - 어떤 클래스에서도 접근이 가능

<br></br>
### Getter, Setter 메소드

- Setter 메소드
    - 데이터는 외부에서 접근할 수 없도록 막고, 메소드는 공개해서 외부에서 메소드를 통해 데이터에 접근하도록 유도  → 메소드는 매개값을 검증해서 유효한 값만 데이터로 저장할 수 있기 때문 ⇒ 이러한 역할을 하는 메소드 : Setter 메소드
    
    ```
    public class Car {
    private int speed;	
    public void setSpeed(int speed) {
    			if (speed < 0) {
    					this.speed = 0;
    					return;
    			} else {
    					this.speed = speed;
    			}
    	}
    }
    ```
    
    ⇒ speed 필드는 외부에서 직접 접근이 불가능하도록 막아놓고, Setter 메소드로 Speed 값을 변경해주도록 공개함
    

- Getter 메소드
    - 외부에서 객체의 데이터를 읽을 때도 메소드를 사용함

```java
private 타입 fieldName;

// Getter
public 리턴타입 getFieldName() {
	return fieldName;
}

// Setter
public void setFieldName(타입 fieldName) {
	this.fieldName = fieldName;
}
```

- 필드 값이 bolean일 경우 관례상 get으로 시작하지 않고, is로 시작

```java
private boolean stop;

// Getter
public boolean **is**Stop() {
	return stop;
}

// Setter
public void setStop(boolean stop) {
	this.stop = stop;
}
```

<br></br>
### 상속

- 기존 클래스를 재활용하여 새로운 클래스를 작성하는 방법
- 클래스간 공유될 수 있는 속성과 기능을 상위클래스로 추상화 시킴
- 부모의 클래스를 재활용하여 속성과 기능을 물려주어 사용
- 처음부터 모든 필드와 메소드를 구현하는 것보다 효율적이고 개발 시간 절약

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/027875a6-0ae7-4759-8d8f-9537d0773890)


```java
public class InheritA {
    int field1;

    void method1() {
        System.out.println("InheritA.method1 field1 : " + field1);
    }
}
```

```java
public class InheritB extends InheritA {
    String field2;

    void method2() {
        System.out.println("InheritB.method2 field2 : " + field2);
    }
}
```

- `부모 class의 private 접근 제한을 갖는 필드와 메소드는 상속 대상에서 제외`
- 부모 클래스와 자식 클래스가 다른 패키지에 존재한다면 default 접근 제한을 갖는 필드와 메소드도 상속 대상에서 제외
- 상속을 이용하면 클래스의 수정 최소화 가능 !

<br></br>
### 부모 생성자 호출

- 모든 객체는 클래스의 생성자를 호출해야만 생성됨  ⇒ 부`모 생성자는 자식 생성자의 맨 첫 출에서 호출`

```java
public Dog {
	super(); //부모의 기본 생성자를 호출
}
```

**부모 클래스에 기본 생성자가 없고 매개 변수가 있는 생성자만 있다면 자식 생성자에서 반드시 부모 생성자 호출을 위해 super(매개값, …)를 명시적으로 호출해야합니다**

⇒ 반드시 자식 생성자 첫주렝 위치해야함 !

```java
public class Person {
	String name;
	String ssn;

	public Person(String name, String ssn) {
		this.name = name;
		this.ssn = ssn;
	}
}
```

```java
public class Student extends Person {
	int studentNo;

	public Student(String name, String ssn, int studentNo) {
		super(name, ssn);
		this.studentNo = studentNo;
	}
}
```
