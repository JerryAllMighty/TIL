[고민 포인트]
- 리턴 방식 통일해야하는지?
> 커스텀 response 객체


- 유연하게 가져가야하는지?
> ResponseEntity

> 그럼 responseEntity는 기본적으로 어떤 내용 담아야하는지?
>> 상태 코드:  HTTP 통신 자체에 대한 결과
> 
>> 헤더 (Headers): "데이터에 대한 설명서"   
헤더는 클라이언트가 응답 바디를 어떻게 해석하고 처리해야 할지 알려주는 지침서 역할을 합니다.   
>
>> 바디 (Body)   
"실제 데이터"   
클라이언트가 화면에 그리거나 로직에 사용할 실질적인 내용물입니다.   
성공 시 (Success Path): 보통 JSON 형식의 객체를 담습니다.   
단일 객체(MemberDto), 리스트(List<MemberDto>), 혹은 공통 응답 객체(CommonResponse<T>) 등이 들어갑니다.   
실패 시 (Error Path): 앞서 논의한 비즈니스 에러 코드와 에러 메시지가 담긴 객체를 보냅니다.   
errorCode, errorMessage, validationErrors 등 프론트엔드가 에러 처리를 할 수 있는 재료를 제공합니다.   

