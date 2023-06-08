# IP

OSI 7 계층에서는 3번째 계층에 위치해 인터넷에 연결된 호스트들의 식별자 입니다. 즉, 인터넷에 연결된 장치(=호스트)의 주소를 뜻합니다.

## 1. IPv4

- IP 주소는 192.168.132.255 와 같이 표현되며 0 ~ 255 사이의 숫자(8bit)를 .으로 분리하여 나타냅니다. 총 32bit의 수를 표현할 수 있으며 이는 약 43억개입니다.

### 1.1 Host ID와 Network ID

- Network ID : 네트워크를 구분하는 ID 입니다.
- Host ID : 같은 네트워크 상에서 서로 다른 장치를 구분하는 ID 입니다.
  - 이 부분이 크다는 것은 같은 네트워크 안에서 많은 장치를 식별해야 한다는 뜻이 됩니다.!

### 1.2 Class

<p align="center">
<img src="https://github.com/voka/Problem-Solving/assets/38587274/e45fdb3e-aa5a-4ad4-b901-e8e791bc32a9"></p>
- 주로 A,B,C 클래스를 사용합니다. 
- 1개의 네트워크내에서 사용할 수 있는 Host 영역은 2^n(host 영역의 bit 수) - 2 가 되는데 그 이유는 Host ID가 모두 0 이면 네트워크 ID가 되고, 1이면 BroadCast 주소로 사용하기 때문이다.
	- ex) c 클래스 -> 192.168.1.0 -> Network ID /  192.168.1.255 -> broadcast 주소

| 클래스 |               용도                | 첫 마디의 범위 | 네트워크 ID 1개당 Host ID 개수 |
| :----: | :-------------------------------: | :------------: | :----------------------------: |
|   A    |   대규모 네트워크 환경에 사용.    |    0 ~ 127     |            2^24 - 2            |
|   B    | 중간 규모의 네트워크 환경에 사용. |   128 ~ 191    |            2^16 - 2            |
|   C    |   소규모 네트워크 환경에 사용.    |   192 ~ 223    |            2^8 - 2             |
|   D    |           멀티 캐스팅용           |                |                                |
|   E    | 연구/개발용 이며 잘 쓰이지 않음 . |                |                                |

- Class에 따른 IP 분할의 한계
  - ex) A 회사가 필요한 IP의 수가 100개라고 하자. 이러면 C class를 A에게 주는 것이 가장 효율적이다. 하지만 이렇게 되면 C Clsss 의 254 개의 Host ID 중 100개만 사용하고 154개는 낭비하게 된다. 이러면 안그래도 적은 IP 수가 낭비되는 것이다. 그래서 나온 개념이 Subnet 이다.

### 1.3 Subnet

- Subnet : Network를 분할한 작은 네트워크
- Subnetting : Network를 분할 하는 것
- Subnet Mask : Subnetting에 사용되는 Network ID와 Host ID를 분리하는 기준
- CIDR(Classless Inter-Domain Routing) : 클래스가 없는 도메인간의 라우팅 방법으로 클래스로만 구분된 네트워크의 한계를 극복하기 위한 수단으로 개발되었다.

- Class 별 기본 Subnet Mask
<p align="center">
<img src="https://github.com/voka/Problem-Solving/assets/38587274/78ae0d9c-2cf7-47a1-8566-88e9cacd2793"></p>

ex) C 클래스 예시 (Subnetting + CIDR 표기)

<p align="center">
<img src="https://github.com/voka/Problem-Solving/assets/38587274/64cb3bab-727a-4488-abe0-830f58987ceb" width=400px></p>

## 2. IP 종류

1. 공인 IP : IP 주소는 임의로 우리가 부여하는 것이 아니라 전 세계적으로 ICANN이라는 기관이 국가별로 사용할 IP 대역을 관리하고, 우리나라는 한국인터넷진흥원(KISA)에서 국내 IP 주소들을 관리하고 있다. 이것을 ISP(Internet Service Provider의 약자로 KT, LG, SKT와 같이 인터넷을 제공하는 통신업체)가 부여받고, 우리는 위 회사에 가입을 통해 IP를 제공받아 인터넷을 사용하게 되는 것이다. 이렇게 발급받은 IP를 공인 IP라고 한다.
2. 사설 IP : 어떤 네트워크 안에서만 **내부적으로 사용되는 고유한 주소**이다. 사설 IP는 보통 내 컴퓨터에서 사용하는 로컬 IP라고도 불리운다.
3. 고정 IP : **고정적으로 부여된 IP**로 한번 부여되면 IP 반납을 하기 전까지는 다른 장비에 부여할 수 없는 고유의 IP로 보안성이 우수하기 때문에 보안이 필요한 업체나 기관에서 사용한다.
4. 유동 IP : 인터넷 사용자 모두에게 고정 IP를 부여해 주기는 힘들기 때문에, 일정한 주기 또는 사용자들이 인터넷에 접속하는 매 순간마다 사용하고 있지 않은 **IP 주소를 임시로 발급해 주는 IP**이다. 대부분의 사용자는 유동 IP를 사용한다.

## 3. IPv6

- IPv4의 개수가 부족해 등장했다.
- IPv6 vs IPv4 간단 비교

|                  | IPv4                                 | IPv6                                      |
| ---------------- | ------------------------------------ | ----------------------------------------- |
| 표현             | 10진수                               | 16진수                                    |
| 길이             | 32비트(4바이트)                      | 128비트(16바이트)                         |
| 제공범위         | 약 43억개                            | 3.4×10^8 개 => 43억×43억×43억×43억개      |
| 메시지 전송 방식 | 유니캐스트, 멀티캐스트, 브로드캐스트 | 유니캐스트, 멀티캐스트, 애니캐스트        |
| 암호화 및 인증   | 제공 X                               | 제공 O                                    |
| 예시             | `192.168.1.1`                        | `2027:0da8:8b73:0000:0000:8a2e:0370:1337` |

하지만 아직도 많은 기기는 IPv4를 사용하는데 이는 IPv6가 v4에 대한 하위 호환성을 제공하지 않고, 이로 인해 기존 네트워크 인프라의 모든 장비를 v6 호환이 되는 장비로 바꿔야 하기 때문. [IPv6 보급율](https://stats.labs.apnic.net/ipv6)

## 4. IP 주소의 부족을 해결하기 위한 방법 !

### 4.1 Subnetting

### 4.2.1 Private IP와 NAT(Network Address Translation) - 공유기

<img width="1000" alt="image" src="https://github.com/voka/Problem-Solving/assets/38587274/cc8171c7-9c46-4513-923d-e7a2ddf695e9">
(2) -> (3) : Outbound
(5) -> (6) : Inbound
<p align="center"><img width="700" alt="image" src="https://github.com/voka/Problem-Solving/assets/38587274/458c6ad9-d279-45c4-939f-7f37d8ed23f0"></p>
- 반대로 외부에서 접근하는 경우 어떻게 될까 ? 
	-  공유기는 내부의 어떤 장치에게 Packet을 전달해야 하는지 몰라 Drop 시킨다. -> 방화벽 역할도 수행

- 그림 출처 (널널한 개발자)
  https://www.youtube.com/watch?v=7BvzxbG4y3Y

### 4.2.2 DHCP(Dynamic Host Configuration Protocol) 서버 - 공유기 내장

- 호스트의 IP주소와 각종 TCP/IP 프로토콜의 기본 설정을 클라이언트(내부 장치들)에게 DHCP를 사용해 자동적으로 제공해주는 서버를 말합니다. (간단히 말하면 내부 장치들이 네트워크에 접속할 수 있게 Private 주소 및 TCP/IP 설정 해주는 서버)

- IP 주소와 함께 유효한 시간을 알려줌 (사용자가 설정 가능) + **클라이언트와 연결된 기본 게이트웨이**(컴퓨터가 처음 접속할 때 맨 처음 거치게 되는 라우터)와 Local DNS 서버 주소

- 7계층 프로토콜이며 UDP를 실제 전송에 사용한다.

- 임대기간 이후에도 계속 해당 IP 주소를 사용하고자 한다면 IP 주소 임대기간 연장(IP Address Renewal)을 DHCP 서버에 요청해야 하고 또한 단말은 임대 받은 IP 주소가 더 이상 필요치 않게 되면 IP 주소 반납 절차(IP Address Release)를 수행하게 됩니다.

- DHCP 장점
  - PC의 수가 많거나 PC 자체 변동사항이 많은 경우 IP 설정이 자동으로 되기 때문에 효율적으로 사용 가능하고, IP를 자동으로 할당해주기 때문에 IP 충돌을 막을 수 있습니다.
- DHCP 단점
  - DHCP 서버에 의존되기 때문에 서버가 다운되면 IP 할당이 제대로 이루어지지 않습니다.

#### 4.2.3 DHCP 서버와 클라이언트간 DHCP 프로토콜을 이용한 통신과정

- Discover 과정
  - Client는 DHCP 서버의 주소를 모르기 떄문에 Broadcast 통신을 하게 된다. -> 빠른 통신 속도 + 연결이 필요 없는 통신 -> UDP 사용 이유.
- Offer 과정

  - DHCP가 브로드캐스트 메세지를 받으면 클라이언트에게 서버 자신의 IP 주소를 알려준다. 이와 함께 클라이언트가 사용할 IP주소, DNS 정보, IP 주소의 사용 시간(Lease Time)을 전달한다. 그런데, 이 DHCP 서버 또한 클라이언트의 주소를 알지 못하여 메세지를 보낼 수 없다.(아직 IP 주소 할당이 안됐다!) 그렇기 때문에 마찬가지로 브로드캐스팅하여 이 정보를 사방으로 뿌린다.

- Request 과정

  - DHCP 서버로부터 제안받은 IP 주소와 DHCP 서버 정보를 포함한 DHCP 요청 메시지를 브로드캐스트로 전송 -> DHCP 서버 여러대 존재할 수 있으며 DHCP Offer 메시지를 보내면서 해당 단말에 할당해 줄 IP 주소와 기타 정보를 내부적으로 저장해 놓기 때문에 선택 받지 못한 DHCP 서버들이 이 IP 주소와 기타 정보들을 삭제할 수 있도록 하기 위함이다

- ACK 과정
  - DHCP 클라이언트로부터 IP 주소를 사용하겠다는 요청을 받으면 DHCP 서버에 해당 IP를 어떤 클라이언트가 언제부터 사용하기 시작했는지 정보를 기록하고 DHCP Request 메시지를 정상적으로 수신했다는 응답을 전송
  - (DHCP 메시지 내에 Broadcast Flag가 존재하는 이유는 단말의 TCP/IP 구현 특성에 기인한다. 어떤 단말은 DHCP Ack 메시지를 통해 최종적으로 IP 주소를 할당 받기 전까지는 해당 IP 주소를 목적지로 하는 유니캐스트 패킷을 수신할 수 없으며 이 경우 단말은 DHCP Discover/ Request 메시지를 보낼 때 Broadcast Flag=1로 하는 것이고, 만약 IP 주소를 할당 받기 전에도 유니캐스트 패킷을 수신 할 수 있는 단말(Windows의 경우)은 Broadcast Flag=0으로 설정하는 것이다)
    <img width="800" alt="image" src="https://github.com/voka/Problem-Solving/assets/38587274/e3d5e767-9896-444a-b41f-72866dbd8c4d">
- 주요 파라미터
  - Client MAC: 단말의 MAC 주소
  - Your IP: 단말에 할당(임대)할 IP 주소
  - Subnet Mask (Option 1)
  - Router (Option 3): 단말의 Default Gateway IP 주소
  - DNS (Option 6): DNS 서버 IP 주소
  - IP Lease Time (Option 51): 단말이 본 IP 주소(Your IP)를 사용(임대)할 수 있는 기간(시간)
  - DHCP Server Identifier (Option 54): 본 메시지(DHCP Ack)를 보낸 DHCP 서버의 주소

### 4.4 IPv6 사용하기

## 5. IP 통신의 한계

### 5.1 비신뢰성

- 데이터의 흐름에 관여하지 않기 때문에 보낸 패킷이 제대로 갔는지 보장하지 않는다. (순서대로 전송해도 순서대로 받아진다는 보장이 없다.)

### 5.2 비연결성

- 패킷을 받을 대상이 없거나 서비스 불능 상태여도 전송 대상의 상태를 파악할 방법이 없기 때문에 패킷을 그대로 전송한다.

### 5.3 한계 극복

- TCP

Network에서 Gateway : **한 네트워크(segment)에서 다른 네트워크로 이동하기 위하여 거쳐야 하는 지점**

- 보통 라우터임.
