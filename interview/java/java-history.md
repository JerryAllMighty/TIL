[서두]
- 자바 버전별 주요 변화 사항을 정리해보았다. 
- 7 ~ 17까지다.
[본론]
# Java 7
switch 에 문자열 사용가능
enum / int만 쓰던 제약 해소
다이아몬드 연산
제네릭 생성 시 우항의 타입을 생략할 수 있습니다.
List<String> list = new ArrayList<>();
non refiable varagrs
제네릭 가변 인자 사용 시 발생하던 경고를 @SafeVarargs로 억제할 수 있게 되었습니다.
동일 처리 예외 통합
Multi-catch: catch (IOException | SQLException e)처럼 | 연산자로 여러 예외를 한 번에 잡을 수 있습니다.
Try-with-resources
AutoCloseable을 구현한 객체를 try() 안에 선언하면, 별도로 close()를 호출하지 않아도 블록 종료 시 자동으로 자원이 반납됩니다.
try (FileInputStream fis = new FileInputStream()) { }
Objects 유틸리티 클래스 추가
null 체크나 해시값 계산 등을 안전하게 도와주는 유틸리티 클래스가 추가되었습니다.
Objects.equals(), Objects.requireNonNull()

fork/join 관련 클래스들 (work steal) 추가
큰 작업을 작은 단위로 쪼개고(Fork), 작업이 끝난 유휴 스레드가 다른 스레드의 대기 작업을 가져와 처리하는 Work-Stealing 알고리즘이 핵심입니다.

2진수 표현법 추가
0b로 시작하는 2진수 표현과 큰 숫자에 언더바(_)를 넣어 가독성을 높이는 방식(1_000_000)이 도입되었습니다.
비트 연산 가독성 개선
TransferQueue
생산자가 소비자가 메시지를 받을 때까지 대기(block)할 수 있는 기능을 제공하여 데이터 전달의 신뢰성을 높였습니다.
BlockingQueue보다 고성능 케이스 존재
NIO2 등장
Files 클래스/ Path 인터페이스
File 클래스를 대체하는 Files, Paths, FileSystems, FileStore가 나왔다.
파일/디렉토리 편의 메서드의 용도이다.
파일 생성/복사/이동/삭제 API 통합되었다.
Files.readAllLines(), Files.copy()

WatchService
특정 디렉토리의 파일 생성, 수정, 삭제 등의 변화를 실시간으로 감시하는 이벤트 기반 API입니다.
SeekableByteChannel
랜덤 접근 IO
파일 내 임의의 위치에서 읽고 쓰기가 가능합니다.
NetworkChannel MuilticastChannel
네트워크 채널 기능 확장
네트워크 소켓 설정을 더 세밀하게 제어하고 멀티캐스트를 지원합니다.
AsynchronousFileChannel
비동기 파일 I/O
파일 입출력을 비동기적으로 처리합니다.
JDBC4.1
Connection, Statement, ResultSet 등이 AutoCloseable을 상속받아 try-with-resources에서 사용 가능해졌습니다.

# Java 8 - 함수형 프로그래밍의 도입
람다(Lambda)
익명 함수를 지칭하며, (parameters) -> { body } 형태로 작성합니다.

메서드 참조(Method Reference)
이미 존재하는 메서드를 더 간결하게 가리키는 방식입니다. (예: System.out::println)

함수형 인터페이스(Functional Interface)
단 하나의 추상 메서드만 가진 인터페이스(예: Predicate, Consumer, Function)로, 람다식의 기반이 됩니다. @FunctionalInterface 어노테이션을 사용해 명시할 수 있습니다.

스트림
stream map/filter
조건에 맞는 데이터를 걸러내거나(filter), 데이터의 형태를 변환(map)합니다.

forEach
스트림의 요소를 하나씩 순회하며 최종 처리를 수행합니다.

병렬 배열
Arrays.parallelSort() 등을 통해 멀티코어 성능을 활용하여 배열을 빠르게 정렬할 수 있습니다.

옵셔널
NullPointerException을 방지하기 위해 탄생한 래퍼(Wrapper) 클래스입니다. null일 수도 있는 값을 객체 안에 담아 안전하게 처리하도록 유도합니다.

인터페이스의 기본 메서드
인터페이스 내부에 실제 로직이 담긴 메서드를 선언할 수 있게 되었습니다.

목적: 기존 인터페이스를 구현하는 하위 클래스들을 깨뜨리지 않고 새로운 기능을 추가하기 위함입니다. (Iterable 인터페이스에 forEach가 추가된 것이 대표적입니다.)

날짜 관련 클래스
기존의 엉망이었던 Date, Calendar를 대체합니다.

특징: 불변(Immutable) 객체이며, LocalDate, LocalTime, LocalDateTime 등 직관적인 API를 제공합니다. 타임존 처리도 훨씬 명확해졌습니다.

StringJoiner
문자열 사이에 구분자(comma 등)를 넣고 앞뒤에 접두사/접미사를 붙여 합치기 매우 편리해졌습니다.

# Java 9
Java 9은 "모듈화"라는 거대한 변화와 함께, 개발자들의 소소한 불편함을 해결해 준 '현대적 자바의 시작점'

Compact Strings
기존 char 구조에서 데이터에 따라 byte를 혼용하도록 변경되어 메모리 사용량을 획기적으로 줄였습니다.
인터페이스의 private 메서드
Java 8에서 default 메서드가 생기면서 내부 로직 중복 문제가 있었는데, 이를 해결하기 위해 인터페이스 안에서도 private 메서드를 쓸 수 있게 되었습니다
pub sub 프레임워크
Flow API (Pub/Sub 프레임워크)
발행-구독(Publisher-Subscriber) 모델을 표준화한 API입니다. RxJava나 Project Reactor 같은 리액티브 라이브러리들이 상호 호환될 수 있는 규격(Flow.Publisher, Flow.Subscriber 등)을 제공합니다.

자바의 모듈화-직소 프로젝트
자바를 조각(모듈)으로 나누어 관리할 수 있게 되었습니다.
JPMS (Java Platform Module System): module-info.java 파일을 통해 모듈 간의 의존성을 정의합니다.
목적: 대규모 시스템의 구조화, 보안 강화, 그리고 경량화를 위함입니다.
내부 API 접근 제한: 그동안 "어차피 되니까" 관례처럼 쓰던 sun.misc.Unsafe 같은 내부 API에 대한 접근을 차단하여, 자바 플랫폼의 안정성을 높였습니다.
JDK 내부 API 접근 제한
→ “어차피 되니까 쓰자” 문화에 제동

JShell
파이썬처럼 터미널에서 즉석으로 자바 코드를 실행해 볼 수 있는 도구입니다. 간단한 API 테스트를 위해 프로젝트를 만들 필요가 없어졌습니다.
컬렉션 팩토리 메서드
List.of(), Set.of(), Map.of()

기존: Arrays.asList()나 여러 줄에 걸친 add() 작업
Java 9: List.of("A", "B") 한 줄로 불변(Immutable) 컬렉션을 즉시 생성합니다.
HTTP/2 클라이언트 (인큐베이팅)
기존의 구식 HttpURLConnection을 대체할 현대적인 HTTP 클라이언트가 처음 등장했습니다. (비동기 처리 및 HTTP/2 지원)
ProcessHandle API
운영체제의 프로세스(PID 등)를 자바 코드 내에서 직접 제어하고 정보를 얻기가 매우 쉬워졌습니다.

Stack-Walking API
스택 트레이스(Stack Trace)를 효율적으로 탐색하고 필터링할 수 있는 기능을 제공합니다. 성능상 이점과 유연성을 동시에 챙겼습니다.

# Java 10
var
초기화 값이 있는 지역 변수에서 타입을 생략할 수 있게 되었습니다.

코드: var list = new ArrayList<String>(); (컴파일러가 타입을 추론함)
주의: 멤버 변수나 메서드 파라미터에는 사용할 수 없으며, 가독성을 해치지 않는 선에서 사용이 권장됩니다.

수정 불가 collection
이미 존재하는 컬렉션을 불변으로 복사하거나, 스트림 결과를 불변 컬렉션으로 모으는 기능이 추가되었습니다.

List.copyOf(), Set.copyOf(), Map.copyOf(): 기존 컬렉션으로부터 불변 컬렉션 생성.

toUnmodifiableList(): 스트림 결과를 불변 리스트로 수집.

GC 개선/ Application Class-Data Sharing
Parallel Full GC (for G1)
G1 GC의 Full GC 성능을 개선하여 'Stop-the-world' 시간을 줄였습니다.

Application Class-Data Sharing (AppCDS)
여러 자바 프로세스가 공유하는 클래스 메타데이터를 메모리에 아카이브하여 애플리케이션 시작 시간과 메모리 점유율을 줄였습니다.

# Java 11
HTTP Client (표준화)
Java 9부터 예고되었던 새로운 HTTP 클라이언트가 드디어 정식 표준이 되었습니다.

장점: Apache HttpClient 같은 외부 라이브러리 없이도 HTTP/2, 비동기(Asynchronous), WebSockets를 깔끔하게 지원합니다.

String & Files 유틸리티 메서드 추가
문자열 처리가 훨씬 "현대적"으로 변했습니다.

isBlank(): 공백만 있는 문자열인지 확인.

lines(): 문자열을 라인별 스트림으로 반환.

repeat(n): 문자열을 n번 반복.

Files.writeString(), Files.readString(): 복잡한 스트림 처리 없이 한 줄로 파일 읽고 쓰기 가능.

Lambda에서 var 사용 가능
Java 10의 var가 람다식 파라미터까지 확장되었습니다.

코드: (var x, var y) -> x + y
왜 쓰는가? 파라미터에 @Nullable 같은 어노테이션을 붙여야 할 때, 타입은 생략하면서 어노테이션만 붙일 수 있어 편리합니다.

레거시 제거 및 실행 간소화
Java EE / CORBA 제거: JDK 몸집을 줄이기 위해 관련 모듈을 완전히 제거했습니다. 이제 JAXB 등은 별도 라이브러리(Maven/Gradle)로 추가해야 합니다.
→ Spring 등 생태계로 완전 위임

컴파일 없이 실행: javac 없이 java HelloWorld.java 명령만으로 소스 파일을 즉시 실행할 수 있게 되어, 가벼운 스크립트 작성용으로 자바를 쓰기 좋아졌습니다.

새로운 가비지 컬렉터 (GC)
Epsilon GC (No-Op): 메모리를 할당만 하고 회수(GC)하지 않습니다. 성능 테스트나 아주 짧은 수명의 작업을 수행할 때 극강의 성능을 위해 사용합니다.

ZGC (실험적 도입): 대용량 메모리에서도 10ms 이하의 정지 시간을 보장하는 혁신적인 GC가 처음 등장했습니다.

# 자바 12
switch 문 확장 (Preview)
case L -> 형태의 화살표 표현식이 등장하여 break 없이도 깔끔하게 값을 반환할 수 있게 되었습니다.

int numLetters = switch (day) {
case MONDAY, FRIDAY, SUNDAY -> 6;
case TUESDAY -> 7;
default -> 0;
};
String 유틸리티
indent()(들여쓰기), transform()(문자열 변환 함수 적용) 메서드 추가.

Teeing Collector
두 개의 서로 다른 컬렉터를 결합해 하나의 결과로 만드는 강력한 기능입니다. (예: 리스트의 합계와 평균을 동시에 구하기)

CompactNumberFormat
숫자 형식을 1M, 1천처럼 축약해서 보여주는 포맷터가 추가되었습니다.

# 자바 13
이 시기에는 나중에 정식 도입될 기능들이 '미리보기(Preview)' 형태로 많이 등장했습니다.

Text Blocks (Preview)
여러 줄 문자열을 """로 감싸서 아주 편하게 작성할 수 있게 되었습니다.

ZGC (개선)
할당되지 않은 메모리를 OS에 반환하는 기능이 추가되었습니다.
지연된 메모리를 반환하여 컨테이너 환경에 유리해졌습니다.

# 자바 14
Switch Expressions (Standard)
드디어 화살표(->) 방식의 스위치 문이 정식 표준이 되었습니다.

Helpful NullPointerExceptions
어떤 변수가 null인지 정확히 짚어주는 친절한 에러 메시지가 출력됩니다.

기존의 자바는 NullPointerException(NPE)이 발생하면 "몇 번째 줄에서 터졌다"는 것만 알려줬습니다. 한 줄에 여러 참조 객체가 있을 경우, 대체 누구 때문에 터졌는지 알 길이 없어 디버깅이 고역이었습니다.
예시 코드
다음과 같은 중첩 객체 호출이 있다고 가정해 봅시다.

// Java 14 미만
String city = user.getDetails().getAddress().getCity();
Java 14 이전: java.lang.NullPointerException (끝)

개발자는 알기 어렵습니다: user가 null인가? getDetails() 결과가 null인가? 아니면 getAddress()가 null인가?

Java 14 이후 (Helpful NPE): Cannot invoke "Address.getCity()" because the return value of "Details.getAddress()" is null

해석: "Details.getAddress()의 반환값이 null이라서 getCity()를 호출할 수 없어요!"라고 정확히 집어줍니다.

# 자바 15
Text Blocks (Standard): """ 멀티라인 문자열이 정식으로 도입되었습니다.
Hidden Classes
런타임에 클래스를 동적으로 생성하는 프레임워크(Spring 등)를 위해, 외부에서 접근할 수 없는 '숨겨진 클래스' 개념이 도입되었습니다.

# 자바 16
Record (Standard)
DTO나 VO를 만들 때 필드, Getter, equals, hashCode, toString을 단 한 줄(record User(String name) {})로 끝내버리는 레코드가 정식 도입되었습니다.

Pattern Matching for instanceof (Standard)
if (obj instanceof String s) 처럼 타입을 확인하면서 동시에 변수를 선언할 수 있게 되어 불필요한 캐스팅이 사라졌습니다.

# 자바 17
Sealed Classes (Standard)
상속받을 수 있는 하위 클래스를 명시적으로 제한(permits)할 수 있는 기능입니다. 도메인 설계 시 보안과 구조적 엄격함을 더해줍니다.

보안 및 레거시 제거
Applet API가 제거되고, 내부 API 접근 제한이 더욱 강력해졌습니다.