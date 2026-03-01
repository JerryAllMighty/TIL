💡 Serializable 심화 키워드
1. 커스텀 직렬화 제어 (Customization)
   기본 직렬화 방식은 모든 필드를 자동으로 처리하지만, 이를 직접 제어해야 할 때 쓰는 기술들입니다.

writeObject() & readObject(): 클래스 내부에 이 프라이빗 메서드들을 구현하면, 기본 직렬화 과정 중간에 개발자가 원하는 로직(암호화, 로그 기록 등)을 끼워 넣을 수 있습니다.

readResolve() & writeReplace(): 싱글톤 패턴을 유지하거나, 직렬화 시점에 객체 자체를 다른 객체로 교체하고 싶을 때 사용합니다. (예: 역직렬화 후에도 기존 싱글톤 인스턴스를 반환하도록 보장)

Externalizable: Serializable을 상속받은 인터페이스로, writeExternal()과 readExternal() 메서드를 통해 직렬화 로직을 0부터 100까지 수동으로 구현해야 합니다. (속도는 빠르지만 구현이 까다로움)

2. 객체 그래프와 순환 참조 (Object Graph)
   Deep Copy vs Shallow Copy: 직렬화는 기본적으로 참조하는 모든 객체를 함께 복사하므로, 의도치 않게 거대한 객체 덩어리(Graph)가 한꺼번에 직렬화되는 현상을 이해해야 합니다.

Cyclic Reference (순환 참조): A가 B를 참조하고 B가 A를 참조할 때, 직렬화 메커니즘이 어떻게 무한 루프에 빠지지 않고 이를 처리하는지(Handle 방식) 이해하는 것이 중요합니다.

3. 안정성과 보안 (Stability & Security)
   Deserialization Vulnerability (역직렬화 취약점): 신뢰할 수 없는 바이트 스트림을 역직렬화할 때 악의적인 코드가 실행될 수 있습니다. 자바의 가장 큰 보안 구멍 중 하나로 꼽힙니다.

ObjectInputFilter: 자바 9부터 도입된 기능으로, 역직렬화할 클래스의 화이트리스트를 지정하여 보안 공격을 방어하는 기술입니다.

Class Shadowing / Versioning: 클래스의 필드가 삭제되거나 타입이 변했을 때, 구버전 데이터와의 호환성을 어떻게 유지할 것인지에 대한 전략입니다.

4. 아키텍처적 고려사항 (Architectural Issues)
   Proxies & Wrappers: Hibernate 같은 ORM 사용 시, 실제 객체가 아닌 프록시 객체가 직렬화되면서 발생하는 문제들을 다룹니다.

Alternative Formats (JSON, Avro, Kryo): 왜 자바 기본 직렬화 대신 이런 포맷을 쓰는지 성능(용량, 속도) 및 언어 중립성 관점에서 비교 학습해야 합니다.