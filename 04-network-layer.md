# Network layer
> The story of routers.
> How routers do route ?

### Loss & delays
 * Pakcet loss
 *  Destination processing delay
    * Route 하는데 걸리는 시간. 
 *  Queueing delay
 *  Transmission delay
 *  Propagation delay
    *  빛의 속도라 어쩔 수 없음.

## Forwarding
> 특정 목적지로 보내는 것.
#### Datagram forwarding table
> Router 안의 table 을 통해 특정 목적지로 보냄.
> 해당 Table 은 ip address 의 범위가 있음.
* Forwarding 하는 데는, longest prefix matching 을 사용한다.
  * JAVA Regex 생각하면 된다.
  * Router 가 주로 하는 일은 Longest prefix matching 이다.

## IP
#### IP datagram
* TTL : Time to live
    * Traffic 안정성 증가
    * Routing table 이 잘못되어서 loop 를 도는 경우.
* Upper layer : TCP ? UDP ? 인지.

#### IPv4
> Host 를 지칭하는 주소
* Network interface card 한 개 --> 한 개의 IP Addr
* 처음에는 막무가내로 배정했다.
  * Forwarding table 이 아주 거지 같음.
  * 그래서 계층화 함.
* Network / Host 형식으로 계층화.
  * Subnet mask 를 통해 확인 가능.
  * Forwarding table 이 아주 단순해진다.
  * Host 가 추가되어도 Network 는 추가할 필요가 없기 때문에 forwarding table 은 변하지 않는다.

#### Classful addressing
> 옛날에 사용하던 Class. 식.. 막 MIT 가 Host 가 2^24개 갖고있음.
> 현재는 사용하지 않음.

#### Subnets
> Network ! Set of same prefix (subnet ID) device
* 같은 Network 안에서는 router 를 거치지 않고 서로 접근이 가능하다.
* Router 는 여러 개의 Subnet 에 속해있다.

#### IPv6
> 20년 지남...
> Architecture 가 한 번 들어오면 바꾸기 힘들기 때문에 신중히 사용.
> Router 의 소유자가 다 다르기 때문에 프로토콜을 바꾸는 작업이 쉽지 않음.
> IPv6 를 사용하지 않을 수도.

## NAT (Network address translation)
> 좋은 방법은 아니지만, IPv4 로도 우리가 많은 통신기기를 사용할 수 있도록 해준다.

* NAT Gateway 가 나가면서 IP Addr 을 바꿔치기함.
* NAT Gateway 가 Port number 를 통해 자신과 통신하는 기기를 판별하기 때문에 gateway 를 나갈 때 Port number 를 바꿔야 하는 일이 필요함.
  * Layer violation
* 일반인이 서버 운영하기 힘들어짐.

#### DHCP (Dynamic Host Configuration Protocol)
> Host 에 IP, Subnet mask, Router, DNS 정보를 주는 Protocol

1. 누군지 모르고 그냥 Broadcasting 함. discover
2. DHCP Server 만 유일하게 받는다. (나머지는 다 버림)
3. 너 혹시 이거 쓰지 않을래? 하고 DHCP server 가 답변한다. (Transaction ID 가 같아야 함) offer
4. 앗 써도 될까요?? 하고 되묻는다. request
5. ㅇㅇ ACK

* 무선 공유기가 NAT, DNS, DHCP 역할을 하기도 함.
* 그래서 같은 건물에서 IP Addr 이 같다면 큰 의미가 있는 것이 아니다!

#### ICMP
> Network 상의 상황을 운반하기 위한 프로토콜

* TTL 만료
* Port 닫힘

## Routing algorithms
* Link state --> DijkStra (Intra AS)
* Distance vector --> DV vector (Intra AS)
  * DV Algorithm 은 자기 자신이 알고 있는 distance 를 전달하기 때문.
  * DV Vector 값이 바뀌면 전달. if not update --> 정지
  * 최소 경로 algorithm 이고 recursive.
  * Poison reverse --> count infinite 막기 용
    * 해당 경로를 결정하는데 Critical 역할 neighbor 에게 infinite distance 를 전달하는 것.
* Hierarchial routing
  * 너무 커서 계층적으로 사용
  * 네트워크 끼리는 각자 결정함. (LS or DV --> Intra AS)
  * 네트워크 사이의 routing 은 어른의 사정으로 LS, DV 를 사용할 수 없음.
    * 한국은 북한에 트래픽을 보내기 싫어한다. 때문에 중국과의 연결에 북한을 거치지 않고 돌아간다.

#### BGP
> 너무 복잡해서 간단히만 보자.
* 각각의 AS 는 번호가 있다.
* AS 는 갑을 관계가 형성된다.
  * Provider and consumer
  * Peering
* 정책에 따라 어떤 네트워크를 통할지 정해진다. 꼭 최단거리가 아니다.
  * 돈 때문에 돌아갈 수도 있다.
  * 구글을 싫어해서 구글을 사용하지 않을 수도 있다. 

