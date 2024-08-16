### HTTP 주요 헤더: WWW-Authenticate, Authorization

인증정보가 충분치 않은 클라이언트가 인증정보가 필요한 서버의 자원에 접근하려 한 경우 `401(Unauthorization)` 응답코드를 받게 된다.

해당 응답코드와 함께 어떤 인증정보가 타입이 필요한지 나타내는 헤더가 `WWW-Authenticate` 이다.

```
WWW-Authenticate: Basic realm="Access to engineering site", charset="UTF-8"
```

- realm: 보안이 적용될 자원영역을 의미한다.

보안 인증타입은 크게 Basic과 Bearer 가 있고 OAuth2등에 사용되는 JWT는 Bearer 타입에 해당되고,

`ID:PW` 형태를 base64 인코딩 방식으로 인코딩하여 전송하는것을 Basic 타입이라고 한다.

<a href="https://docs.tosspayments.com/blog/everything-about-basic-bearer-auth">둘의 차이에 대한 정보</a>

Authorization은 인증정보 타입과 함께 인증정보를 전송하는 요청헤더에 속한다.

```
Authorization: Basic <인증정보>
```

따라서 처음에 401과 함께 WWW-Authenticate 헤더로 어떤 인증종류가 필요한지 알고서 

필요한 인증정보타입을 인증정보와 함께 Authorization 헤더에 담아서 보내면 된다.

### 브라우저 캐시

<a href="https://inpa.tistory.com/entry/HTTP-%F0%9F%8C%90-%EC%9B%B9-%EB%B8%8C%EB%9D%BC%EC%9A%B0%EC%A0%80%EC%9D%98-%EC%BA%90%EC%8B%9C-%EC%A0%84%EB%9E%B5-Cache-Headers-%EB%8B%A4%EB%A3%A8%EA%B8%B0">브라우저 캐시에 관한 글</a>

캐시는 기본적으로 원본 데이터의 사본을 저장해놓는 기술이다.

여기서 캐시 유지기간이 너무 길다고 하면, 원본은 이미 아득히 최신사항으로 업데이트 되었을지어도, 해당 캐시데이터만 받을 수 있다.

그래서 캐시된 사본 데이터가 얼마나 효력이 있는지를 나타내는 말로 `캐시 신선도`가 있다.

캐싱을 적용하는 기본적인 방법은 `응답헤더`에 `Expires`로 날짜를 설정해주거나, `Cache-Control: max-age= (sec)`로 설정한다면

해당 유효기간동안 자원에 대한 캐시 신선도를 유지한다.

그러고 캐시 신선도를 넘어선 자원에 대한 요청에 있어서, 캐시가 말소가 되는건 아니다. `재 검증`을 하게 된다.

- 날짜기반 재검증

    - If-Modified-Since: 특정 날짜를 기준으로 변경사항이 있는지 검증한다.

        - 변경되었을 경우 `200`번을 통해 새로운 자원을 반환한다.

        - 변경되지 않은 경우 `304`번을 통해 Not Modified 알린다.

            - `304`의 경우 응답헤더에 `Last-Modified`를 통해 언제 마지막으로 갱신했는지 알려준다.

        - 사라진 경우 `404`번을 통해 삭제됨을 알린다.

- 엔티티 태그 기반 재검증

    - Etag라고 하는 자원의 버전을 식별하기 위한 정보를 통해 재검증을 한다.

    - If-None-Match: 특정 태그명을 기준으로 현재 해당하는 태그명이 달린 자원이 있는지 검증한다.

        - 해당 자원의 태그가 현재와 다른경우: `200`

        - 현재와 같은경우: `304`

        - 자원이 삭제된 경우: `404`


### 콘텐츠 협상: GET

`콘텐츠 협상`이란 같은 URI에 대해 가장 적합한 `자원의 형태`를 제공하는 매커니즘을 의미한다.

여기서 동일한 자원이지만 다양한 형태로 제공할 수 있음을 `표현`이라고 한다.

흔히 자원을 얻고자 할때 사용하는 HTTP 메소드 GET이 이러한 자원의 형태에 대한 의미를 담고 있다.

```
"타겟 리소스"에 대한 "현재 선택된 표현"의 전송을 요청한다.
```

결국 클라이언트가 해당 자원에 대해서 데코레이션을 요청하는 것인데

그 헤더에는 `Accept`, `Accept-Language`, `Accept-Encoding`등이 있다.

- Accept: 선호하는 미디어타입

- Accept-Language: 선호하는 언어

- Accept-Encoding: 선호하는 압축방식

이러한 콘텐츠 협상에서 중요한점은 `선호도에 대한 우선순위`를 반영할 수 있다는 것이다.

`q`문자로 표현되며, 0~1사이의 값을 가지고, 없을경우 1로 의미된다.

```
Accept-Language: ko-KR,ko;q=0.9,en-US;q=0.8,en;q=0.7
Accept: text/html, application/xml;q=0.9,text/plain;q=0/6,*/*;q=0.5
```