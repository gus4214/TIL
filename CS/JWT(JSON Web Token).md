# JWT(JSON Web Token)

## JWT(JSON Web Token)란?

JWT 란 데이터가 JSON으로 이루어져 있는 토큰을 의미한다.

JWT는 토큰 자체를 정보로 사용하는 Self-Contained 방식으로 정보를 안전하게 전달한다.

> **JSON (JavaScript Object Notation)**
> ”자바스크립트 객체 표기법”
> 데이터를 쉽게 교환하고 저장하기 위한 텍스트 기반의 데이터 교환 표준이다.
> JSON은 텍스트 기반이기 때문에 다양한 프로그래밍 언어에서 데이터를 읽고 사용할 수 있다.

🤝 JWT는 주로 static 변수와 로컬 스토리지에 저장한다고 함

→ static 변수에 저장하는 이유는 HTTP 통신을 할 때 마다 JWT를 HTTP 헤더에 담아서 보내야 하는데,
이를 로컬 스토리지에서 계속 불러오면 오버헤드가 발생하기 때문 !

- static 변수란?
  - 클래스 변수, 정적변수 라고도 함
  - 메모리 할당을 한번만 하게 되어 메모리 사용에 이점이 있음
  - 전역 변수와 static 변수가 할당되는 영역인 static 영역에 저장된다.
  - 프로그램의 시작과 동시에 할당되고, 프로그램이 종료되어야 메모리에서 소멸
- 오버헤드란?
  - 특정 기능을 수행하는데 드는 간접적인 시간, 메모리 등 자원을 말한다.
  - 예를 들어, 5초 걸리는 기능이 간접적인 원인으로 10초 걸린다면 오버헤드는 5초

<br />

## JWT의 구조를 알아보자

JWT는 `.` 을 구분자로 3가지의 문자열로 구성되어 있다.

aaaa.bbbbb.ccccc 의 구조로 앞부터 헤더(header), 내용(payload), 서명(signature)로 구성

### 1. 헤더 (Header)

- 토큰의 타입과 해시 암호화 알고리즘으로 구성

alg는 헤더를 암호화 하는 것이 아닌, **Signature를 해싱하기 위한 알고리즘을 지정**

typ는 토큰의 타입을 지정한다. JWT이기에 "JWT"라는 값이 들어간다.

alg : 해싱 알고리즘을 지정한다.

```jsx
{
  "alg": "HS256",
  "typ": "JWT"
}
```

### 2. Payload(내용)

- 토큰에 사용자가 담고자 하는 정보를 담는 곳

Payload에는 토큰에서 사용할 정보의 조각들인 Claim 이 담겨있고,

이는 JSON(Key/Value) 형태의 한 쌍으로 이루어져 있다.

클레임은 크게 세분류로 나뉘어짐

1. **등록된 클레임 (Registered Claim)**

   서비스에 필요한 정보들이 아닌, 토큰에 대한 정보를 담기위해 이름이 이미 정해진 클레임들
   등록된 클레임의 사용은 모두 선택적(optional)이며, 사용할 것을 권장

   **iss :** 토큰 발급자 (issuer)

   **sub :** 토큰 제목 (subject)

   **aud :** 토큰 대상자 (audience)

   **exp :** 토큰의 만료시간 (expiraton) : NumericDate 형식으로 되어 있어야 함

   **nbf :** 토큰 활성 날짜(not before) :  이 날이 지나기 전의 토큰은 활성화되지 않는다.

   **iat :** 토큰 발급 시간(issued at) : 토큰 발급 이후의 경과 시간을 알 수 있음

   **jti :** JWT 고유 식별자(JWT ID) : 중복 방지를 위해 사용하며, 일회용 토큰(Access Token) 등에 사용

2. **공개 클레임 (Public Claim)**

   사용자 정의 클레임으로, 충돌이 방지된 이름을 가져야 함
   → 충돌 방지를 위하여 클레임 이름을 URI 형식으로

   ```jsx
   {
   	"https://hyun.tistory.com/jwt_claims/is_admin" : true
   }
   ```

3. **비공개 클레임 (Private Claim)**

   사용자 정의 클레임으로, 클라이언트와 서버가 협의하에 임의로 지정한 정보를 저장하여 사용

   ```jsx
   {
    "userId": "gus4214"
    "username": "hyun"
   }
   ```

### 3. Signature(서명)

- 토큰을 인코딩 하거나 유효성 검증을 할 때 사용하는 고유한 암호화 코드
- 헤더(Header)와 내용(Payload)의 값을 각각 BASE64로 인코딩하고, 인코딩한 값을 비밀키를 이용해
  헤더에서 정의한 알고리즘으로 해싱을 하고, 이 값을 다시 BASE64로 인코딩하여 생성

---

<br />

## “서버 기반 인증”과 “토큰 기반 인증”에 대해서

<br />

### > 서버 기반 인증 시스템 (Session / Cookie)

- 세션 기반의 인증시스템으로 서버 측에서 사용자들의 정보를 기억하기 위해 세션을 유지함
  → 이는 메모리, 디스크, 데이터베이스 등을 통해 관리
- 클라이언트로부터 요청을 받으면 클라이언트의 상태 정보를 저장하여 유지해야 하기 때문에
  **Stateful** 한 구조를 가진다.

🤔 **인증 방식**

1. 사용자가 로그인 시 올바른 사용자인지 확인을 하고, 고유한 세션 ID 값을 부여하여 세션 저장소에 저장하고 클라이언트에게 발급
2. 클라이언트는 세션 ID를 받아 브라우저 쿠키에 저장하고, 인증이 필요한 요청마다 쿠키에 세션 ID를 담아 헤더에 보냄
3. 서버에서는 쿠키를 받아 세션 저장소와 비교하여 올바른 요청인지 확인
4. 인증이 완료되고 서버는 요청에 응답

👉 **장점**

- 중요한 정보는 서버에 있으므로 쿠키 자체(세션 ID)에는 유의미한 값을 가지고 있지 않음

👉 **단점**

- 만약 해커가 훔친 쿠키를 이용하여 HTTP 요청을 보내면 서버에선 올바른 사용자가 보낸 요청인지 알 수 없음
  → 세션에 유효시간을 넣어줘야 함
- 서버에 세션을 저장하므로 사용자가 늘어남에 따라 과부하를 줄 수 있어 확장성이 불리하다.

<br />

### > 토큰 기반 인증 시스템 (JWT)

- 위의 단점을 극복하기 위해 나온 것이 “토큰 기반 인증 시스템”
- 인증 받은 사용자에게 토큰을 발급해주고, 서버에 요청을 할 떄 HTTP 헤더에 토큰을 함께 보내
  인증받은 사용자(유효성 검사)인지 확인
- 사용자의 인증 정보를 서버에 저장하지 않고 클라이언트의 요청으로만 인가를 처리하므로 **Stateless** 한 구조
- JWT ⇒ 인증에 필요한 정보를 암호화 시킨 토큰
  세션 / 쿠키 방식과 유사하게 클라이언트는 Access Token(JWT)을 HTTP 헤더에 실어 server로 보낸다.

🤔 **인증 방식**

1. 사용자가 로그인 시 올바른 사용자임을 확인하고 클라이언트에게 Access Token(JWT)을 발급해준다.
2. 클라이언트는 전달받은 토큰을 저장해 두고, 인증이 필요한 요청마다 토큰을 HTTP 헤더에 담아 보낸다.
3. 서버에서는 암호화된 토큰을 복호화 하여 올바른 요청인지 확인한다.
4. 인증이 완료되고 서버는 요청에 응답!

👉 **장점**

- 서버 기반 인증 시스템은 저장소의 관리가 필요하다. 하지만 토큰 기반은 Access Token을 발급해준 후 요청이 들어오면 검증만 해주면 되기 때문에 추가 저장소가 필요 없음 ⇒ Stateless 함
- 쿠키를 사용함으로 인해 발생하는 취약점이 사라진다. 하지만, 토큰을 사용하는 환경에서의 취약점에 대비해야 함
- 확장성이 뛰어남 ⇒ 토큰 기반으로 하는 다른 인증 시스템에 접근이 가능 ex) 구글, 페이스북

👉 **단점**

- 이미 발급된 JWT를 돌이킬 수 없음 ⇒ 서버 기반 인증 시스템처럼 저장소를 사용하는 경우에는 해당 세션이 악의적으로 사용될 경우 지워버리면 되지만, JWT는 한 번 발급되면 유효기간이 완료될 때 까지는 계속 사용 가능함 ⇒ 유효기간이 지나기 전까진 털릴 수도;;
  🤔 토큰 기반 인증 방식을 사용한다고 해서 해킹의 위험에서 벗어난 것은 아님
- JWT의 길이가 김 ⇒ 인증이 필요한 요청이 많아질수록 서버의 자원 낭비가 발생!!

---

<br />

## Stateful과 Stateless의 개념

이 둘은 클라이언트와 서버간의 네트워크 통신이 어떻게 이루어지는지에 대한 개념이다. ⇒ **네트워크 프로토콜**

### Stateful

- **세션이 종료될 때까지, 클라이언트의 세션 정보를 저장**하는 네트워크 프로토콜
- ex) 은행(서버)은 고객(클라이언트)의 인증 정보(세션 상태)와 결제 내역(세션 정보)를 가지고 있다.
- **장점**: 서버는 클라이언트의 세션 정보를 저장하므로, 갑자기 통신이 중단되도 중단된 곳 부터 다시 시작 가능
- **단점**: 클라이언트의 세션 정보가 새로 scale out 된 서버에 저장 되어 있지 않다. ⇒ 확장성이 좋지 않다.

### Stateless

- **서버가 클라이언트의 세션 상태 및 세션 정보를 저장하지 않는** 네트워크 프로토콜
  → 요청에 대한 응답만 처리하는 방식
  → 클라이언트가 송신하려 했던 모든 데이터가 서버쪽에 수신 되었는지 확인하지 않는다.
- ex) 온라인 검색창에 질문을 입력하다가 요청이 중단돼도, 다시 검색하면 된다.
- **장점**: 서버가 클라이언트의 세션 상태 및 세션 정보를 저장하지 않음 ⇒ 확장성이 좋음
  → 이전의 클라이언트의 요청을 유지하지 않는다.
  → 기존의 서버가 혼잡해져 새로운 서버를 가져다 놓아도 계속 일을 처리할 수 있다.
- **단점**: 서버가 세션 상태 및 세션 정보를 저장하지 않기 때문에, 송신할 데이터의 양이 많아짐
  → 클라이언트가 하고자하는 최종 목적을 위해 전달해야하는 내용이 많아진다.

- 세션 상태란?
  - 클라이언트와 서버간 통신 인증이 된 상태 / 인증된 상태에서 데이터 송수신이 가능하다.
- 세션 정보란?
  - 한 세션 내에서, 클라이언트가 서버에 전송할 데이터 정보를 의미한다.
  - 서버는 세션 유지 시간이 지나거나, 클라이언트가 전송하려했던 데이터를 모두 수신할 때까지 클라이언트와의 세션 상태를 유지한다.

💡 참고

- [JWT란 무엇일까?](https://dev-coco.tistory.com/103)
- [https://nyeongnyeong.tistory.com/194](https://nyeongnyeong.tistory.com/194)
- [https://wooono.tistory.com/366](https://wooono.tistory.com/366)
