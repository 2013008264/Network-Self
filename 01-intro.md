# Chapter 1.

### Network
* 어렵게 생각하지 말고, Process 와 Process 간의 통신이다 라고 생각하자.
* 같은 컴퓨터 안에서의 통신이라면, Message passing, PIPE 를 통해서 해결하겠지만, 다른 컴퓨터의 Process 와 통신을 해결하는 것은 Socket 이라는 API 이다.


### Network structure.
* Network edge
    * Applications and hosts
* Network core <br>
    * Routers (almost)
    * Network of network

### The network edge.
 * Hosts
 * Client / Server model.
 * Peer to peer model
 * End user 의 관점에서는 아주 마법처럼 서비스 됨.
    * TCP --> 등기
    * UDP --> 그냥 우체통 (잃어버려도 상관 없음.)

### TCP
* Reliable
* In-order byte-stream data transfer
* Flow control
    * Super computer & 286 간의 속도 차이 제어.

* Congestion control
    * Network 상황에 맞게 보낸다.
    * Condition control
* 데이터를 소실하지는 않는다.
* 다만 Expensive.
* http, ftp, SMTP, telnet

### UDP
* Connectionless service
* 우체통에 넣고 보내지길 기대하는 것.
* Resource 소모가 작다.
* 값싸고 빠를 수 있다.
* 다만 데이터가 소실될 수 있다.
* DNS, Streaming

### The network core
* Circuit switching
    * 전화
* Packet switching
    * 인터넷 사용 패턴에 조금 더 적합함.

### Circuit switching
* End - end resources reserved for "call"
    * resource 를 계속 보유함..

### Packet switching
* 보내고자 하는 Message 를 Packet 으로 쪼개서, Multiplexing.
* 공유가 쉽다.
* 회선을 Circuit switching 에 비해 조금 더 효율적으로 사용할 수 있다.
    * 모든 회선을 사용자가 계속 점유하는 것이 아니기 때문에, Smoothing 효과를 기대하면서,<br>
    회선을 Circuit switching 에 비해서 더 효율적으로 사용할 수 있다.
<br>
*********************************
## Delay & loss in packet-switched network.
### Delay
* Processing delay
    * 항상 생길 수 밖에 없는 delay
    * 어디로 보낼지 판단하는 delay
* Queueing delay
    * Network condition 에 따른 delay
    * 들어온 순서대로 내보내줌.
* Transmission delay
    * Router 에서 보내려는 Data 가 다 빠져나가는 delay
* Propagation delay
    * Data 는 빛의 속도로 움직이기 때문에, 어디서든 큰 차이를 보이는 곳은 없다.

* Router 가 건드릴 수 있는 delay
    * Processing delay
    * Transmission delay

### Packet loss
* Router 가 queue 를 쓰고 있기 때문에 일어나는 일.
    * Queue 가 꽉 찼다!
    * 새로 들어온 데이터를 넣을 공간이 없다!
    * 고로 버린다.

* Packet loss 가 있을 때, 재전송 해주는 것은 TCP 의 역할이다.
* Router 는 TCP stack 이 없기 때문에, 재전송 하지 않는다.

![TCPLOSS](/pictures/01/TCP-LOSS.png)
*********************************************
## Network layering
* Network 는 굉장히 복잡하다. 그 굉장한 복잡함을 조금이라도 쉽게 해결하기 위해서는, Layering 이 필수이다. 그래서, 일어난 일이다.