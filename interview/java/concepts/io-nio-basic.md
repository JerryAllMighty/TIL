Java IO / NIO 기본 면접 질문

Java IO와 NIO의 가장 큰 차이는 뭐라고 생각하나요?

<details>
<summary>Stream 기반 I/O의 구조적 특징은 무엇인가요?</summary>
<div markdown="1">
단방향, 블로킹, 계층 구조(기본 스트림과 보조(필터)스트림 연결) 등이 있습니다. 
</div>
</details>


Blocking I/O란 정확히 어떤 상태를 의미하나요?

Blocking I/O가 서버 애플리케이션에서 문제가 되는 이유는 뭘까요?

<details>
<summary>InputStream / OutputStream과 Reader / Writer는 어떤 기준으로 나뉘나요?</summary>
<div markdown="1">
무엇을 처리하는게 목적이냐로 나뉜다고 생각합니다. Stream은 바이트를 처리하는 것, 후자는 문자열을 처리하는 것에 목적이 있다고 생각합니다. 
</div>
</details>

<details>
<summary>flush는 왜 사용하나요?</summary>
<div markdown="1">
버퍼링의 결과로 지연된 데이터를 출력하기 위해 사용한다고 생각합니다. 실제 입출력 요청을 예로 들면 네트워크를 통해서 전송 요청을 하는 것과, write 메서드를 활용해서 메모리에 쓰는 것은 기본적인 속도 차이가 많이 나는데요,
따라서 메모리에 충분히 썼다가, 한 번에 네트워크 요청을 하는 것이 성능상의 이점이 있기 때문에 버퍼링을 사용하지만, 버퍼링의 결과로 그만큼 데이터의 출력이 지연되는 부분도 생긴다고 생각하고, 이를 flush를 통해 해소할 수 있습니다. 
</div>
</details>

<details>
<summary>flush는 그럼 어떤 문제점이 있나요?</summary>
<div markdown="1">
flush를 만약 하지 못한다면 데이터가 유실될 수 있다고 생각합니다.
프로그램이 다운되면 모두 유실되기때문에 방어 코드도 함께 작성해야한다고 생각합니다.  
</div>
</details>

<details>
<summary>동기/비동기, block/non-block에 대해서 차이를 설명해주세요</summary>
<div markdown="1">
동기와 비동기는 요청한 작업에 대해 완료 여부를 신경 써서 작업을 순차적으로 수행할지 아닌지에 대한 관점.
블로킹과 논블로킹은 현재 스레드 멈출지 말지에 대한 관점입니다.
동기 + 블로킹은 IO 패키지의 stream 클래스, 
비동기 + 논블로킹은 NIO 클래스의 Channel 클래스 등이 대표적입니다.
</div>
</details>

<details>
<summary>동시성과 병렬의 차이를 설명해주세요</summary>
<div markdown="1">
논리적, 물리적 개념의 차이라고 생각합니다.
동시성은 동시에 진행되는 것처럼 보이게 처리하는 것이라 싱클 코어에서 멀티 스레드 번갈아 실행하는 것 등이 예시가 될 수 있고,
병렬은 아예 물리적으로 다른것, 실제로 동시에 실행되는 것이라, 멀티 코어에서 각각 1스레드씩 작업 수행하는 것 등이 예시라고 생각합니다.
</div>
</details>



BufferedInputStream 같은 버퍼링 스트림은 왜 필요한가요?

Java IO에서 데코레이터 패턴이 적용된 예를 들어볼 수 있나요?

NIO에서 Channel은 Stream과 어떤 점이 다르나요?

Channel이 “양방향”이라는 말은 무슨 의미인가요?

NIO에서 Buffer는 왜 반드시 필요할까요?

ByteBuffer의 position, limit, capacity는 각각 어떤 역할을 하나요?

flip(), clear()는 언제 사용하나요?

Non-blocking I/O는 Blocking I/O와 실행 흐름에서 어떻게 다르나요?

Non-blocking I/O에서 데이터가 아직 없으면 어떻게 처리되나요?

Selector는 왜 필요한 컴포넌트인가요?

Selector 없이 NIO를 사용하면 어떤 문제가 생길 수 있나요?

SelectionKey는 어떤 정보를 담고 있나요?

하나의 스레드로 여러 채널을 처리할 수 있는 이유는 뭘까요?

Event-driven I/O 모델이란 무엇인가요?

Direct Buffer는 일반 Heap Buffer와 어떤 차이가 있나요?

Direct Buffer의 단점은 뭐가 있나요?

Scatter / Gather I/O는 어떤 상황에서 유리할까요?

FileChannel은 기존 File I/O와 비교해 어떤 장점이 있나요?

MappedByteBuffer는 어떤 방식으로 동작하나요?

NIO.2의 AsynchronousChannel은 Non-blocking I/O와 뭐가 다른가요?

콜백 기반 비동기 I/O의 단점은 뭐라고 생각하나요?

Path / Files API가 기존 File API보다 나은 점은 뭔가요?

Spring MVC는 기본적으로 IO와 NIO 중 어떤 모델에 가깝나요?

그럼에도 Netty 같은 프레임워크가 NIO를 사용하는 이유는 뭘까요?

모든 상황에서 NIO가 IO보다 좋은 선택일까요? 아니라면 언제 IO가 더 나을까요?