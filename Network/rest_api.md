## REST API

### 1. REST

**REST**(Representational State Transfer)는 [월드 와이드 웹](https://ko.wikipedia.org/wiki/월드_와이드_웹)과 같은 분산 [하이퍼미디어](https://ko.wikipedia.org/wiki/하이퍼미디어) 시스템을 위한 [소프트웨어 아키텍처](https://ko.wikipedia.org/wiki/소프트웨어_아키텍처)의 한 형식이다. 이 용어는 로이 필딩(Roy Fielding)의 2000년 박사학위 논문에서 소개되었다. 엄격한 의미로 **REST**는 네트워크 아키텍처 원리의 모음이다. 여기서 '네트워크 아키텍처 원리'란 자원을 정의하고 자원에 대한 주소를 지정하는 방법 전반을 일컫는다. 간단한 의미로는, 웹 상의 자료를 [HTTP](https://ko.wikipedia.org/wiki/HTTP)위에서 [SOAP](https://ko.wikipedia.org/wiki/SOAP)이나 쿠키를 통한 세션 트랙킹 같은 별도의 전송 계층 없이 전송하기 위한 아주 간단한 인터페이스를 말한다.



### 2. REST 이전에

REST도 결국은 네트워크 상에서 HTTP를 기반으로 정보를 제어하기 위한 방법론 중 하나다. 비교적 최근에 등장한 방법론인데, 이전에는 어떤 방법들이 있었는지 살펴보자.

- RMI
- SOAP
- Corba
- DEC
- DCOM

다양한 방법들이 있다. 이들을 만든 벤더들의 목록은 다음과 같다.

- Sun
- Microsoft
- IBM
- OASIS,
- OMG

이렇게 다양한 방법들이 있는데, 거대 벤더들의 지원까지 받을 수 있는데 왜 **REST**라는 방법이 개발됐고, 게다가 이렇게 까지 관심을 받게 됐을까?

- 상호운용성이 나쁘다. 거대 벤더들이 만든 방법들의 대부분이 그렇듯이, "강력하지만 복잡한 경우"가 많다. 복잡하면 상호운용성이 떨어지기 마련이다.
- 벤더에 종속적이다. 물론 툴을 개발한 벤더는 누구나 사용할 수 있는 방법이라고 설명을 하긴한다. 하지만 대게는 "운영체제에 종속적이거나", "복잡해서 벤더의 지원이 없으면 제대로된 애플리케이션 개발이 힘들다거나" 등등의 이유로 사실상 벤더에 종속되는 경우가 많다.
- 바퀴를 만들기 위해서 바퀴를 만들어야 한다. 복잡하다는 이야기다.

등의 문제가 발견됐다. 이러한 문제들을 해결하기 위해서 REST를 만들었다.



### 3. RESTful

RESTful은 위의 **아키텍처 스타일, 아키텍처 원칙을 모두 만족**하는 것을 의미한다.

REST라는 아키텍처 스타일이 있는거고 RESTful API라는 말은 REST 아키텍처 원칙을 모두 만족하는 API라는 뜻이다.

우리가 REST와 RESTful을 동일한 의미로 사용하곤 하는데 엄격하게는 다르다는 것을 알 수 있다.



### 4. REST 구성

쉽게 말해 REST API는 다음의 구성으로 이루어져있다.

- **자원(RESOURCE)** - URI
- **행위(Verb)** - HTTP METHOD
- **표현(Representations)**

HTTP URI(Uniform Resource Identifier)를 통해 자원(Resource)을 명시하고, HTTP Method(POST, GET, PUT, DELETE)를 통해 해당 자원에 대한 CRUD Operation을 적용하는 것을 의미한다.
즉, REST는 자원 기반의 구조(ROA, Resource Oriented Architecture) 설계의 중심에 Resource가 있고 HTTP Method를 통해 Resource를 처리하도록 설계된 아키텍쳐를 의미한다.

### 5. REST API 디자인 가이드

REST API 설계 시 가장 중요한 항목은 다음의 2가지로 요약할 수 있다.

**첫 번째,** URI는 정보의 자원을 표현해야 한다.
**두 번째,** 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE)로 표현한다.

#### 5-1. REST API 중심 규칙

------

##### 1) URI는 정보의 자원을 표현해야 한다. (리소스명은 동사보다는 명사를 사용)

```
    GET /members/delete/1
```

위와 같은 방식은 REST를 제대로 적용하지 않은 URI이다. URI는 자원을 표현하는데 중점을 두어야 한다. delete와 같은 행위에 대한 표현이 들어가서는 안된다.

##### 2) 자원에 대한 행위는 HTTP Method(GET, POST, PUT, DELETE 등)로 표현

위의 잘못 된 URI를 HTTP Method를 통해 수정해 보면

```
    DELETE /members/1
```

으로 수정할 수 있다.
회원정보를 가져올 때는 GET, 회원 추가 시의 행위를 표현하고자 할 때는 POST METHOD를 사용하여 표현한다.

**회원정보를 가져오는 URI**

```
    GET /members/show/1     (x)
    GET /members/1          (o)
```

**회원을 추가할 때**

```
    GET /members/insert/2 (x)  - GET 메서드는 리소스 생성에 맞지 않습니다.
    POST /members/2       (o)
```

**[참고]HTTP METHOD의 알맞은 역할** 
POST, GET, PUT, DELETE 이 4가지의 Method를 가지고 CRUD를 할 수 있다.

| METHOD |                             역할                             |
| :----: | :----------------------------------------------------------: |
|  POST  |      POST를 통해 해당 URI를 요청하면 리소스를 생성한다.      |
|  GET   | GET를 통해 해당 리소스를 조회한다. 리소스를 조회하고 해당 도큐먼트에 대한 자세한 정보를 가져온다. |
|  PUT   |              PUT를 통해 해당 리소스를 수정한다.              |
| DELETE |               DELETE를 통해 리소스를 삭제한다.               |

다음과 같은 식으로 URI는 자원을 표현하는 데에 집중하고 행위에 대한 정의는 HTTP METHOD를 통해 하는 것이 REST한 API를 설계하는 중심 규칙이다.

#### 5-2. URI 설계 시 주의할 점

---------

##### 1) 슬래시 구분자(/)는 계층 관계를 나타내는 데 사용

```
    http://restapi.example.com/houses/apartments
    http://restapi.example.com/animals/mammals/whales
```

##### 2) URI 마지막 문자로 슬래시(/)를 포함하지 않는다.

URI에 포함되는 모든 글자는 리소스의 유일한 식별자로 사용되어야 하며 URI가 다르다는 것은 리소스가 다르다는 것이고, 역으로 리소스가 다르면 URI도 달라져야 한다. REST API는 분명한 URI를 만들어 통신을 해야 하기 때문에 혼동을 주지 않도록 URI 경로의 마지막에는 슬래시(/)를 사용하지 않는다.

```
    http://restapi.example.com/houses/apartments/ (X)
    http://restapi.example.com/houses/apartments  (0)
```

##### 3) 하이픈(-)은 URI 가독성을 높이는데 사용

URI를 쉽게 읽고 해석하기 위해, 불가피하게 긴 URI경로를 사용하게 된다면 하이픈을 사용해 가독성을 높일 수 있다.

##### 4) 밑줄(_)은 URI에 사용하지 않는다.

글꼴에 따라 다르긴 하지만 밑줄은 보기 어렵거나 밑줄 때문에 문자가 가려지기도 한다. 이런 문제를 피하기 위해 밑줄 대신 하이픈(-)을 사용하는 것이 좋다.(가독성)

##### 5) URI 경로에는 소문자가 적합하다.

URI 경로에 대문자 사용은 피하도록 해야 한다. 대소문자에 따라 다른 리소스로 인식하게 되기 때문이다. RFC 3986(URI 문법 형식)은 URI 스키마와 호스트를 제외하고는 대소문자를 구별하도록 규정하기 때문.

```
    RFC 3986 is the URI (Unified Resource Identifier) Syntax document
```

##### 6) 파일 확장자는 URI에 포함시키지 않는다.

```
    http://restapi.example.com/members/soccer/345/photo.jpg (X)
```

REST API에서는 메시지 바디 내용의 포맷을 나타내기 위한 파일 확장자를 URI 안에 포함시키지 않는다. Accept header를 사용하도록 하자.

```
    GET / members/soccer/345/photo HTTP/1.1 Host: restapi.example.com Accept: image/jpg
```

#### 4-3. 리소스 간의 관계를 표현하는 방법

------

REST 리소스 간에는 연관 관계가 있을 수 있고, 이런 경우 다음과 같은 표현방법으로 사용한다.

```
    /리소스명/리소스 ID/관계가 있는 다른 리소스명

    ex)    GET : /users/{userid}/devices (일반적으로 소유 ‘has’의 관계를 표현할 때)
```

만약에 관계명이 복잡하다면 이를 서브 리소스에 명시적으로 표현하는 방법이 있다. 예를 들어 사용자가 ‘좋아하는’ 디바이스 목록을 표현해야 할 경우 다음과 같은 형태로 사용될 수 있다.

```
    GET : /users/{userid}/likes/devices (관계명이 애매하거나 구체적 표현이 필요할 때)
```

#### 4-4. 자원을 표현하는 Colllection과 Document

------

DOCUMENT는 단순히 문서, 컬렉션은 문서들의 집합이며 컬렉션과 도큐먼트는 모두 리소스라고 표현할 수 있으며 URI에 표현된다. 

```
    http:// restapi.example.com/sports/soccer/players/13
```

sports, players 컬렉션과 soccer, 13(13번인 선수)를 의미하는 도큐먼트로 URI가 이루어지게 된다. 여기서 중요한 점은 **컬렉션은 복수**로 사용하고 있다는 점이다. 좀 더 직관적인 REST API를 위해서는 컬렉션과 도큐먼트를 사용할 때 단수 복수도 지켜준다면 좀 더 이해하기 쉬운 URI를 설계할 수 있다.

### 5. HTTP 응답 상태 코드

 잘 설계된 REST API는 URI만 잘 설계된 것이 아닌 그 리소스에 대한 응답을 잘 내어주는 것까지 포함되어야 한다. 정확한 응답의 상태코드만으로도 많은 정보를 전달할 수가 있기 때문에 응답의 상태코드 값을 명확히 돌려주는 것은 생각보다 중요한 일이 될 수도 있다. 

| 상태코드 |                                                              |
| :------: | :----------------------------------------------------------: |
|   200    |            클라이언트의 요청을 정상적으로 수행함             |
|   201    | 클라이언트가 어떠한 리소스 생성을 요청, 해당 리소스가 성공적으로 생성됨(POST를 통한 리소스 생성 작업 시) |

| 상태코드 |                                                              |
| :------: | :----------------------------------------------------------: |
|   400    |    클라이언트의 요청이 부적절 할 경우 사용하는 응답 코드     |
|   401    | 클라이언트가 인증되지 않은 상태에서 보호된 리소스를 요청했을 때 사용하는 응답 코드 |
|          | (로그인 하지 않은 유저가 로그인 했을 때, 요청 가능한 리소스를 요청했을 때) |
|   403    | 유저 인증상태와 관계 없이 응답하고 싶지 않은 리소스를 클라이언트가 요청했을 때 사용하는 응답 코드 |
|          | (403 보다는 400이나 404를 사용할 것을 권고. 403 자체가 리소스가 존재한다는 뜻이기 때문에) |
|   405    | 클라이언트가 요청한 리소스에서는 사용 불가능한 Method를 이용했을 경우 사용하는 응답 코드 |

| 상태코드 |                                                              |
| :------: | :----------------------------------------------------------: |
|   301    | 클라이언트가 요청한 리소스에 대한 URI가 변경 되었을 때 사용하는 응답 코드 |
|          |  (응답 시 Location header에 변경된 URI를 적어 줘야 합니다.)  |
|   500    |          서버에 문제가 있을 경우 사용하는 응답 코드          |



### 6. REST 의 특징

##### 1) Uniform (유니폼 인터페이스)

EST는 HTTP 표준에만 따른 다면, 어떠한 기술이라던지 사용이 가능한 인터페이스 스타일이다. 예를 들어 HTTP + JSON으로 REST API를 정의했다면, 안드로이드 플랫폼이건, iOS 플랫폼이건, 또는 C나 Java/Python이건 특정 언어나 기술에 종속 받지 않고 HTTP와 JSON을 사용할 수 있는 모든 플랫폼에 사용이 가능한 느슨한 결함(Loosely coupling) 형태의 구조이다.

##### 2) Stateless (무상태성)

상태가 있다 없다는 의미는 사용자나 클라이언트의 컨택스트를 서버쪽에 유지 하지 않는다는 의미로,쉽게 표현하면 HTTP Session과 같은 컨텍스트 저장소에 상태 정보를 저장하지 않는 형태를 의미한다.

상태 정보를 저장하지 않으면 각 API 서버는 들어오는 요청만을 들어오는 메시지로만 처리하면 되며, 세션과 같은 컨텍스트 정보를 신경쓸 필요가 없기 때문에 구현이 단순해진다.

##### 3) Cacheable (캐시 가능)

REST의 가장 큰 특징 중 하나는 HTTP라는 기존 웹표준을 그대로 사용하기 때문에, 웹에서 사용하는 기존 인프라를 그대로 활용이 가능하다. 따라서 HTTP가 가진 캐싱 기능이 적용 가능하다. HTTP 프로토콜 표준에서 사용하는 Last-Modified태그나 E-Tag를 이용하면 캐싱 구현이 가능하다.Client가 HTTP GET을 “Last-Modified” 값과 함께 보냈을 때, 컨텐츠가 변화가 없으면 REST 컴포넌트는 “304 Not Modified”를 리턴하면 Client는 자체 캐쉬에 저장된 값을 사용하게 된다.

이렇게 캐쉬를 사용하게 되면 네트웍 응답시간 뿐만 아니라, REST 컴포넌트가 위치한 서버에 트렌젝션을 발생시키지 않기 때문에, 전체 응답시간과 성능 그리고 서버의 자원 사용률을 비약적으로 향상 시킬 수 있다.

##### 4) Self-descriptiveness (자체 표현 구조)

REST의 또 다른 큰 특징 중 하나는 REST API 메시지만 보고도 이를 쉽게 이해 할 수 있는 자체 표현 구조로 되어 있다는 것이다.

##### 5) Client - Server 구조

REST 서버는 API 제공, 클라이언트는 사용자 인증이나 컨텍스트(세션, 로그인 정보)등을 직접 관리하는 구조로 각각의 역할이 확실히 구분되기 때문에 클라이언트와 서버에서 개발해야 할 내용이 명확해지고 서로간 의존성이 줄어들게 된다.

##### 6) 계층형 구조

REST 서버는 다중 계층으로 구성될 수 있으며 보안, 로드 밸런싱, 암호화 계층을 추가해 구조상의 유연성을 둘 수 있고 PROXY, 게이트웨이 같은 네트워크 기반의 중간매체를 사용할 수 있게 한다.







[출처]

https://bcho.tistory.com/953 

https://meetup.toast.com/posts/92

https://www.joinc.co.kr/w/man/12/rest/about

https://jeong-pro.tistory.com/180

https://gmlwjd9405.github.io/2018/09/21/rest-and-restful.html