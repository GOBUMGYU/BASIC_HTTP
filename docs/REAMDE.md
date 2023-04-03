# 인터넷 네트워크, URI와 웹 브라우저 요청 흐름

### IP
- **지정한 IP주소 (IP Adress)에 데이터 전달**  
- **패킷(Packet)이라는 통신 단위로 데이터 전달 ((출발지 IP, 목적지 IP, 기타...) + 전송데이터)**  

### IP프로토콜의 한계 
- **비연결성**
  - **패킷을 받을 대상이 없거나 서비스 불능 상태여도 패킷 전송(결국 받지 못함)**
- **비신뢰성**
  - **서버에 문제가 생기던지 전송중 노드에 문제가 생겨 패킷이 소실되어도 그 사실을 알지 못함**
  - **패킷 전달 순서가 보장되지 않는다.**
  
### TCP, UDP
**위에서 설명했던 IP프로토콜의 문제들을 TCP프로토콜이 해결해준다.**

**인터넷 프로토콜의 4계층**
- **애플리케이션 계층 - HTTP, FTP**
- **전송계층 - TCP, UDP**
- **인터넷 계층 - IP**
- **네트워크 인터페이스 계층 (Lan드라이버, Lan장비, Lan카드)**

### TCP 
출발지 Port, 목적지 Port, 전송제어, 순서, 검증정보..

**TCP/IP 패킷 정보**
![Untitled](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/d42467b8-a669-402c-89e9-a66faef1c6a0/Untitled.png)  

**TCP 특징**
**전송 제어 프로토콜**
- 연결지향 - TCP 3 way handshake(가상연결)
  - 나랑 상대방이랑 연결이 되었는지 확인을 하고 연결이 되었으면 메시지를 보냄
  - 1. SYN(요청) 2. SYN+ACK(요청+응답) 3. ACK응답(데이터전송) 1,3 클라이언트 2 서버

- 데이터 전달 보증 
  - 데이터를 보냈는데 중간이 누락되었다면 누락이 되었다는 것을 알 수 있다.
    - 클라이언트가 서버로 데이터 전달을 하면 서버가 데이터를 잘 받았다고 응답을 함
    - 만약 서버에서 응답이 없으면 문제가 있다고 인지
- 순서보장
- 신뢰할 수 있는 프로토콜 
  - TCP방식은 전송제어 장소, 순서정보, 검증정보들이 추가되어있다.
  - 그렇기 때문에 TCP가 신뢰할 수 있는 프로토콜이라고 함
  
### UDP 특징
**사용자 데이터그램 프로토콜**
- 기능이 거의 없음
- 연결지향 - TCP 3 way handshake를 사용하지 않음
- 데이터 전달 및 순서가 보장되지 않지만, 단순하고 빠름
- 정리 
  - IP와 거의 같고 + PORT + 체크섬 정도 추가
  - 애플리케이션 추가 작업이 필요  
    
최근에 UDP가 뜨고 있는데 HTTP 통신을하는데 TCP3 way handshake에서 하는 일까지 줄여 최적하를 하려는 움직임이 있기 때문에 뜨고 있음.

### PORT
IP는 목적지 서버를 찾는 것이고 포트는 서버 안에서 돌아가는 애플리케이션을 구분하는 것이라 이해하면 된다.
- 즉 같은 IP내에서 프로세스 구분 
- 0 ~ 65535 할당 가능
- 0 ~ 1023 : 잘 알려진 포트, 사용하지 않는 것이 좋음
  - FTP - 20, 21
  - TALNET - 23
  - HTTP - 80
  - HTTPS - 443

### DNS 
도메인 네임 시스템
- DNS서버에 아이피와 도메인 명으로 매핑한 것을 바탕으로 응답을 내려준다.
- 도메인은 구입해야 함

### URI
리소스를 식별하는 통합된 방식  
URI는 로케이터(locator), 이름(name) 또는 둘다 추가로 분류될 수 있다.
- URI(Uniform Resource Identifier)리스소를 식별한다 (주민번호 처럼 식별한다고 생각) 가장 큰 개념
- URL(Unifrom Resource Locator) 리소스의 위치 
- URN(Uniform Resource Name) 리소스의 이름

### URL 전체 문법

scheme://[userInfo@]host:[:port][/path][?query][#fragment]

**scheme**

- 주로 프로토콜 사용
- 프로토콜 : 어떤 방식으로 자원에 접근할 것인가 하는 약속 규칙
    - 예) http,https,ftp등등
- http는 80포트, https는 443 포트를 주로 사용, 포트는 생략 가능
- https는 http에 보안 추가 (HTTP Secure)

**[userInfo@]**

- URL에 사용자정보를 포함해서 인증
- 거의 사용하지 않음

**host**

- 호스트명
- 도메인명 (www.google.com같은 것을 말함) 또는 IP주소를 직접 사용 가능

**port**

- **[:port]**부분
- 포트(PORT)
- 접속 포트
- 일반적으로 생략, 생략시 http는 80, https는 443

**path**

- **[/path] = search부분에 해당**
- 리소스 경로(path), 계층적 구조
- 예 ) /home/file1.jpg
    - /members
    - /members/100, /items/iphone12

**query**

- **[?query] =  ?q=hello&hi=ko 부분에 해당**
- key = value 형태
- ?로 시작, &로 추가 가능 ?keyA=valueA&keyB=valueB
- query parameter, query string 등으로 불림, 웹서버에 제공하는 파라미터, 문자형태

**fragment**

[#fragment]

- scheme://[userinfo@]host[:port][/path][?query]**[#fragment]**
- https://docs.spring.io/spring-boot/docs/current/reference/html/getting-started.html**#getting-started-introduce-spring-boot**
- fragment
- html내부 북마크 등에 사용
- 서버에 전송하는 정보가 아님

https://www.google.com/search?q=hello&hi=ko

- 프로토콜(https)
- 호스트명(www.google.com)
- 포트번호(443)
- 패스(/search)
- 쿼리 파라미터(q=hello&hi=ko)