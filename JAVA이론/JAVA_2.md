# 타입 변환

- 자동 타입 변환
    - 작은 크기의 타입은 큰 크기의 타입으로 자동 타입 변환
    
    ```jsx
    byte byteValue = 10;
    int intValue = byteValue;   //byte -> int
    ```
    
- 강제 타입 변환 (Casting)
    - 큰 크기에서 작은 크기의 타입은 자동 타입 변환 X
        
        ```jsx
        long longValue = 300;
        int intValue = (int) longValue;
        ```
        
        int intValue = (int) longValue;
        

<br></br>


# 기본 자료형과 참조 자료형
    
![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/26e9aa38-2ba6-48f2-9d0e-6f952f1000f4)

    
- 기본 자료형은 선언된 변수는 실제 값을 인수 안에 저장
- 참조 자료형의 선언된 변수는 메모리의 번지를 값으로 가짐

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/06805af2-a34c-483c-8f41-04727f1e87a4)

```jsx
int age = 10;
Calculator name = new Calculator(”java”);
```

- 자바에서는 new를 사용하여 초기화하는 것을 참조 자료형, new 없이 바로 초기화 가능한 것을 기본 자료형이라고 함

- 예외적 초기화 ⭐️
    - String은 참조 자료형이지만 new를 사용해서 객체를 생성하지 않아도 되는 유일한 타입
    
    ```jsx
    String name = "sung yeon";
    String name = new String("sung yeon");
    ```
    

<br></br>

# 오토박싱 & 언박싱, 문자열과 숫자형 변환

- Wrapper type : 기본 자료형을 참조 자료형처럼 사용하기 위한 클래스
- 기본형 타입 : byte, short, int, long, float, double, char, boolean
- 래퍼 클래스 : Byte, Short, Integer, Long, Float, Double, Character, Boolean

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/0a801176-adf3-4d35-a356-4aaf3eb742db)

- 오토박싱
    - 기본타입의 데이터를 Wrapper 클래스의 객체로 변환하는 것
    
    ```jsx
    int index = 11;
    Integer number = Integer.valueOf(index);  // 박싱(Boxing)
    
    int index = 11;
    Integer number = index;   // 오토박싱
    ```
    
- 언박싱
    - 래퍼 클래스의 기본형 타입으로 변환하는 것
    - Integer → int
    

오토박싱과 언박싱은 내부적으로 추가 연산 작업을 거치게 됨  → 오토방식과 언박싱이 일어나지 않도록 동일한 타입 연산이 이루어지도록 구현해야 함

<br>

### 문자열과 숫자 형변환

- String → int/Integer

`Integer.parseInt() ⇒ int 객체 생성`

`Integer.valueOf() ⇒ Integer 객체 생성`

- String → Long

`Long.parseLong();`

- String → Float/Double

`Float.pareFloat();`

`Double.parseDouble();`
