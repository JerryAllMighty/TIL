[설계 포인트]
- null을 리턴하지 말라. 호출부에서 null 방어 코드를 또 짜야한다.
대신 불변으로 설계된 빈 리스트나 배열을 리턴하라. Collections.emptyList나  emptySet, emptySet을 써라
- 