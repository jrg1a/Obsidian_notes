#flashcards 
> The Network Layer is responsible for packet forwarding and routing through intermediate routers. It provides services to the [[Transport Layer]], and sits on top of the [[Link Layer]]

Some of the key characteristics and functions of the network layer includes logical addressing, routing, packet forwarding, fragmentation and reassembly, quality of service, network address translation(NAT), and other network layer protocols such as IP, IPv4 and IPv6.

Examples of network layer protocols and technologies include IP, Internet Control Message Protocol (ICMP), Internet Group Management Protocol (IGMP), Routing Information Protocol (RIP), Open Shortest Path First (OSPF), Border Gateway Protocol (BGP), and others.

Overall, the network layer plays a crucial role in ensuring the efficient and reliable transmission of data across different networks, enabling global connectivity in modern computer networks and the internet.

## Routing
Routing in the network layer of the [[TCP]]/IP protocol suite is the process of determining the optimal path for data packets to travel from a source to a destination across an interconnected network. The network layer uses routing protocols and algorithms to make routing decisions and ensure efficient packet delivery.

![[Pasted image 20230529182439.png]]

## Routers

> **Node:** A device that implements the Internet Protocol (IP).
> **Router**:  A node that forwards IP packets not explicitly addressed to itself.
> **Host**:  Any node that is not a router. 

### Hardware Perspective
From a hardware perspective, routers are specialized devices that perform network-layer forwarding, allowing data packets to be directed efficiently across networks.

#### Router as a Computer: 
A router is essentially a computer with components such as a CPU, RAM, storage, and other standard computer hardware. However, what distinguishes a router from a typical computer is its specialized hardware designed specifically for network-layer forwarding.

#### Application-Specific Integrated Circuit (ASIC):
An ASIC is an integrated circuit chip customized for a specific purpose rather than being intended for general-purpose use. In the context of routers, ASICs are often used to implement high-speed network-layer forwarding. They offer optimized performance for routing and forwarding tasks.

#### Content-Addressable Memory (CAM):
CAM is a type of computer memory used in high-speed searching applications. In the context of routers, CAM is used for efficient lookup operations. It compares input search data against a table of stored data and returns the address of matching data, enabling fast routing table lookups.

#### Ternary CAM (TCAM): 
TCAM is an extension of CAM that allows a third matching state or the ability to ignore one or more bits. This flexibility is beneficial for more complex matching requirements in routing and forwarding.

#### Forwarding using Specific (Network) Hardware: 
In this approach, routing and forwarding operations are offloaded to specialized hardware components, such as ASICs with TCAMs. These components are designed for high-speed packet processing and can interact with all layers of the networking stack. It enables efficient and fast lookup operations for routing and forwarding tables

#### Forwarding using Generic (Network) Hardware: 
In this approach, routing and forwarding operations are performed by the operating system (OS) kernel running on general-purpose hardware, such as a PC, smartphone, or low-end router. The routing and forwarding tables are typically managed and processed by the OS kernel. The link-layer functionality is implemented within network interface cards (NICs).


It's important to note that the specific hardware details of routers can vary across vendors, and some information may not be readily available to the public. Different router models and manufacturers may employ various hardware designs to achieve optimal performance and functionality in routing and forwarding data packets.


## Packet Scheduling
Packet scheduling is a crucial aspect of network management and quality of service (QoS) provisioning. It involves the prioritization and ordering of data packets in a network for transmission over limited network resources. Packet scheduling algorithms determine how packets are selected and transmitted, taking into account factors such as network congestion, QoS requirements, and fairness.

### Purpose of Packet Scheduling
Packet scheduling aims to efficiently utilize network resources, manage congestion, and provide fair and reliable transmission of packets. It plays a significant role in optimizing network performance, ensuring QoS guarantees, and maintaining a balanced flow of traffic.

- What is the purpose of packet scheduling?:: aims to efficiently utilize network resources, manage congestion, and provide fair and reliable transmission of packets.
<!--SR:!2023-06-03,1,210-->

### Scheduling Algorithms:
There are various packet scheduling algorithms, each with its own characteristics and objectives. Some common used algorithms include FIFO, RR, WFQ, PQ, CBQ, DRR, etc.

#### First-in, First-out.
First-in, First-out (FIFO) is a simple and widely used packet scheduling algorithm in networking. It operates on the principle that the first packet to arrive at a buffer or queue is the first one to be transmitted. FIFO scheduling follows a strict ordering based on the arrival time of packets, without considering any priority or specific requirements.

FIFO scheduling maintains a sequential order of packets based on their arrival time. As packets arrive, they are placed in a buffer or queue, and the packets are transmitted in the same order as they arrived. FIFO scheduling also ensures fairness in the sense that all packets have an equal opportunity to be transmitted. It treats all packets equally, regardless of their size, priority, or QoS requirements.
- a straightforward and easy-to-implement scheduling algorithm. It does not require complex computations or additional metadata associated with packets.
- A downside of FIFO scheduling is head-of-line (HOL) blocking. If a long or high-bandwidth-consuming packet is ahead in the queue, it can delay the transmission of subsequent packets, even if they are smaller or have higher priority. This can lead to increased latency and potential performance degradation.
![[Pasted image 20230529185455.png]]
Is suitable for certain scenarios where strict ordering based on arrival time is sufficient and where fairness is the primary concern. It may be employed in low-bandwidth or low-priority applications where QoS guarantees or prioritization is not critical.
![[Pasted image 20230529185515.png]]
FIFO scheduling is commonly used in basic queuing systems, such as the output queues of routers or switches. While it has limitations in terms of prioritization and QoS, it remains a widely used approach due to its simplicity and ease of implementation. More advanced scheduling algorithms, such as weighted fair queuing (WFQ) or priority queuing (PQ), are often employed to address the limitations of FIFO and provide better control over packet transmission based on various criteria.

- What is the downside of FIFO?:: head-of-line (HOL) blocking. If a long or high-bandwidth consuming packet is ahead in the queue, it can delay the transmission of subsequent packets, even if they are smaller or have higher priority. This can lead to increased latency and potential performance degradation.
<!--SR:!2023-06-03,1,228-->
- Where is FIFO commonly used?:: in basic queuing systems, such as the output queues of routers or switches. 
<!--SR:!2023-06-03,1,228-->

#### Priority Queuing
Priority Queuing (PQ) is a packet scheduling algorithm used in networking to prioritize packets based on their assigned priority levels. It ensures that higher-priority packets are transmitted ahead of lower-priority packets, regardless of their arrival order. PQ allows for differentiated treatment of packets based on their importance or QoS requirements.

Priority Queuing manages to prioritize by assigning packets different queues based on their priority levels, where each queue represents a distinct priority class. Packets are typically marked or classified with a priority value in their [[WEB Requests#HTTP Headers|header]] or metadata. The queue is illustrated here in this picture: 
![[Pasted image 20230529190711.png]]
Within each priority queue, packets are transmitted in a First-In, First-Out (FIFO) manner. This means that packets within a priority queue are transmitted in the order they arrived. However, higher-priority queues are always serviced before lower-priority queues, ensuring priority-based transmission. While PQ prioritizes higher-priority packets, it does not neglect lower-priority traffic. Lower-priority packets are still transmitted; they are simply held back until higher-priority packets have been serviced.
![[Pasted image 20230529190825.png]]

Preemption: higher-priority packets can interrupt the transmission of lower-priority packets. This ensures that urgent or critical packets with higher priority are immediately serviced, even if lower-priority packets are currently being transmitted.

Priority Queuing allows for the allocation of bandwidth among different priority queues. Higher-priority queues can be assigned a larger portion of the available bandwidth, ensuring that important packets receive a higher share of network resources.

Priority Queuing is often used to enforce quality of service (QoS) differentiation in networks. It allows for the prioritization of specific traffic classes, such as voice or video streams, to ensure their timely and uninterrupted delivery. By giving higher-priority packets preferential treatment, PQ can meet the QoS requirements of critical applications.

A potential downside of PQ is head-of-line (HOL) blocking. If a higher-priority queue has a continuous stream of packets, it may prevent the transmission of lower-priority packets, causing increased latency or potential starvation for those queues.

Priority Queuing provides a mechanism to give preferential treatment to higher-priority packets, ensuring timely delivery and meeting the specific requirements of critical applications. It is commonly used in scenarios where strict prioritization is necessary, such as Voice over IP (VoIP) or real-time video streaming, where minimizing latency and ensuring uninterrupted transmission are crucial.

#### Round Robin
Round Robin (RR) is a packet scheduling algorithm used in networking to allocate network resources fairly among multiple flows or connections. It aims to provide an equal opportunity for all flows to transmit their packets by cyclically serving each flow in a round-robin fashion.
![[Pasted image 20230529191406.png]]
Round Robin assigns time slots or transmission opportunities to different flows or connections in a cyclic manner. Each flow gets a turn to transmit its packets in a predetermined order. Packets arriving are classified into classes (without priority) upon arrival, these classes are served in a cycle, one packet at a time. Round Robin typically divides time into fixed-length slots or time slices. Each flow is given a time slice during which it can transmit its packets. When a flow's time slice is completed, the next flow in the rotation gets its turn.
![[Pasted image 20230529191551.png]]
The scheduling ensures fairness among flows by providing an equal share of network resources to each flow. It prevents any single flow from dominating the available bandwidth and gives every flow an opportunity to transmit its packets. In Round Robin scheduling, flows are generally served in a non-preemptive manner. Once a flow is given its time slice, it can transmit its packets without interruption until the time slice expires or its allocated packet count is reached.

Round Robin strives to provide an equal amount of service time or bandwidth to each flow. Each flow is allotted a fixed amount of time or a fixed number of packets to transmit before the scheduling cycle repeats.

RR schedules packets based on the order of flows, not based on packet priorities or QoS requirements. All flows are treated equally, regardless of their size, priority, or specific needs. It tries to ensure efficient utilization of network resources by preventing any flow from monopolizing the available bandwidth. It shares the network capacity fairly among multiple flows, promoting balanced traffic distribution. But it may not be suitable for real-time or delay-sensitive applications where strict prioritization or QoS guarantees are required. Since RR treats all flows equally, it may not provide preferential treatment for time-critical traffic.

Round Robin scheduling provides a simple and fair approach to allocate network resources among multiple flows or connections. It prevents any single flow from monopolizing the available bandwidth and promotes equitable sharing. While it may not address prioritization or specific QoS requirements, RR is widely used in various networking environments to achieve balanced traffic distribution.

The issue with Round Robin is that its fair regarding the number of served packets, but not regarding bandwidth sharing among classes. That means that the class with the largest packets also gets the largest share of bandwidth. 

#### Fair Queuing

>Can we achieve perfect bandwidth sharing? *No.*

If we want to achieve close to fair bandwidth sharing, we have ways to almost get a fair policy. The problem with achieving perfect bandwidth sharing is that packets should **NOT** be further split when queued, and the bits cant be split either. We solve this by implementing the Fair Queuing algorithm, which is designed to achieve fair bandwidth sharing among different flows or classes of traffic in a network. It aims to divide the available bandwidth among flows in a manner that closely approximates fairness, similar to how a pipe can be fairly shared when multiple fluids flow through it. fluid analogy to illustrate the concept of fair bandwidth sharing:
![[Pasted image 20230529192558.png]]
- The link is a pipe and the data is a fluid.
- The pipe can be fairly shared
- The classes do not mix with each other when flowing together.

Fair Queuing is a popular scheduling algorithm for achieving fair bandwidth sharing among different flows or traffic classes. It ensures that each flow receives its fair share of the available bandwidth, approximating the concept of fairness in network resource allocation. By considering the individual needs and priorities of flows, Fair Queuing facilitates efficient and equitable transmission of packets in a network.

**Virtual transmission delay of the i-th packet (per class):**
$$d_{i} = \frac{mL_{i}}{R}$$

- m: number of classes
- R: transmission rate
- Li: number of bits in the i-th packet. 

**Virtual departure time (VDT) of the i−th packet (per class)**
$$t_{i} = max(a_{i}, t_{i-1}) + d_{i}$$
- ai: arrival time of the i-th packet
- di: virtual transmission delay of the i-th packet. 

> In the ideal scenario packets should depart at their VDTs

- The packet with the least VDT is served first.
![[Pasted image 20230529193537.png]]
![[Pasted image 20230529193550.png]]

#### Weighted Fair Queuing
Weighted Fair Queuing (WFQ) is an advanced variant of Fair Queuing that enhances the fairness and quality of service (QoS) capabilities of packet scheduling in networking. WFQ assigns different weights to flows or traffic classes, allowing for prioritization and proportional allocation of bandwidth based on their relative importance or QoS requirements.

> The same as fair queuing, but with a different formula for the virtual transmission delay.

$$d_{i} = \frac{L_{i}}{W_{j}R} $$
- Wj: weight for the j−th class
- R: transmission rate
- Li: number of bits in the i−th packet

![[Pasted image 20230529193657.png]]

Weighted Fair Queuing is widely used in network environments where differentiated QoS and fairness in bandwidth sharing are essential. By assigning weights to flows, WFQ ensures that critical traffic receives appropriate resources while still providing fair sharing among different flows. It allows network administrators to prioritize traffic based on their specific needs, achieving an efficient and balanced allocation of bandwidth.


## The Internet Protocol
The Internet Protocol (IP) is a core protocol of the TCP/IP suite, which is the foundation of the modern internet. IP provides the addressing and routing mechanisms that enable the delivery of packets across interconnected networks. It is responsible for the logical addressing and fragmentation/reassembly of data into discrete packets for transmission.

There are two versions of IP in use today, the IPv4 and the IPv6. The IPv6 has been proposed to replace IPv4. 

### IPv4
IPv4 (Internet Protocol version 4) is the fourth version of the Internet Protocol, which has been the predominant protocol used for network communication since its development in the early 1980s. IPv4 is the foundation of the modern internet and provides the addressing scheme and packet structure for data transmission.
IPv4 has been the backbone of internet communication for several decades. While its address space limitations led to the development of IPv6, IPv4 remains widely used and supported across networks worldwide. Understanding IPv4 is essential for comprehending the fundamentals of networking and the internet infrastructure.

- As we see, the Internet Protocol provides node-to-node communication services based on a label called IP addresses. 
- The communication may involve many intermediate nodes.
- Communication as a best effort delivery service, i.e. it does not provide [[Transport Layer#Principles of Reliable Data Transfer|reliable data transfer]].
![[Pasted image 20230530130229.png]]
- even though the IPv4 is still the most prevalent version, IPv6 is increasing in rate of deployment. 
#### IPv4 Datagram Format
As we recall, the internets [[Network Layer]] packets is referred to as a datagram. The syntax and semantics of the IPv4 diagram and its packet bits, plays a central role in the Internet, and is therefore important to study and master.
- Here is the datagram format from [[Computer Networking A Top-Down Approach, Global Edition, 8th Edition (Kurose, James, Ross, Keith) (Z-Library).pdf|Computer Networking]]
![[Pasted image 20230530130216.png]]
- And here is the header format from [[lecture14-handout.pdf|lecture slide]]
![[Pasted image 20230530130757.png]]

- As we see, the ``Version``-field specifies the IP version of the datagram, but note that different versions of IP use diffident datagram formats and the version determines the interpretation of the datagram. 
- The **internet header length** (IHL) specifies the number of 32-bit words in the header, and an IPv4 datagram can contain a variable number of options
	- What does the Internet Header Length(IHL) in an IPv4 datagram specify?:: The number of 32-bit words in the header. 
<!--SR:!2023-06-03,1,228-->
- The **DSCP** stands for Differentiated Services Code Point, and specifies a code used for managing network traffic and providing quality of service(QoS).
	- What does the **DSCP** filed in the IPv4 datagram do?::specifies a code used for managing network traffic and providing quality of service(QoS)
<!--SR:!2023-06-03,1,228-->
- The **ECN** field stands for Explicit Congestion Notification and allows for end-to-end notification of network congestion without dropping packets.
	- What does the ECN field do in the IPv4 datagram?::allows for end-to-end notification of network congestion without dropping packets.
<!--SR:!2023-06-03,1,228-->
- The **Total length** / **Datagram Length** field contains the total length of the IP datagram(header plus data) in bytes
	- What does the Total Length/Datagram Length Field contain in the IPv4 datagram?:: the total length of the IP datagram(header plus data) in bytes
<!--SR:!2023-06-04,2,248-->
- The **Time To Live field (TTL)** contains the expiration time for the packet, to avoid routing loops.
	- TTL is decrease by 1 when the datagram is processed by a router.
	- If TTL is 0, the router drops the datagram
		- In the IPv4 datagram, **Time To Live field (TTL)** contains?::the expiration time for the packet, to avoid routing loops.
<!--SR:!2023-06-04,2,248-->
		- What happens if the TTL in IPv4 is 0?:: The router drops the datagram
<!--SR:!2023-06-03,1,228-->
		- What happens when TTL is processed by a router? :: TTL is decreased by 1.
<!--SR:!2023-06-04,2,248-->
- The **Protocol** field specifies the [[Transport Layer]] protocol to which the data portion of the IP datagram should be passed. 
	- The Protocol field in IPv4 specifies what layer protocol to handle the data? :: It specifies where the data portion should be passed in the Transport Layer protocol.
<!--SR:!2023-06-03,1,228-->
- The **Header Checksum** field is used for error-checking of the header. Errors in the data filed must be handled by the encapsulated protocol. 
	- The Header Checksum plays a crucial role in ensuring the integrity of the IP header, as any errors or corruption in the header could lead to misrouting or delivery issues
	- Header Checksum does not provide end-to-end error detection for the entire packe
		- What does the Header Checksum filed in IPv4 datagram check for?:: It error-checks the IP header itself.
<!--SR:!2023-06-03,1,228-->
	- Errors in the payload or data field are handled by the encapsulated transport or application layer protocols.
- The **Identification**, **Flags**, and **Fragment Offset** fields are used for IP fragmentation
	- Which fields in the IPv4 Datagram are used for IP fragmentation?::Identification, Flags, Fragment Offset. 
<!--SR:!2023-06-03,1,228-->

##### MTU and Fragmentation

The **Maximum Transmission** Unit (MTU) represents the maximum size of the payload that can be transmitted in a single IP packet without fragmentation. It's determined by the underlying network technology or [[Link Layer]] protocol used for transmission.
- When an IP packet is being transmitted over a network, it must adhere to the MTU of the network interface
- If the size of the packet, including the IP header and payload, exceeds the MTU, the packet needs to be fragmented into smaller units to fit within the MTU constraints.
	- Fragmentation involves breaking the packet into smaller fragments at the sender, which can then be reassembled at the receiver.
- The process of fragmentation and reassembly adds overhead to the network communication, as it requires additional processing and increases the likelihood of retransmission in case of any lost or damaged fragments. Therefore, it is generally desirable to avoid fragmentation whenever possible.

Fragmentation refers to the process of breaking larger packets into smaller fragments to fit within the Maximum Transmission Unit (MTU) constraints of a network. It occurs when the size of the original packet, including the IP header and payload, exceeds the MTU of a network link along the path of transmission. The router divides the packet into fragments having the following changes:
- The datagram length is the fragment size
- The More Fragments flag is set for all fragments except the last one, which is set to 0.
- The Fragmentation Offset is set, based on the offset of the fragment in the original data payload.
- The Header checksum field is recomputed.
![[Pasted image 20230530134232.png]]
Example of fragmentation:
For an MTU of 1500 bytes and a header size of 20 bytes, the fragment offsets are multiples of:
$$\frac{1500-20}{8} = 185$$
These multiples are 0, 185, 370, 555,...
In this example we see that:
- To find the size of the data payload that can be included in each fragment, we need to subtract the IP header size from the MTU: Data Payload Size = MTU - IP Header Size
	- In this case, it is 1500 - 20 = 1480 bytes.
- The Fragmentation Offset field in the IP header indicates the position of each fragment within the original data payload. The offset is measured in units of 8 bytes.
	- To determine the number of fragments required, we divide the Data Payload Size by 8:
	- Number of Fragments = Data Payload Size / 8
	- In this case, it is 1480 / 8 = 185 fragments.
- To calculate the fragment offsets, we multiply the fragment index (starting from 0) by the Data Payload Size divided by 8: Fragment Offset = Fragment Index * (Data Payload Size / 8). For the given example, the fragment offsets are multiples of 185:
	- Fragment 0: 0 * 185 = 0
	- Fragment 1: 1 * 185 = 185
	- Fragment 2: 2 * 185 = 370
	- Fragment 3: 3 * 185 = 555
- The division by 8 is performed to convert the offset measurement from bytes to units of 8 bytes, as specified by the Fragmentation Offset field in the IP header. This division ensures that the fragment offsets align with the appropriate position in the original data payload.
- By dividing the Data Payload Size by 8, the resulting multiples of 185 indicate the position of each fragment within the original packet, allowing the receiving device or subsequent routers to correctly reassemble the fragments.
- Note that this calculation is specific to the given example and assumes a particular MTU and header size. In practice, different network configurations and MTU sizes may result in different calculations for fragment offsets.

Fragment detection at the receiver refers to the process of identifying and handling the incoming fragments of a fragmented IP packet to reconstruct the original packet. It involves examining the IP header fields and using the Fragment Offset and Identification fields to determine the correct order and reassemble the fragments. If at one of the following conditions is true, the conditions for fragment detection at the receiver are as follows:
- The MF flag is set.
	- The MF flag is a flag in the IP header that indicates whether there are more fragments to follow in the original fragmented packet. If the MF flag is set to 1, it means that there are additional fragments to be received for the complete reassembly of the original packet. The receiver detects that the received packet is a fragment if the MF flag is set.
- The field Fragmentation is nonzero
	- The Fragmentation Offset field in the IP header indicates the position of the received fragment within the original data payload. If the Fragmentation Offset field has a nonzero value, it indicates that the received packet is a fragment and not a standalone packet. The nonzero value specifies the position of the fragment within the original packet, measured in units of 8 bytes.
By examining these conditions, the receiver can determine if the received packet is a fragment and proceed with fragment reassembly or if it is a complete standalone packet that does not require further processing or reassembly.
If at least one of the mentioned conditions is true, it suggests that the received packet is a fragment, and the receiver should store it temporarily for reassembly with other fragments. On the other hand, if both conditions are false, it implies that the received packet is a complete standalone packet that does not require further fragment reassembly.
Fragment detection at the receiver is an essential step in handling fragmented IP packets and ensures the correct reconstruction of the original packet from received fragments. It allows the receiver to process fragmented packets correctly and deliver the data payload to the appropriate upper-layer protocols or applications.

- Questions:
	- What does it mean when the field fragmentation is nonzero?:: The Fragmentation Offset field in the IP header indicates the position of the received fragment within the original data payload. If the Fragmentation Offset field has a nonzero value, it indicates that the received packet is a fragment and not a standalone packet.
<!--SR:!2023-06-25,3,208-->
	- In fragmentation, what happens if the receiver registers that the MF flag is set?:: It indicates that there are more fragments to follow in the original fragmented packet. 
<!--SR:!2023-06-03,1,228-->
	- In MF flag, what does it mean if its value is set to 1?:: it means that there are additional fragments to be received for the complete reassembly of the original packet
<!--SR:!2023-06-04,2,248-->
	- What does the Fragmentation Offset Field in the IP header indicate?::indicates the position of each fragment within the original data payload. The offset is measured in units of 8 bytes.
<!--SR:!2023-06-03,1,228-->
	- 

Reassembly:
- The receiver identifies fragments using the foreign and local address, the protocol ID, and the identification field.
-  The receiver reassembles the data from fragments with the same ID using both the fragment offset and the more fragments flag.

#### IPv4 Addressing

>IPv4 addresses are 32 bits long (equivalently, 4 bytes)

IPv4 addressing is a fundamental aspect of the Internet Protocol version 4 (IPv4) used to identify and locate devices on a network. IPv4 addresses are 32-bit binary numbers, typically represented in a human-readable format known as dotted-decimal notation. They consist of four groups of decimal numbers separated by dots, with each group representing 8 bits or one octet.

Dotted-decimal notation is used to represent the address, where each byte of the address is written in its decimal form. The bytes are separated by a period. ![[Pasted image 20230530142708.png]]
and in a network it would look something like this:
![[Pasted image 20230530142806.png]]
- How is an address in IPv4 formated? :: dotted-decimal notation. 
<!--SR:!2023-06-03,1,228-->
- 
#### Subnet

>Subnets make networks more efficient. Through subnetting, network traffic can travel a shorter distance without passing through unnecessary routers to reach its destination.

Subnetting is the process of dividing a network into smaller sub-networks or subnets. It allows network administrators to allocate IP addresses more efficiently and manage network resources effectively. Its a logical subdivision of an IP network, where computers that belong to a subnet are addressed with an identical most-significant bit-group in their IP addresses.

In IPv4 addressing, an IP address is logically divided into two parts: the routing prefix and the host identifier. This division allows for efficient routing of IP packets within a network.
- Routing Prefix:
	- The routing prefix, also known as the network prefix or network address, represents the network portion of the IP address. It identifies the specific network to which a device belongs. The size of the routing prefix is determined by the subnet mask applied to the IP address.
	- The routing prefix specifies the network address and indicates which bits in the IP address are used to identify the network. It helps routers determine the appropriate network to forward packets and facilitates efficient routing within the network infrastructure.
- Host Identifier:
	- The host identifier represents the unique identifier assigned to each individual device within a network. It identifies a specific host or device on the network. The host identifier portion of the IP address identifies a particular device within the identified network.
	- The size of the host identifier is determined by the remaining bits in the IP address after the routing prefix. The host identifier allows for differentiation among individual devices within the same network and enables communication between them.
By dividing the IP address into the routing prefix and the host identifier, it becomes possible to efficiently route IP packets across networks. Routers use the routing prefix to make forwarding decisions, while the host identifier helps identify specific devices within a network.

For example, consider the IP address 192.168.1.100 with a subnet mask of 255.255.255.0 (/24). In this case:
- The routing prefix is 192.168.1.0, which represents the network portion.
- The host identifier is 0.0.0.100, which identifies the specific device within the network.
This logical division allows routers to determine the destination network based on the routing prefix and route packets accordingly. It also enables devices within the network to communicate with each other using their unique host identifiers.


##### **IP forwarding** 
plays a crucial role in routing packets between different subnets within an IP network. It involves the process of determining the appropriate next-hop destination for an incoming packet based on its destination IP address.
![[Pasted image 20230530144733.png]]
- Have a default, if possible. IP forwarding often involves having a default route. A default route acts as a fallback option for forwarding packets when a more specific match for the destination IP address is not found in the routing table.
- Be as specific as possible. IP forwarding aims to be as specific as possible when routing packets. It considers the subnet information and the hierarchy of bits in the IP addresses to determine the most appropriate route for a given packet.
	- When forwarding an IP packet, the router looks for the longest prefix match in its routing table. The longest prefix match is the entry in the routing table with the most significant bits that match the destination IP address of the packet. This ensures that the router selects the most specific route available.
- Respect the hierarchy of bits from left to right. The concept that IP forwarding decisions should be made based on the most significant bits of the destination IP address. This principle is essential in determining the routing path for IP packets.
	- By respecting the hierarchy of bits from left to right, the router prioritizes the more significant bits of the IP address during the forwarding decision-making process. This means that the router first looks at the most significant bits (leftmost bits) of the destination IP address and matches them against the prefixes in the routing table.
	- respecting the hierarchy of bits from left to right ensures that IP forwarding follows a logical and efficient path, leading to proper packet delivery and optimal network performance.

##### Classless Inter-Domain Routing (CIDR) notation
The routing prefix is expressed as the first address of a network, followed by / and ending with the bit-length of the prefix. *Classless Inter-Domain Routing* (CIDR) notation is a method of representing IP addresses and their associated subnet masks in a concise and flexible manner. It provides a more efficient and flexible way of allocating IP addresses and subnetting networks compared to the original class-based addressing scheme used in IPv4.

- **Classful vs. Classless Addressing**: 
	- In classful addressing, IP addresses were divided into fixed classes (A, B, and C) based on the range of network addresses. However, this led to inefficient address allocation, as it did not allow for flexibility in assigning different-sized networks. CIDR was introduced to overcome the limitations of classful addressing.
- **IP Address and Prefix Length**: 
	- CIDR notation represents an IP address and its associated subnet mask using a combination of the IP address itself and a prefix length. The prefix length indicates the number of network bits (or the length of the network prefix) in the IP address. It determines the size of the network and the number of available host addresses.
- **Format**: 
	- CIDR notation combines the IP address and prefix length using a forward slash (/) separator. The IP address is followed by the prefix length, indicating the number of network bits. For example:
	    - 192.168.0.0/24: The IP address is 192.168.0.0, and the prefix length is 24 bits, representing a subnet with a 24-bit network prefix (255.255.255.0).
	    - 10.0.0.0/16: The IP address is 10.0.0.0, and the prefix length is 16 bits, representing a subnet with a 16-bit network prefix (255.255.0.0).
- **Variable-Length Subnet Masking**: 
	- CIDR allows for variable-length subnet masks (VLSM), which means that networks can be divided into subnets of different sizes depending on their specific needs. This flexibility allows for efficient utilization of IP addresses and optimal allocation of address space.
- **Aggregation and Routing Efficiency**: 
	- CIDR enables route aggregation, which involves combining multiple smaller networks into a larger network prefix. Aggregating networks reduces the size of routing tables, improves routing efficiency, and minimizes the amount of routing information exchanged between routers.

CIDR notation revolutionized IP addressing and subnetting by providing a more flexible and efficient way to allocate IP addresses and subnet networks. It allows for variable-length subnet masks, route aggregation, and more precise representation of network prefixes. CIDR notation is widely used in modern IP networks, including the Internet, to manage IP address space effectively.

#important
##### Subnet mask
A subnet mask is a bitmask used in IP networking to determine the network portion of an IP address. It is applied to an IP address using a bitwise AND operation to extract the routing prefix or network identifier.
- Bitmask that when applied by a bitwise AND operation to any IP address in the network, yields the routing prefix.
	- The subnet mask consists of a sequence of contiguous 1s followed by a sequence of contiguous 0s. The length of the sequence of 1s represents the number of network bits in the subnet mask, and the length of the sequence of 0s represents the number of host bits.
- Subnet masks are also expressed in dotted-decimal notation.
	- Subnet masks are typically expressed in dotted-decimal notation, similar to IP addresses. In this notation, each octet of the subnet mask is represented by its decimal value, separated by dots. For example, 255.255.255.0 represents a subnet mask with 24 bits of network and 8 bits of host.
- Network and Host Portions:
	- By applying the subnet mask to an IP address, the network portion of the address can be obtained. The network portion represents the identifier for the specific network to which the IP address belongs. The host portion identifies the individual device or host within the network.
- Determining Network and Host:
	- To determine the network address from an IP address, the subnet mask is applied using a bitwise AND operation. Each corresponding bit in the IP address and subnet mask is compared, and the result is 1 if both bits are 1; otherwise, it is 0. The resulting value represents the network portion of the IP address.
	- For example, if the IP address is 192.168.0.100 and the subnet mask is 255.255.255.0, the network portion of the IP address is obtained by performing the bitwise AND operation:
		- IP address: 11000000.10101000.00000000.01100100
		- Subnet mask: 11111111.11111111.11111111.00000000
		- Network: 11000000.10101000.00000000.00000000 (192.168.0.0)
The subnet mask is a crucial component in IP networking as it determines the network and host portions of an IP address. It helps routers and devices identify the appropriate network for routing and communication purposes. Subnet masks are essential for subnetting, network design, and efficient utilization of IP address space.

More subnet mask examples:
![[Pasted image 20230530145754.png]]
![[Pasted image 20230530145911.png]]

Benefits of subnetting:
- Efficient allocation of the address space.
- Efficient routing.
- Advantageous for network management.
- improved network performance
- Enhanced Network Security
- Flexibility and Scalability
![[Pasted image 20230530150419.png]]

[Subnet Calculator](https://www.calculator.net/ip-subnet-calculator.htm)

##### Subnet Exam Question:
Consider a router that interconnects three subnets: Subnet 1, Subnet 2, and Subnet 3. Suppose all of the interfaces in each of these three subnets are required to have the prefix 192.168.5.0/24. Also suppose that Subnet 1 is required to support up to 14 interfaces, Subnet 2 is to support up to 30 interfaces, and Subnet 3 is to support up to 62 interfaces. Provide three network addresses (of the form a.b.c.d/x) that satisfy these constraints and explain how you obtained them.
![[Pasted image 20230530150645.png]]
The following network addresses fulfill the constraints:
- Subset 1: 192.168.5.0/28.
- Subset 2: 192.168.5.32/27.
- Subset 3: 192.168.5.64/26.


#### Global address allocation
Global address allocation refers to the process of assigning and managing unique IP addresses for devices connected to the global Internet. It involves the distribution of IP addresses on a worldwide scale to ensure that each device has a globally unique identifier for communication purposes.
- The IP address space is managed globally by the Internet Assigned Numbers Authority (IANA).
- IANA has typically allocated address space in the size of /8 prefix blocks for IPv4.
- The top-level exhaustion of IPv4 addresses occurred on 31.01.2011.

### DHCP
The Dynamic Host Configuration Protocol (DHCP) is a network protocol used to automatically assign IP addresses and other network configuration parameters to devices within a network. It simplifies the process of network configuration by providing a centralized mechanism for dynamic IP address allocation.
- Allows a host to obtain an IP address automatically.
- Gives access to the subnet mask, the address of the first-hop router and the address of local DNS server.
- Runs over UDP.
- DHCP is a network management protocol
![[Pasted image 20230530151411.png]]

--- 
From the Microsofts official page:
Dynamic Host Configuration Protocol (DHCP) is a client/server protocol that automatically provides an Internet Protocol (IP) host with its IP address and other related configuration information such as the subnet mask and default gateway. RFCs 2131 and 2132 define DHCP as an Internet Engineering Task Force (IETF) standard based on Bootstrap Protocol (BOOTP), a protocol with which DHCP shares many implementation details. DHCP allows hosts to obtain required TCP/IP configuration information from a DHCP server.

Every device on a TCP/IP-based network must have a unique unicast IP address to access the network and its resources. Without DHCP, IP addresses for new computers or computers that are moved from one subnet to another must be configured manually; IP addresses for computers that are removed from the network must be manually reclaimed.

With DHCP, this entire process is automated and managed centrally. The DHCP server maintains a pool of IP addresses and leases an address to any DHCP-enabled client when it starts up on the network. Because the IP addresses are dynamic (leased) rather than static (permanently assigned), addresses no longer in use are automatically returned to the pool for reallocation.

The network administrator establishes DHCP servers that maintain TCP/IP configuration information and provide address configuration to DHCP-enabled clients in the form of a lease offer. The DHCP server stores the configuration information in a database that includes:
- Valid TCP/IP configuration parameters for all clients on the network.
- Valid IP addresses, maintained in a pool for assignment to clients, as well as excluded addresses.
- Reserved IP addresses associated with particular DHCP clients. This allows consistent assignment of a single IP address to a single DHCP client.
- The lease duration, or the length of time for which the IP address can be used before a lease renewal is required.

A DHCP-enabled client, upon accepting a lease offer, receives:
- A valid IP address for the subnet to which it is connecting.
- Requested DHCP options, which are additional parameters that a DHCP server is configured to assign to clients. Some examples of DHCP options are Router (default gateway), DNS Servers, and DNS Domain Name.

DHCP provides the following benefits:
- **Reliable IP address configuration**. DHCP minimizes configuration errors caused by manual IP address configuration, such as typographical errors, or address conflicts caused by the assignment of an IP address to more than one computer at the same time.
- **Reduced network administration**. DHCP includes the following features to reduce network administration:
    - Centralized and automated TCP/IP configuration.
    - The ability to define TCP/IP configurations from a central location.
    - The ability to assign a full range of additional TCP/IP configuration values by means of DHCP options.
    - The efficient handling of IP address changes for clients that must be updated frequently, such as those for portable devices that move to different locations on a wireless network.
    - The forwarding of initial DHCP messages by using a DHCP relay agent, which eliminates the need for a DHCP server on every subnet.
---

- Flashcard Questions:
	- What is the purpose of DHCP (Dynamic Host Configuration Protocol)?:: DHCP automates the process of assigning IP addresses and network configuration parameters to devices on a network.
<!--SR:!2023-07-19,27,248-->
	- What is the role of the subnet mask in IP networking?::The subnet mask is used to determine the network portion of an IP address and separate it from the host portion.
<!--SR:!2023-06-03,1,228-->
	- What is the significance of the longest prefix match in IP forwarding?::The longest prefix match is used to determine the most specific match for forwarding a packet based on the network prefix in the routing table
<!--SR:!2023-06-03,1,228-->
	- How does fragmentation work in IP networking?::Fragmentation is the process of dividing IP packets into smaller fragments to fit within the Maximum Transmission Unit (MTU) of a network, allowing them to be transmitted across networks with different link capacities.
<!--SR:!2023-06-03,1,228-->
	- What is CIDR notation in IP addressing?:: CIDR notation is a method of representing IP addresses and their associated subnet masks using a combination of the IP address and a prefix length.
<!--SR:!2023-06-03,1,228-->
	- What is the difference between routing and forwarding?:: Routing refers to the process of determining the path for data packets to travel from the source to the destination network, while forwarding is the actual act of sending the packets along the determined path.
<!--SR:!2023-06-03,1,228-->
	- What is the function of a router in computer networking?:: Routers are responsible for forwarding data packets between different networks or subnets.
<!--SR:!2023-06-03,1,228-->
	- What is the purpose of the ARP (Address Resolution Protocol) in computer networking?::ARP is used to map an IP address to a MAC address on a local network.
<!--SR:!2023-06-03,1,228-->
	- What are the four steps in the DHCP process?:: The four steps are Discover, Offer, Request, and Acknowledge (DORA).
<!--SR:!2023-06-03,1,228-->
	- What is the lease time in DHCP?:: The lease time is the duration for which a device holds an assigned IP address before it needs to be renewed.
<!--SR:!2023-06-03,1,228-->
	- How does DHCP help with IP address management?:: DHCP simplifies IP address management by automating the assignment and tracking of IP addresses, reducing the chances of IP address conflicts.
<!--SR:!2023-06-04,2,248-->
	- Can DHCP assign other network configuration parameters besides IP addresses?:: Yes, DHCP can assign various parameters like subnet masks, default gateways, DNS server addresses, and more.
<!--SR:!2023-06-03,1,228-->
	- What is the size of an IPv4 address in bits?:: An IPv4 address is 32 bits long.
<!--SR:!2023-06-05,3,268-->
	- How is an IPv4 address represented?:: An IPv4 address is typically represented in dotted-decimal notation, such as 192.168.0.1.
<!--SR:!2023-06-03,1,228-->
	- What is the purpose of the subnet mask in IPv4?:: The subnet mask is used to separate the network portion from the host portion of an IPv4 address.
<!--SR:!2023-06-03,1,228-->
	- How many unique IPv4 addresses are possible?:: IPv4 allows for approximately 4.3 billion unique addresses.
<!--SR:!2023-06-03,1,228-->
	- What is the structure of an IPv4 datagram?:: An IPv4 datagram consists of a header followed by a data payload.
<!--SR:!2023-06-03,1,228-->
	- What are some common fields in the IPv4 header?:: Common fields include source and destination IP addresses, TTL (Time-to-Live), protocol field, and header checksum.
<!--SR:!2023-06-03,1,228-->
	- What is the purpose of TTL in the IPv4 header?:: TTL (Time-to-Live) specifies the maximum number of hops (routers) a packet can traverse before being discarded.
<!--SR:!2023-06-03,1,228-->
	- What is the maximum size of an IPv4 datagram?:: The maximum size of an IPv4 datagram, including header and data payload, is 65,535 bytes.
<!--SR:!2023-06-03,1,228-->
	- What is the purpose of NAT (Network Address Translation) in IPv4?:: NAT allows multiple devices within a private network to share a single public IPv4 address for Internet connectivity.
<!--SR:!2023-08-25,64,248-->
---

### Network Address Translation
Network Address Translation (NAT) is a technique used in computer networking to enable the sharing of a single public IP address among multiple devices within a private network. NAT allows devices within the private network to communicate with devices on the Internet using a translated IP address.
- Method for mapping an IP address space into another one by modifying the IP header of packets
- IP masquerading: Technique that hides an entire IP address space behind a single IP address. Port numbers and Header checksums will be altered too
![[Pasted image 20230530154025.png]]
Why NAT?
- The ISP does not need to allocate addresses for each device in a private networks.
- Addresses can change locally without notifying the ISP.
- Private addresses remain the same after changing the ISP.
- Devices inside a LAN are not explicitly visible to the outside world.

IP masquerading: example:
![[Pasted image 20230530154146.png]]

#### NAT traversal
> Can peers behind different NATs communicate with each other? Port forwarding or some NAT traversal technique must be used!

NAT traversal refers to techniques and mechanisms used to establish and maintain network connections between devices located behind Network Address Translation (NAT) devices. NAT traversal enables communication between devices on private networks that are protected by NAT and devices on public networks, such as the Internet

##### Port Forwarding:
- A port number is set aside, using NAT, for the exclusive use of a specific host.
Port forwarding, also known as port mapping, is a common NAT traversal technique. It involves configuring the NAT device to forward incoming network traffic on a specific port to a device on the internal network. This allows external devices to access services hosted on devices within the private network.

##### NAT Hole Punching:
- UDP hole punching: third-party hosts are used to exchange ports needed for direct communications between the hosts.
- TCP hole punching: one solution is to use port preservation.
	- What is NAT hole punching?:: NAT hole punching is a technique that exploits the behavior of NAT devices to create temporary openings, or "holes," in their network address translations to enable direct communication between devices behind different NATs.
<!--SR:!2023-06-03,1,228-->
NAT hole punching is a technique used to establish direct communication between two devices located behind different NAT devices. It involves exploiting the behavior of NAT devices to create temporary openings, or "holes," in their network address translations. This allows packets to traverse NAT and establish direct communication between devices

---

### IPv6
IPv6, or Internet Protocol version 6, is the most recent version of the Internet Protocol that serves as the foundation for communication on the internet. It was developed to address the limitations of its predecessor, IPv4, which has been widely used since the early days of the internet.

>A prime motivation for IPv6 was the exhaustion of the IPv4 address space. 

Expanded addressing capabilities of IPv6 include unicast addressing, anycast addressing, and multicast addressing. Let's explore each of these addressing types:
- **Unicast addressing** is the most common type of IPv6 addressing and is used for one-to-one communication between a source and a specific destination. Each device in an IPv6 network is assigned a unique unicast address that identifies it on the network. Unicast addresses are typically used for direct communication between individual devices.
	- The address identifies a single interface.
	- IP delivers packets sent to a unicast address to that specific interface.
- **Anycast addressing** is a mechanism that allows multiple devices to share the same IPv6 address. With anycast addressing, a packet sent to an anycast address is delivered to the nearest device or service that announces that address. Anycast is used primarily for load balancing, fault tolerance, and service optimization. It enables efficient routing to the nearest available server or service based on network topology.
	- The address is the same for several interfaces.
	- It looks like the unicast address.
	- A packet sent to an anycast address is delivered to just one of the interfaces (typically in the nearest host).
- **Multicast addressing** is used for one-to-many or many-to-many communication. It allows a sender to send a single packet to multiple recipients who are interested in receiving the data. Multicast addresses are used to identify groups of devices that want to receive multicast traffic. Routers and network devices can efficiently distribute the multicast packets to the intended recipients within the multicast group.
	- The address is the same for several interfaces.
	- The address is different from the unicast address.
	- A packet that is sent to a multicast address is delivered to all interfaces that have joined a multicast group.
These expanded addressing capabilities in IPv6 provide more flexibility and functionality compared to IPv4. Unicast addressing enables direct communication between individual devices, anycast addressing facilitates efficient routing to the nearest service or server, and multicast addressing allows for efficient distribution of data to multiple recipients interested in receiving multicast traffic. These addressing types contribute to the scalability and efficiency of IPv6 networks.

***Note***: 
- IPv6 does not implement broadcast addressing
- The address of the all-nodes link-local multicast group is ff02::1
<!--SR:!2023-06-03,1,228-->

#### Header Format
The IPv6 datagram, or packet, has a specific header format that carries the necessary information for the routing and delivery of IPv6 packets.
![[Pasted image 20230530160236.png]]
- The **Version** field (4 bits) specifies the IP version od the datagram, and determines the interpretation of the remainder of the datagram.
	- ***Note***: Different versions of IP use different datagram formats
- The **Traffic class** field is the six most-significant bits for the differentiated services field (DS filed) and the remaining two bit are used for ECN
- The Flow label field is used to identify a flow of datagrams.
	- Provides special handling for a specific flow of packets, such as real-time multimedia or a particular application.
- The Payload Length indicates the total lengt of data in the IPv6 payload, and does so in octets. 
- The Next header field specifies the type of next header:
	- Usually specifies the [[Transport Layer]] protocol used by packets payload
	- Specifies the extension headers when they are used
- The Hop limit field is similar to the TTL field in IPv4, it determines the maximum numbers of routers (hops) that a package can pass through before being discarded. 
	- Its value is decremented by one by each router that forwards the datagram.
	- If the hop limit count reaches zero, the datagram is discarded.


#### IPv4 vs IPv6
There are some differences in how the two versions of IP performs certain actions. We can see in this picture that the structure of the datagram has been changed in version 6.
![[Pasted image 20230530161241.png]]
There are some key differences between between the two versions:
- Address Space:
	- Pv4 uses 32-bit addresses, allowing for approximately 4.3 billion unique addresses. However, due to increasing demand, IPv4 addresses have become scarce. 
	- On the other hand, IPv6 uses 128-bit addresses, providing an enormously larger address space of approximately 3.4 × 10^38 unique addresses, ensuring the availability of addresses for future growth.
- Address Format: 
	- IPv4 addresses are expressed in dotted-decimal notation, such as 192.168.0.1. 
	- IPv6 addresses are represented in hexadecimal format, separated by colons, such as 2001:0db8:85a3:0000:0000:8a2e:0370:7334.
- Header Size:
	- The IPv4 header is 20 bytes in size, while the IPv6 header is 40 bytes.
	- However, IPv6 has a more efficient and simplified header structure, with optional extension headers that provide additional functionalities when needed.
- Fragmentation:
	- IPv4 routers can fragment packets if their size exceeds the maximum transmission unit (MTU) along the path.
	- IPv6, on the other hand, mandates that fragmentation is the responsibility of the source host, which helps reduce processing overhead on routers.
		- ***IPv6 only allows for fragmentation at hosts!***
- Header checksum: 
	- IPv6 does not have error checking.
- Options: 
	- The IPv6 header does not have a field for options.
	- Instead, options can be passed after the header.
- Security:
	- While IPv4 has limited built-in security features, IPv6 includes native support for IPsec (IP security), providing encryption, authentication, and integrity for IP packets.
- Quality of Service (QoS):
	- IPv6 includes a Traffic Class field that can be used for packet prioritization and quality of service. 
	- It replaces the IPv4 Type of Service (ToS) field and allows for more granular control over packet handling and QoS features.

#### IPv6 Tunneling
IPv6 tunneling is a technique used to enable communication between IPv6 networks over an IPv4 infrastructure. It allows IPv6 packets to be encapsulated within IPv4 packets, facilitating the transmission of IPv6 traffic over an IPv4 network. This was implemented to help up answer questions like "How will the public Internet transition to IPv6" and dealing with routers that are not capable of handling IPv6 datagrams.

IPv6-in-IPv4 tunneling or  also called IPv6 tunneling, is where a node sends the entire IPv6 datagram as the payload of an IPv4 datagram, to carry them across IPv4 networks. By doing this it helps IPv6 traffic to traverse areas of the network that do not yet support native IPv6 connectivity. 
When an IPv6 node encapsulates the entire IPv6 datagram as the payload of an IPv4 datagram, the IPv4 header becomes the outer header, while the original IPv6 datagram is embedded withing it. When it reaches its destination, it is decapsulated to retrive the original IPv6 Datagram. Here is an illustration of this:
![[Pasted image 20230530162933.png]]

### Generalized forwarding and SDN
Generalized forwarding, in the context of computer networking, refers to the concept of flexible and programmable forwarding behavior in network devices. It involves the ability to define and implement forwarding decisions based on various criteria beyond traditional destination-based routing, such as specific application requirements, quality of service (QoS) policies, traffic engineering, and security considerations. Generalized forwarding allows for more intelligent and adaptable routing within a network, enabling greater control and optimization of traffic flows.

#### Forwarding
>Transit of packets from one network interface to another.

When a packet arrives at a network device, such as a router or switch, it undergoes a forwarding process. The device examines the destination IP address in the packet header to determine the next hop or interface towards which the packet should be forwarded. This decision is typically based on the device's routing table(forwarding table), which contains information about network topology, available paths, and associated metrics.
The forwarding process involves looking up the destination address in the routing table to determine the appropriate output interface for the packet. The packet is then encapsulated in a new frame or packet, depending on the network technology, and transmitted out of the corresponding interface towards the next hop or destination.
Efficient and accurate forwarding is crucial for network performance and connectivity. It involves considerations such as routing protocols, route optimization, load balancing, Quality of Service (QoS) policies, and security policies. Forwarding mechanisms can be static or dynamic, with dynamic forwarding relying on routing protocols to exchange network information and determine optimal paths in real-time.

#### Forwarding table
A data structure that maps values, such as addresses, from an incoming packet's header to the appropriate outgoing interface for forwarding the packet.
- It maps values (addresses) of an arriving packet’s header to the outgoing interface.

A forwarding table is typically maintained within network devices, such as routers or switches, and it is used to make forwarding decisions based on the destination address of the packet. The table contains information about the network topology, available paths, and associated metrics, allowing the device to determine the best interface or next hop for transmitting the packet towards its destination.

The forwarding table, or routing table, is populated with routes learned through various routing protocols or configured manually by network administrators. These routes provide the necessary information to guide the forwarding process and ensure that packets are delivered to the correct destination.

#### Characteristics of (basic) forwarding
Characteristics of basic forwarding refer to the fundamental principles and features of the forwarding process in computer networking.
- ***Destination and Label-Based (Address-Based) Forwarding***:
	- Basic forwarding can be destination-based, where the forwarding decision is solely determined by the destination address of the packet. However, in certain cases, forwarding decisions can also be influenced by additional factors such as labels associated with the packet. Label-based forwarding involves using labels or tags attached to packets to determine their forwarding path. This approach is commonly used in technologies like MPLS (Multiprotocol Label Switching) where labels are used to guide packet forwarding.
- ***Layer-Specific Forwarding***:
	- Basic forwarding can operate at different layers of the networking protocol stack. Each layer has its own forwarding mechanisms and considerations. For example, at the network layer (Layer 3), IP forwarding is performed based on the IP destination address. At the data link layer (Layer 2), forwarding decisions are made based on MAC addresses in Ethernet frames. Layer-specific forwarding ensures that packets are forwarded according to the requirements and protocols of the specific layer in which the forwarding operation is performed.
These two points highlight additional aspects of basic forwarding. The first point emphasizes that forwarding decisions can consider factors beyond the destination address, such as labels, to determine the appropriate path for packet transit. The second point recognizes that forwarding can vary across different layers of the networking stack, with each layer employing its own forwarding mechanisms and criteria.

#### Characteristics of generalized forwarding
Characteristics of generalized forwarding refer to the key attributes and capabilities of forwarding mechanisms that go beyond basic forwarding.

- Match-Plus-Action Paradigm:
	- Generalized forwarding is better described as a match-plus-action paradigm. In addition to the transit of packets from one interface to another, generalized forwarding supports a wide range of possible actions. These actions can include traffic shaping, traffic prioritization, traffic filtering, quality of service (QoS) enforcement, encryption, and other advanced processing tasks beyond simple packet forwarding
- Comprehensive Pattern Matching:
	- Generalized forwarding involves pattern matching that considers various fields in the packet beyond just the source and destination addresses. It takes into account multiple packet attributes, such as source and destination ports, protocol types, packet sizes, VLAN tags, QoS markings, and other relevant fields. This comprehensive pattern matching allows for more granular forwarding decisions based on specific packet characteristics.
- Statistical Considerations:
	- Generalized forwarding can also take into account statistical information in addition to the packet attributes. It may consider factors such as traffic load, bandwidth utilization, historical data, or other metrics to make more informed forwarding decisions. Statistical analysis helps optimize network performance, load balancing, and resource utilization.
- Not Layer-Specific:
	- Unlike basic forwarding, generalized forwarding is not limited to a specific layer of the networking stack. It operates across multiple layers and can consider packet attributes and statistics from various layers, including the network, transport, and application layers. Generalized forwarding takes a holistic approach to packet processing and forwarding, considering a broader range of factors beyond layer-specific criteria.

#### Match-plus-action (flow) table
The match-plus-action table, also known as the flow table, is a fundamental component of generalized forwarding in modern networking architectures. It serves as a mapping mechanism that associates patterns identified in an arriving packet with the corresponding action to be performed on that packet. This table allows for more flexible and granular control over packet processing and forwarding.
- It maps patterns found in an arriving packet to the corresponding action.
- typically resides within a network device, such as a switch or router
	- consists of a set of rules or entries, each specifying a pattern to match against the incoming packet's attributes and the action to be taken if a match is found.
- 
The actions defined in the flow table can include a range of operations, such as forwarding the packet to a specific interface, modifying packet headers or fields, applying QoS policies, redirecting the packet to a different device or network function, dropping the packet, or sending it to a specific processing module for further analysis.
By using a match-plus-action table, network administrators can define and implement customized forwarding behaviors based on specific requirements and policies. It provides a powerful mechanism for fine-grained control over packet forwarding and processing, enabling networks to efficiently handle diverse traffic patterns and meet the evolving needs of applications and services.


#### Characteristics of match-plus-action tables
A match-plus-action (flow) table is more complex than (basic) forwarding tables, it can be nested, and used to analyze the packet using another table. This helps support advanced forwarding mechanisms and provides great flexibility in defining packet processing and action. By more complex, we mean that the ability to define multiple patterns and associated actions withing a single table. This offers a fine-grained control over packets, meaning specialization of detailed patterns that considers various packet attributes, and enabling precise matching and corresponding actions. 
The tables can be nested, meaning we can use an action defined in the table, to then analyze the packet using another match-plus-action table. This enables us to see that specific actions can trigger deep analysis or further classification by using additional tables, with hierarchical and modular packet processing.


#### SDN
Software-Defined Networking (SDN) is an architectural approach that aims to simplify and centralize network management and control by decoupling the control plane from the data plane. SDN separates the network's control logic (software-based controller) from the forwarding hardware (switches, routers), providing a centralized view and control over the network infrastructure. SDN allows network administrators to dynamically configure and manage network resources, define forwarding policies, and optimize traffic flows through a programmable and centralized controller.

- Approach to network management that allows for dynamic network configuration
- It aims to improve network performance and monitoring
- Centralize network intelligence by separating the data plane from the control plane.
- Example:
![[Pasted image 20230530175501.png]]
- Example: firewall
![[Pasted image 20230530175529.png]]
- Example: load balance
![[Pasted image 20230530175553.png]]
- Example: NAT
![[Pasted image 20230530175611.png]]

SDN enables generalized forwarding by providing a platform for implementing advanced forwarding behaviors and policies. The controller in an SDN architecture can programmatically define forwarding rules and policies for individual network devices based on specific requirements. It allows for dynamic adjustments and real-time control of network traffic, facilitating traffic engineering, load balancing, QoS provisioning, and security enforcement. This programmability and centralized control make SDN an enabling technology for generalized forwarding, where forwarding decisions can be tailored to suit specific network needs.

By combining the principles of generalized forwarding with the flexibility and programmability offered by SDN, networks can achieve more efficient, agile, and adaptive forwarding behavior. This approach enhances network scalability, performance, and security while providing a framework for innovation and the introduction of new services and applications.

#### Middleboxes

>Intermediary device that performs functions aside IP forwarding and routing

A middlebox refers to an intermediary network device that performs specific functions beyond IP forwarding and routing. While routers and switches focus on the efficient transfer of packets between networks, middleboxes provide additional services and functionality to enhance network operations. They are typically deployed at key points within a network to fulfill specific purposes.

##### Type of services:
- NAT translation
	- NAT middleboxes are commonly used to perform address translation, allowing multiple devices within a private network to share a single public IP address. They modify the source and/or destination IP addresses and port numbers of packets to enable communication between the private network and the external public network.
- Security
	- Some middleboxes are designed to provide security-related functions to protect network traffic and resources. These may include firewalls, intrusion detection/prevention systems (IDS/IPS), deep packet inspection (DPI) for traffic analysis, virtual private network (VPN)
- Performance enhancement
	- Middleboxes can optimize network performance by applying various techniques. For example, load balancers distribute incoming traffic across multiple servers to ensure efficient resource utilization. Traffic shapers prioritize or restrict bandwidth usage to manage network congestion. Application delivery controllers (ADCs) can optimize traffic flow, caching, and content delivery for better performance.

These services are just a few examples of what middleboxes can provide. Other types of middleboxes may focus on specific functionalities such as content filtering, data compression, protocol optimization, protocol conversion, or quality of service (QoS) enforcement.

Middleboxes play a critical role in network architectures, enabling the implementation of additional services and functionalities beyond traditional IP forwarding and routing. They enhance security, improve network performance, and ensure compatibility with various protocols and network requirements. However, the deployment of middleboxes can also introduce complexity and potential points of failure, requiring careful management and coordination within a network infrastructure.

- **Questions:**
	- What is the purpose of the match-plus-action (flow) table in networking?:: It maps patterns found in an arriving packet to the corresponding action.
<!--SR:!2023-06-03,1,228-->
	- What is the significance of the subnet mask in IPv4?:: The subnet mask is a bitmask used for efficient addressing and routing, and it helps identify the network portion of an IP address.
<!--SR:!2023-06-03,1,228-->
	- What is NAT traversal in networking?:: NAT traversal refers to techniques used to establish communication between devices behind Network Address Translation (NAT) devices.
<!--SR:!2023-06-03,1,228-->
	- What is the purpose of DHCP (Dynamic Host Configuration Protocol)?:: DHCP is used to dynamically assign IP addresses and provide network configuration information to devices on a network.
<!--SR:!2023-06-03,1,228-->
	- What are the characteristics of match-plus-action (flow) tables?:: They are more complex than basic forwarding tables, can be nested to analyze packets using another table, and are not layer-specific.
<!--SR:!2023-06-03,1,228-->
	- What are the differences between IPv4 and IPv6?:: IPv6 has a larger address space, improved header format, simplified header structure, built-in support for security and mobility, and better support for multicast communication.
<!--SR:!2023-06-03,1,228-->
	- What is the purpose of Network Address Translation (NAT)?:: NAT allows multiple devices in a private network to share a single public IP address and provides a level of security by hiding internal IP addresses.
<!--SR:!2023-06-04,2,248-->
	- What is the purpose of IPv6 tunneling?:: IPv6 tunneling enables the encapsulation and transport of IPv6 packets over IPv4 networks, allowing for the coexistence and transition between IPv4 and IPv6 protocols.
<!--SR:!2023-06-04,2,248-->
	- How will the public Internet transition to IPv6?:: The transition to IPv6 on the public Internet involves a gradual adoption of IPv6 alongside IPv4, dual-stack implementations, and the use of transition mechanisms like tunneling, translation, and hybrid approaches
<!--SR:!2023-09-02,11,208-->
	- What are some common services provided by middleboxes?:: NAT translation, security (firewalls, IDS/IPS), performance enhancement (load balancing, traffic shaping), content filtering, protocol optimization, and QoS enforcement.
<!--SR:!2023-06-03,1,228-->

---

## Routing Algorithms
Routing algorithms are essential components of computer networking that determine the paths data packets take when traveling from a source to a destination across a network. These algorithms help optimize the efficient and reliable delivery of data by selecting the best routes based on various metrics, network conditions, and routing protocols
![[Pasted image 20230530181152.png]]

Some important routing algorithms aspects:
- Shortest Path Algorithm
	- Djikstra's
	- Bellman-Ford
- Distance Vector Algorithm
	- Routing Information Protocol (RIP)
- Link State Algorithms
	- Open Shortest Path First (OSPF)
- Path Vector Algorithm
	- Border Gateway Protocol (BGP)

![[Pasted image 20230530181209.png]]

### Routing Protocol
A routing protocol specifies how routers exchange information that enables them to select routes between any two nodes on a computer network. They do this with defining the rules and procedures for routers, on how they will exchange information and build up their routing tables. By doing this, we enable routers to select the most appropriate paths or routes between two nodes. The routing protocols facilitates the dynamic and efficient discovery, maintenance and dissemination of routing information across routers. 
Some of the key aspects for routing protocols include: Routing information Exchange, Route Discovery, Route selection, Routing Table Updates, Types of Routing Protocols, Protocol Convergence, and scalability and flexibility. 

Different routing protocols have their strengths and are suitable for specific network environments. Network administrators choose the appropriate routing protocol based on factors like network size, complexity, performance requirements, scalability, and administrative policies. Overall, routing protocols play a crucial role in facilitating efficient and reliable routing within computer networks, ensuring that data packets are delivered to their intended destinations using the most optimal paths.

---
The Routing algorithm selects good paths from senders to receivers, through the network of routers. 

### Determining the costs
In routing algorithms, determining the costs of edges (links) is an important aspect in selecting the best routes for data transmission. The cost associated with an edge represents the desirability or suitability of using that particular link in the routing process. An edge's cost may reflect:
- The **physical length** of link:
	- The physical length of a link can be a factor in determining its cost. Longer links may have higher costs associated with them, as data transmission over longer distances can introduce more latency, potential for errors, and increased propagation delays.
- The **monetary cost** associated with a link:
	- In some cases, the cost of using a link can be related to the monetary expenses associated with its usage. For example, certain high-speed or dedicated links may have higher costs in terms of monetary charges or subscription fees.
- **Bit Rate**:
	- The bit rate or bandwidth of a link can also influence its cost. Higher bandwidth links that can transmit data at faster rates may be assigned lower costs, as they can provide better performance and accommodate more traffic.

**Note**: that the specific factors used to determine costs can vary depending on the routing algorithm, network requirements, and the metrics being considered. Different algorithms may prioritize different cost factors based on the desired objectives, such as minimizing delay, maximizing bandwidth utilization, or minimizing financial expenses.

The goal of routing algorithms is to find the least-cost path. There are several types of classifications for routing algorithms that we'll take a look at. 

### Centralized Routing Algorithms
A centralized routing algorithm is a type of routing algorithm that operates based on having complete knowledge about the entire network topology. It computes the least-cost path for data packets to travel from a source to a destination by considering the network as a whole.
- This requires the algorithm to gather and maintain global state information about the network before performing the routing calculations.
- It computes the least-cost path using knowledge about the whole network.
- It obtains this information **before** performing the calculations

Centralized routing algorithms are often referred to as link-state (LS) algorithms because they rely on the collection of link-state information from all routers in the network. The link-state information includes details about the connectivity, status, and metrics of all links in the network.
Each router shares this information with others, allowing each router to build a comprehensive and accurate view of the network topology.
- Algorithms with global state information are referred to as link-state algorithms (LS).

### Decentralized Routing Algorithms
In contrast to centralized routing algorithms, decentralized routing algorithms operate in a distributed manner where the calculation of the least-cost path is carried out iteratively by the routers themselves. Unlike centralized algorithms, decentralized algorithms do not rely on any single node having complete information about the costs of all network links. Instead, routers exchange routing information with their neighboring routers to collectively determine the optimal paths.
- The calculation of the least-cost path is carried out in an iterative, distributed manner by the routers.
- No node has complete information about the costs of all network links

### Static Routing Algorithm
Static routing is a routing algorithm where network routes are manually configured and do not change automatically based on network conditions or topology changes. In static routing, routes are pre-defined and remain constant unless manually modified by a network administrator. Static routes are typically configured by specifying the destination network or IP address and the next-hop router or outgoing interface to reach that destination.
- Routers change very slowly over time.
- Is predicable and stable
- Simple implementation
- Low overhead


### Dynamic Routing Algorithm
Dynamic routing algorithms are designed to adapt to changing network conditions and topology. These algorithms automatically determine the best routes based on real-time information about network congestion, link failures, or changes in topology. Dynamic routing protocols enable routers to exchange routing information and collaboratively calculate and update routes.
- Changes the routing paths as the network traffic loads or topology changes.
	- Automatic Route Calculation: Dynamic routing algorithms dynamically calculate and update routes based on network conditions. Routers exchange routing information to build and maintain routing tables.
- Adapts and is responsive to changes in network topology.
- Increased Overhead compared to static. The routers continuously exchange routing updates and engage in route calculations, which increases the consume in processing power and bandwidth.
- Is more complex to configure and manage compared to static routing. Requires carefull configuration and monitoring, to prevent issues like routing loops or convergence problems

### Link-state routing protocols
Link-state routing protocols are a type of routing protocol used in computer networks to determine the best paths for routing data packets. 
In link-state routing, each node in the network exchanges information about its attached links with all other nodes, allowing each node to have a complete understanding of the network's topology. This information is used by each node to compute the least-cost paths to reach different destinations within the network.

#### Link-State Packets
In link-state routing, each node generates and broadcasts link-state packets to all other nodes in the network. These packets contain information about the node's own identity and the costs associated with its attached links. The information is usually represented as a link-state database or a link-state advertisement (LSA).
- Contains the identities and costs of its attached links.

### Dijkstra's Algorithm
Dijkstra's algorithm is a [[Informatikk/INF102/Graphs|graph]] search algorithm used to find the shortest path from a source node to all other nodes in a weighted graph. It is commonly used in network routing algorithms and path-finding applications. Here are some key points about Dijkstra's algorithm:
![[Pasted image 20230530192825.png]]

#### Properties of Dijkstra's Algorithm:
- Iterative: Dijkstra's algorithm works in an iterative manner, gradually exploring nodes and updating the least-cost paths to reach each node from the source.
-  Least-Cost Paths: After each iteration of the algorithm, the least-cost paths from the source node to a subset of destinations are known. These paths have the k smallest costs among all possible paths.
- After the ``k``-th iteration, the least-cost paths are known to ``k`` destinations.
- Among the least-cost paths to all destinations, these ``k`` paths will have the ``k`` smallest costs.

#### Notations in Dijkstra's Algorithm:
- D(v): It represents the least cost from the source node to node v at the current iteration. D(v) is initially set to infinity for all nodes except the source node, whose cost is set to 0.
- p(v): It denotes the previous node along the current least-cost path from the source to node v. The value of p(v) is updated during the algorithm's execution as the least-cost paths are discovered.
- N': It is a subset of nodes whose least-cost path from the source node is definitely known. In other words, N' contains the nodes that have been explored and their least-cost paths are finalized. The set of unexplored nodes is represented as N \ N', where N is the set of all nodes in the graph.
![[Pasted image 20230530192854.png]]

#### The Steps of Dijkstra's Algorithm:
1. Initialization: Set the cost of the source node to 0 and the cost of all other nodes to infinity. Set the source node as the current node.
2. Iteration: While there are unexplored nodes, select the node with the smallest cost (D(v)) among the unexplored nodes. Mark it as explored and add it to the N' set.
3. Update Costs: For each neighbor of the current node, calculate a tentative cost by summing the cost of the current node and the weight of the edge connecting them. If this tentative cost is smaller than the previously recorded cost for that neighbor, update the cost and set the previous node (p(v)) to the current node.
4. Repeat Steps 2 and 3 until all nodes have been explored or until the destination node is reached.
5. Path Reconstruction: Once the algorithm terminates, the least-cost path from the source to any destination can be reconstructed by following the previous nodes (p(v)) back from the destination node to the source node.
Dijkstra's algorithm guarantees that the least-cost path to each node is found in a systematic manner. By iteratively exploring nodes and updating the costs, it efficiently finds the shortest paths from a source node to all other nodes in the graph.

#### Dijkstra's Algorithm Code:
Here's an pseudo-code implementation of Dijkstra's algorithm in Python:
```Python
import numpy as np

def dijkstra(graph, source):
    unvisited = set(graph)
    distances = dict.fromkeys(graph, np.inf)
    previous = dict.fromkeys(graph)

    def visit(node):
        unvisited.remove(node)
        unvisited_neighbors = unvisited.intersection(graph[node])
        for neighbor in unvisited_neighbors:
            temp = distances[node] + graph[node][neighbor]['distance']
            if temp < distances[neighbor]:
                distances[neighbor] = temp
                previous[neighbor] = node
                
    def init_table():
        unvisited = set(graph)
        distances = dict.fromkeys(graph, np.inf)
        previous = dict.fromkeys(graph)
        
    init_table()
    distances[source] = 0
    visit(source)
    
    while unvisited:
        next_node = min(unvisited, key=distances.get)
        visit(next_node)
        
    return distances, previous

```
And here is a graph where we can use the `dijkstra` function:
```Python
# Example graph
graph = {
    'A': {'B': {'distance': 5}, 'C': {'distance': 3}},
    'B': {'A': {'distance': 5}, 'C': {'distance': 2}, 'D': {'distance': 6}},
    'C': {'A': {'distance': 3}, 'B': {'distance': 2}, 'D': {'distance': 7}},
    'D': {'B': {'distance': 6}, 'C': {'distance': 7}}
}

source_node = 'A'
distances, previous = dijkstra(graph, source_node)

print(f"Shortest distances from node {source_node}:")
for node, distance in distances.items():
    print(f"{node}: {distance}")

print("\nShortest paths:")
for node in graph:
    path = []
    current_node = node
    while current_node is not None:
        path.insert(0, current_node)
        current_node = previous[current_node]
    print(f"{node}: {' -> '.join(path)}")
```
Each key in the `graph` dictionary represents a node, and its value is another dictionary containing the neighboring nodes as keys and the corresponding distances as values.
This code will output the shortest distances from the source node to each node in the graph, as well as the shortest paths from the source node to each node.


### The Distance-Vector routing algorithm
The Distance-Vector (DV) routing algorithm is an iterative, distributed algorithm used in computer networks to determine the best path for data packets to travel from a source node to a destination node. It operates based on the exchange of distance vectors, which are estimates of the costs to reach various destinations.

#### The Distance-Vector (DV) algorithm properties
- **Iterative**:
	- The algorithm iteratively updates the distance vectors based on information received from neighboring nodes. Each iteration improves the accuracy of the distance estimates.
- **Distributed**:
	- Each node interacts with its neighbors
	- Nodes in the network independently calculate and update their own distance vectors. They exchange this information with their neighbors to gradually converge on the optimal paths.
- **Asynchronous**:
	- Nodes do not operate in lockstep with each other.
	- They update their distance vectors and exchange information at their own pace, based on the received updates.


#### Bellman-Ford equation
The Bellman-Ford equation is a key component of the Distance-Vector algorithm. It allows nodes to calculate the shortest path to a destination by considering the minimum cost among all possible routes via their neighboring nodes. The equation states that the cost from node x to node y (dx(y)) is the minimum of the costs from node x to each of its neighbors (c(x, i) + di(y)), where di(y) is the distance vector estimate of node i for node y.
![[Pasted image 20230530194111.png]]

![[Pasted image 20230530194301.png]]
#### Distance-Vector
In the Distance-Vector algorithm, each node maintains its own distance vector, denoted as Dx. The distance vector Dx contains the estimates of the costs to reach various destinations, where Dx(y) represents the estimate of the cost from the node to destination y. The estimates in the distance vector are updated based on the received information from neighboring nodes.
![[Pasted image 20230530194347.png]]
Through the iterative updates and exchange of distance vectors, the Distance-Vector algorithm aims to converge on the most optimal paths in the network. Under normal conditions, where the network topology and link costs remain stable, the distance vector estimates Dx(y) converge to the actual shortest path costs dx(y).
![[Pasted image 20230530194400.png]]
The Distance-Vector algorithm has been widely used in various routing protocols, such as Routing Information Protocol (RIP) and Interior Gateway Routing Protocol (IGRP), to determine routing paths in networks. It provides a distributed and scalable approach to finding efficient paths through the exchange of information among neighboring nodes.
![[Pasted image 20230530194411.png]]
- Under natural conditions the estimate Dx(y) converges to dx(y)

---
## Routing in the Internet
When routing in networking, there are several problems/issues due to the large scale of the Internet. There are billions of destinations out there, and it is not appropriate to store all them in routing tables.
Routing in the Internet is a complex task due to the scale of the network and the presence of multiple autonomous systems. The goal of routing in the Internet is to efficiently and effectively forward data packets from source to destination across different networks.
![[Pasted image 20230531232622.png]]
One of the main challenges in routing at Internet scale is the sheer number of destinations. With billions of devices and networks connected to the Internet, it is not feasible to store the routing information for all destinations in a centralized routing table. Such an approach would require enormous storage capacity and would result in excessive routing message traffic, overwhelming the network links.

To address this scalability challenge, the Internet uses a hierarchical routing structure. The Internet is divided into autonomous systems (ASes), which are networks operated by a single administrative entity. Each AS is responsible for its own internal routing and can make routing decisions independently. This allows each AS to manage its own routing table without the need to have knowledge of every destination in the entire Internet.

Routing messages are exchanged between ASes to exchange information about network reachability. Border Gateway Protocol (BGP) is the primary routing protocol used for inter-domain routing in the Internet. BGP allows autonomous systems to exchange routing information and make routing decisions based on policies and preferences.

Within an AS, routing can be carried out ignoring the specific details of other networks. This allows each network administrator to have control over the routing decisions within their own network. Within an AS, interior gateway protocols (IGPs) such as Open Shortest Path First (OSPF) or Intermediate System to Intermediate System (IS-IS) are commonly used to determine the best paths within the network.

By combining hierarchical routing and the autonomy of individual networks, routing in the Internet can scale to handle the vast number of destinations while still allowing network administrators to have control over their own routing decisions. This decentralized and distributed approach ensures efficient and robust routing across the Internet.

### Autonomous systems
![[Pasted image 20230601031337.png]]
