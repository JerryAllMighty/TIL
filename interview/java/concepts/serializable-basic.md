[재시도]
직렬화 / 역직렬화는 언제 발생하나요?
3-way Handshake와 4-way Handshake 과정에 대해 설명해 주세요.
HTTP/1.1과 HTTP/2.0의 주요 차이점은 무엇인가요?
Java에서 ServerSocket과 Socket 클래스로 간단한 TCP 클라이언트-서버를 구현할 때 주의점은?

---------
Serializable 기본 키워드 면접 질문

Serializable이 정확히 어떤 역할을 하는 인터페이스인가요?

<details>
<summary>Serializable은 왜 사용하나요?</summary>
<div markdown="1">
바이트 코드로 바꿔야하기 때문에 사용합니다. 바이트 코드로 바뀌면 디스크에 쓰면 저장, 네트워크에 쓰면 전송이 되는데, 
각 역할에 맞게 역할을 수행하기 전에 필요한 바이트 코드로 바뀌어야하기 때문에 사용합니다.
</div>
</details>

<details>
<summary>Serializable은 왜 외부에 영속하는 용도로는 쓰지말라고 할까요?</summary>
<div markdown="1">
버전 호환성에 취약하고, Gadgets 체인처럼 역직렬화 공격에 취약하기 때문입니다. 또한 언어에 종속적이라서 JSON처럼 범용인 것과 차이가 있습니다. 
</div>
</details>

<details>
<summary>멀티플렉싱이란 뭘까요?</summary>
<div markdown="1">
여러 개를 하나로 묶는 기술이라고 생각합니다. IO를 예로 들면, 하나의 스레드가 select나 epoll로 여러 소켓의 이벤트를 탐지하는 부분에서 활용하고 있습니다.
</div>
</details>


Serializable에는 메서드가 없는데, JVM은 어떻게 직렬화 대상을 판단하나요?

자바에서 객체 직렬화는 어떤 흐름으로 동작하나요?

ObjectOutputStream과 ObjectInputStream은 각각 어떤 책임을 가지나요?

serialVersionUID는 왜 직접 정의하는 게 좋다고 하나요?

serialVersionUID를 정의하지 않으면 어떤 문제가 생길 수 있나요?

transient 키워드는 어떤 경우에 사용하나요?

transient로 선언한 필드는 역직렬화 후 어떤 상태가 되나요?

필드 중 하나가 Serializable을 구현하지 않으면 어떤 일이 발생하나요?

부모 클래스가 Serializable을 구현하지 않은 상태에서 자식 클래스가 구현하면 어떤 점을 주의해야 하나요?

기본 직렬화(default serialization)는 어떤 방식으로 필드를 처리하나요?

writeObject / readObject 메서드는 왜 제공될까요?

Externalizable은 Serializable과 어떤 점에서 다르나요?

Serializable을 사용했을 때 발생할 수 있는 대표적인 단점은 무엇인가요?

네트워크 통신에서 Serializable을 잘 사용하지 않는 이유는 뭘까요?

Spring 기반 애플리케이션에서 Serializable이 필요한 상황을 예로 들어볼 수 있을까요?