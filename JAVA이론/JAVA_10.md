예외처리 방법

- throws를 통해 예외 던지기
- try-catch로 본인이 처리

로깅 = 에러 메시지를 기록  ⇒ 오류 트래킹

자바의 라이브러리 SLF4J, Logback, Log4J

<br></br>
## 사용자 정의 예외와 예외발생

자바에서 처리할 수 없는 예외 및 코드의 직관성을 위해 사용 `[어떤 작업을 강제화하고 싶을 때]`

unchecked 예외 (컴파일러가 체크하지 않는)

checked 예외(컴파일러가 체크하는)

사용자 정의 예외 예시

```java
package ch09.account;

public class Account {
    private long balance; //잔액

    public Account() {
        balance = 0;
    }

    public long getBalance() {
        return balance;
    }

    public void deposit(long money) {
        balance += money;
    }

    public void withdraw(long money) throws BalanceInsufficientException{
        if(balance < money){
            throw new BalanceInsufficientException("잔액부족! 현재 잔액: " + balance + ", 출금하고자 하는 금액: " + money);
        }
        balance -= money;
    }
}

public class BalanceInsufficientException extends Exception{
    public BalanceInsufficientException(String message){
        super(message);
    }
}

public class Bank {
    public static void main(String[] args) {
        Account account = new Account();
        account.deposit(2000);
        System.out.println("" + account.getBalance());

        try {
            account.withdraw(3000);
        }catch (BalanceInsufficientException e){
            System.out.println(e.getMessage());
        }
    }
}
```

throw와 throw의 차이

- throw : 메소드 내에서 예외를 발생시키는데 사용됨
- throws : 메소드 선언부에서 사용되며, 호출한 곳에서 예외처리를 하게 시킴

<br></br>
## 예외 트랜잭션 처리 방법

`트랜잭션 : ‘하나의 논리적 기능을 수행하기 위한 작업의 단위’` 

⇒ 하나의 작업을 처리하는 단위

ex) 송금 트랜잭션

⇒ 송금 ‘처리중’

⇒ 송금 계좌에 돈이 빠져나감

⇒ 수금인 계좌에 돈이 채워짐

⇒ 송금 ‘완료’ 상태로 변경

만약 송금 프로세스 중 하나라도 실패하면 송금 전의 상태로 되돌려야 함 → 이렇게 모두 취소하는 행위를 `롤백(rollback)` 이라 함

데이터들의 값이 서로 일관성있게 일치하는 것 ⇒ `데이터 정합성`
