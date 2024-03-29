## 자바의 특징

### ⭐객체 지향 언어

부품에 해당하는 “객체”들을 먼저 만들고 그 부품들을 조립하고 부품들끼리 연결하여 전체 프로그램을 완성하는 기법을 객체지향 프로그래밍(OOP)

이때 사용하는 언어를 “객체 지향 언어”

### ⭐메모리를 자동으로 관리

자바는 개발자가 직접 메모리를 접근할 수 없게 설계되어있으며 메모리는 자바가 직접 관리(Gabage Collector)

### ⭐운영체제에 독립적

자바를 실행하기 위한 가상의 운영체제 역할을 하는 **Java Virtual Machine(JVM)**이 있기 때문에 서로 다른 실행환경을 가진 시스템 간에 프로그램을 옮겨 실행할 수 있음

## JVM 이란

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/f34704df-823b-4fb5-94c7-3f76d24d135e)

**Java Virtual Machine**은 자바를 실행하기 위한 가상 머신입니다. 실 운영체제를 대신해서 자바 프로그램을 실행하는 가상의 운영체제 역할

## 자바 파일 실행 과정

자바 프로그램은 확장자가 .java인 자바 소스 파일을 작성하는 것부터 시작되어 컴파일러로 컴파일하면 확장자가 .class인 바이트 코드가(클래스 파일) 생성

이 클래스 파일은 JVM 에 의해 JVM에서 해석되고 해당 운영체제에 맞게 기계어로 번역됩니다. 

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/1d391835-46c3-44e4-86ff-de5d20cfd23d)


⇒ IntelliJ Run 버튼 하나로 해결 !
