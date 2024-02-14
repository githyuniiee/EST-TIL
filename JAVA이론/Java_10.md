`제네릭 : 데이터의 타입을 일반화 하는 것`

### 제네릭 타입

(class<T>, interface<T>)

- 타입 안정성
- 형변환을 해주지 않아도 됨
<br></br>
## 제한된 타입 파라미터

- 타입 파라미터에 구체적인 타입을 제한하는 기능
- 숫자를 연산하는 제네릭 메소드라면, 이 메소드는 매개값으로 Number타입 혹은 Byte, Short, Integer, Long, Double타입의 인스턴스만 가져야 함

예시

```java
public class Util {
    public static <T extends Number> int compare(T t1, T t2) {
        double value1 = t1.doubleValue();
        double value2 = t2.doubleValue();
        //value1이 작다면 -1, value1이 크다면 1, 같다면 0
        return Double.compare(value1, value2);
    }
}
```

```java
public class BoundedTypeExample {
    public static void main(String[] args) {
        int result = Util.compare(1,2); //int -> Integer
        System.out.println(result);

        int result2 = Util.compare(4.5, 4.5); //double ->Double
        System.out.println(result2);
    }
}
```
<br></br>
## 와일드카드 타입 <?>, <?extends ..>, <?super ..>

- ?를 일반적으로 와일드카드라고 부름
- 제네릭타입<?> : 타입 파라미터를 대치하는 구체적인 타입으로 모든 클래스나 인터페이스 타입이 올 수 있음
- 제네릭타입<? extends 상위타입> : 타입 파라미터를 대치하는 구체적인 타입으로 상위 타입이나 하위 타입만 올 수 있음
- 제네릭타입 <? super 하위타입> : 타입 파라미터를 대치하는 구체적인 타입으로 하위 타입이나 상위 타입이 올 수 있음

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/47583a1a-d39e-481c-979a-e1a4b63ec7c0)


- Course<?> : 수강생은 모든 타입(Person, Worker, Student, HighStudent)이 될 수 있음 ⇒ 제한 없음
- Course<? extends Student> : 수강생은 Student와 HighStudent만 될 수 있음 ⇒ 상위 클래스 제한
- Course<? super Worker> : 수강생은 Worker와 Person만 될 수 있음 ⇒ 하위 클래스 제한
- 제네릭은 suepr X

<br></br>
## 제네릭 타입의 상속과 구현

상속 예제

제네릭 타입도 다른 타입과 마찬가지로 부모 클래스가 될 수 있음

```java
package chapter10.inherit;

public class Product<T,M> {

    private T kind;
    private M model;

    public Product(T kind, M model){
        this.kind = kind;
        this.model = model;
    }

    public T getKind() {
        return kind;
    }

    public M getModel() {
        return model;
    }

}

package chapter10.inherit;

public class ChildProduct <T, M, C> extends Product<T,M>{

    private C company;

    public ChildProduct(T kind, M model, C company) {
        super(kind, model);
        this.company = company;
    }

    public C getCompany(){
        return company;
    }
}

package chapter10.inherit;

public class TV {
}

package chapter10.inherit;

public class ChildProductExample {
    public static void main(String[] args) {
        ChildProduct<TV, String, String> product = new ChildProduct<>(new TV(), "smartTV", "samsung");

        System.out.println(product.getKind());
        System.out.println(product.getModel());
        System.out.println(product.getCompany());

    }
}
```

<br></br>
### Quiz.

## 제네릭에 대한 설명으로 틀린 것은 무엇입니까?

1) 컴파일시 강한 타입 체크를 할 수 있다.

2) 타입 변환(casting)을 제거한다.

3) 제네릭 타입은 타입 파라미터를 가지는 제네릭 클래스와 인터페이스를 말한다.

4) 제네릭 메소드는 리턴 타입으로 타입 파라미터를 가질 수 없다.

⇒ 4번 제네릭은 리턴 타입으로 타입 파라미터를 가질 수 있음
