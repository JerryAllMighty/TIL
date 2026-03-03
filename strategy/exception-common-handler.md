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