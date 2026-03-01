[재시도]
IO → NIO → Netty로 갈수록 추상화가 증가하는데, 그 대가로 잃는 제어권은 무엇인가?
-----------
🚀 자바 NIO 심화 학습 키워드
1. 메모리와 데이터 효율 (Memory Efficiency)
   Direct Buffer: JVM 힙 메모리가 아닌 운영체제의 커널 메모리를 직접 사용하여 데이터 복사 비용(CPU 오버헤드)을 줄이는 버퍼입니다.

Zero Copy (TransferTo/From): 커널 공간에서 사용자 공간을 거치지 않고 데이터를 전송하여 컨텍스트 스위칭을 최소화하는 기술입니다.

Memory Mapped File (MappedByteBuffer): 파일의 내용을 프로세스의 가상 메모리에 직접 매핑하여 대용량 파일을 매우 빠르게 읽고 쓰는 방식입니다.

Scatter / Gather: 여러 개의 버퍼에 데이터를 나누어 쓰거나(Scatter), 여러 버퍼의 내용을 한 번에 읽어서 전송(Gather)하여 입출력 효율을 높이는 기법입니다.

2. 네트워크 및 동시성 (Scalability)
   Reactor Pattern: Selector를 사용하여 여러 이벤트(연결, 데이터 도착 등)를 감지하고, 이를 전담 핸들러에게 분배하여 처리하는 NIO의 기본 설계 패턴입니다.

Acceptor / Handler: Selector에서 발생한 이벤트를 분류하여 새로운 연결은 Acceptor가, 실제 데이터 읽고 쓰기는 Handler가 담당하도록 역할을 분리하는 방식입니다.

SelectionKey Status: 채널의 상태(OP_ACCEPT, OP_READ, OP_WRITE 등)를 비트마스크로 관리하여 현재 입출력이 가능한 상태인지 판별하는 메커니즘입니다.

Edge Triggered vs Level Triggered: 상태가 변화하는 순간에만 이벤트를 발생시킬 것인지, 아니면 상태가 유지되는 동안 계속 발생시킬 것인지에 대한 이벤트 통지 방식입니다.

3. 비동기 및 현대적 처리 (Advanced I/O)
   AIO (Asynchronous I/O): 작업을 던져놓고 완료되면 콜백(Callback)이나 Future를 통해 통지받는 완전 비동기 방식의 NIO2 API입니다.

CompletionHandler: AIO에서 입출력 작업이 성공하거나 실패했을 때 실행될 로직을 정의하는 비동기 콜백 인터페이스입니다.

Thread Pooling in NIO: Selector가 감지한 이벤트를 실제 비즈니스 로직으로 넘길 때 작업 스레드 풀을 어떻게 운영하여 병목을 방지할지에 대한 전략입니다.