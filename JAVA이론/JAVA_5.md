### 클래스의 구성 (필드, 생성자, 메소드)

- 필드 (멤버변수)
    - 객체의 고유 데이터가 저장되는 곳
    
    ```java
    public class Car {
    	String company;
    
    	public static void main(String[] args) {
    	  Car car = new Car();  //필드
      }
    }
    ```
    

- 생성자
    - 클래스로부터 객체를 생성할 때 호출되어 객체의 초기화 담당
    - 클래스명과 메서드명이 같음
    - 리턴 타입 정의 X
    - 객체가 생성될 때 호출되는데 new 키워드가 사용될 때 호출
    
    ```java
    public class Car {
    	String company;
    
    	// 생성자에서 필드 초기화
    	Car() {
    		company = "현대자동차";
    	}
    
    	public static void main(String[] args) {
    	  Car car = new Car(); 
      }
    }
    ```
    
    - 오류 케이스
        - 객체의 생성 방법이 생성자의 규칙과 맞지 않음
    
    ```java
    public class Car {
    	String company;
    
    	Car(String company) {
    		this.company = company;
    	}
    
    	public static void main(String[] args) {
    	  Car car = new Car();  // Error: 아무런 값도 입력하지 않는 생성자
      }
    }
    ```
    
- 디폴트 생성자
    - 클래스에 생성자가 하나도 없다면, 컴파일러는 자동으로 디폴트 생성자를 추가
    - 만약 사용자가 작성한 생성자가 하나라도 구현되어 있다면 컴파일러는 디폴트 생성자를 추가하지 않음

```java
public class Car {
	String company;

	Car() {
	
	}
}
```

- 생성자 오버로딩
    - 오버로딩이란 클래스 내에 같은 이름의 함수를 여러개 선언하는 것
    
    ```java
    public class Car {
    	String company;
    	String model;
    	int maxSpeed;
    
    //1번 생성자
    	Car(String company) {
    		this.company = company;
    	}
    
    //2번 생성자
    	Car(String company, String model) {
    		this.company = company;
    		this.model = model;		
    	}
    }
    ```
    
- 메소드
    - 클래스 내에 구현된 함수
    
    ```java
    public class Car {
    	String model
    
    	void setModel(String model) { //메소드
    		this.model = model
    	}
    }
    ```
    
    - 메소드 선은
    
    ```java
    리턴타입  메소드이름([매개변수 선언, ...]) {  // 선언부
    
     // 실행블록
    
    }
    ```
    
- 매개변수와 인수
    - `매개변수는 메소드에 전달된 입력값을 저장하는 변수` ⇒ 입력값 저장 변수
    - `인수는 메서드를 호출할 때 전달하는 입력값` ⇒ 전달하는 입력값

```java
public class Calculator {
  double divide(int x, int y) {     // x, y는 매개변수
		return x / y;	
  }

  public static void main(String[] args) {
	  Calculator calculator = new Calculator();
		calculator.divide(10, 20);      // 10, 20은 인수
  }
```

- this 활용
    - this라는 키워드를 이용하여 객체에 접근
    
    ```java
    public class Calculator {
    
        int a;  // 필드 a
    
        void postfixOperator() {
            this.a++;     // 본인 객체 접근시 this 사용
        }
    
        public static void main(String[] args) {
            Calculator cal = new Calculator();
            cal.a = 1;
            cal.postfixOperator();     // Before) cal.postfixOperator(cal);
            System.out.println(cal.a);
        }
    }
    ```
