<details>
<summary>인증(Authentication)과 인가(Authorization)의 차이는?</summary>
<div markdown="1">

인증은 사용자가 누구인지 확인하는 과정이고, 인가는 인증된 사용자가 어떤 자원에 어떤 행동을 할 수 있는지 권한을 확인·제어하는 과정이다.

</div>
</details>

<details>
<summary>세션 기반 인증과 JWT 기반 인증의 차이는?</summary>
<div markdown="1">

세션 기반은 서버가 세션 상태를 저장하는 stateful 방식이고, JWT는 서명된 토큰만 클라이언트가 들고 다니고 서버는 상태를 저장하지 않는 stateless 방식이다.

</div>
</details>

<details>
<summary>JWT의 Header·Payload·Signature는 각각 어떤 역할을 하나요?</summary>
<div markdown="1">

Header는 토큰 타입과 알고리즘 정보를, Payload는 사용자·만료시간 등 클레임을, Signature는 비밀키로 서명해 토큰 위변조 여부를 검증하는 역할을 한다.

</div>
</details>

<details>
<summary>JWT를 사용할 때 대표적인 보안 이슈와 대응 방법은 무엇인가요?</summary>
<div markdown="1">

토큰 탈취와 강제 로그아웃 어려움이 대표 이슈라서 HTTPS 강제, 짧은 만료 시간, Refresh Token + 서버 저장, 블랙리스트·토큰 버전 관리 등을 함께 사용한다.

</div>
</details>

<details>
<summary>Access Token과 Refresh Token을 왜 분리해서 사용하나요?</summary>
<div markdown="1">

Access Token은 짧게 가져가서 탈취 피해를 줄이고, Refresh Token은 서버가 저장·검증하면서 Access Token을 재발급하기 위해 분리해 사용한다.

</div>
</details>

<details>
<summary>Spring Security에서 인증 흐름을 간단히 설명해보세요.</summary>
<div markdown="1">

필터가 요청에서 인증 정보를 추출해 AuthenticationManager에 위임하고, 검증에 성공하면 Authentication을 SecurityContext에 저장한 뒤 이후 인가 판단에 사용한다.

</div>
</details>

<details>
<summary>JWT 기반 인증을 Spring Security에 넣을 때 필터는 어떻게 동작하나요?</summary>
<div markdown="1">

커스텀 OncePerRequestFilter가 Authorization 헤더에서 JWT를 읽어 검증하고, 유효하면 UserDetails로 Authentication을 만들어 SecurityContext에 넣은 뒤 체인을 계속 진행한다.

</div>
</details>
