[서두]
- 예외처리를 각종 기준에 따라 구현했다면 이를 효과적으로 관리할수 있는 것도 필요하다
- 토비의 스프링 학습을 해보니 핸들러 예외 리졸버를 사용하면 조금 더 수월하게 관리를 할 수 있는 것 같다.

[내용]
- 예외 공통 처리 전략
기본적으로 예외를 처리하기 위한 클래스를 만들 때 사용 가능한 리졸버와 어노테이션들이다.
AnnotationMethodHandlerExceptionResolver
@ExceptionHandler를 통해서 예외처리를 맡겨주는 핸들러 예외 리졸버.

ResponseStatusExceptionResolver
@ResponseStatus를 붙이고 특정 예외 발생시 의미 있는 HTTP 응답 상태를 돌려주는 방법이다.

```
@RestControllerAdvice
public class ExceptionController {
    private String getClassName(Exception e) {
        return e.getClass().getName();
    }

    @ExceptionHandler(MemberDuplicateException.class)
    @ResponseStatus(HttpStatus.CONFLICT)
    public ErrorMessage memberDuplicateExceptionHandler(MemberDuplicateException memberDuplicateException) {
        return new ErrorMessage(getClassName(memberDuplicateException), memberDuplicateException.getMessage());
    }
}
```

이런 식으로 @RestControllerAdvice 를 사용하면 스프링 AOP를 활용해 컨트롤러로 올라온 예외들을 잡아서 한 번에 처리할 수 있다.

[결론]
- 서비스 레이어에서 커스텀으로 던져진 예외들이나 기타 예외들이 컨트롤러 등의 호출부로 예외가 던져지면 이를 공통으로 잡아서 처리하는 방식도 고려해볼 수 있다
- 한 곳에서 예외 처리를 집중식으로 관리가 가능하고, AOP를 활용하여 예외를 관리할 수 있기 때문에 로그에 집중할 수 있다는 점도 이점이다.



[리턴 형태]
- 리턴해주는 부분에 있어서 어떠한 정보를 리턴하고, 어떠한 형태로 가져갈지 고민 필요
> Throwable 클래스의 정보가 담겨서 외부로 노출되면 안되니 반드시 커스텀 객체를 통해서 정보를 전달할 것
> 만약 개발자가 많아지거나 프론트와 소통 결과로 리턴 형태를 반드시 픽스해야한다면 SucceessResponse, ErrorResponse 등을 고민할 것
> 상황에 따라 dto 도 가능
> 서버 정보는 개발자 등이 보고 디버깅 가능하게 로그로만 남길 것.
> http 상태 코드의 필요에 대해서 고민할 것 (ErrorCode안에서의 응집도, advice에서의 관심사분리냐)
>> 상태코드가 변경이 많다면 밖으로 빼도 되고, 만약 에러 코드의 생성 형태를 통일해서 가져가고 싶다면 enum에서 강제해도 괜찮다.  
>> 또한 여러명이 작업한다 가정하면 BaseException을 활용해도 좋다.
>> 개발자 내부 기록용으로는 Thrwoable 클래스의 정보를, 외부 노출은 ErrorCode를 활용하여 커스텀하여 리턴해주는 것도 좋은 방법이다. 