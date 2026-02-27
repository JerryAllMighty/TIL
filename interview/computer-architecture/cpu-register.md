<details>
<summary>레지스터와 일반 메모리의 차이점은 무엇인가요?
</summary>
<div markdown="1">
레지스터는 CPU 내부의 매우 작은 데이터 저장 최상위 계층으로 현재 연산을 저장하는 목적이며, 일반 메모리보다 빠른 접근이 가능합니다.
반면 일반 메모리는 CPU 외부의 저장소로 매우 용량이 크며, 활성화된 프로그램이나 데이터 저장소의 목적입니다.
</div>
</details>

<details>
<summary> 레지스터와 캐시 메모리의 관계는 무엇인가요?
</summary>
<div markdown="1">
레지스터와 캐시 메모리 모두 CPU의 작업의 효율을 도모한다는 부분은 유사합니다. 다만 레지스터는 CPU가 접근 가능한
가장 빠른 작업대이며, 현재의 연산에 필요한 정보를 저장합니다. 반면에 캐시 메모리는 CPU가 RAM에 접근하는 시간을 줄이기 위하여 자주 사용되는
정보를 저장하여 CPU의 작업 효율을 향상시킵니다.
검색 키워드: register vs cache memory, cache memory management
</div>
</details>


<details>
<summary> 캐시 메모리가 커질수록 어떤 장단점이 있을까요?
</summary>
<div markdown="1">
캐시 적중률이 올라가고 전체적인 시스템 성능이 개선되는 장점은 있습니다. 하지만 캐시가 커진다는 것은 사용되는 sram이 많이 필요해
제조 비용이 높아지고 전력 소모나 발열 등의 높아질 가능성이 있습니다. 또한 특정 데이터를 찾아내는 시간이 늘어나 접근 지연 시간이 늘어납니다.
따라서 적절한 수준의 계층 구조 설계가 중요합니다.
검색 키워드: cache memory size impact, cache memory design considerations
</div>
</details>

<details>
<summary> 지역성이 뭔가요?
</summary>
<div markdown="1">
CPU가 메모리의 특정 부분에 있는 데이터나 명령어를 짧은 시간동안 집중적으로 참조하는 현상. 최근에 참조된 데이터가 가까운 미래에 다시 참조될 가능성이 높다는 시간 지역성과
특정 데이터가 참조되면 그 데이터 주변의 조소에 있는 데이터들도 곧 참조될 가능성이 높다는 공간 지역성이 있다.
</div>
</details>