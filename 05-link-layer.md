# Link layer
> 단 한번의 Hop 에 관한 이야기.
> Collision handling 을 중심으로

### Where is the link layer implemented ?
> Link layer 는 NIC (Network interface card) 에 구현되어 있습니다.

### Why MAC?
> Because the network environment is "Broadcast medium" 
 * There must be collision.
 * How to handle these?
   * MAC Protocol
     * R data rate 전부를 쓰고 싶다.
     * M Node 가 동시에 보내면 R / M 의 Data rate 를 개인에 할당하고 싶다.
     * 분산 처리가 가능하면 좋겠다.
     * Protocol 이 simple 했으면 좋겠다.

### TDMA ?
> Time division multiple access
 * 사용률이 떨어진다.
 * Packet switching 에 맞지 않음.

### Random access
> You can use whenever you want! but..
 * How to handle the collision?
   * How to detect collision
   * How to recover from collision.
 * ALOHA / slotted ALOHA
 * CSMA
 * CSMA/CD (Ethernet)
 * CSMA/CA (Wireless)

### CSMA
> Carrier sense multiple access
> **Listen before transmit** like human!
 * If someone says something, don't transmit!
 * But this cannot guarantee that the collision is not happened.

### CSMA/CD
> CSMA with collision detection!
> CSMA cannot guarantee that the collision is not happened, so we must detect collision
 * If the collision has been detected, transmit is stopped.
 * After aborting NIC enters **binary(exponential) backoff**
   * Pick the random number from {0, 1, 2, 2^m - 1}
   * This is the short point of random access.

### Trade - offs
 * In channel partitioning
   * Good : When a number of heavy users are using.
   * Bad : Not good when many of the users using sometimes..
 * In random access
   * Good : Many of the users using sometimes.
   * Bad : When a number of heavy users are using.
 > So there are another protocols for both worlds! but...

 ### Taking turns protocols
 > Looks like the best protocol for MAC but there are huge concerns.
  * Polling
    *  Single point of failure (in master node..)
  * Token passing
    * Also single point of failure (Where is the token!?) 

### In conclusion
> There are no winner protocol.
> But random access suits for Packet, we use CSMA/CD in Ethernet.