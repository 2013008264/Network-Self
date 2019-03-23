# Ethernet and ARP
> The Local Area Network. (LAN)

### Frame
> The transmission structure in link layer.
 * Dest address : Destination MAC address.
 * Src address : Source MAC address.
 * Type : IP protocol
 * CRC : Error checker.

### Minimum frame size
> The transmission is guaranteed if there is no collision.
> So the collision detection is the most important in Ethernet.
* To guarantee the collision must be detected, we make the minimum frame size as 64 bytes.

### MAC Address
> The address which is used by link layer.
> First 24 bit is corporation number.
> Last 24 bit is special number.

### ARP
> The protocol which matches IP and MAC
> Address Resolution Protocol
> There are ARP Table, but at first, the table is empty.
1. First device broadcasts the ARP message.
2. If the receiver has that IP address receiver replies.
3. Device add it the ARP table.

**This is very different to Router's forwarding table!!**
**This is just for one hop!!**

### CSMA/CD
> Talk when medium is clear.
> But this cannot guarantee that there are no collisions.
* If collision is detected
  * Stop immediately.
  * Exponential backoff.

### Switch
> Link layer device

* Divide collision domain.
* Network does not know about this device.
* Switch table
  * Self learning
    * If unknown MAC addr -> flooding and write it.

* Router --> Make subnet. But switch uses same network!
* Use switches in data center.
  * Handling traffics --> layering.