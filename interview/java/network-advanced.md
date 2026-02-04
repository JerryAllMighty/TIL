<details>
<summary>TCP UDP는 언제 쓰나요?</summary>
<div markdown="1">
TCP는 데이터 전체가 정확하게 도착해야 할 떄입니다.
연길지향성, 신뢰성, 순서보장, 재전송 등의 성격이 있기 때문입니다.
UDP는 속도가 생명이고, 데이터가 유실되더라도 지연이 최소화되어야 할 때 사용합니다.
</div>
</details>

<details>
<summary>소켓이 뭔가?</summary>
<div markdown="1">
네트워크 상의 프로세스 식별자입니다. 컴퓨터는 네트워크 통신을 위해 소켓을 생성해서 데이터를 주고 받습니다.
종류로는 TCP와 UDP가 있습니다. 
</div>
</details>

<details>
<summary>소켓의 구성 요소는 뭔가?</summary>
<div markdown="1">
IP와 포트번호, 프로토콜, 소켓 디스크립터(OS가 부여하는 핸들)입니다.
</div>
</details>

<details>
<summary>TCP에서 보장해주는 전송은 어디까지인가요?</summary>
<div markdown="1">
프로토콜 레벨에서 전송을 보장해준다고 생각합니다. 네트워크 카드에서 네트워크까지 도착하는 걸 보장해주는게 TCP이고, 
OS에서 프로그램까지의 전달을 보장해주는 건 비즈니스 로직의 영역이라 TCP가 보장해주는 영역은 아닙니다.
</div>
</details>

<details>
<summary>4 way handshake는 뭔가요?</summary>
<div markdown="1">
통신 끝난 후 소켓 연결을 해제할 때, 양방향 모두 데이터 유실 없이 안전하게 통신을 마무리짓기 위해 사용하는 기술입니다.
데이터를 주고받는 과정인 3-way handshake가 "연결 시작"을 위한 것이라면, 4-way handshake는 양쪽 모두 더 이상 보낼 데이터가 없음을 확인하고 **"연결 종료"**를 확정 짓는 절차입니다.

TCP는 전이중(Full-Duplex) 통신 방식이기 때문입니다. 전이중 통신이란 양쪽에서 동시에 데이터를 보낼 수 있는 구조를 말합니다.
따라서 한쪽에서 "나는 이제 보낼 게 없어!"라고 말해도(FIN), 반대편에서는 "잠깐만, 나는 아직 줄 게 남았어!"라고 할 수 있기 때문에 양쪽의 의사를 각각 확인하는 과정이 필요합니다.

** 참고 
4-way handshake 진행 단계
클라이언트가 먼저 종료를 요청한다고 가정할 때의 과정입니다.
FIN (클라이언트 → 서버): 클라이언트가 연결을 끊고 싶다는 신호(FIN 패킷)를 보냅니다. 클라이언트는 FIN_WAIT1 상태가 됩니다.
ACK (서버 → 클라이언트): 서버는 일단 "알았어, 확인했어. 근데 나 아직 보낼 데이터가 남았을 수 있으니 기다려줘"라고 응답(ACK)합니다. 서버는 CLOSE_WAIT 상태가 되고, 클라이언트는 이를 받고 FIN_WAIT2 상태가 됩니다.
FIN (서버 → 클라이언트): 서버도 보낼 데이터를 모두 보냈다면, 이제 "나도 다 보냈어! 이제 정말 끊자"라고 신호(FIN)를 보냅니다. 서버는 LAST_ACK 상태가 됩니다.
ACK (클라이언트 → 서버): 클라이언트는 "응, 확인했어. 안녕!"이라고 마지막 응답(ACK)을 보냅니다. 이때 클라이언트는 바로 소켓을 닫지 않고 앞서 설명드린 TIME_WAIT 상태로 들어갔다가 일정 시간 후 종료됩니다.
</div>
</details>

[재시도]
🔹 TCP / OS 레벨
<details>
<summary>TIME_WAIT은 왜 필요하고, 서버에서 많아지면 어떤 문제가 생기나요?</summary>
<div markdown="1">
TCP의 4-Way Handshake 과정에서 연결 종료를 먼저 요청한 쪽(Active Closer)이 마지막 ACK를 보낸 뒤, 일정 시간(기본 2MSL, 약 1~4분) 동안 소켓을 바로 닫지 않고 유지하는 상태를 말합니다.
마지막 ACK의 전달 보장: 
클라이언트가 보낸 마지막 ACK가 서버에 도달하지 못하고 유실될 수 있습니다.
이때 서버는 FIN 패킷을 다시 보내게 되는데, 클라이언트가 이미 소켓을 닫았다면 서버는 오류(RST)를 받게 됩니다. 
TIME_WAIT 상태는 이 재전송된 FIN을 받아 다시 ACK를 보내줌으로써 연결을 우아하게(Graceful) 종료하도록 돕습니다.
지연 패킷(Stray Segments) 처리:
네트워크 혼잡으로 인해 이전 연결에서 보낸 패킷이 뒤늦게 도착할 수 있습니다.
만약 연결을 즉시 새로 맺었는데 이전 연결의 패킷이 도착하면 데이터가 오염될 수 있죠. TIME_WAIT은 이 **유령 패킷들이 자연 소멸(TTL 만료)**될 때까지 기다려 데이터의 무결성을 지킵니다.

서버에 TIME_WAIT이 많아질 때의 문제점
보통은 클라이언트가 연결을 끊지만, 서버가 먼저 연결을 끊는 구조(예: Rest API 서버)에서는 서버에 수만 개의 TIME_WAIT 소켓이 쌓일 수 있습니다.
로컬 포트 고갈 (Ephemeral Port Exhaustion): 
 서버가 다른 서버(DB 등)에 요청을 보내는 클라이언트 역할도 겸할 때 문제입니다. 포트 번호는 유한(보통 65535개 중 일부 사용)한데, 
TIME_WAIT 상태의 소켓이 포트를 점유하고 있으면 새로운 연결을 맺을 포트가 없어 서비스가 중단될 수 있습니다.
메모리 및 리소스 낭비:
각 소켓은 미세하지만 커널 메모리를 점유합니다. 수만 개가 쌓이면 시스템 전체의 리소스 효율이 떨어집니다.
성능 저하:
새로운 연결 시 소켓 테이블을 탐색하는 시간이 늘어나 미세한 지연 시간(Latency)이 발생할 수 있습니다.
</div>
</details>

🔹 Socket / OS 자원

자바에서 Socket을 닫았는데도 포트가 바로 반환되지 않는 이유는 무엇인가요?

🔹 Blocking vs Non-blocking

Non-blocking I/O가 스레드 수를 줄일 수 있는 구조적 이유는 무엇인가요?

🔹 Selector / 이벤트 모델

Selector 하나로 여러 채널을 처리할 수 있는 이유는 무엇인가요?

🔹 버퍼 / 메모리

Direct Buffer는 언제 성능 이점보다 위험이 더 커지나요?

🔹 Zero Copy

Zero Copy는 어떤 복사를 제거하며, 언제 효과가 가장 큰가요?

🔹 비동기 모델

Event Loop 구조에서 블로킹 코드가 왜 치명적인가요?

🔹 Netty

Netty는 왜 EventLoop당 하나의 스레드 모델을 유지하나요?

🔹 HTTP 심화

Keep-Alive가 있는데도 Connection Pool이 필요한 이유는 무엇인가요?

🔹 장애 / Timeout

네트워크 타임아웃을 반드시 설정해야 하는 이유는 무엇인가요?

🔹 보안 (TLS)

TLS 핸드셰이크가 비싼 이유는 무엇인가요?

------------------------------------------------------------------------
1TCP 상태 머신 (LISTEN / SYN_SENT / ESTABLISHED / TIME_WAIT)
→ TCP 연결의 생성·유지·종료 과정을 상태 전이로 관리하는 메커니즘입니다.

TIME_WAIT이 왜 필요한가요?
→ 지연된 패킷이 다음 연결에 영향을 주지 않도록 이전 연결을 안전하게 정리하기 위해서입니다.

TIME_WAIT과 서버 포트 고갈의 관계는 무엇인가요?
→ TIME_WAIT 소켓이 많아지면 사용 가능한 포트가 줄어 포트 고갈이 발생할 수 있습니다.

Half-open connection이란 무엇인가요?
→ 한쪽은 연결이 완료됐다고 생각하지만 반대쪽은 연결이 완료되지 않은 상태입니다.

SYN만 보내고 ACK가 오지 않는 상황은 어떤 문제인가요?
→ 서버 리소스를 점유만 하고 연결을 완료하지 않는 Half-open 상태를 유발합니다.

SYN Flood 공격이란 무엇인가요?
→ 대량의 SYN 요청으로 서버의 연결 큐를 고갈시키는 DoS 공격입니다.

Nagle 알고리즘이란 무엇인가요?
→ 작은 패킷을 모아서 한 번에 전송해 네트워크 효율을 높이는 전략입니다.

Nagle과 Delayed ACK의 트레이드오프는 무엇인가요?
→ 지연(latency)은 늘어나지만 처리량(throughput)은 증가합니다.

Socket과 File Descriptor의 관계는 무엇인가요?
→ 자바 Socket은 내부적으로 OS의 File Descriptor를 감싸는 추상화 객체입니다.

자바 소켓과 GC의 관계는 무엇인가요?
→ Socket 객체는 GC 대상이지만, 네이티브 FD는 명시적 close가 필요합니다.

Blocking Socket과 Non-blocking Socket의 차이는 무엇인가요?
→ Blocking은 I/O 완료까지 대기하고, Non-blocking은 즉시 반환합니다.

Socket과 SocketChannel의 차이는 무엇인가요?
→ Socket은 Blocking 기반, SocketChannel은 Non-blocking 및 Selector 기반입니다.

Blocking과 Non-blocking의 OS syscall 차이는 무엇인가요?
→ Non-blocking은 커널에서 즉시 상태를 반환하고 대기하지 않습니다.

SO_TIMEOUT 옵션은 무엇인가요?
→ read 호출의 최대 대기 시간을 제한하는 옵션입니다.

TCP_NODELAY는 어떤 옵션인가요?
→ Nagle 알고리즘을 비활성화해 지연 없이 즉시 전송하도록 합니다.

SO_REUSEADDR는 어떤 역할을 하나요?
→ TIME_WAIT 상태의 포트를 재사용할 수 있게 합니다.

Selector 내부 동작은 어떻게 이루어지나요?
→ 여러 채널의 이벤트를 OS 이벤트 큐를 통해 감시합니다.

select / poll / epoll의 차이는 무엇인가요?
→ epoll은 이벤트 기반으로 대량 연결에서도 효율적으로 동작합니다.

Linux에서 NIO 성능이 좋은 이유는 무엇인가요?
→ epoll 기반 구현으로 대규모 동시 연결 처리에 유리하기 때문입니다.

Selector.wakeup()은 왜 필요한가요?
→ 블로킹 중인 select를 즉시 깨우기 위해서입니다.

멀티 스레드 환경에서 wakeup의 역할은 무엇인가요?
→ 다른 스레드에서 Selector 상태 변경을 안전하게 반영하기 위해 사용됩니다.

Busy Loop 문제란 무엇인가요?
→ select가 계속 즉시 반환되며 CPU를 100% 사용하는 현상입니다.

Heap Buffer와 Direct Buffer의 차이는 무엇인가요?
→ Heap은 GC 관리 대상, Direct는 네이티브 메모리를 사용합니다.

언제 Direct Buffer를 사용하나요?
→ 대용량 I/O처럼 복사 비용을 줄여야 할 때 사용합니다.

Zero Copy란 무엇인가요?
→ 사용자 공간을 거치지 않고 커널에서 직접 데이터를 전송하는 방식입니다.

FileChannel.transferTo()의 역할은 무엇인가요?
→ 파일 데이터를 커널 레벨에서 네트워크로 직접 전송합니다.

ByteBuffer의 position / limit / capacity는 무엇을 의미하나요?
→ 읽기·쓰기 위치, 유효 데이터 범위, 전체 버퍼 크기를 나타냅니다.

flip과 compact의 차이는 무엇인가요?
→ flip은 읽기 전환, compact는 남은 데이터를 앞으로 당겨 재사용합니다.

Reactor Pattern이란 무엇인가요?
→ 이벤트 감지와 처리를 분리해 비동기 I/O를 처리하는 패턴입니다.

Netty와 Spring WebFlux의 근간은 무엇인가요?
→ Reactor 기반 이벤트 루프 모델입니다.

Proactor Pattern이란 무엇인가요?
→ OS가 I/O 완료까지 책임지고 완료 결과만 통지하는 모델입니다.

Java에서 Proactor가 제한적인 이유는 무엇인가요?
→ OS 의존성이 크고 JVM 추상화 한계가 있기 때문입니다.

Netty Channel Pipeline이란 무엇인가요?
→ I/O 이벤트를 Handler 체인으로 처리하는 구조입니다.

Inbound / Outbound Handler의 역할 차이는 무엇인가요?
→ Inbound는 수신, Outbound는 송신 로직을 담당합니다.

디코딩과 비즈니스 로직을 분리하는 이유는 무엇인가요?
→ 책임 분리로 유지보수성과 확장성을 높이기 위해서입니다.

EventLoopGroup에서 Boss / Worker를 나누는 이유는 무엇인가요?
→ 연결 수락과 데이터 처리를 분리해 병목을 줄이기 위해서입니다.

Netty의 Back Pressure는 어떻게 동작하나요?
→ 쓰기 가능 여부를 기준으로 송신 속도를 제어합니다.

HTTP/1.1과 HTTP/2의 가장 큰 차이는 무엇인가요?
→ HTTP/2는 하나의 연결에서 멀티플렉싱을 지원합니다.

HOL Blocking이란 무엇인가요?
→ 하나의 요청 지연이 전체 응답을 막는 현상입니다.

Keep-Alive와 Connection Pool의 관계는 무엇인가요?
→ Keep-Alive가 있어야 커넥션 풀이 재사용 효과를 냅니다.

Chunked Transfer Encoding이란 무엇인가요?
→ 응답 크기를 알 수 없을 때 데이터를 나눠 전송하는 방식입니다.

네트워크 장애는 어떻게 분류할 수 있나요?
→ 연결 실패, 지연, 부분 실패로 나눌 수 있습니다.

connect / read / write timeout의 차이는 무엇인가요?
→ 연결, 수신, 송신 단계별 최대 대기 시간을 제한합니다.

Retry가 위험한 이유는 무엇인가요?
→ 중복 요청으로 데이터 불일치나 장애 확산을 유발할 수 있습니다.

Idempotency가 중요한 이유는 무엇인가요?
→ 재시도 시에도 결과가 동일함을 보장하기 위해서입니다.

TLS 세션 재사용이란 무엇인가요?
→ 기존 세션 정보를 활용해 핸드셰이크 비용을 줄이는 방식입니다.

Full Handshake와 Resumption의 차이는 무엇인가요?
→ Resumption은 인증 단계를 생략해 빠르게 연결합니다.

mTLS란 무엇인가요?
→ 서버와 클라이언트가 서로 인증서를 검증하는 방식입니다.

인증서 체인 검증이란 무엇인가요?
→ 서버 인증서가 신뢰 가능한 Root CA까지 이어지는지 확인하는 과정입니다.