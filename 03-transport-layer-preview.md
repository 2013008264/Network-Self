# Transport layer
* End point 에만 존재하는 layer.
    * 보내는 process, 받는 process 에만 존재한다.
*******************
## Mux & Demux
* TCP 와 UDP 가 둘 다 해주는 것.
* 여러 개의 Process 들이 보내는 것을 통제한다.
* 목적지 Process 에 대한 전달은 Port number 를 통해 한다.
* 둘 다 해주지만 다른 방식으로 해준다.
    * UDP : UDP 에서는 dest port number, dest IP address 만 알면 통신이 가능하다.
    * TCP : dest port number, dest IP addr 뿐만 아니라  src port number, src IP address 모두 알아야 통신이 가능하다.
        * 이게 어떻게 가능하냐? 라고 하면, 스레드에 소켓을 열어서 사용하기 때문이다.

********************
## UDP
Header 에 고작 4개 뿐이다.


|source port| dest port | length | checksum |
|---|---|---|---|


* Checksum 을 통한 Error checking 이 가능합니다.
    * Error 임이 확인되었을 경우, 해당 Message 는 유실됩니다.

* UDP 는 Message 유실이 크게 상관있지 않을 때 사용됩니다.
    * Streaming service

* 예외적으로 DNS 는 UDP 를 사용합니다.
    * TCP 의 3 way handshake 가 DNS 서버 입장에서 매우 큰 오버헤드 입니다.
    * DNS 서버는 connection 을 유지할 필요가 없습니다.
    * DNS 요청은 굉장히 크기가 작기 때문에, UDP Segment 에 아주 딱 맞습니다.
    * UDP 가 reliable 하지 않아도, application layer 에서 해당 기능을 추가할 수 있습니다.

*********************
## Before TCP...
> Make reliable data transfer protocol! <br>
> Protocol ' s name : rdt
* Message 는 1 개씩 주고받는다.

### RDT 1.0
> There's no packet loss. <br>
> There's no packet error.
* == We have nothing to do.

### RDT 2.0
> There are packet errors
* 전화하면서 여보세요? 네? 이런 경우를 생각하면 된다.
* Error detection 필요. (뭔가 잘못됨을 확인)
    * 
* Feedback 필요. (네? 라고 말함.)
    * ACK, NAK
* Error feedback 시, 재전송. (상대방이 다시 말해줌.)<br>
    * Retransmission

#### RDT 2.0 flow examples.
![RFE](/pictures/03/RDT2-FLOW-EXAMPLES1.png)
<br><br>
> Fatal flaw! (if there's an error in ACK & NAK)
* ACK, NAK 에 오류가 생기면, DATA 의 Sequence 를 Receiver 입장에서 확인할 길이 없다.
    * Data sequence 를 추가한다.

**RDT 2.0 이 완성되었다!**

![RFE](/pictures/03/RDT2-FLOW-EXAMPLES2.png)

### RDT 3.0
> There are packet errors <br> There are packet loss
* 전화하면서, 갑자기 통화가 안들릴 때를 생각하면 된다.
* 몇 초 기다린 후 "여보세요?"
* Timer 를 둔 다.
* Timeout 후 retransmission.
    * Timeout 은 그 때 그 때 다르다.
        * Timeout 을 짧게 두면, 불필요한 retransmission 이 있을 수 있다.
        * Timeout 을 길게 두면, 너무나도 느려질 수 있다.
    * RTT 측정 후, 1 RTT 이상으로 잡는다.

> RDT 3.0 은 결국 ACK, Data sequence, Timeout 으로 구현 가능하다.
<br>

### RDT summary
* ACK
* Data sequence
* Timeout
* TCP 도 사실 기반은 이거다.
* 다만, RDT 는 한 개를 주고 받고 주고 받고 하는 과정이 너무나도 느리기 때문에, 비효율적이다.
