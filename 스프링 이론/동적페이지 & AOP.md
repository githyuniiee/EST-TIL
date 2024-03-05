## 동적 페이지 구현

요청 ~ 응답까지의 흐름 절차

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/33c0cbd6-58e9-47e8-902b-666db0d64a15)


- 모든 요청을 수신하는 프론트 컨트롤러인 DispatcherServlet이 클라이언트로부터 요청을 수신
- DispatcherServlet이 컨트롤러의 요청 핸들러 메서드를 호출
- 컨트롤러는 비즈니스 로직 처리를 호출하고, 처리 결과를 받음
- 처리 결과를 모델로 설정하고 뷰의 이름으로 반환
- 반환된 뷰 이름을 받아서 DispatcherServlet이 뷰 이름에 해당하는 뷰를 화면에 처리할 수 있도록 연결
- 클라이언트가 응답을 받고 브라우저에 화면이 표시

<br></br>
## 제어의 역전(IoC)과 의존성 주입 (DI)

- IoC(Inversion of Control) : 제어의 역전
    
    필요한 객체를 직접 생성하거나 제어하는 것이 아니라 외부에서 관리하는 객체를 가져와서 사용
    
    ```java
    //기존 자바 코드
    public class A {
    		B b = new B();  // 클래스 A 에서 필요한 B 객체를, new 키워드를 사용하여 생성
    }
    
    //제어의 역전
    /* 스프링 컨테이너가 객체를 관리하는 방식 예 */
    public class A {
    		private B b;    // 코드에서 객체를 생성하지 않고, 어디선가 받아온 객체를 b에 할당
    }
    ```
    
- 의존성 주입 (DI) : Dependency Injection
    
    어떤 클래스가 다른 클래스에 의존하기 위해 주입
    
    ```java
    public class A {
    	@Autowired //스프링 컨테이너에 빈 주입
    	B b;
    }
    ```
    
    스프링은, `클래스 A에서 B 객체를 쓰고 싶은 경우에 직접 객체를 생성하는게 아니라 스프링 컨테이너에서 객체를 주입받아 사용` → IoC/DI 개념
    
<br></br>
## 빈과 스프링 컨테이너

스프링 컨테이너 : 빈을 생성하고 관리

- 빈이 생성/소멸되는 모든 생명주기를 관리
- 개발자가 @Autowired, 혹은 생성자를 사용하여 빈을 주입받을 수 있게 DI 지원

`빈 : 스프링 컨테이너가 관리하고 생성하는 객체`

```java
public class A {
	@Autowired
	B b; // B 가 바로 빈
}

@Component  // 클래스 MyBean을 스프링 컨테이너에 등록 
public class MyBean {
}
```
<br></br>
## 관점 지향 프로그래밍 (AOP)

- Aspect Oriented Programming
- 코드를 수정하지 않으면서 공통 기능의 구현을 추가하는 것
- 스프링 AOP는 프록시 객체를 자동으로 만들어줌
- 핵심 관심사항 코드에만 집중할 수 있을 뿐만 아니라, 프로그램의 변경과 확장에도 유연하게 대응 가능
- 스프링 AOP는 Bean에서만 동작

ex)

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/4d7e1ad1-7c8e-4d2a-8a04-b798093a7ef7)

```java
package hello.hellospring.aop;

import org.aspectj.lang.ProceedingJoinPoint;
import org.aspectj.lang.annotation.Around;
import org.aspectj.lang.annotation.Aspect;
import org.springframework.stereotype.Component;

@Component
@Aspect //여러 객체에 공통으로 적용되는 기능
public class TimeLoggingAop {

    @Around("execution(* hello.hellospring..*(..))")
    public Object execute(ProceedingJoinPoint joinPoint) throws Throwable {
        long startTimeMs = System.currentTimeMillis();
        System.out.println("START: " + joinPoint.toString());
        try {
            return joinPoint.proceed();
        } finally {
            long finishTimeMs = System.currentTimeMillis();
            long timeMs = finishTimeMs - startTimeMs;
            System.out.println("END: " + joinPoint.toString()+ " " + timeMs + "ms"); 
				}
		}

}

```
