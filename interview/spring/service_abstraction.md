<details> <summary> 서비스 추상화(Service Abstraction)란 무엇이며 왜 필요한가요?</summary>
<div markdown="1"> 서비스 추상화는 특정 기술의 세부 구현에 종속되지 않도록 인터페이스를 통해 로우레벨 기술을 분리하는 것을 말합니다. 이를 통해 비즈니스 로직을 변경하지 않고도 환경이나 기술(예: DB 연결 방식, 메일 서버 등)을 자유롭게 바꿀 수 있으며, 테스트 작성이 용이해집니다.
</div> </details>

<details> <summary> PlatformTransactionManager 인터페이스의 역할은 무엇인가요?</summary> <div markdown="1"> 
스프링이 제공하는 트랜잭션 추상화의 핵심 인터페이스입니다. 
JDBC(DataSourceTransactionManager), JPA(JpaTransactionManager) 등 각 기술에 맞는 트랜잭션 관리 방식을 통일된 방법(getTransaction, commit, rollback)으로 사용할 수 있게 해줍니다. </div> </details>

<details> <summary> 트랜잭션 동기화(Transaction Synchronization)란 무엇인가요?</summary> <div markdown="1"> 트랜잭션을 시작하기 위해 생성된 커넥션 객체를 특별한 저장소(ThreadLocal)에 보관해두고, 이후에 호출되는 DAO들이 동일한 커넥션을 사용할 수 있도록 관리하는 메커니즘입니다. 이를 통해 파라미터로 커넥션을 일일이 전달하지 않아도 트랜잭션을 유지할 수 있습니다. </div> </details>

<details> <summary> 테스트 대역 중 '목 오브젝트(Mock Object)'와 '스텁(Stub)'의 차이는 무엇인가요?</summary> <div markdown="1"> '스텁'은 호출 시 미리 준비된 데이터를 반환하여 테스트가 중단되지 않게 돕는 역할에 집중합니다. 반면, '목 오브젝트'는 스텁의 기능을 포함하면서도, 특정 메서드가 실제로 호출되었는지, 몇 번 호출되었는지 등 '행위 검증'을 수행하기 위해 사용됩니다. </div> </details>

<details> <summary> 단일 책임 원칙(SRP) 관점에서 5장의 의의는 무엇인가요?</summary> <div markdown="1"> 사용자 관리라는 '비즈니스 로직'과 트랜잭션/메일 발송이라는 '인프라 로직'을 분리함으로써, 하나의 클래스가 하나의 책임만 갖도록 설계하는 과정을 보여줍니다. 이는 코드의 응집도를 높이고 변경에 강한 구조를 만듭니다. </div> </details>