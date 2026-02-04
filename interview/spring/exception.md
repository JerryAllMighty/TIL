<details>
<summary>예외 전환이란 무엇인가요?</summary>
<div markdown="1">
서로 다른 계층·기술마다 제각각인 로우 레벨 예외를, 상위 계층에서 이해하고 공통 처리하기 쉬운 추상적인 예외로 통일하기 위해 나온 개념입니다
</div>
</details>


<details>
<summary>예외 포장이란 무엇인가요?</summary>
<div markdown="1">
원래 발생한 예외의 원인·스택트레이스를 보존하면서, 더 의미 있는 새 예외 타입으로 감싸 전달해 디버깅과 예외 처리를 동시에 쉽게 하려는 시도입니다.
</div>
</details>


<details>
<summary>예외 전환과 예외 포장의 차이는 무엇인가요?</summary>
<div markdown="1">
단순히 타입만 바꾸는 것이 아니라, 원인 예외까지 함께 유지하며 계층 간 의미를 바꾸어 전달해 “원인 정보 손실” 문제를 줄이려는 구분입니다.
</div>
</details>

<details>
<summary>모든 예외를 DataAccessException으로 전환하는 것이 항상 좋은가요?</summary>
<div markdown="1">
데이터 접근 예외와 도메인/비즈니스 예외를 구분하지 않으면 처리 전략을 나누기 어려워져, 예외 의미를 잃는 문제를 막으려고 “항상 그렇진 않다”는 기준이 생겼습니다.
</div>
</details>


<details>
<summary>서비스 계층에서 예외를 어떻게 다루는 것이 이상적인가요?</summary>
<div markdown="1">
서비스가 인프라 기술에 끌려다니지 않고, “복구 가능/불가능”을 구분해 도메인 관점에서 예외를 다루도록 하기 위해 명확한 예외 처리 전략이 필요해졌습니다.
</div>
</details>


<details>
<summary>체크 예외보다 런타임 예외가 선호되는 이유는 무엇인가요?</summary>
<div markdown="1">
호출자가 복구할 수 없는 예외까지 체크 예외로 강제해 코드 곳곳이 throws/catch로 오염되는 문제를 줄이기 위해 런타임 예외 중심 전략이 등장했습니다.
</div>
</details>



<details>
<summary>JdbcTemplate은 어떤 예외 처리 전략을 따르나요?</summary>
<div markdown="1">
JDBC SQLException이 모든 메서드 시그니처에 새어 나와 계층 전체를 더럽히는 문제를, 런타임 예외 추상화로 숨기고 통일하기 위해 DataAccessException 전환 전략을 씁니다.
</div>
</details>


<details>
<summary>JdbcTemplate이 예외를 런타임 예외로 전환하는 이유는 무엇인가요?</summary>
<div markdown="1">
매 레이어마다 불필요한 체크 예외 처리를 강제하지 않고도, 공통 예외 추상화를 유지하면서 코드 단순성을 높이기 위해서입니다.
</div>
</details>


<details>
<summary>SQLState 기반 예외 분류가 신뢰하기 어려운 이유는 무엇인가요?</summary>
<div markdown="1">
DB 벤더마다 SQLState 사용이 제각각이라 같은 코드라도 의미가 달리 해석되는 문제 때문에, 보다 안정적인 에러 코드 매핑 전략이 필요해졌습니다.
</div>
</details>


<details>
<summary>DataAccessException이란 무엇인가요?</summary>
<div markdown="1">
JDBC, JPA, Hibernate 등 데이터 접근 기술마다 다른 예외들을, 상위 계층에서 기술 독립적으로 다루기 위해 공통 부모 타입이 필요해서 나온 추상 클래스입니다.
</div>
</details>


<details>
<summary>DataAccessException 계층 구조의 장점은 무엇인가요?</summary>
<div markdown="1">
“데이터 무결성 위반, 락 실패, 리소스 실패” 등 다양한 상황을 한 타입으로 뭉개지 않고, 기술에 독립적인 의미 단위로 세분화해 다른 대응 전략을 가질 수 있게 하려는 구조입니다.
</div>
</details>

<details>
<summary>DataAccessException의 하위 예외에는 어떤 것들이 있나요?</summary>
<div markdown="1">
각각의 전형적인 DB 오류 상황(제약 위반, 중복 키, 락 실패, 낙관적 락 충돌 등)을 구분해, 서비스/컨트롤러에서 상황별로 다르게 처리할 수 있게 하려는 목적입니다.
</div>
</details>


<details>
<summary>DataAccessException과 트랜잭션은 어떻게 연관되나요?</summary>
<div markdown="1">
데이터 액세스 실패 시 “자동 롤백 기준”을 일관되게 정하고, 트랜잭션 경계를 구현 기술에 상관없이 관리하기 위해 공통 런타임 예외 계층이 필요했습니다.
</div>
</details>

<details>
<summary>같은 예외라도 롤백되면 안 되는 경우는 어떻게 처리하나요?</summary>
<div markdown="1">
모든 예외를 무조건 롤백하면, 일부 예외는 비즈니스적으로 처리해야 하는 상황(알림, 재시도 등)을 표현하기 어렵기 때문에 예외별 롤백 정책을 분리하는 메커니즘이 나왔습니다.
</div>
</details>


<details>
<summary>낙관적인 락킹이란 무엇인가요?</summary>
<div markdown="1">
낙관적인 락킹은 데이터 충돌이 자주 발생하지 않는다는 가정 하에,
락을 미리 걸지 않고 수정 시점에 충돌 여부를 검사하는 동시성 제어 방식이다.
</div>
</details>


<details>
<summary>낙관적인 락킹은 어떻게 구현하나요?</summary>
<div markdown="1">
동시에 수정된 데이터를 감지하지 못하는 “마지막 커밋 우승자” 문제를 막기 위해, 버전 필드 등으로 변경 여부를 검증하는 체크 메커니즘을 추가한 구현입니다.
</div>
</details>


<details>
<summary>낙관적인 락킹의 장점과 단점은 무엇인가요?</summary>
<div markdown="1">
락 비용과 데드락은 줄이지만, 충돌 시 예외·재시도 로직을 애플리케이션이 직접 처리해야 하는 부담이 생기기 때문에, 이 트레이드오프를 관리하려는 논의입니다.
</div>
</details>


<details>
<summary>낙관적 락킹과 비관적 락킹은 언제 각각 적합한가요?</summary>
<div markdown="1">
“충돌 가능성 vs 락 비용”이라는 상반된 요구를 상황에 따라 선택할 수 있게, 두 가지 상이한 락 전략의 사용 기준을 정리하기 위해 나온 구분입니다.
</div>
</details>


<details>
<summary>낙관적 락킹 실패 시 애플리케이션은 어떻게 대응해야 하나요?</summary>
<div markdown="1">
단순 예외 발생만으로는 사용자 경험이 나빠지고 데이터 손실 위험이 있으므로, “재시도, 최신 데이터 표시, 병합” 같은 후속 전략을 명시적으로 설계하기 위해 대응 패턴이 필요해졌습니다.
</div>
</details>
