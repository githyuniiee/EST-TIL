## ERD

- ERD는 Entity-Relationship Diagram(개체-관계 다이어그램)의 약자
- 실제 데이터베이스를 구현하기 전에 데이터 요구 사항을 이해하고 문서화하는데 사용

## ERD의 구성 요소

### **1. 개체(Entity)**

개체는 고유하게 식별할 수 있는 사물, 개념, 사건 등을 의미

개체는 데이터베이스에서 테이블로 표현

### **2. 속성(Attribute)**

속성은 개체의 특징이나 성질

하나의 개체는 여러 개의 속성을 가질 수 있음

속성은 데이터베이스에서 테이블의 column(열)로 표현

### **3. 관계(Relationship)**

관계는 개체 간의 연결

관계에는 일대일(1:1), 일대다(1:N), 다대다(N:M) 유형


## 관계(Relationship) 표현 방법

관계에는 일대일(1:1), 일대다(1:N), 다대다(N:M) 유형

### 1. 일대일(1:1) 관계

학생(student)과 신체정보(physical_info)는 일대일 관계

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/4d864ea8-17f9-42ac-a720-75c367c6e691)


### 2. 일대다(1:N) 관계

한 개체가 다른 여러 개체와 연결

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/3e7b9832-b04f-42f0-9819-402f3185d37b)


### 3. 다대다(N:M) 관계

여러 개체가 여러 개체와 연결

제품(product)과 제조업체(manufacturer)는 다대다 관계라고 할 수 있습니다.

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/64b7c1f3-ff1a-4f31-a0e6-6bece92eefaf)
