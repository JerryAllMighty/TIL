<details>
<summary>템플릿/콜백 패턴이란 무엇인가요?</summary>
<div markdown="1">
템플릿/콜백 패턴은 변하지 않는 흐름은 템플릿에 두고,
변하는 로직은 콜백으로 분리하는 구조이다.
이를 통해 중복 코드를 제거하고 유연한 확장이 가능해진다.
</div>
</details>

<details>
<summary>템플릿/콜백 패턴과 템플릿 메서드 패턴의 차이는 무엇인가요?</summary>
<div markdown="1">
템플릿 메서드 패턴은 상속을 통해 변하는 부분을 구현하고,
템플릿/콜백 패턴은 합성과 위임을 통해 변하는 로직을 전달한다.
템플릿/콜백 패턴이 더 유연하고 결합도가 낮다.
</div>
</details>

<details>
<summary>템플릿/콜백 패턴이 상속보다 선호되는 이유는 무엇인가요?</summary>
<div markdown="1">
상속은 컴파일 타임에 구조가 고정되고 결합도가 높아진다.
템플릿/콜백은 런타임에 로직을 주입할 수 있어
변경과 테스트에 더 유리하다.
</div>
</details>


<details>
<summary>JdbcTemplate에서 콜백 객체는 상태를 가져도 되나요?</summary>
<div markdown="1">
콜백 객체는 보통 메서드 호출 범위 내에서만 사용되므로
상태를 가져도 되지만,
외부 공유 상태를 가지면 동시성 문제가 발생할 수 있다.
</div>
</details>



<details>
<summary>템플릿/콜백 패턴은 어떤 문제를 해결하나요?</summary>
<div markdown="1">
공통 처리 로직과 개별 처리 로직이 섞여 중복이 발생하는 문제를 해결한다.
변경 가능성이 높은 코드를 외부로 분리해 유지보수성을 높인다.
</div>
</details>


<details>
<summary>JdbcTemplate은 템플릿/콜백 패턴을 어떻게 적용했나요?</summary>
<div markdown="1">
JdbcTemplate이 템플릿 역할을 하고,
StatementCreator나 RowMapper가 콜백 역할을 한다.
리소스 관리와 예외 처리는 템플릿이 담당한다.
</div>
</details>


<details>
<summary>전략 패턴이란 무엇인가요?</summary>
<div markdown="1">
전략 패턴은 동일한 목적을 가진 알고리즘들을 인터페이스로 정의하고,
구현을 분리해 런타임에 교체 가능하도록 만드는 패턴이다.
</div>
</details>


<details>
<summary>전략 패턴과 템플릿/콜백 패턴의 관계는 무엇인가요?</summary>
<div markdown="1">
템플릿/콜백 패턴은 전략 패턴의 특수한 형태로 볼 수 있다.
전략 객체를 익명 클래스나 람다로 전달해
일회성 전략을 간결하게 표현한다.
</div>
</details>


<details>
<summary>전략 패턴의 장점은 무엇인가요?</summary>
<div markdown="1">
조건문 없이 알고리즘을 교체할 수 있고,
OCP를 만족해 새로운 전략 추가 시 기존 코드를 수정하지 않아도 된다.
</div>
</details>

<details>
<summary>전략 패턴을 사용하지 않으면 어떤 코드 냄새가 나타나나요?</summary>
<div markdown="1">
if-else 또는 switch 문이 계속 증가하며,
기능 추가 시 기존 코드를 수정해야 한다.
이는 OCP 위반의 전형적인 신호이다.
</div>
</details>

<details>
<summary>전략 패턴을 과도하게 사용하면 어떤 문제가 생길 수 있나요?</summary>
<div markdown="1">
클래스 수가 과도하게 증가해 구조가 복잡해질 수 있다.
변경 가능성이 실제로 높은 경우에만 적용하는 것이 좋다.
</div>
</details>



<details>
<summary>중첩 클래스란 무엇인가요?</summary>
<div markdown="1">
중첩 클래스는 클래스 내부에 정의된 클래스를 말한다.
외부 클래스와 논리적으로 강하게 결합된 경우 사용된다.
</div>
</details>


<details>
<summary>토비의 스프링 3장에서 중첩 클래스를 사용하는 이유는 무엇인가요?</summary>
<div markdown="1">
템플릿/콜백 구조에서 콜백 구현이
특정 메서드나 클래스에서만 사용되기 때문이다.
중첩 클래스를 사용해 가독성과 응집도를 높인다.
</div>
</details>


<details>
<summary>중첩 클래스의 장점은 무엇인가요?</summary>
<div markdown="1">
관련 있는 코드들을 한 곳에 모을 수 있어 가독성이 좋아지고,
외부에 불필요한 클래스를 노출하지 않아 캡슐화를 강화할 수 있다.
</div>
</details>


<details>
<summary>중첩 클래스의 단점은 무엇인가요?</summary>
<div markdown="1">
구조가 복잡해질 수 있고,
외부 클래스와 강하게 결합되어 재사용성이 떨어질 수 있다.
</div>
</details>


<details>
<summary>중첩 클래스와 익명 클래스의 차이는 무엇인가요?</summary>
<div markdown="1">
중첩 클래스는 이름을 가지며 재사용이 가능하고,
익명 클래스는 일회성 구현에 적합하다.
토비 3장에서는 일회성 콜백 구현에 익명 클래스를 주로 사용한다.
</div>
</details>


<details>
<summary>람다 표현식은 템플릿/콜백 패턴을 어떻게 더 단순하게 만드나요?</summary>
<div markdown="1">
함수형 인터페이스 기반 콜백을
간결한 문법으로 전달할 수 있어
보일러플레이트 코드를 크게 줄인다.
</div>
</details>
