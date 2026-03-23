<details>
<summary> 자바의 동시성 문제를 해결하기 위한 방법론과 예제를 들어 설명하시오. </summary>
<div markdown="1">
원자성 측면에서는 reEntrantLock이나 synchronized 키워드를 활용해 비관적 락 관점에서 순차적인 접근을 할 수있고, 낙관적 락 측면에서  atomic 클래스를 활용해
하드웨어 레벨에서 cas 알고리즘을 통해 수정 후의 예상값을 확인하며 수정할 수 있습니다. 가시성 측면에서 단순 값을 읽기만 해야하는 상황이라면 volatile 키워드도 고려할 수 있습니다.
</div>
</details>


<details>
<summary> synchronized 키워드와 reentrantLock의 주요한 차이점은 무엇인가요? </summary>
<div markdown="1">
synchronized 키워드는 암시적인 락입니다. 키워드 하나로 락을 지정할 수 있고, 가독성이 좋습니다. jvm이 자동으로 락의 획득과 해제를 관리하기에 데드락 위험이 적습니다.
하지만 락을 거는 순서나 타임아웃을 설정할 수 없습니다. 또한 메서드 전체에 락을 걸면 성능 저하가 크므로 블록을 활용해야합니다.
reEntrantLock은 명시적인 락입니다. 락의 획득과 해제를 명시적으로 관리해야합니다. 대신 순서나 타임 아웃을 설정할 수 있으며, 공정성을 선택해 기아 현상을 해결할 수 있습니다.
</div>
</details>

<details>
<summary> reentrantLock을 사용할 때 주의해야 할 점이 무엇인가요? </summary>
<div markdown="1">
명시적으로 락을 해제해주어야합니다. try-finally 구문을 활용하여 finally에서 획득한 락을 해제해주어야 예외가 생기더라도 락이 해제됩니다.
또한 락 획득 위치를 선정해야합니다. try 구문 밖에서 획득해야 finally에서 해제시 문제가 없습니다.
기아 현상을 방지하기 위해 공정성 설정을 할 수 있는데, 이는 내부적으로 복잡한 스케쥴링 연산을 포함합니다. 따라서 비즈니스 로직상 순서가 아주 중요하지 않다면 성능 저하를 야기할 수 있기에 기본값인 비활성화를 권장합니다.
</div>
</details>



<details>
<summary> ReentrantLock과 synchronized 키워드 중 어떤 상황에서 어떤 것을 선택해야 하는지에 대해 어떻게 판단하나요? </summary>
<div markdown="1">
가독성과 유지보수가 명확하고, 락의 관리 요소를 줄이고 싶다면 synchronized 키워드를 활용할 수 있습니다.
하지만 공정성이 중요하고 락의 대기 시간 설정이 필요하다거나 복잡한 대기 구조가 필요하다면 ReEntrantLock을 사용할 수 있습니다.
</div>
</details>