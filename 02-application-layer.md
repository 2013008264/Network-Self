# Chapter 2. Application layer
|Application layer|
|---|
|Transport layer |
|Network layer|
|Data link layer |
| Physical layer |

* Application layer 는 아주 다양하다.
* 실제로 코딩도 가능하다.
* Application layer 의 입장에서 보면, 정말 마법처럼 다른 Application layer 와 통신할 수 있는 것 처럼 보인다.

*********************************
## Client - server architecture
### Server
* 24시간
* 고정된 주소로
### Client
* 가끔
* 고정되지 않는 주소로
* 서버와 통신

### Socket
* 다른 컴퓨터의 Process 간 통신을 위해, 사용되는 API
* OS level 에서 제공됨.
* UDP socket, TCP socket
* Port number 로 구분 가능.
* IP address + Port number = 특정 컴퓨터의 특정 process
* Server 의 port number 는 정해져있어야 한다.
* Client 의 port number 는 바뀌어도 상관이 없다.

### TCP / UDP
* Does not support
    * Security
    * Timing guarantee
        * 해당 서비스는 Application layer 에서 해줘야 한다는 소리임.
* DNS, Multimedia streaming 과 같은 특수한 경우를 제외하면, 대부분 TCP 를 사용중에 있다.
*******************************
## HTTP
* Hyper text 를 요청하고 끝이 나는 protocol.
* Request <--> Response 가 정말로 끝임.
* TCP 를 사용.
    * TCP connection 과정 필요
    * 3-way, 4-way handshake.
* Stateless protocol
    * State 가 없기 때문에, Cookie 라는 꼼수를 만들어서, State 를 만듦.

### Non persistence http
* TCP connection 을 만들고 바로 없앤다.
* 비효율적이라 지금 사용되진 않음.
### Persistence http
* TCP connection 을 만들고 지우지 않는다. - 현재 default

*********************************

## Proxy
* Web cache
* 캐시와 동작은 비슷함.
* 장점도 같고, 빨라지는 이유도 같음.
* 사용자 : 빠르다 !
* 네이버 : 서버 부하 줄어들었다 !
* Proxy server 주인 : 통신비 줄어들었다!

### Conditional get
* 달라지면 새로운 파일을 받아옴.
* 달라지지 않았으면 Header 만 날라옴.

### Disadvantages
* 데이터의 무결성이 깨질 수 있다.
    * 하드웨어 캐시와 같은 이유.

**********************************
## DNS
* 1차원적인 Database
* DNS 는 굉장히 중요하기 때문에, 여러 개의 DNS가 부하를 분산받는 구조로 되어 있습니다.
* 각 Host 들은 자기 자신의 DNS 를 가지고 있어야 합니다.

### DNS hierarchy

![DNS-HIER](/pictures/02/DNS-HIERARCHY.png)

### Local DNS Server
* ISP 가 가지고 있는 것입니다.
* 누군가가 DNS Query 를 날렸을 때, Local DNS Server 로 먼저 갑니다.
* Proxy 와 같은 역할을 비슷하게 수행합니다.
* 역시나 Cache 와 같은 단점이 있습니다
    * 자료에 유통기한을 두는 방식으로 해결했습니다.

### DNS records
|name| value | type | ttl |
|---|---|---|---|
|my-dns| 1.1.1.1 | name server | 1 day|
|my-server | 2.2.2.2 | answer | 1 day |
이런 형식입니다.

### DNS flow
1. Local dns server 에 물어본다.
2. 없으면 .com .edu 등 맞는 포맷의 dns server 에 물어본다.
3. 없으면 root 에 가서 물어본다.
4. root 가 그건 사실 .com 에 있다고 말한다.
5. .com 은 2.2.2.2 가 그 ip 를 갖고 있다고 말한다.
6. 2.2.2.2는 3.3.3.3 이 답이라고 말한다.