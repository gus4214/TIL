# HTTP

> HTTP (HyperText Transfer Protocol)의 약자
> 

## 🤔 용어에 대한 뜻 살펴보기

1. **HyperText**
    
    HTTP에서 HyperText는 HTML의 HyperText와 그 의미가 동일하다.
    
    HTML은 문서와 문서가 링크로 연결되도록 하는 태그로 구성된 언어
    
    👉 웹페이지를 만들기 위해 웹브라우저 위에서 동작하는 언어를 뜻한다
    
    💡 **그렇다면 HTML로 만든 웹페이지를 어떻게 주고 받을까 ??**
    
2. **Transfer**
    
    > 사전적 의미 : “전송하다” → 물건이나 편지 따위를 보낸다.
    > 
    
    로컬호스트에서 작성한 HTML 파일을 로컬에서만 띄운다면 무슨 의미가 있을까?
    
    우리는 우리가 만든 웹사이트를 널리 알리고 다른 사람들과 공유하기 위해서 다른 컴퓨터에게 **전송**해야 한다. 
    
    → 전송은 보내는 주체와 받는 주체가 있다는 것이 큰 특징!
    
3. **Protocol**
    
    > 프로토콜 : 협약, 통신 규약 이라는 의미를 가진다.
    > 
    
    물리적으로 떨어진 컴퓨터 끼리 어떻게 HTML파일을 주고 받을지에 대한 **약속**
    
    우린 한국에 살고 있고, 한국 사회의 소통방식인 한국어(약속)로 소통을 하듯 컴퓨터도 컴퓨터 끼리의 소통 방법이 필요하다.
    이런 필요에 의해 만들어진 소통하는 방식 또는 약속이 바로 **HTTP**
    
    우리가 사용하는 인터넷 상에서 일어나는 소통은 대부분 HTTP 규약을 따른다.
    

👉 **HTTP란?** 컴퓨터들끼리 HTML 파일을 주고받을 수 있도록 하는 소통방식 또는 약속

## 🤔 HTTP의 특징

> HTTP는 컴퓨터들 끼리의 약속이고 약속에는 언제나 조항들이 따르기 마련이다. 그렇다면 HTTP는 어떤 조항으로 이루어져 있을까 ?
> 
1. **Request / Response (요청 / 응답)**
    
    💡 **HTTP 통신의 핵심은 요청과 응답이다.**
    
    Transfer에서 전송은 보내는 주체와 받는 주체가 있는데, 보내는 주체는 받는 주체에게 요청을 보내고, 받는 주체는 요청을 보낸 주체에게 응답을 보내게 된다.
    
    예를들어 편지의 발신자는 보내는 주체이고, 수신자는 받는 주체 
    → 수신자는 잘 받았다는 응답을 다시 발신자에게 보낸다.
    
    컴퓨터 끼리의 소통도 사람이 필요에 의해서 만든 소통 방식이기 때문에 우리의 소통 방식과 큰 차이점이 없다.
    
    “노트북을 연다. 구글에 접속한다. → 그 순간 노트북은 구글의 서버에게 요청을 보낸다. “오늘의 날씨를 검색.” 구글의 서버는 이 요청을 처리해서 다시 요청을 보낸 나의 노트북에 응답을 보낸다. 
    
    😃 HTTP도 사실은 우리에게 친숙한 소통방식을 컴퓨터의 소통방식에 적용한 것!
    
2. **Stateless**
    
    **💡 State(상태) + less(없음)**
    
    HTTP에 대한 설명 중 **절대 잊어서는 안 될 특징**이 **Stateless**이다.
    
    각각의 HTTP 통신(요청/응답)은 독립적이기 때문에 과거의 통신(요청/응답)에 대한 내용을 전혀 알지 못한다. → 이전의 상태를 알지 못한다는 것은 무엇을 의미할까 ?
    
    👉 **매 통신마다 필요한 모든 정보를 담아서 요청을 보내야 한다.**
    
    마치 이미 자기소개를 한 사람에게 계속해서 똑같은 내용으로 자기소개를 해야하는 것과 같다.
    
    따라서 여러번의 통신의 진행과정에서 연속된 데이터 처리가 필요한 경우(ex. 온라인 쇼핑몰에서 로그인 후 장바구니 기능)를 위해 로그인 토큰 또는 브라우저의 쿠키, 세션, 로컬스토리지 같은 기술이 필요에 의해 만들어졌다!
    
3. **Request / Response**
    
    💡 실제 프로젝트에선 프론트엔드에서 백엔드에게 데이터를 요청하고 백엔드는 요청을 처리해서 응답을 준다. → 이러한 요청과 응답에 대한 구조와 메세지를 잘 파악하면 대부분의 에러를 잡아낼 수 있다.
    
4. **Request 메세지 구조**
    
    💡 **요청은 그저 메세지에 불과** : 프론트(클라이언트) 에서 백엔드(서버)에 일(데이터 처리)을 시작하게 하기 위해 보내는 메세지
    
    이 메세지의 구조는 크게 **세 부분**으로 구성되어 있다.
    
    1. **Start Line** : 요청의 첫번째 줄에 해당한다. 
        - **HTTP Method:** 해당 요청이 의도한 액션을 정의하는 부분. 주로 **GET**, **POST**, **DELETE**가 많이 쓰임
        - **Request target:** 해당 request가 전송되는 목표 url
        - **HTTP Version:** 말 그대로 사용되는 HTTP 버전을 뜻한다. 주로 1.1 버전이 널리 쓰임
        
        ```jsx
        GET /login HTTP/1.1
        # 해석: GET 메소드로 login 이라는 요청 타겟에 HTTP 1.1 버전으로 요청을 보내겠다!
        ```
        
    2. **Headers** : 해당 요청에 대한 추가 정보(메타 데이터)를 담고있는 부분
        - **Key: Value** 값으로 되어있다 (JavaScript의 객체, Python의 딕셔너리 형태라고 보면 된다)
        - **Host:** 요청을 보내는 목표(타겟)의 주소. 즉, 요청을 보내는 웹사이트의 기본 주소가 된다. (ex. www.apple.co.kr)
        - **User-Agent:** 요청을 보내는 클라이언트의 대한 정보 (ex. chrome, firefox, safari, ~~explorer~~)
        - **Content-Type:** 해당 요청이 보내는 메세지 body의 타입 (ex. application/json)
        - **Content-Length:** body 내용의 길이
        - **Authorization:** 회원의 인증/인가를 처리하기 위해 로그인 토큰을 Authroization 에 담는다
        
        ```jsx
        Headers: {
            Host:  
            User-Agent: 
            Content-Type: 
            Content-Length: 
            Authorization: 
        }
        ```
        
    3. **Body** : 해당 요청의 실제내용 → 주로 Body를 사용하는 메소드는 **POST**
        
        ```jsx
        ex) 로그인 시에 서버에 보낼 요청의 내용
        Body: {
        "user_email":"wecode@gmail.com" "user_password": "wecode"
        }
        ```
        
5. **Response** 메세지 구조
    
    💡 응답도 요청과 마찬가지로 메세지
    
    HTTP 규약에 따른 응답의 구조도 또한 크게 **세 부분**으로 구성되어 있다.
    
    1. **Status Line**: 응답의 상태 줄
        - 응답은 요청에 대한 처리상태를 클라이언트에게 알려주면서 내용을 시작한다. 마치, 편지의 응답에 "응. 잘 지냈어" 라고 안부 인사를 건네는 것과 같다. 응답의 Status Line 도 세 부분으로 구성된다.
        - **HTTP Version**: 요청의 **HTTP버전**과 동일
        - **Status Code**: 응답 메세지의 **상태 코드**
        - **Status Text**: 응답 메세지의 상태를 간략하게 설명해주는 **텍스트**
        
        ```jsx
        HTTP/1.1 404 Not Found
        # 해석: HTTP 1.1 버전으로 응답하고 있는데, 프론트엔드에서 보낸 요청(ex. 로그인 시도)에 대해서
        # 유저의 정보를 찾을 수 없기 때문에(Not Found) 404 상태 메세지를 보낸다.
        
        HTTP/1.1 200 SUCCESS
        # 해석: HTTP 1.1 버전으로 응답하고 있는데, 프론트엔드에서 보낸 요청에 대해서 성공했기 때문에
        # 200 상태 메세지를 보낸다.
        ```
        
    2. **Headers**: 요청의 헤더와 동일하다. 응답의 추가 정보(메타 데이터)를 담고있는 부분
        - 다만, 응답에서만 사용되는 헤더의 정보들이 있다. 
        (ex. 요청하는 브라우저의 정보가 담긴 User-Agent 대신, Server 헤더가 사용된다.)
    3. **Body**: 요청의 Body와 일반적으로 동일하다.
        - 요청의 메소드에 따라 Body가 항상 존재하지 않듯이 응답도 응답의 형태에 따라 데이터를 전송할 필요가 없는 경우엔 Body가 없을 수도 있다.
        - 가장 많이 사용되는 Body 의 데이터 타입은 **[JSON(JavaScript Object Notation)](https://developer.mozilla.org/ko/docs/Web/JavaScript/Reference/Global_Objects/JSON)**
        - **로그인 요청에 대해 성공했을 때 응답의 내용**
        
        ```jsx
        Body: {
            "message": "SUCCESS"
            "token": "kldiduajsadm@9df0asmzm" (암호화된 유저의 정보)
        }
        ```
        

## 🤔 HTTP Method

### HTTP Request Methods

💡 프론트엔드(클라이언트) 입장에서 요청의 의도가 담긴 **자주 사용되는 HTTP 통신 메소드 세가지**

1. **GET**
    - 이름 그대로 어떤 데이터를 서버로 부터 받아(GET)올 때 주로 사용하는 메소드
    - **데이터를 받아오기만** 할 때 사용
    - 가장 간단하고 많이 사용되는 HTTP 메소드 (사실 우리가 웹페이지를 띄울 때 필요한 정보들을 모두 GET메소드로 요청을 보내서 받아온 응답을 화면에 띄우는 것!)
    
    <aside>
    💡 장바구니에 담은 제품을 조회
    
    </aside>
    
    ```jsx
    // (축약된 요청 메세지)
    GET /shop/bag HTTP/1.1
    Headers: { 
        "HOST": "https://www.apple.com/kr",
        "Authroization": "kldiduajsadm@9df0asmzm" (유저가 본인임을 증명할 수 있는 인증/인가 토큰)
    }
    
    // (축약된 응답 메시지) 
    HTTP/1.1 200 OK
    Body: {
        "message": "SUCCESS",
        "carts": [
            {
              "productId": 10
              "name": "Pro Display XDR - Nano-texture 글래스"
              "price": "₩7,899,000"
              "quantity": 1
           },
           {
             "productId": 20
             "name": "Mac Pro"
             "price": "₩73,376,000"
             "quantity": 2
           } 
        ]
    }
    ```
    
2. **POST**
    - 데이터를 생성 / 수정 할 때 주로 사용되는 메소드
    - 데이터를 생성 및 수정 할 때 많이 사용되기 때문에 대부분의 경우 요청에 body가 포함되서 보내진다.
    
    <aside>
    💡 장바구니에 맘에 드는 상품을 담는다.
    
    </aside>
    
    ```jsx
    // (축약된 요청 메세지)
    POST /shop/bag HTTP/1.1
    Headers: {
      "HOST": 
      "https://www.apple.com/kr"
      "Authroization": 
      "kldiduajsadm@9df0asmzm" (유저가 본인임을 증명할 수 있는 인증/인가 토큰)
    }
    Body: {
      product: {
        "productId": 30
        "name": "12.9형 iPad Pro Wi-Fi + Cellular 128GB"
        "color": "스페이스 그레이"
        "price": "₩1,499,000"
        "quantity": 1
      }
    }
    
    // (축약된 응답 메시지)
    HTTP/1.1 201 Created
    Body: {
      "message": "SUCCESSFULLY CARTS UPDATED"
    }
    ```
    
3. **DELETE**
    - 메소드의 이름에서 유추 가능하듯, 특정 데이터를 서버에서 삭제 요청을 보낼때 쓰는 메소드
    
    <aside>
    💡 장바구니에서 제품을 삭제
    
    </aside>
    
    ```jsx
    // (축약된 요청 메세지)
    DELETE /shop/bag HTTP/1.1
    Headers: {
      "HOST": "https://www.apple.com/kr"
      "Authroization": "kldiduajsadm@9df0asmzm" (유저가 본인임을 증명할 수 있는 인증/인가 토큰)
    }
    Body: {
      productId: 30
    }
    
    // (축약된 응답 메시지)
    HTTP/1.1 204 No Content
    ```
    

## 🤔 Status Code

### Response Status Code

😃 Status Code의 숫자에 각각 의미가 내포되어 있다. 이 코드만 보아도 응답이 제대로 됐는지 안 됐는지를 파악할 수 있다!

1. **Success**
    1. **200: OK**
        - 가장 자주 보게되는 Status Code
        - 문제없이 요청에 대한 처리가 백엔드 서버에서 이루어지고 나서 오는 응답코드
    2. **201: Created**
        - 무언가가 잘 생성되었을 때에(Successfully Created) 오는 Status Code
        - 대게 POST 메소드의 요청에 따라 백엔드 서버에 데이터가 잘 생성 또는 수정 되었을 때에 보내는 코드
    3. **204: No Content**
        - 요청이 성공했으며 제공할 응답메세지가 없을 경우 사용하는 Status Code
        - 주로 DELETE 메소드의 요청으로 성공적으로 삭제되어서 응답으로 제공할 컨텐츠가 없을 때 사용된다.
2. **Client Error**
    1. **400: Bad Request**
        - 해당 요청이 잘못되었을 때 보내는 Status Code
        - 주로 요청의 Body에 보내는 내용이 잘못되었을 때 사용되는 코드
        - ex) 전화번호를 보내야 하는데 숫자가 아닌 문자열의 주소가 대신 Body에 담겼을 경우
    2. **401: Unauthorized**
        - 유저가 해당 요청을 진행하려면 먼저 로그인을 하거나 회원가입이 필요하다는 의미를 나타내는 Status Code
        - ex) wish list, 좋아요 기능은 회원이 아니면 요청을 보낼 수 없습니다.
    3. **403: Forbidden**
        - 유저가 해당 요청에 대한 권한이 없다는 의미를 나타내는 Status Code
        - 접근 불가능한 정보에 접근했을 경우를 의미
        - ex) 오직 유료회원만 접근할 수 있는 데이터를 요청 했을 때
    4. **404: Not Found**
        - 요청된 URI 가 존재하지 않는다는 의미를 나타내는 Status Code
3. **Server Error**
    1. **500: Internal Server Error**
        - 서버에서 에러가 났을 때의 Status Code