에러 : 프로그램 코드, 하드웨어 물리 장비 등에 의해서 수습될 수 없는 심긱한 오류

예외 : 프로그램 코드에 의해서 수습될 수 있는 다소 미약한 오류

## 예외 처리

- 프로그램 실행 시 발생할 수 있는 예외의 발생에 대비한 코드를 작성하는 것
- 목적 : 프로그램의 비정상 종료를 막고, `정상적인 실행상태를 유지`하는 것

### 프로그램 오류

- 컴파일 에러 : 컴파일 과정에서 컴파일러가 이해하지 못하는 문법적 오류 ⇒ 신택스 에러, 타입체크 에러
- 런타임 에러 : 컴파일 완료된 이후 어플리케이션이 작동시에 발생하는 에러 ⇒ 0 나누기 에러, 널 참조 오류, 메모리 부족 오류…
- 논리적 오류

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/36b30279-ce1e-4cff-bf57-770ab0d3061b)

예외의 최상위 계층 ⇒ Throwable

Error - OutOfMemory ⇒ 개발자가 처리할 수 없는 부분

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/9b442d95-628b-44ef-bd37-790371584485)


Excetpion : 컴파일러가 체크하는 checked exception

RuntimeException : 컴파일러가 체크하지 않는 unchecked exception

ArithmeticException ⇒ 산술적 문제에 따른 오류

## 예외처리 방법

- throw로 던지기 (메소드 뒤쪽 선언부로 선언하기)
- try catch로 예외처리 해주기 (메소드 안에서 처리)

⭐️ 다중 catch문 작성시 주의사항

```sql
상위 예외클래스가 하위 예외 클래스보다 아래쪽에 위치해야함
try {
	(ArrayIndexOutOfBoundsException 발생)

	(NumberFormatException 발생)
} catch(Exception e) {
	예외처리1
} catch(ArrayIndexOutOfBoundsException e) {
	예외처리2    // 컴파일 오류
}
```

### finally

어떤 예외가 발생하더라도 반드시 실행되는 부분 → finally
