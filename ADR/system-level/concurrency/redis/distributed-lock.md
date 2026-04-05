[왜 쓰나 분산락? 언제 쓰면 좋나?]
- 동시성 이슈?


[ZooKeeper vs Redis vs MySql]


[Redis]
- 메모리 내에서의 데이터 접근은 RDB보다 빠른 응답시간 제공

[Redisson]
- Lock Interface 지원, 락에 대한 타임아웃과 같은 설정 지원
- pub-sub : 락이 해제되면 구독하던 클라이언트가 해제 신호를 받고 락을 획득
- 락은 트랜잭션 커밋 이후 해제해야한다

[Lettuce]
- setnx, setex 등을 이용해 개발자가 retry나 timeout을 구현해야하는 비용
- spin lock : 지속적으로 레디스에게 락이 해제되었는지 요청을 보냄

[MySql]
- User_Level Lock은 락에 이름을 지정해 어플리케이션 레이어에서 제어가 가능
- 별도의 커넥션 풀 관리 필요


[참고]
- https://techblog.woowahan.com/2631/
- https://helloworld.kurly.com/blog/distributed-redisson-lock/