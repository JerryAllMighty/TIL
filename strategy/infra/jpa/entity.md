[설계 포인트]
- 키 값 생성 전략은 db 벤더마다 다를 수 있다. auto 도 좋은 전략
- org.hibernate,cfg.ImprovedNamingStrategy는 기본적으로 테이블 명이나 컬럼 명이 생략되면 자바의 카멜 표기법은 테이블의 언더 스코어 기법으로 매핑

- 엔티티 id 값은 왜 다르게 명명해야하나?
orderItem에서 다 에러남.



[연관관계 판단 기준]
- 양방향이다?
연관관계 편의 메서드를 생각하자. 관리 요소를 줄이고 휴먼 에러를 줄인다.

- 연관관계 편의 메서드?
일단 단방향으로 시작: 우선 @ManyToOne만 설정해서 기능을 구현.
필요할 때 양방향 추가: 개발하다 보니 "주문 객체에서 아이템 리스트가 꼭 필요하네?"라는 상황이 오면 그때 @OneToMany를 추가하고 mappedBy를 설정.
반대 방향(OneToMany)은 권력 없음: 양방향을 추가하더라도 **"주인은 항상 외래 키가 있는 ManyToOne 쪽이다"**
또 명시적으로 순환 참조를 방지할 수 있다.

[직렬화 시 무한 루프 생기나 양방향은? 어떻게 해결하나?]
- 연관관계는 양방향은 다대일이 2개인 것.
  되도록이면 ManyToOne으로 다대일 방향에서 관계 주인 정립하는 것이 좋다.

[생성자]
- 기본 생성자 필수이다. jpa는 기본적으로 db의 테이블을   자바 객체로 바꿀 떄 리플렉션이라는 기술을 사용.
  리플렉션은 클래스의 이름만 알아도 객체를 만들 수 있지만, 어떤 생성자를 주입해야할 지 알 수 없기에 일단 기본 생성자를 만든 후 필드 값을 주입.
- jpa는 연관된 엔티티를 나중에 가져오는 레이지 로딩을 위해서 프록시를 활용합니다. 하지만 이 프록시는 엔티티를 상속합니다.
  상속의 특성상 자식이 생성될 떄 부모의 생성자도 호출됩니다. 이 때 부모의 생성 인자 결정이 어려워 기본 생성자를 호출합니다.
  접근 제어자는 protected가 좋다. 프록시 생성 시 기존 엔티티 클래스를 상속받는 객체를 만들기에 protected로도 접근이 가능하다.
  public은 무분별한 객체 생성이 가능해서 지양한다.
- 정적 팩토리 메서드? 빌더 패턴?
생성자 파라미터 개수가 많아지거나 선택적인 파라미터가 많으면 빌더 고려해볼만 하다.
간단하고 명확한 객체 생성이 필요하거나 메서드 이름을 사용해야하는 경우(명확한 의도 드러내기), 유연한 반환 타입 지정이 필요하면 정적 팩토리 메서드 사용 가능하다 
  https://www.inflearn.com/community/questions/1359972/%EB%B9%8C%EB%8D%94-%ED%8C%A8%ED%84%B4-vs-%EC%A0%95%EC%A0%81-%ED%8C%A9%ED%86%A0%EB%A6%AC-%EB%A9%94%EC%84%9C%EB%93%9C?srsltid=AfmBOoouiQLt4xX0QTDBpyeawCm_-jQ-kqZkd6a83xgWlBiUa82NNAyb
  https://kwonnam.pe.kr/wiki/java/lombok/pitfall
  https://f-lab.kr/insight/java-static-factory-methods
  https://inpa.tistory.com/entry/GOF-%F0%9F%92%A0-%ED%8C%A9%ED%86%A0%EB%A6%AC-%EB%A9%94%EC%84%9C%EB%93%9CFactory-Method-%ED%8C%A8%ED%84%B4-%EC%A0%9C%EB%8C%80%EB%A1%9C-%EB%B0%B0%EC%9B%8C%EB%B3%B4%EC%9E%90#%ED%8C%A9%ED%86%A0%EB%A6%AC_%EB%A9%94%EC%84%9C%EB%93%9C_%ED%8C%A8%ED%84%B4_%EA%B5%AC%EC%A1%B0

[equals와 hashCode의 구현입니다]
  프록시 객체를 사용하기 때문에 instanceof 비교를 사용해야 하며, 필드에 직접 접근하기보다는 Getter를 사용해야 프록시가 초기화되어 정상적인 값을 비교할 수 있습니다.??

[Getter는 반드시 다 필요한가?]


