## DNS 에 대해 알아보자

우선 네트워크상의 특정 호스트 즉 수신지를 특정하기 위한 주소가 IP라고 하였다.

그런데 IP는 수시로 바뀔수 있다. 그래서 IP와 대응되는 이름인 `도메인 네임`을 사용한다.

그러면 호스트가 원하는 서버의 도메인 네임만 알고있을 때, IP주소를 얻기위한 서버를 `네임 서버` 라고 부른다.

물론 그 역도 가능하다. (IP를 통한 도메인 네임을 얻는것도 가능하단 이야기)

### 계층적인 도메인 네임

도메인 네임은 계층적으로 분류된다.

즉, 루트 도메인부터 시작하여 (.)으로 구분되어 최상위 도메인(TLD)가 있고 

그 이후로 N단계 도메인까지 분류된다.

```
www.example.com

에서 사실 생략된 맨 뒷자리 . 이 있고 이것이 루트 도메인이 된다.

그리고 com이 TLD가 되고, example이 2단계 도메인, www가 3단계 도메인이 된다.
```

결국 N단계 도메인은 N-1단계 도메인의 `서브 도메인`이 된다.

```
google.com 은 2단계 도메인으로서, 해당 도메인에서 3단계 도메인들이 서브 도메인이 된다.

즉 아래는 2단계 도메인의 서브도메인인것

mail.google.com
www.google.com < 이 이상 단계가 없고 이걸로 구분됨 FQDN (Full Qualified Domain Name)
```

### DNS의 정의

위와같이 도메인은 계층적으로 분류되게 되고, 이 계층적 분류를 실제 네임서버에도 적용되어 있다.

이와 같은 체계를 `도메인 네임 시스템` 즉 `DNS`라고 한다. 

다시말해

`DNS`는 `도메인 네임 시스템`으로 도메인을 효율적으로 관리하기 위해 도메인의 계층적 구조를 네임서버에도 적용시켜 

계층적인 네임서버를 통해 도메인 네임을 관리하는 체계를 의미한다

즉 `DNS`는 `계층적 네임서버를 통해 구현`된다.

### 계층적인 네임서버와 질의 방식

우선 DNS 체계를 이루는 구현체는 계층적인 네임서버가 된다.

즉 IP에 대해 궁금한 호스트는 계층적으로 된 구조로 도메인을 얻는다는 의미가 된다.

- 로컬 DNS 서버

    - 클라이언트가 젤 먼저 찾아가는 네임서버

    - 정적 IP주소 할당시 적어넣는 DNS가 바로 이것

    - 일반적으로 ISP에서 로컬 DNS 서버주소를 할당해줌

        - 우리나라로 따지면 LG 유플러스, KT 같은게 아닐까?

    - 공개 DNS 서버를 사용할 수 도 있음

        - 대표적으로 구글의 8.8.8.8 이나 클라우드 플레어의 1.1.1.1이 있음

- 루트 네임 서버

    - 루트 도메인을 관리하며, TLD 네임서버의 주소를 반환함

        - www.example.com에서 com에 대한 네임서버 주소를 반환한단것

- TLD 네임 서버

    - TLD 를 관리하는 네임서버로서, TLD 네임 하위 도메인의 네임서버 주소를 반환한다.

        - www.example.com에서 com에 해당하는 TLD 서버에 갔더니 example.com에 대한 네임서버 주소를 얻는것

- 책임 네임 서버

    - 말그대로 얘보다 더 넘어가는 계층 네임서버는 없고 최종적으로 IP를 얻는곳이다.


즉, 로컬 네임서버에 묻고 없으면 루트 네임서버 갔다가 없으면 TLD 네임서버 갔다가 없으면 책임 네임서버 가서 얻어오는 과정이다.

여기서 "없으면"에 해당하는것이 바로 `DNS 캐시`로서 네임서버들이 기존에 응답받은 결과를 저장해놓는 곳이다.

그래서 더 짧은시간에 IP주소를 얻을 수 있고, 이는 영구적인것이 아니어서 TTL이라는 살아남는 기준을 가진다.

그러면 묻는 순서는 알겠고, 어떻게 질의를 하는가?

- 재귀적 질의: 로컬 네임서버에게 물으러가면, 그기에서부터 루트 -> TLD -> 책임 까지 필요한 순간가지 계층을 거슬러 올라가서 응답을 반환하는 방식

- 반복적 질의: 로컬 네임서버가 각 계층구조 네임서버를 순서대로 묻고 응답받는 방식

### DNS 레코드 타입

`레코드`란 네임서버에게 입력하는 도메인 네임과 IP쌍을 의미한다.

여기서 다양한 레코드의 유형이 있는데, 유형에 따라 입력하는 이름과 값의 의미가 달라진다.

실제로 CMD에 `ipconfig /dnsdisplay` 라고 치면 나오는 값들에서

현재 네임서버가 갖고있는 레코드와 유형을 알 수 있다.

숫자로 되어있는 레코드 타입은 <a href="https://en.wikipedia.org/wiki/List_of_DNS_record_types">레코드 타입확인</a>에서 알 수 있다.

## URI

URI(Uniform Resource Identifier)는 `자원`을 `식별`하는 `통일된 방식`을 의미한다.

여기서 `자원`은 네트워크 상에 메세지로 주고받는 대상을 의미한다. (.html, .txt 등)

엄밀하게 RFC 9110에 의거하면 "HTTP 요청에 대한 대상을 `자원` 이라고 부른다" 라고 적혀있긴 하다.

이러한 식별하는 방식에 있어서 자원의 위치를 기반으로 한 URL(Uniform Resource Locator) 와 

자원의 이름을 기반으로한 URN(Uniform Resource Name)이 있다.

오늘날 대부분은 URL방식이라고 보면된다.

URL은 다음과 같은 구조로 되어있다.

```
foo://www.example.com:8042/over/there?name=ferret#nose
```

- schema: foo까지가 schema이며 사용할 프로토콜을 의미한다.

- authority: www.example.com:8042 까지이며 질의 하고자하는 자원을 가진 호스트 이름을 의미한다.

- path: /over/there 까지로 위치기반이기 때문에 해당 호스트내의 루트 주소부터 자원이 위치한 경로를 의미한다.

- query: 자원을 얻어오는것 까지는 path 까지 정보로 충분하지만 서버입장에서 정렬이라던지 이런 추가정보를 얻기위해서 사용된다.

- fragment: HTML와 같은 자원에서 특정 위치를 나타내는 목적으로 사용된다.


