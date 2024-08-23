# Self-Learning_Network

혼자 공부하는 네트워크, 키워드 위주 정리

## Chapter 01 컴퓨터 네트워크 시작하기

<table>
    <tr>
        <th>
            제목
        </th>
        <th>
            주요 키워드
        </th>
    </tr>
    <tr>
        <td><a href="docs/메세지 교환방식.md">메시지 교환방식과 전송 방식</a></td>
        <td>회선 연결 방식, 패킷 전송 방식, 유니캐스트, 브로드캐스트, 애니캐스트, 멀티캐스트, 헤더, 페이로드</td>
    </tr>
    <tr>
        <td><a href="docs/네트워크 계층 모델.md">네트워크 계층 모델</a></td>
        <td>OSI 7Layer, TCP/IP 모델(4Layer, 5Layer), 프로토콜, IP 패킷, 캡슐화 & 역 캡슐화</td>
    </tr>
</table>

## Chapter 02 물리 계층과 데이터링크 계층

<table>
    <tr>
        <th>
            제목
        </th>
        <th>
            주요 키워드
        </th>
    </tr>
    <tr>
        <td><a href="docs/이더넷 프레임.md">이더넷 프레임</a></td>
        <td>물리계층, 데이터링크 계층, 데이터 프레임, MAC 주소, FCS, CRC 체크</td>
    </tr>
    <tr>
        <td><a href="docs/허브와 스위치.md">허브와 스위치</a></td>
        <td>물리계층, 데이터링크 계층, 허브, CSMA/CD, 전이중모드, 반이중모드, MAC 주소, VLAN</td>
    </tr>
</table>

## Chapter 03 네트워크 계층

<table>
    <tr>
        <th>
            제목
        </th>
        <th>
            주요 키워드
        </th>
    </tr>
    <tr>
        <td><a href="docs/인터넷 프로토콜.md">인터넷 프로토콜</a></td>
        <td>네트워크 계층, 라우터, IPv4, IPv6, IP단편화, IP주소지정, MTU, IP Header, ARP</td>
    </tr>
    <tr>
        <td><a href="docs/IP주소할당과 DHCP.md">IP주소할당과 DHCP</a></td>
        <td>IP, DHCP, 클래스 풀, 클래스 리스, 서브넷 마스크, 네트워크 주소, 호스트 주소</td>
    </tr>
    <tr>
        <td><a href="docs/라우팅.md">라우팅</a></td>
        <td>라우팅 테이블, 정적 라우팅, 동적 라우팅, AS, IGP, RIP, OSPF, EGP, BGP</td>
    </tr>
</table>

## Chapter 04 전송 계층

<table>
    <tr>
        <th>
            제목
        </th>
        <th>
            주요 키워드
        </th>
    </tr>
    <tr>
        <td><a href="docs/전송 계층 개요.md">전송 계층 개요</a></td>
        <td>전송 계층, 신뢰성, 연결성, 프로세스 식별, 포트, NAT & NAPT</td>
    </tr>
    <tr>
        <td><a href="docs/TCP 연결과 해제 그리고 UDP 개요.md">TCP 연결과 해제 그리고 UDP 개요</a></td>
        <td>포트, MSS, TCP 3 Hand Shake, TCP 4 Hand Shake, TCP State, UDP</td>
    </tr>
    <tr>
        <td><a href="docs/TCP 오류 흐름 혼잡제어.md">TCP 오류, 흐름, 혼잡제어</a></td>
        <td>RTT(Round Trip Time), 파이프라이닝 Stop-and-Wait ARQ, Go-Back-N ARQ, Selective repeat ARQ, Sliding Window, 송신버퍼, 수신버퍼, 혼잡 윈도우, 느린시작, 느린시작 임계치, 혼잡 회피, 빠른 회복</td>
    </tr>
</table>

## Chapter 05 응용 계층

<table>
    <tr>
        <th>
            제목
        </th>
        <th>
            주요 키워드
        </th>
    </tr>
    <tr>
        <td><a href="docs/DNS와 자원.md">DNS와 자원</a></td>
        <td>DNS(Domain Name System), DNS 서버, 네임 서버, 루트 도메인, TLD 도메인, 로컬 네임서버, 루트 네임서버, TLD 네임서버, 책임 네임서버, 재귀적 질의, 반복적 질의, URI, URL</td>
    </tr>
    <tr>
        <td><a href="docs/HTTP.md">HTTP</a></td>
        <td>요청-응답 기반 프로토콜, 미디어 독립적, Stateless, 지속연결 기능 지원, HTTP Method, HTTP Response status code</td>
    </tr>
    <tr>
        <td><a href="docs/HTTP 주요 헤더와 캐시.md">HTTP 주요 헤더와 캐시</a></td>
        <td>WWW-Authenticate, Authorization, 브라우저 캐시, If-Modified-Since, Not-Modified(304), Etag, If-None-Match. Content negotiation</td>
    </tr>
</table>

## Chapter 07 네트워크 심화

<table>
    <tr>
        <th>
            제목
        </th>
        <th>
            주요 키워드
        </th>
    </tr>
    <tr>
        <td><a href="docs/안정성을 위한 기술.md">안정성을 위한 기술</a></td>
        <td>안정성, 가용성, 고가용성(High Availiablity), SPoF(Single Point of Failure), 이중화, 다중화, 로드밸런스, 라운드로빈, 최소연결, 포워드 프록시, 리버스 프록시</td>
    </tr>
    <tr>
        <td><a href="docs/안전성을 위한 기술.md">안전성을 위한 기술</a></td>
        <td>대칭키 암호화, 비 대칭키 암호화, HTTPS, TLS HandShake, CA(Certification Authority)</td>
    </tr>
</table>

