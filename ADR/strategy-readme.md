[목표]
- 설계 능력을 함양하기 위함
- 이를 위해서 어떤 능력을 길러야하고, 그걸 위해서 어떤 방법을 적용하면 되는지 지속적인 고찰을 하기 위함.

[이를 위해서 고민해야할 포인트]
문제 정의 능력 (problem framing / problem definition)
모호한 상황에서 “우리가 진짜로 결정해야 하는 핵심 질문이 뭔지”를 뽑아내는 능력입니다.
예: “어떤 리턴 타입을 쓸까?”가 아니라 “클라이언트가 최소한으로 필요로 하는 정보는 무엇인가?”, “우리 팀 API 가이드라인은 무엇인가?” 같은 질문으로 재구성하는 것.

요구사항 분석 능력 (requirements analysis)
비즈니스 목표, 품질 속성(가독성, 일관성, 확장성 등), 이해관계자 요구를 정리해서 설계 기준으로 바꾸는 능력입니다.
예: “팀에서 응답 포맷 일관성을 제일 중요하게 본다” → 그럼 개별 엔드포인트 최적화보다 공통 Response 래퍼를 우선 고려해야겠죠.

설계 트레이드오프 판단 능력 (design trade-off analysis)
여러 대안을 놓고 장단점을 비교해서 “이 맥락에선 어떤 걸 택하는 게 맞는가”를 고르는 능력입니다.
예: ResponseEntity<HttpStatus> vs ResponseEntity<Void> vs ResponseEntity<CommonResponse<T>>를, 단순 취향이 아니라 팀 컨벤션, 유지보수성, 클라이언트 UX 기준으로 비교하는 것.


[키워드]
“trade-off”
“prioritize requirements”
“evaluate design alternatives”

[책]
소프트웨어 요구사항의 정수」
Michael Jackson의 “Problem Frames” 계열


