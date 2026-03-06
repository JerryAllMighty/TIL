<details>
<summary>enum을 사용하여 타입 안전한 상태 머신을 구현하는 방법은 무엇인가요?</summary>
<div markdown="1">
enum 기반 상태 머신은 각 상태를 enum 상수로 표현해서 타입 수준에서 상태를 한정하기 때문에 타입 안전성을 얻을 수 있다. 또한 enum의 각 상수는 
jvm 내에서 싱글톤으로 만들어지기 때문에 상태 객체를 불변으로 설계하면 공유해도 안전한다.
</div>
</details>