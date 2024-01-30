### 데이터 타입 분류

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/72c34ca2-2879-44fb-9625-7f26ef1af400)


- Primitve type은 값을 변수 안에 저장
- Reference Type은 메모리 번지 (주소) 를 값으로 갖음
- `String 변수 또한 참조 자료형`

### 메모리 사용영역

- 자바는 운영체제 위에 JVM 이 올라가서 동작하는 언어

- JVM의 메모리는 크게 3가지
    - Heap 영역
    - Stack 영역
    - Static(Method) 영역

- Heap 영역
    - 객체 혹은 배열이 생성되는 영역
    - 힙 영역에 생성된 객체 혹은 배열은 JVM 스택 영역의 변수나 다른 객체들에 의해 참조
    - 만약 참조하는 변수가 없다면 JVM에서는 Garbage Collecotr를 실행시켜 쓰레기를 자동으로 제거 → 개발자가 따로 객체를 제거하기 위한 코드를 작성할 필요 X

- Stack 영역
    - JVM 스택은 메소드를 호출할 때마다 처리해야할 작업(Frame)을 추가(push)하고 메소드가 종료되면 해당 Frame을 제거(pop)하는 동작을 수행
    - 보통은 기본 자료형(Primitive type - byte, short, int, long, double, boolean, float), 지역변수, 매개변수가 저장되는 메모리 영역을 말하고, 참조 자료형의 경우 Heap 영역에 생성된 데이터의 참조값이 이 스택 영역에 할당

- 메소드 영역
    - JVM이 시작할 때 생성되고 모든 스레드가 공유하는 영역
    - 코드에서 사용되는 클래스들을 Class Loader로 읽어서 분류해서 저장
    
    ![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/925c7dc3-49d3-483e-a4d3-786bbaa47989)

    

### NULL , NPE

- 참조 타입 변수는 `힙 영역의 객체를 참조하지 않는다는 뜻`으로 null 값을 가질 수 있음 → null로 초기화된 참조변수는 스택 영역에 생성

- NPE(NullPointerException) 오류 ⇒ 참조 자료형 변수를 잘못 사용하면 발생

```java
int[] intArray = null;
intArray[0] = 10;     // NullPointerException 발생 
```

- `String 값을 “”으로 초기화하다면 NullPointerException 피할 수 있음`

### 배열 관련 오류

```java
ArrayIndexOutOfBoundsException
```

- 배열 크기가 초기에 정한 공간을 넘어 할당된다면 발생

### 객체지향언어

- 자동차를 만들려고 할 때의 각각의 부품들을 자바에서는 `객체`
- 객체를 하나씩 조립하여 완성된 프로그램을 개발하는 기법 → 객체 지향 프로그래밍(OOP : Object Oriented Programming)

- 객체지향 프로그래밍 특징
    - 캡슐화 : 클래스 안에 서로 연관있는 속성과 기능들을 하나의 캡슐로 만들어 데이터를 외부로부터 보호 → 데이터 보호, 데이터 은닉
    - 캡슐화를 구현하기 위한 방법 중 하나는 접근제어자를 활용하는 것
    
    - 다형성 : 다형성이란 어떤 객체의 속성이나 기능이 상황에 따라 여러가지 형태를 가질 수 있는 성질

### 클래스와 객체

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/e768cf97-6723-422b-a255-ec627bd736ba)

<br></br>
<aside>
💡 클래스에 의해서 만들어진 객체 ‘인스턴스’

</aside>


<br></br>
Daily Quiz

1.

```java
// for문을 이용해서 a배열의 값을 b배열로 복사해보세요.
        int[][] a = {{1, 2, 3}, {4, 5, 6}};
        int[][] b = new int[3][3];

        // for문 작성하는 부분
        for(int i=0; i<a.length; i++){
            for(int j=0; j<a[i].length; j++){
                b[i][j] = a[i][j];
            }
        }

        // a배열과 b배열 출력
        for (int i = 0; i < a.length; i++) {
            for (int j = 0; j < a[i].length; j++) {
                System.out.println("a[" + i + "][" + j + "]: " + a[i][j]);
                System.out.println("b[" + i + "][" + j + "]: " + b[i][j]);
            }
        }
```

2.

```java
// for문을 이용하여 배열에 있는 숫자들의 최대값과 평균을 구하세요.
        int[] array = {12, 4, 7, 20, 1};

        // 코드 작성하는 부분
        int max = array[0];
        int min = array[0];

        for(int i =0; i<array.length; i++){

            if(max < array[i]){
                max = array[i];
            }

            if(min > array[i]){
                min = array[i];
            }
        }

        int avg = (max + min)/2;
        
        // 결과 출력 (최대값: max, 평균: avg)
        System.out.println(max);
        System.out.println(avg);
```

3.

```java
for(int i=1; i<=20; i++){
            if(i % 2 == 0){
                System.out.println(i);
            }
        }
```
