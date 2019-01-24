# TCP
> Transport layer protocol

### TCP seq. #'s and ACKs
 * TCP uses cumulative ack
 * Sequence and ACK number in header.

 ### Timeout -- RTT
 - Not fixed time.
 - RTT must be shorter than timeout.
 - Using exponential avg.
    * EstimatedRTT = (1-a) * EstimatedRTT + a * SampleRTT <br>
      typically a = 0.125
    * DevRTT = (1-b) * devRTT + b * | SampleRTT - EstimatedRTT | <br>
      typically b = 0.25
    * TimeoutInterval = EstimatedRTT + 4 * DevRTT

### Fast retransmission
 - 3 duplicated ACK

### Pipelined protocol.
 * GBN (Go back N)
    * using Cumulative ACK
    * Pros
        - Easy to implement
        - Using network inefficient (유실된건 한 개 인데, 재전송은 4개)
        ![GBN](/pictures/03/GBN-example.PNG)
 * Selective repeat
    * Donot using cumulative ACK
    * Every segment has each timeout.
    * 먼저 들어온 것은, 순서의 보장을 위해 Buffer 에 저장되어 있음
    * Sequence number --> Header overhead
        * 2 Times or 2 Times - 1 (Window size)

### Point to point protocol.
 > One sender, one receiver. <br>

### Reliable, in-order byte stream
 > no "message boundaries"

### send & receive buffers

### Full duplex data

### Connection-oriented
> Three way handshake and four way handshake.
 * Three-way-handshake
    - SYN -> SYNACK -> ACK
    - FIN -> ACK -> {DATA Transfer} -> FIN -> ACK

### Flow control
> 보내는 속도와 받는 속도의 제어
 * Receive window 라는 field 를 통해 제어.
 * Window size is dynamic
 * Nagle's algorithm
    1. First segment 는 그냥 출발시킨다.
    2. Next segment waits for ACK or it is full.
    3. For RTT and some other plus issues
    4. Recv window size 가 항상 작을 경우 계속 보내지 말라구 한다.

### Congestion control
> Network 가 public 이기 때문에, 일어나는 일. <br>
> TCP 는 자신이 스스로 조심해서 공공의 자원을 사용함. ~~무법자 UDP~~

 * 막힐것 같다 --> DATA RATE 를 스스로 낮춤.
    * Network assisted congestion control
        * Router : 나 바쁘다 ㅡㅡ 딴일 시키지마라.
    * End to end congestion control
        * 각자 유추해서 써라!

 * Three main phases
 1. Slow start
    * 첨에는 1부터 보낸다.
    * Exponentially increased
 2. Additive increase
    * Linear increase after threshold
 3. Multiplicative decrease
    * Segment가 유실되면, 반만큼 줄여버림. <br>
    ![Congestion-control](/pictures/03/Congestion-control.PNG)

    * Three duplicated ACK --> 반으로.
        * 안타깝게 하나만 유실되어서, 네트워크 상황이 완전 나쁘다고 생각할 순 없음.
    * Timeout --> 처음부터.
        * 네트워크가 데프콘임.

### TCP fairness
> Congestion control 을 각각의 pair 마다 하지만, TCP 는 생각보다 fair 하다. <br>
> 하지만, TCP socket 마다 fair 한 것이지, TCP connection 많이 열면 많이 쓰는거다.
