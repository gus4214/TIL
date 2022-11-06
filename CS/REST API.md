# REST API

## **REST(REpresentational State Transfer)란?**

웹에 존재하는 모든 자원(resource ⇒ 이미지, 동영상, 데이터)에 고유한 URI를 부여하여 자원에 대한 주소를 지정하는 방법론 또는 규칙

👉 **자원**의 **표현**에 의한 **상태 전달**

- 자원: 해당 소프트웨어가 관리하는 모든 것 (이미지, 영상, 그림, 문서, 데이터 등등)
- 표현: 그 자원을 표현하기 위한 이름 (DB의 도시 정보 자원이면, ‘city’를 자원의 표현으로 정한다.)
- 상태 전달: 데이터가 요청되는 시점에 자원의 상태를 전달 (JSON 혹은 XML을 통해 데이터를 주고 받음)

<br />

### > REST의 가장 중요한 특성

- 각 요청이 어떤 동작이나 정보를 위한 것인지를 그 요청의 모습 자체로 추론이 가능하다.
- RESTful 하게 만든 API는 요청을 보내는 주소만으로도 대략 이것이 무엇을 하는 요청인지 파악이 가능
  → 인수인계 받을 때도 편하다.

ex)

https://(도메인)/city → 도시의 목록을 받아오는 요청

https://(도메인)/city/3 → 그 도시 중에 인덱스 번호가 3인 도시의 정보

https://(도메인)/city/3/man?sex=male → 인덱스 번호가 3인 도시의 남자들의 정보

- 이런 식으로 자원을 구조와 함께 나타내는 형태의 구분자를 URI 이라고 한다.
- 하지만 이런 조회 뿐만 아니라 정보를 새로 넣거나 수정하거나 삭제하는 작업도 필요하다.

RESTful API는 REST 특징을 지키면서 API를 제공한다는 의미

= (프론트에서 백엔드 API를 호출할 url을 어떻게 만들것인가?)

<br />

### > REST의 구성 요소

**자원(Resource) - URI**

- 모든 자원에는 고유한 ID가 존재하고, 이 자원은 Server에 존재한다.
- 자원을 구별하는 ID는 '/exgroups/:exgroup_id'와 같은 HTTP URI
- Client는 URI를 이용해 자원을 지정하고 해당 자원의 상태(정보)에 대한 조작을 Server에 요청한다.

**행위(Verb) - Method**

- HTTP 프로토콜의 Method를 사용한다.
  - Create : POST
  - Read : GET
  - Update : PUT(정보를 통째로 갈아끼울 때) / PATCH(정보 중 일부를 특정 방식으로 변경할 때 사용)
  - Delete : DELETE

**표현 (Representation of Resouce)**

- Client와 Sever가 데이터를 주고받는 형태로 JSON, XML, TEXT, RSS 등이 있다.
- JSON, XML이 일반적으로 데이터를 주고 받는 형식

<br />

### > REST의 특징

1. **Server-Client (서버 - 클라이언트 구조)**

- 자원이 있는 쪽: Server / 자원을 요청하는 쪽: Client
- REST Server는 API를 제공하고 비즈니스 로직 처리 및 저장을 책임진다.
- Client는 사용자 인증이나 context(세션, 로그인 정보) 등을 직접 관리하고 책임진다.
- 역할을 확실히 구분시키며 서로 간의 의존성을 줄인다.

1. **Stateless (무상태)**

- HTTP 프로토콜은 Stateless 특성을 가지고 있으므로 REST 역시 무상태성을 갖는다.
- Client의 context를 Server에 저장하지 않는다.
  → 세션과 쿠키와 같은 context 정보를 신경쓰지 않아도 되므로 구현이 단순해짐
- Server는 각각의 요청을 완전히 별개의 것으로 인식하고 처리한다.
  → 각 API 서버는 Client의 요청만을 단 순 처리
  → 즉, 이전 요청이 다음 요청의 처리에 연관 돼서는 안된다.
  → Server의 처리방식에 일관성을 부여하기 때문에 서비스의 자유도가 높아짐

1. **Cacheable (캐시 처리 기능)**

- 웹 표준 HTTP 프로토콜을 그대로 사용하므로 웹에서 사용하는 기존의 인프라를 그대로 활용 가능
  → HTTP가 가진 강력한 특징 중 하나인 캐싱 기능을 적용할 수 있다.
- 대량의 요청을 효율적으로 처리할 수 있다.

1. **Layered System (계층 구조)**

- Client 는 REST API Server만 호출한다.
- REST Server는 다중 계층으로 구성될 수 있다.

1. **Uniform Interface (인터페이스 일관성)**

- URI로 지정한 Resource에 대한 요청을 통일되고, 한정적으로 수행하는 아키텍쳐 스타일을 의미한다.
- HTTP 표준 프로토콜에 따르는 모든 플랫폼에서 사용 가능하다.

1. **Self-Descriptiveness (자체 표현)**

- 요청 메시지만 보고도 쉽게 이해할 수 있는 자체 표현 구조로 되어있다.

---

<br />

## REST API란?

**REST API는 정보들이 주고 받아지는데 있어 개발자들 사이에 널리 쓰이는 일종의 형식이다!**

API = 소프트웨어가 다른 소프트웨어로 부터 지정된 형식으로 요청, 명령을 받을 수 있는 수단

프론트엔드 웹에서 서버에 데이터를 요청하거나 배달의 민족 앱에서 서버에 주문을 넣거나 등등

→ REST란 형식의 API

👦 **REST API의 가장 큰 특징은 각 요청이 어떤 동작이나 정보를 위한 것인지를 그 요청의 모습 자체로
추론이 가능하다.**

서버에 REST API로 요청을 보낼 때는 HTTP 규약에 따라 신호를 전송한다. ⇒ **CRUD**

- C : Create → 사진을 예로 들면 **올리는** 요청을 뜻함
- R : Read → 사진을 예로 들면 **불러오는** 요청을 뜻함
- U : Update → 사진을 예로 들면 **바꾸는** 요청을 뜻함
- D : Delete → 사진을 예로 들면 **지우는** 요청을 뜻함

💡 CRUD 요청은 CRUD별로 주소를 가지는데 이렇게 주소를 구성하면 주소가 너무 많아지고 관리하기 힘들다는 단점이 생김 → 예시로 이런 주소들이 10,000개가 있다고 가정하면 프로그래밍은 사람이 하는 일이므로 몇몇 주소가 겹칠 가능성이 생김

사람들은 좀 더 체계적으로 API를 관리하고 싶어했고, 그 영향으로 좀 더 체계적인 API라는 사회 운동이 만들어지는데 그게 바로 **REST(Representational State Transfer)ful API** 이다.

RESTful API에서는 이전보다 주소 개수가 줄어든다.

→ 즉 **CRUD를 하나의 주소로 관리 →** 요청을 보낼 때 다음과 같이 어떤 요청을 보냈는지 파악할 수 있는 스티커를 붙여서 함께 전송한다.

- Create : POST
- Read : GET
- Update : PUT(정보를 통째로 갈아끼울 때) / PATCH(정보 중 일부를 특정 방식으로 변경할 때 사용)
- Delete : DELETE

### Rest API 설계 시 가장 중요한 항목

1. URI는 정보의 자원을 표현해야 한다.
2. 자원에 대한 행위 HTTP Method(GET, POST, PUT, PATCH, DELETE)로 표현한다.

   → 행위는 URI에 포함하지 않는다.

### REST API와 RESTful API의 차이가 뭐지 그래서

RESTful한 API는 REST의 설계 규칙을 잘 지켜서 설계된 API !!

👉 REST의 원리를 잘 따르는 시스템을 RESTful이란 용어로 지칭된다.

**RESTful** 하게 만든 API는 요청을 보내는 주소만으로도 어떤 것을 요청 하는지 파악이 가능하다!

### ⭐ 요약

**REST API에서 URI는 정보의 자원만 표현해야 하며, 자원의 행위는 HTTP Method에 명시한다.**

👦 **RESTful API 설계 가이드**: [https://library.gabia.com/contents/8339/](https://library.gabia.com/contents/8339/)

<br />

💡 참고

- [REST API가 뭔가요?](https://www.youtube.com/watch?v=iOueE9AXDQQ&t=107s)
- [REST란? REST API와 RESTful API의 차이점](https://dev-coco.tistory.com/97#REST%--API%EB%A-%BC%--%EA%B-%--%EB%-B%A-%ED%-E%--%--%EC%-A%--%EC%--%BD%ED%--%--%EB%A-%B-)
- [REST API 제대로 알고 사용하기](https://meetup.toast.com/posts/92)
