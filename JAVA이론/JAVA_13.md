## Collection

- Colliection : 자바에서 제공해주는 인터페이스

배열은 쉽게 생성하고 사용할 수 있지만, 저장할 수 있는 객체 수가 배열을 생성할 때 결정되기 때문에 불특정 다수의 객체를 저장하기에는 문제가 있음 !

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/0094e8dc-aa8e-4041-96a7-589ef7674a0c)


`Collection : 배열과 같이 Index로 요소가 관리되거나 요소 자체만을 관리` 

`Map : Key-Value 쌍으로 요소가 관리`

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/2278b203-46c4-44ba-a0d0-b7eaf5d68694)

## List- ArrayList, LinkedList

List는 객체를 일렬로 늘어놓은 구조

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/ef4d7e13-7585-4d94-828d-212f5ae251f8)


### ArrayList

배열은 생성할 때 크기가 고정되고 사용 중에 크기를 변경할 수 없지만, ArrayList는 저장 용량(capacity)을 초과한 객체들이 들어오면 자동적으로 저장 용량(capacity)이 늘어남

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/d45d98de-1168-48ac-b67a-770ec2e02d5b)


ArrayList에서 특정 인덱스의 객체를 **제거**하면 바로 뒤 인덱스부터 마지막 인덱스까지 모두 앞으로 1씩 당겨짐. 마찬가지로 특정 인덱스에 객체를 삽입하면 해당 인덱스부터 마지막 인덱스까지 모두 1씩 밀려남

⇒  빈번한 객체 삭제와 삽입이 일어나는 곳에서는 ArrayList를 사용하는 것이 바람직하지 않음

### LinkedList

ArrayList는 내부 배열에 객체를 저장해서 **인덱스**로 관리하지만, LinkedList는 인접 참조를 링크해서 체인처럼 관리

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/2990cfac-d841-4fc9-bff5-0c899d481738)


LinkedList에서 특정 인덱스의 객체를 제거하면 앞뒤 링크만 변경되고 나머지 링크는 변경되지 않음

<aside>
💡 중간에 추가 또는 삭제할 경우는 앞뒤 링크만 변경하면 되는 LinkedList가 더 빠름
ArrayList는 뒤쪽 인덱스들을 모두 1씩 증가 또는 감소 시키는 시간이 필요하므로 처리 속도가 느립니다.

</aside>

## Set - HashSet

 List 컬렉션은 저장 순서를 유지하지만, **Set 컬렉션은 저장 순서가 유지되지 않습니다.** 또한 **객체를 중복해서 저장할 수 없다는 큰 특징**

⇒ index 단위로 데이터를 관리하지 않음

`HashSet은 객체를 저장하기 전에 먼저 객체의 hashCode() 메소드를 호출해서 해시코드를 얻어냄` 

그리고 이미 저장되어있던 객체들의 해시코드와 비교하지요. `만약 동일한 해시코드가 있다면 다시 equals() 메소드로 두 객체를 비교해서 true가 나오면 동일한 객체로 판단하고 중복 저장하지 않습니다.`

forEach구문에 Set을 넣을 때, 당시 Set의 요소들로 이터레이터를 만들기 때문에 forEach의 remove 사용할 경우, 에러 남 ! `삭제 되었으면 이터레이터의 크기가 변경되는데, foreach에서는 삭제 전의 이터레이터를 가지고있음`

⇒ **`for-each`** 문법은 내부적으로 반복자를 사용하며, 동시에 컬렉션을 수정하는 작업은 반복자를 사용하는 동안 허용되지 않음!!

```java
public class HashSetExample {
    public static void main(String[] args) {
        //객체 생성
        Set<String> stringSet = new HashSet<>();
        stringSet.add("요소1");
        stringSet.add("요소2");
        stringSet.add("요소3");
        stringSet.add("요소1");

        System.out.println(stringSet);

        Iterator<String> iterator = stringSet.iterator();
        while(iterator.hasNext()){
            System.out.println(iterator.next());
        }

        for(String str : stringSet){ //잘못된 코드
            stringSet.remove(str);   
        }
    }
}
```

```java
import java.util.HashSet;
import java.util.Set;

public class HashSetExample2 {
	public static void main(String[] args) {
		Set<Member> set = new HashSet<>();

		set.add(new Member("홍길동", 30));
		set.add(new Member("홍길동", 30));

		System.out.println("총 객체수: " + set.size());   //2개
	}
}

public class Member {
	String name;
	int age;

	public Member(String name, int age) {
		this.name = name;
		this.age = age;
	}
}
```

두 번 중복으로 삽입한 Member 인스턴스는 내부 데이터가 동일하지만, 인스턴스가 다르기 때문에 객체 둘 다 저장

`의도한대로 size가 1로 나오기 위해서는 아래와 같은 hashCode와 equals 재정의가 필요` 

```java
public class Member {
	String name;
	int age;

	public Member(String name, int age) {
		this.name = name;
		this.age = age;
	}

	@Override
	public int hashCode() {
		return name.hashCode() + age;
	}

	@Override
	public boolean equals(Object obj) {
		if (obj instanceof Member) {
			Member member = (Member)obj;
			return member.name.equals(this.name) && member.age == this.age;
		} else {
			return false;
		}
	}
}
```

## Map - HashMap, Hashtable

![image](https://github.com/githyuniiee/EST-TIL/assets/109260733/c5daa89c-f80d-4ee8-b916-ea769a8e4ed9)

Map 컬렉션은 키(key)와 값(value)으로 구성된 객체를 저장하는 구조

여기서 키와 값은 모두 객체

키는 중복될 수 없지만 값은 중복 저장될 수 있음

HahMap 실습

```java
public class HashMapExample {
    public static void main(String[] args) {

        Map<String, Integer> hashmap = new HashMap<>();

        hashmap.put("key1", 1);
        hashmap.put("key2", 2);
        hashmap.put("key3", 3);
        System.out.println(hashmap);

        Integer v = hashmap.getOrDefault("key", 0); //0 출력
        Integer v2 = hashmap.get("key"); //null 출력
        System.out.println(v);
        System.out.println(v2);

        //객체 검색
        boolean isContains = hashmap.containsKey("없는Key");
        System.out.println("isContains = " + isContains);

        boolean containsValue = hashmap.containsValue(3);
        System.out.println("containsValue = " + containsValue);

        Set<String> keySet = hashmap.keySet();
        System.out.println(keySet);

        Iterator<String> iterator = hashmap.keySet().iterator();
        while (iterator.hasNext()) {
            String key = iterator.next();
            Integer value = hashmap.get(key);
            System.out.println(key + ":" + value);
        }

        Set<Map.Entry<String, Integer>> entrySet = hashmap.entrySet();
        for (Map.Entry<String, Integer> entry : entrySet) {
            entry.getKey();
            entry.getValue();
        }
    }
}
```
