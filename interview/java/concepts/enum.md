<details>
<summary>enum을 사용하여 타입 안전한 상태 머신을 구현하는 방법은 무엇인가요?</summary>
<div markdown="1">
enum 기반 상태 머신은 각 상태를 enum 상수로 표현해서 타입 수준에서 상태를 한정하기 때문에 타입 안전성을 얻을 수 있다. 또한 enum의 각 상수는 
jvm 내에서 싱글톤으로 만들어지기 때문에 상태 객체를 불변으로 설계하면 공유해도 안전한다.
</div>
</details>

<details>
<summary> enum 기반 상태 머신을 설계할 때 불변 상태 객체를 어떻게 구현해야 공유를 안전하게 할 수 있을까요?</summary>
<div markdown="1">
 각각의 열거 상수들이 기본적으로 싱글톤에 스레드 세이프하게 보장이 되어도, 이들이 가진 필드 변수도 불변으로 설계되어야합니다.
기본적으로 수정자 메서드를 만들어 공유된 이후에 수정이 가능하게 되면 race condition 현상으로 인한 데이터 정합성 이슈가 있을 수 있습니다.
따라서 수정자 메서드는 만들지 않고, 각 변수들도 private final로 설계해야합니다. 동일한 이유인데, 생성 이후로 수정이 가능하지 않게 만들어야 스레드에 안전해 
공유가 가능하게 설계 가능합니다. 필드 접근은 getter 역할의 메서드를 통해 접근할 수 있으면 좋습니다. 
</div>
</details>


<details>  
<summary>열거 상수의 필드가 mutable인 경우에는 어떻게 race condition을 방지하고 불변성을 유지할 수 있을까요?</summary>
<div markdown="1">
원시 타입의 경우에는 final 키워드 사용 가능합니다. 
스택에 값이 저장되기에 이후 수정되는 것을 막을 수 있습니다. 
하지만 참조타입이라면 주소가 재할당되는 것을 막아주기에 추가적으로 생성시에 
List.copyOf() 처럼 불변 객체를 생성해주는 메서드를 활용하거나 기존 객체를 복사해서 변수에 할당해야합니다.
</div>
</details>


<details>  
<summary>참조 타입에서 불변 객체를 생성하는 방법 중 List.copyOf() 외에 다른 자바 내장 메서드나 방법이 있을까요?</summary>
<div markdown="1">
Collections.unmodifiableList 메서드나, List.of(), 혹은 record를 사용할 수 있습니다.
Collections.unmodifiableList는 복사 이후 원본 객체가 바뀌면 따라 바뀌기에 방어적 복사 이후 사용해야합니다. 
List.of는 ArrayList를 생성하지 않지만 매번 인자값을 모두 입력해줘야합니다. 
record는 보일러 코드를 제거해주고, 도메인 모델 자체를 불변으로 설계하는데 유용합니다. 
</div>
</details>