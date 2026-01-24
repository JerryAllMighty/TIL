[서두]
- 스프링 생성자 키워드 기본 꼬리 질문 리스트이다.

1. DI(의존성 주입)의 3가지 방법과 차이점은?
   생성자 주입 / 필드 주입 / Setter 주입

2. Spring에서 생성자 주입을 권장하는 이유 3가지? 
- 순환 참조 방지 (BeanCurrentlyInCreationException 발생)
- 불변성 보장 (final 필드 가능)
- 테스트 용이 (new로 직접 주입 가능)

3. 필드 주입(@Autowired 필드)의 단점 3가지?   
- 순환 참조 시 애플리케이션 시작됨 (런타임 오류)
- 불변성 없음 (Setter처럼 변경 가능)
- 프레임워크 의존성 (테스트 어려움)
  
4. 생성자에 @Autowired 생략 가능한 조건은?   
   생성자 1개 + 주입받는 객체가 모두 @Component 빈인 경우

5. Lombok @RequiredArgsConstructor와 생성자 주입 관계는?
   final/private 필드 → 자동 생성자 생성 → @Autowired 생략 가능

6. @Lazy와 생성자 주입의 상호작용은?
   Lazy 빈은 생성자 시점에 주입 안됨 → Proxy로 대체

7. 순환 참조 해결 방법 3가지?
- @Lazy 어노테이션
- Setter 주입 사용
- @PostConstruct로 지연 초기화
   

8. Spring Boot 3.x에서 생성자 주입 기본값 변경?
   spring.main.allow-circular-references=false → 생성자 주입 우선 강제

9. @Configuration 클래스에서 생성자 주입 시 주의점?
   Proxy 모드 시 순환 참조 발생 가능 → @DependsOn 사용

10. @ComponentScan과 생성자 주입 순서?
- 컴포넌트 스캔 → 2. 빈 등록 → 3. 생성자 주입 → 4. @PostConstruct

11. @AssistedInject와 생성자 주입 조합은?
    Google Guice에서 런타임 파라미터 + DI 조합

12. Validation과 생성자 주입 충돌 해결?
- @Valid 생성자 파라미터 + BindingResult 처리

13. Profiling 시 생성자 주입 성능 영향?
- 필수 의존성만 로드 → 메모리 효율 ↑
    

