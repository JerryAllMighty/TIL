<details> <summary> AOP(Aspect Oriented Programming)란 무엇이며, 도입 시 어떤 장점이 있나요?</summary> <div markdown="1"> AOP는 '관점 지향 프로그래밍'으로, 애플리케이션의 핵심 비즈니스 로직과 공통으로 발생하는 부가 기능(로그, 트랜잭션, 보안 등)을 분리하여 모듈화하는 기술입니다. 이를 통해 코드의 중복을 제거하고, 핵심 로직의 가독성을 높이며, 유지보수를 용이하게 만듭니다. </div> </details>

<details> <summary> 스프링 AOP의 핵심인 프록시 패턴(Proxy Pattern)의 동작 원리는?</summary> <div markdown="1"> 클라이언트가 타겟 객체의 메서드를 직접 호출하는 대신, 타겟을 감싸고 있는 프록시 객체를 호출하는 방식입니다. 프록시는 부가 기능(전처리/후처리)을 수행한 뒤 실제 타겟 객체에 작업을 위임합니다. 스프링은 빈 후처리기를 통해 빈 생성 시점에 프록시를 자동으로 생성하여 주입해줍니다. </div> </details>

<details> <summary> 포인트컷(Pointcut)과 어드바이스(Advice)의 개념을 설명해주세요.</summary> <div markdown="1"> 포인트컷은 부가 기능을 어디에 적용할지 결정하는 선택 로직(필터링)입니다. 주로 메서드 선정 규칙을 정의합니다. 어드바이스는 실질적으로 실행될 부가 기능 코드(트랜잭션 시작, 로그 출력 등) 그 자체를 의미합니다. 이 둘을 결합한 것이 어드바이저(Advisor) 혹은 **애스펙트(Aspect)**입니다. </div> </details>

<details> <summary> 프록시 패턴(Proxy Pattern)과 데코레이터 패턴(Decorator Pattern)의 차이는 무엇인가요?</summary> <div markdown="1"> 두 패턴 모두 타깃 객체와 동일한 인터페이스를 구현하고 요청을 위임하지만 목적이 다릅니다. 프록시 패턴은 타깃에 대한 접근 권한을 제어하거나 초기화 시점을 늦추는 등의 '접근 제어'가 목적이며, 데코레이터 패턴은 타깃에 새로운 '부가 기능(트랜잭션, 로깅 등)'을 동적으로 추가하기 위해 사용합니다. </div> </details>

<details> <summary> 다이내믹 프록시(Dynamic Proxy)란 무엇이며 왜 도입되었나요?</summary> <div markdown="1"> 기존의 프록시는 인터페이스의 모든 메서드를 직접 구현해야 하고 부가 기능 코드가 중복되는 단점이 있었습니다. 다이내믹 프록시는 자바의 리플렉션(Reflection)을 이용해 런타임 시점에 프록시 객체를 자동으로 생성해줍니다. 이를 통해 수많은 메서드에 일일이 프록시를 만들지 않아도 InvocationHandler 하나로 부가 기능을 처리할 수 있습니다. </div> </details>

<details> <summary> 
빈 후처리기(Bean Post-Processor)가 AOP에서 중요한 이유는 무엇인가요?</summary> 
<div markdown="1">
빈 후처리기는 스프링 컨테이너가 빈 객체를 생성한 직후에 이를 가로채서 조작할 수 있게 해줍니다.
이를 통해 일일이 ProxyFactoryBean을 설정하지 않아도, 조건에 맞는 빈들을 자동으로 프록시로 바꿔치기해주어 자동 프록시 생성을 가능하게 합니다.
</div> 
</details>

<details> <summary> 타깃 오브젝트에 대한 프록시 생성 방식 두 가지(JDK, CGLIB)의 차이는?</summary>
<div markdown="1">
JDK 다이내믹 프록시: 자바 표준 API를 사용하며, 타깃이 반드시 '인터페이스'를 구현하고 있어야 합니다.
CGLIB: 타깃 클래스를 상속받아 프록시를 만듭니다. 인터페이스가 없는 구체 클래스에도 적용 가능하지만, 상속을 이용하므로 final 클래스나 메서드에는 적용할 수 없습니다. 스프링 부트는 기본적으로 CGLIB 방식을 사용합니다.
</div> 
</details>