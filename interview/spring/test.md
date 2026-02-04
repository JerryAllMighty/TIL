<details> 
<summary>동등 분할이란 무엇인가요?</summary>
<div markdown="1"> 
동등 분할은 입력값을 **동일한 동작을 보장하는 그룹(동등 클래스)**으로 나누고,
각 그룹에서 **대표 값 하나만 테스트**하는 테스트 기법이다. 
모든 값을 테스트하지 않고도 효율적으로 오류를 발견할 수 있다.
</div> 
</details> 

<details>
<summary>동등 분할은 어떤 문제를 해결하기 위해 사용하나요?</summary>
<div markdown="1">
입력 값의 경우의 수가 너무 많을 때 발생하는 테스트 케이스 폭증 문제를 줄이기 위해 사용한다.
중복 테스트를 제거하고 테스트 비용 대비 효과를 높일 수 있다.
</div>
</details>

<details>
<summary>동등 분할의 예시를 들어 설명해보세요.</summary>
<div markdown="1">
예를 들어 나이 입력이 1~100까지 허용된다면,
유효 동등 클래스는 1~100이고,
무효 동등 클래스는 0 이하, 101 이상, 숫자가 아닌 값이다.
각 클래스에서 하나의 대표 값만 테스트하면 전체 동작을 검증할 수 있다.
</div>
</details>

<details>
<summary>경계값 분석이란 무엇인가요?</summary>
<div markdown="1">
경계값 분석은 오류가 경계 근처에서 가장 많이 발생한다는 경험적 사실에 기반한 테스트 기법이다.
동등 분할로 나눈 범위의 최소값, 최대값과 그 주변 값을 집중적으로 테스트한다.
</div>
</details>


<details>
<summary>동등 분할과 경계값 분석의 차이는 무엇인가요?</summary>
<div markdown="1">
동등 분할은 각 입력 범위에서 대표 값 하나만 테스트하는 기법이고,
경계값 분석은 입력 범위의 최소값, 최대값과 그 직전·직후 값을 테스트하는 기법이다.
보통 두 기법은 함께 사용된다.
</div>
</details>


<details>
<summary>경계값 분석의 예시를 들어보세요.</summary>
<div markdown="1">
입력 범위가 1~100인 경우,
0, 1, 2, 99, 100, 101과 같이
경계값과 경계 주변 값을 테스트하여 오류를 효과적으로 발견할 수 있다.
</div>
</details>


<details>
<summary>침투적 테스트 기술이란 무엇인가요?</summary>
<div markdown="1">
침투적 테스트 기술은 테스트를 위해 기존 코드 구조를 변경하거나
객체의 내부 구현에 직접 접근하는 방식이다.
예를 들어 private 메서드 접근이나 테스트용 코드 추가가 이에 해당한다.
</div>
</details>


<details>
<summary>비침투적 테스트 기술이란 무엇인가요?</summary>
<div markdown="1">
비침투적 테스트 기술은 프로덕션 코드를 수정하지 않고,
공개된 인터페이스를 통해 객체의 외부 행위만을 검증하는 테스트 방식이다.
</div>
</details>


<details>
<summary>침투적 테스트 기술의 단점은 무엇인가요?</summary>
<div markdown="1">
테스트를 위해 코드가 오염될 수 있고,
캡슐화가 깨지며,
리팩토링 시 테스트가 쉽게 깨질 수 있어 유지보수성이 떨어진다.
</div>
</details>


<details>
<summary>토비의 스프링에서는 침투적 테스트와 비침투적 테스트 중 무엇을 선호하나요?</summary>
<div markdown="1">
토비의 스프링에서는 비침투적 테스트를 선호한다.
DI와 인터페이스를 활용해 내부 구현이 아닌 객체의 행위 중심 테스트를 강조하며,
이는 스프링의 객체지향 철학과도 잘 맞는다.
</div>
</details>


<details>
<summary>Mock 객체는 침투적 테스트 기술인가요, 비침투적 테스트 기술인가요?</summary>
<div markdown="1">
일반적으로 Mock 객체를 사용하는 테스트는 비침투적 테스트에 해당한다.
프로덕션 코드를 수정하지 않고 의존성을 대체하여 객체의 행위를 검증하기 때문이다.
</div>
</details>

<details>
<summary>토비의 스프링 2장에서 다루는 DI를 이용한 테스트 방법은?</summary>
<div markdown="1">
DI를 이용한 테스트 방법은 ① 직접 setter 주입, ② 스프링 컨테이너를 이용한 테스트, ③ 스프링 컨테이너 없이 테스트의 3가지로 나뉜다.
</div>
</details>

<details>
<summary>스프링 컨테이너를 이용한 테스트의 단점은?</summary>
<div markdown="1">
매 테스트마다 스프링 컨테이너를 새로 생성해 초기화 시간이 오래 걸리고, 리소스 정리 문제로 일관된 결과를 보장하기 어렵다.
</div>
</details>

<details>
<summary>스프링 컨테이너 없이 테스트하는 이유는?</summary>
<div markdown="1">
빠르고 안정적인 테스트를 위해 컨테이너 초기화 시간을 줄이고, 작은 단위의 순수한 로직 테스트에 집중하기 위함이다.
</div>
</details>

<details>
<summary>UserDaoTest의 문제점은 무엇인가?</summary>
<div markdown="1">
수동 확인 작업의 번거로움(콘솔 출력 확인)과 실행 작업의 번거로움(main() 메서드 반복 실행)이 있다.
</div>
</details>

<details>
<summary>웹을 통한 테스트의 문제점은?</summary>
<div markdown="1">
모든 레이어(DAO, Service, Controller, View)를 완성한 후에야 테스트 가능하고, 문제 발생 시 원인 파악이 어렵다.
</div>
</details>

<details>
<summary>단위 테스트의 한계는 무엇인가?</summary>
<div markdown="1">
각 단위는 잘 동작해도 전체 시스템에서 에러가 발생할 수 있고, 고객의 다양한 행동 패턴을 모두 테스트하기 어렵다.
</div>
</details>

<details>
<summary>통합 테스트의 필요성은?</summary>
<div markdown="1">
단위 테스트만으로는 전체 시스템의 안정성을 보장할 수 없으므로, 여러 단위가 조합된 긴 테스트도 필요하다.
</div>
</details>

<details>
<summary>포괄적인 테스트란?</summary>
<div markdown="1">
경계값, 다른 타입의 값, null값, 찾을 수 없는 값 등 다양한 케이스를 테스트하는 것으로, 네거티브 테스트를 포함한다.
</div>
</details>


<details>
<summary>단위 테스트(Unit Test)를 작성할 때 '고립(Isolation)'이 중요한 이유는 무엇인가요?</summary>
<div markdown="1"> 외부 자원이나 타 객체에 의존하지 않고 로직의 정합성만 검증하기 위함입니다. 테스트 속도를 높이고, 환경에 무관하게 항상 같은 결과를 보장할 수 있습니다. 
</div>
</details>

<details>
<summary>TDD(테스트 주도 개발)의 3단계 사이클과 각 단계의 목적을 설명해주세요.</summary> <div markdown="1"> Red: 실패하는 테스트 작성, Green: 통과하는 최소한의 코드 작성, Refactor: 코드 개선. 기능 사양을 명확히 정의하고 자연스럽게 객체지향적인 설계를 유도합니다. </div> </details>

<details> 
<summary>스프링 테스트 컨텍스트 프레임워크의 '컨텍스트 캐싱'이란 무엇인가요?</summary> 
<div markdown="1">
동일한 설정을 공유하는 테스트 클래스끼리 애플리케이션 컨텍스트를 재사용하는 기능입니다. 빈 생성 비용을 줄여 전체 테스트 수행 시간을 획기적으로 단축합니다. </div>
</details>

<details> 
<summary>테스트 메서드에서 @DirtiesContext 어노테이션은 언제 사용해야 하나요?</summary>
<div markdown="1"> 테스트 중 빈의 상태를 변경하거나 컨텍스트 구성을 오염시켰을 때 사용합니다. 해당 테스트 종료 후 컨텍스트를 폐기하여 다음 테스트에 영향을 주지 않도록 합니다.
</div>
</details>

<details> 
<summary>JUnit에서 테스트 '픽스처(Fixture)'를 구성할 때 @BeforeEach를 사용하는 이유는 무엇인가요?</summary> 
<div markdown="1">
테스트 실행 전 공통으로 필요한 객체나 데이터를 준비하기 위해서입니다. 테스트 간 독립성을 보장하고, 반복되는 준비 코드를 줄여 유지보수성을 높여줍니다.
</div>
</details>

<details>
<summary>좋은 단위 테스트를 위한 F.I.R.S.T 원칙 중 'Fast'와 'Independent'의 의미는?</summary>
<div markdown="1">
Fast: 수시로 돌려볼 수 있을 만큼 빨라야 함.
Independent: 각 테스트는 서로 의존하지 않고 어떤 순서로 실행되어도 결과가 같아야 함.
</div>
</details>

<details> <summary>학습 테스트(Learning Test)란 무엇이며 왜 작성하는가?</summary> <div markdown="1"> 자신이 만든 코드가 아닌, 외부 라이브러리나 프레임워크의 기능을 확인하고 사용법을 익히기 위해 작성하는 테스트입니다. 버전 업데이트 시 API 변경 사항을 빠르게 감지할 수 있고, 팀 내에서 기술의 동작 원리를 공유하는 문서 역할을 합니다. </div> </details>

<details> <summary>버그 테스트(Bug Test)를 작성함으로써 얻는 이점은?</summary> <div markdown="1"> 발생한 버그를 재현하는 테스트를 먼저 만듦으로써, 해당 버그가 해결되었음을 명확히 증명할 수 있습니다. 또한 향후 리팩토링이나 기능 추가 시 동일한 버그가 다시 발생하는 '회귀(Regression)' 현상을 방지하는 안전장치가 됩니다. </div> </details>

<details> <summary>테스트를 작성하는 것이 장기적으로 개발 속도를 높이는 이유는 무엇인가?</summary> <div markdown="1"> 작성한 코드에 대한 확신을 주어 과감한 리팩토링을 가능하게 하고, 결함을 조기에 발견하여 수정 비용을 낮추기 때문입니다. 수동 테스트의 반복적인 비용을 줄이고, 코드 변경 시 발생할 수 있는 사이드 이펙트를 즉각적으로 감지할 수 있습니다. </div> </details>

<details> <summary>단위 테스트(Unit Test)와 통합 테스트(Integration Test)를 구분하는 기준은?</summary> <div markdown="1"> 단위 테스트는 외부 리소스(DB, 네트워크) 없이 오직 해당 클래스의 로직만 고립시켜 검증하는 것입니다. 통합 테스트는 두 개 이상의 모듈이 연결되어 동작하거나, 실제 DB 등 외부 환경과 연동하여 시스템의 전체적인 흐름을 확인하는 테스트를 의미합니다. </div> </details>

<details> <summary>스프링이 테스트 컨텍스트를 캐싱할 때, 기준이 되는 것은 무엇인가?</summary> <div markdown="1"> 테스트 클래스에 설정된 @ContextConfiguration의 설정 파일 경로(XML)나 클래스 목록(JavaConfig)입니다. 동일한 설정 구성을 가진 테스트들은 같은 컨텍스트를 공유하며, 하나라도 설정이 다르면 새로운 컨텍스트를 생성하여 캐싱합니다. </div> </details>

<details> <summary>테스트에서 '침투적(Intrusive)'이라는 표현은 어떤 의미인가?</summary> <div markdown="1"> 애플리케이션 코드가 특정 테스트 프레임워크나 테스트만을 위한 로직에 종속되는 상태를 의미합니다. 스프링은 비침투적 프레임워크를 지향하므로, 비즈니스 로직에 스프링 관련 코드가 나타나지 않게 설계하는 것이 중요합니다. </div> </details>
