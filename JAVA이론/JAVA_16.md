JAVA_15 관련 Quiz

### 

### 1. 람다식에 대한 설명으로 틀린것은?

1) 람다식은 함수형 인터페이스의 익명 구현 객체를 생성한다.

2) 매개 변수가 없을 경우 ( ) → { … } 형태로 작성한다.

3) (x, y) → { return x + y; }는 (x, y) → x + y;로 바꿀 수 있다.

`4) @FunctionalInterface가 기술된 인터페이스만 람다식으로 표현이 가능하다.`

⇒ @FunctionalInterface 선택 사항임, 애노테이션 이용할 경우 컴파일러가 함수형 인터페이스의 추상 메서드가 1개라는 것을 인지

### 2. 메소드 참조에 대한 설명으로 틀린 것은?

1) 메소드 참조는 함수적 인터페이스의 익명 구현 객체를 생성한다.

2) 인스턴스 메소드는 “참조변수::메소드”로 기술한다.

3) 정적 메소드는 “클래스::메소드”로 기술한다.

`4) 생성자 참조인 “클래스::new”는 매개 변수가 없는 디폴트 생성자만 호출한다.`

⇒ 매개 변수가 있는 생성자 또한 호출 가능, 함수형 인터페이스 타입을 통해 매개변수가 있는지 확인 할 수 있음

### 3. 잘못 작성한 람다식은?

1)  a → a + 3

`2) a, b → a * b`

3) x → System.out.println(x/5)

4) (x, y) → Math.max(x, y)

⇒ (a,b) → a*b 로 작성해야, 함 매개 변수가 하나인 경우만 괄호 생략 가능

추가) 4번 (x,y) → Math::max 로 변경 가능

### 4. 다음 코드는 컴파일 에러가 발생합니다. 그 이유는?

```java
public class LambdaExample {
    public static int method(int x, int y) {
        IntSupplier supplier = () -> {
            x *= 10;
            int result = x + y;
            return result;
        };
        int result = supplier.getAsInt();
        return result;
    }

    public static void main(String[] args) {
        System.out.println(method(3, 5));
    }
}
```

⇒ 람다식 안에서는 `외부 메서드의 매개 변수는 final의 특징`을 지니고 있어 변경이 불가능하다. (값 변경 또는 재할당 불가능) x *= 10; 값 변경 불가능!

### **5. 다음은 배열 항목 중 최대값 또는 최소값을 찾는 코드입니다. maxOrMin() 메소드의 매개값을 람다식으로 기술해보세요.**

```java
public class LambdaExample_5 {
   private static int[] scores = {10, 50, 3};

    public static int maxOrMin(IntBinaryOperator operator) {
        int result = scores[0];
        for (int score : scores) {
            result = operator.applyAsInt(result, score);
        }
        return result;
    }

    public static void main(String[] args) {
        int max = maxOrMin(

                //최값 얻기 구현
                Math::max

        );
        System.out.println("최대값 : " + max);

        int min = maxOrMin(
                //최소값 얻기 구현
                Math::min
        );
        System.out.println("최소값: " + min);
    }
}

최대값 : 50
최소값: 3
```

### 6. 다음은 학생의 영어 평균 점수와 수학 평균 점수를 계산하는 코드입니다. avg() 메소드를 선언해보세요.

```java
public class Quiz6 {
    private static Student[] students = {
            new Student("홍길동", 90, 96),
            new Student("저팔계", 95, 93)
    };

    /*  avg() 메소드 작성
     */
    public static double avg(int score){

       //Input, Output 존재 => Function
       //s => student자로형, s.getEnglishScore() => Integer
       public static double avg(Function<Student, Integer> function){

        int sum = 0;
        for (Student student : students){
            sum += function.apply(student);
        }
        return (double) sum / students.length;

    }

    }

    public static void main(String[] args) {

        //s => student자로형, s.getEnglishScore() => Integer
        double englishAvg = avg( s -> s.getEnglishScore() );
        System.out.println("영어 평균 점수: " + englishAvg);

        double mathAvg = avg( s -> s.getMathScore() );
        System.out.println("수학 평균 점수: " + mathAvg);
    }

    public static class Student {
        private String name;
        private int englishScore;
        private int mathScore;

        public Student(String name, int englishScore, int mathScore) {
            this.name = name;
            this.englishScore = englishScore;
            this.mathScore = mathScore;
        }

        public String getName() {
            return name;
        }

        public int getEnglishScore() {
            return englishScore;
        }

        public int getMathScore() {
            return mathScore;
        }
    }
}
```

### 7. 6번의 main() 메소드에서 avg() 호출할 때 매개값으로 준 람다식을 메소드 참조로 변경해보세요.

```java
double englishAvg = average( s -> s.getEnglishScore() );
-> double englishAvg = avg (Student::getEnglishScore);

double mathAvg = average( s -> s.getMathScore() );
-> double mathAvg = avg (Student::getMathScore);

클래스명::메소드명
```
<br></br>
## 매핑 - map, flatMap

map 메소드는 스트림의 요소를 하나씩 특정 값으로 변환

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/7fe10c58-c001-4a60-ad2b-61e7d74e0f57)


map 메소드 이용한 대문자 변경

[새로운 스트림 객체로 반환]

```java
List<String> list = Arrays.asList("a", "b", "c", "d", "e");

        list.stream()
                .map(x -> x.toUpperCase())
                .forEach(System.out::println);
```

flatMap

map과 마찬가지로 스트림의 요소들을 다른 값으로 대체하는 것은 같지만, 대체하는 값이 스트림일 경우에 flatMap을 사용

2차원배열도 flat하게 해줌

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/c131fd1b-650a-4e22-add9-f9dbd140871d)

<br></br>
## 정렬 - sorted

스트림의 요소들을 정렬하기 위해 사요하는 메소드

Comparator를 이용하면 원하는 방식으로 정렬 가능

```java
List<Integer> list = Arrays.asList(12, 4, 2, 8, 11);

// [2, 4, 8, 11, 12]
list.stream()
	.sorted()
	.forEach(System.out::println);
```

```java
List<String> list = Arrays.asList("e", "a", "c", "z", "d");

// [z, e, d, c, a]
list.stream()
	.sorted(Comparator.reverseOrder())  // 역순 정렬
	.forEach(System.out::println);
```
<br></br>
## 루핑

peek

- 그냥 확인해본다는 단어 뜻처럼 특정 결과를 반환하지 않음

```java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);

int sum = list.stream()
			.mapToInt(n -> n)
			.filter(n -> n % 2 == 0)
			.peek(n -> System.out.println(n))   // [2, 4]
			.sum();  // sum을 사용하지 않으면 peek은 동작하지 않음
			
System.out.println(sum);    // 6
```

forEach

- 픽과 다르게 결과 단계에서 사용하는 메소드, sum과 같은 결과 메소드와 중복해서 사용 X

```java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);

list.stream()
	.mapToInt(n -> n)
	.filter(n -> n % 2 == 0)
	.forEach(n -> System.out.println(n));
```
<br></br>
## 수집 - collect()

```java
List<Integer> list = Arrays.asList(1, 2, 3, 4, 5);

Set<Integer> set = list.stream()
							.filter(n -> n % 2 == 1)
							.collect(Collectors.toCollection(HashSet::new));
							
set.stream().forEach(System.out::println);  // {1, 3, 5}
```

| Collectors 정적 메소드 | 설명 |
| --- | --- |
| toList | 요소를 List에 저장 |
| toSet | 요소를 Set에 저장 |
| toCollection | 요소를 특정 컬렉션에 저장 |
| toMap | 요소를 Map에 저장 |

<br></br>
## Optional

Optinal은 null을 포함한 모든 데이터를 저장할 수 있는 Wrapper 클래스

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/31dd6f8c-40d9-4cb1-b573-db2bcfa149b6)


| 메소드 | 설명 |
| --- | --- |
| static <T> Optional<T> empty() | 아무런 값도 가지지 않는 비어있는 Optional 객체를 반환함. |
| static <T> Optional<T> of(T value) | null이 아닌 명시된 값을 가지는 Optional 객체를 반환함. |
| static <T> Optional<T> ofNullable(T value) | 명시된 값이 null이 아니면 명시된 값을 가지는 Optional 객체를 반환하며, 명시된 값이 null이면 비어있는 Optional 객체를 반환함. //null허용 |
