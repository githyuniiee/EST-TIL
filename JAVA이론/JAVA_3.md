### 숫자 → 문자 형변환

**Int → String**

- `Integer.toString() // NullPointerException 발생`
- `String.valueOf()  //문자열 ‘’null’’로 변환됨`
- `변수 + “” // 정수 값에 빈 문자열 더해 문자열 합치기 연산`

### 연산 방향과 우선순위

### 우선 순위

단항 > 이항 > 삼항

산술 > 비교 > 논리 > 대입 연산자

| 연산자 | 연산 방향 | 우선 순위 |
| --- | --- | --- |
| 증감(++, --), 부호(+, -), 비트(~), 논리(!) | ← | 높음 |
| 산술(*, /, %) | → |  |
| 산술(+, -) | → |  |
| 쉬프트(<<, >>, >>>) | → |  |
| 비교(<, >, <=, >=) | → |  |
| 비교(==, !=) | → |  |
| 논리(&) | → |  |
| 논리(^) | → |  |
| 논리(|) | → |  |
| 논리(&&) | → |  |
| 논리(||) | → |  |
| 조건(?:) | → |  |
| 대입(=, +=, -=, *=, /=, %=, &=, ^=, …) | ← | 낮음 |

### 이항 연산자

- String 타입의 문자열은 대소 비교를 할 수 없고, 동등 비교는 할 수 있음

```java
String str1 = "Hello";
String str2 = "Hello";
String str3 = new String("Hello");

System.out.println(str1.equals(str2));  // true
System.out.println(str1.equals(str3));  // true
```

### 삼항 연산자

아래 연산식에서 ? 앞의 조건식에 따라 콜론( : ) 앞 뒤의 연산자가 선택되는 `조건 연산식`

### 비트 연산자 
![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/5b5654c6-96d5-4720-b02f-e51ebf90dfb1)

### 조건문 / 반복문

if문, switch/case문, for문
