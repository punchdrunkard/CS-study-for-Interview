
## First, HTTP란

![](https://i.imgur.com/Vl5H6gF.png)

- **HTTP : HyperText Transfer Protocol**
    - 웹 어플리케이션층 프토토콜
    - 클라이언트와 서버 모델
- **HTTP는 TCP 프로토콜을 사용**
    1. Client : 서버에 TCP 연결을 요청
    2. Server : 클라이언트의 TCP 연결을 허가
    3. Client : 서버에 HTTP 요청
    4. Server : 클라이언트에 HTTP 응답
        - ACK 메세지가 포함된다
    5. TCP 연결 종료
- **HTTP는 상태가 없다 (비상태 프로토콜)**
    - 서버는 클라이언트의 어떠한 정보도 포함하지 않는다
    - 단지 요청 응답의 관계
        - ➡️ 이러한 특성이 RESTful API 로 이끔
    - 상태를 가지는 순간 순서가 생기면서 매우 복잡해진다

## HTTP 비지속 연결 vs 지속 연결

![](https://i.imgur.com/axmSrhZ.png)

- **Non-persistent 비지속 HTTP**
    1. TCP 연결을 엶
    2. 하나의 객체를 TCP 연결을 통해 전송
    3. TCP 연결이 종료

➡️ 매 객체마다 TCP 연결을 열고 닫기를 반복함으로 비효율적이다

![](https://i.imgur.com/v72VYaq.png)

- **Persistent 지속 HTTP**
    1. TCP 연결을 엶
    2. 여러개의 객체를 하나의 TCP연결에서 전송함
    3. TCP 연결이 종료

➡️ 비지속 연결 방법 보다 효율적

## 비지속 HTTP의 응답 시간

![](https://i.imgur.com/Z9o8aEO.png)

- **객체별 비지속 HTTP의 응답 시간**
    - - TCP 연결을 초기화하는 하나의 RTT
    - - HTTP 요청과 돌아오는 첫 HTTP 응답을 위한 하나의 RTT
    - - 객체 전송 시간

**➡️ 비지속 HTTP의 응답 시간은 2RTT + 파일 전송 시간**

- 한 객체당 RTT나 필요함
- OS 오버헤드가 크다
- 이러한 단점을 극복하기 위해 **HTTP/1.1 (Persistent HTTP)**

### 🤔 **RTT (Round-trip time) 이란?  

> 작은 패킷을 클라이언트에서 서버로 갔다가 응답이 돌아오는 시간
> 전파지연, 큐잉지연, 처리지연을 모두 포함한다.

## 지속 HTTP (HTTP/1.1) 의 응답 시간

- 객체를 전송한 후에도 TCP연결을 닫지 않고 열어준다
- 이어지는 HTTP 메세지가 클라이언트-서버간에 전송된다
- 하나 이하의 RTT를 사용하게 됨으로 비지속 방법에 비해 절반정도 빠르다
- **BUT!**
    - 계속해서 TCP연결을 유지하면 부담이 간다.
    - 연결에 timeout을 설정하여 사용하지 않으면 연결을 닫는다.

### HTTP 요청 메세지 포맷

![](https://i.imgur.com/TTTXrbW.png)

- 인간이 읽을 수 있는 ASCII 텍스트로 쓰인다
- 각 줄은 CR (캐리지리턴) LF (라인피드)로 구별된다 (마지막줄)
- 메세지의 첫 줄 은 요청 라인 (request line) 이라고 함
    - method 필드 : GET, POST, HEAD, PUT, DELETE 등
    - URL 필드 : ex) _/somedir/page.html_
    - HTTP 버전필드 : 위 그림에서는 HTTP/1.1 을 사용하고 있다
- 이후의 줄들은 헤더 라인 (header line) 이라고 함