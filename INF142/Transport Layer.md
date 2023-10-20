>The transport layer is a central piece of the layered network architecture. It has the critical role of providing communication services directly to the application processes running on different hosts

One of the most fundamental problems in computer networking—how two entities can communicate reliably over a medium that may lose and corrupt data.
Second fundamentally important problem in networking—controlling the transmission rate of transport-layer entities in order to avoid, or recover from, congestion within the network.

### Introduction and Transport-Layer Services

>In the [[Application Layer]] and [[Computer Networks and the Internet]] note we have touched on the role of the transport layer and the services that it provides.

- A transport-layer protocol provides for logical communication between two application processes running on different hosts. This logical communication makes it appear as if the hosts running the processes are directly connected, regardless of their physical locations and the underlying network infrastructure.
- Transport-layer protocols are implemented in the end systems (hosts) and not in network routers. They operate on transport-layer segments, which are packets containing application-layer messages. The transport layer adds a transport-layer header to each segment, breaking down the application messages into smaller chunks if necessary. 
- On the sending side, the transport layer passes the segments to the network layer, which encapsulates them into network-layer packets (datagrams) and forwards them to the destination. Routers in the network act only on the network-layer fields of the datagrams and do not inspect the transport-layer segment within.
- On the receiving side, the [[network layer]] extracts the transport-layer segment from the datagram and passes it up to the transport layer. The transport layer then processes the segment and makes the received data available to the receiving application process.
- The Internet provides two transport-layer protocols: [[TCP]] (Transmission Control Protocol) and [[UDP]] (User Datagram Protocol). Each protocol offers a different set of services to the applications. [[TCP]] provides reliable, ordered, and error-checked delivery of data, while [[UDP]]provides unreliable and unordered delivery.
- Applications can choose the appropriate transport-layer protocol based on their specific requirements. For example, applications that prioritize data integrity and reliability, such as web browsing and file transfer, often use [[TCP]]. Applications that require low-latency and are tolerant of data loss, such as real-time streaming and online gaming, may opt for [[UDP]].

>Overall, the transport layer plays a crucial role in facilitating communication between application processes across networks. It abstracts the complexities of the underlying network infrastructure and provides a reliable and efficient means of data transfer between hosts.

###### Relationship Between Transport and Network Layers
The relationship between the transport layer and the network layer can be understood through an analogy with a household and postal service. 
- In the analogy, consider two households with cousins living on the East Coast and West Coast. The cousins love to write letters to each other, and the postal service facilitates the communication between the two households by delivering the mail. In each household, there is one cousin responsible for collecting and distributing the mail within their respective house.
- In this analogy:
	- The postal service represents the network-layer protocol, which provides logical communication between the two houses (hosts) by moving mail from one house to another, without concerning itself with the individual cousins (processes).
	- The cousins represent the application processes, who write letters (application messages) to each other. They rely on the postal service to deliver their letters.
- Similarly, in the context of networking:
	- The network layer protocol provides logical communication between hosts (end systems) in the network, irrespective of their physical locations. It moves network-layer packets (datagrams) from one host to another.
	- The transport layer protocol operates within the hosts (end systems) and provides logical communication between application processes. It takes the application messages and encapsulates them into transport-layer segments, which are then encapsulated into network-layer packets for transmission.

- The transport-layer protocol, like the cousins in the analogy, is responsible for the end-to-end delivery of messages between application processes. It operates within the end systems and interacts with the network layer for sending and receiving segments.
- It's important to note that the transport-layer protocol is independent of the specific mechanisms used by the network-layer protocol to forward packets within the network. Intermediate routers in the network core do not recognize or modify the transport-layer information added to the application messages.
- The services that a transport protocol can provide to applications may be influenced by the service model offered by the underlying network-layer protocol. For example, if the network-layer protocol does not guarantee specific delay or bandwidth characteristics, the transport-layer protocol cannot provide such guarantees either. However, transport-layer protocols can offer additional services, such as reliable data transfer or encryption, even if the underlying network protocol does not provide them.

>In summary, the transport layer and the [[network layer]] work together to enable logical communication between application processes across the network. The [[network layer]] focuses on host-to-host communication, while the transport layer ensures reliable and efficient communication between processes running on different hosts.


###### Overview of the Transport Layer in the Internet
[[UDP]] (User Datagram Protocol) and [[TCP]] (Transmission Control Protocol) are two distinct transport-layer protocols available in the Internet.

- [[UDP]] is a connectionless protocol that provides an unreliable service to applications. It offers a minimal set of services, including process-to-process data delivery and error checking. [[UDP]] segments, also known as datagrams, are sent from one host to another without establishing a connection beforehand. [[UDP]] does not guarantee delivery of data, the order of delivery, or the integrity of the data. Applications using [[UDP]] have the freedom to send data at any rate they please, without any regulation.

- On the other hand, [[TCP]] is a connection-oriented protocol that provides a reliable service to applications. [[TCP]] extends the best-effort delivery service of the [[network layer]] (IP) to a reliable data transport service between processes running on end systems. [[TCP]] ensures reliable data transfer by employing techniques such as flow control, sequence numbers, acknowledgments, and timers. It guarantees that data is delivered correctly and in order from the sending process to the receiving process. [[TCP]] also provides congestion control, which aims to prevent any one [[TCP]] connection from overwhelming the network with excessive traffic. It regulates the rate at which data is sent into the network to ensure fair sharing of the available bandwidth among all connections.
- Unlike [[UDP]], which focuses on simplicity and minimal services, [[TCP]] is a complex protocol due to its additional services of reliable data transfer and congestion control. The principles of reliable data transfer and congestion control are covered in sections 3.4 to 3.7 of the text.
- Transport-layer multiplexing and demultiplexing play a crucial role in both [[UDP]] and [[TCP]]. These processes enable the delivery of data between specific processes running on end systems, going beyond host-to-host communication. Multiplexing involves combining multiple data streams into a single transport-layer segment, while demultiplexing involves extracting the individual data streams at the receiving end.

>In summary, [[UDP]] provides an unreliable, connectionless service, while [[TCP]] provides a reliable, connection-oriented service. [[UDP]] offers minimal services, whereas [[TCP]] offers additional services such as reliable data transfer and congestion control. Transport-layer multiplexing and demultiplexing facilitate process-to-process communication and are essential components of both protocols.

![[Pasted image 20230513165350.png]]


### Multiplexing and Demultiplexing
>Transport-layer multiplexing and demultiplexing: the process of extending the host-to-host delivery service provided by the network layer to a process-to-process delivery service for applications running on hosts.

When data arrives at the receiving host from the network layer, it is directed to an intermediary socket in the transport layer, rather than directly to the application process. Each socket has a unique identifier depending on whether it is a UDP or TCP socket. The transport layer examines the fields in the transport-layer segment to identify the receiving socket and then delivers the segment to that socket. This process of delivering data to the correct socket is called demultiplexing.

On the other hand, multiplexing involves gathering data chunks from different sockets, encapsulating them with header information, and creating segments to be passed to the network layer. The transport layer in the middle host must demultiplex segments from the network layer and direct them to the corresponding process's socket, as well as gather outgoing data from sockets, form segments, and pass them to the network layer.

Transport-layer multiplexing and demultiplexing are essential considerations whenever a single protocol at one layer is used by multiple protocols at the next higher layer.

To facilitate multiplexing and demultiplexing, each transport-layer segment has source port number and destination port number fields. Port numbers are 16-bit numbers, ranging from 0 to 65535. Port numbers from 0 to 1023 are reserved for well-known application protocols, while higher port numbers can be assigned to specific applications.

The transport layer implements demultiplexing by assigning each socket a port number and directing incoming segments to the corresponding socket based on the destination port number. UDP performs demultiplexing in a straightforward manner, while TCP's multiplexing/demultiplexing is more complex, as will be discussed in subsequent sections.

![[Pasted image 20230513165942.png]]

###### Connectionless Multiplexing and Demultiplexing
- UDP sockets are created using the socket() function, and the transport layer automatically assigns a port number to the socket.
- UDP multiplexing/demultiplexing is based on port numbers.
- The source port number serves as part of the return address, allowing the receiving host to send a segment back to the sender.
- UDP sockets are identified by a two-tuple consisting of a destination IP address and a destination port number.
- If two UDP segments have the same destination IP address and destination port number, they will be directed to the same destination process via the same socket.

###### Connection-Oriented Multiplexing and Demultiplexing
- TCP sockets are identified by a four-tuple consisting of a source IP address, source port number, destination IP address, and destination port number.
- TCP segments are demultiplexed based on all four values.
- TCP connection establishment involves a three-way handshake, with a connection-establishment request segment sent from the client to the server.
- The server process creates a new socket for the connection and identifies it based on the source port number, source IP address, destination port number, and its own IP address.
- Subsequently arriving segments with matching values are demultiplexed to the connection socket.
- Multiple simultaneous [[TCP]] connections can be supported on a server host, with each connection socket identified by its own four-tuple.
- Demultiplexing takes into account all four fields (source IP address, source port, destination IP address, destination port) to direct segments to the appropriate socket.

###### Web Servers and TCP
- Web servers, such as Apache, typically run on port 80.
- Clients (e.g., browsers) send segments to the server with destination port 80.
- The server distinguishes segments from different clients using source IP addresses and source port numbers.
- Web servers can spawn new processes or threads for each client connection, with each process or thread having its own connection socket.
- High-performing Web servers often use a single process and create new threads with new connection sockets for each client connection.
- Persistent HTTP connections allow clients and servers to exchange HTTP messages via the same server socket, while non-persistent HTTP connections create and close a new [[TCP]] connection and socket for each request/response.
- The frequent creation and closing of sockets for non-persistent HTTP can impact the performance of a busy Web server.
- UDP adds little more to the network-layer protocol than a multiplexing/demultiplexing service.

### Connectionless Transport: UDP
- UDP is a connection-less transport protocol that adds minimal functionality to IP.
- UDP provides a multiplexing/demultiplexing service and light error checking.
- UDP takes messages from the application process, attaches source and destination port number fields, adds a few other fields, and passes the segment to the network layer.
- [[UDP]] segments are encapsulated into IP datagrams and delivered to the receiving host.
- [[UDP]] uses the destination port number to deliver the segment's data to the correct application process.
- UDP does not involve handshaking between sending and receiving transport-layer entities.
- Applications may choose [[UDP]] over [[TCP]] for finer control over data sending, no connection establishment delay, no connection state maintenance, and small packet header overhead.
- DNS is an example of an application that typically uses [[UDP]].
- UDP is used in multimedia applications, where a small amount of packet loss is tolerable and [[TCP]]'s congestion control can negatively impact real-time communication.
- Running multimedia applications over [[UDP]] requires careful consideration of congestion control mechanisms to prevent network congestion and high loss rates.
- An application can achieve reliable data transfer using [[UDP]] if reliability is built into the application itself or implemented as an application-layer protocol on top of [[UDP]].
- The QUIC protocol is an example of implementing reliability on top of [[UDP]].
- Building reliability into the application allows for reliable communication without the transmission-rate constraints imposed by TCP's congestion control mechanism.

Example of internet applications and their transport-protocols. 
![[Pasted image 20230513171314.png]]

###### UDP Segment Structure
The [[UDP]] segment structure consists of a header and a data field. The header has four fields, each consisting of two bytes. The fields are:
1. Source port number: Specifies the port number of the sending process.
2. Destination port number: Specifies the port number of the receiving process for demultiplexing.
3. Length: Specifies the length of the [[UDP]] segment, including the header and data, in bytes.
4. Checksum: Used by the receiving host to check for errors in the segment.

The data field contains the application data, such as query or response messages for [[Application Layer#DNS|DNS]] or audio samples for a streaming audio application. The length field is necessary because the size of the data field may vary between [[UDP]] segments.

The checksum is calculated to detect errors in the segment, and it is also computed over a few fields in the IP header in addition to the [[UDP]] segment. However, the details of this calculation are not discussed in this section.

Overall, the [[UDP]] segment structure is simple, with minimal fields for port numbers, length, and checksum.

###### UDP Checksum
The [[UDP#UDP Header structure:|UDP checksum]] is used for error detection in the [[UDP]] segment. It checks whether the bits within the segment have been altered during transmission. The checksum calculation is performed by taking the 1s complement of the sum of all the 16-bit words in the segment. If any overflow occurs during the sum, it is wrapped around. The result is placed in the checksum field of the [[UDP]] segment.

- UDP segment structure:
![[Pasted image 20230513172256.png]]

At the receiver, all the 16-bit words, including the checksum, are added. If no errors were introduced, the sum will be all 1s. If any bit is 0, it indicates that errors have been introduced into the packet.
[[UDP]] provides its own [[UDP#UDP Header structure:|checksum]] because not all link-layer protocols guarantee error checking, and errors can also occur when a segment is stored in a router's memory. By providing error detection at the transport layer, [[UDP]] ensures end-to-end error detection for the data transfer service.
Although [[UDP]] provides error checking, it does not include mechanisms for error recovery. Some implementations of [[UDP]] discard damaged segments, while others pass them to the application with a warning.

Overall, the [[UDP#UDP Header structure:|UDP checksum]] serves as a safety measure to detect errors in [[UDP]] segments, ensuring reliability at the [[transport layer#Overview of the Transport Layer in the Internet|transport layer]].

**Example:**

Suppose that we have the following three 16-bit words:

0110011001100000
0101010101010101
1000111100001100

The sum of first two of these 16-bit words is

0110011001100000
<u>0101010101010101</u>
1011101110110101

Adding the third word to the above sum gives

1011101110110101
<u>1000111100001100</u>
0100101011000010

We notice that during the addition, there was an overflow. To handle this, we wrap around the overflow and continue the addition.

Now, to obtain the [[UDP]] checksum, we perform a 1s complement of the sum. This means we convert all the 0s to 1s and all the 1s to 0s. After performing the 1s complement, we get:
- 0100101011000010 (original sum) ->
- 1011010100111101 (1s complement) -> This is the checksum!

At the receiver side, all four 16-bit words, including the checksum, are added together. If no errors were introduced during transmission, the sum at the receiver will be all 1s (1111111111111111). If any of the bits is 0, it indicates that errors have been introduced into the packet.

The [[UDP]] checksum allows the receiver to check if any bits in the [[UDP]] segment have been altered during transmission, ensuring the integrity of the data.

***Here's a furter explaination to what happens in this example:***

In the [[UDP#UDP Header structure:|UDP checksum]] calculation example, the bits change as part of the process to perform error detection. The purpose of the checksum is to determine whether any bits in the UDP segment have been altered during transmission.

Here's a breakdown of why the bits change in the example:

1. Summation of 16-bit words: The first step involves summing the 16-bit words. When adding binary numbers, a carry-over can occur when the sum of two bits is greater than 1. In the example, the addition of the first two 16-bit words produces a sum with some bits that are different from the original bits.
2. Overflow and wrap-around: When the third 16-bit word is added to the sum, an overflow occurs. This means that the addition produces a result that is larger than what can be represented using 16 bits. To handle the overflow, the extra bits beyond 16 are disregarded, resulting in a wrap-around effect. This wrap-around can cause changes in the bits.
3. 1s complement: To obtain the checksum, the 1s complement of the sum is taken. In this process, all the 0s are converted to 1s, and all the 1s are converted to 0s. This inversion of bits further changes the values.

The changes in the bits during these calculations are intentional and necessary to ensure that even a single bit alteration in the [[UDP]] segment will lead to a different checksum value at the receiver. By comparing the received checksum with the recalculated checksum, the receiver can detect any errors that might have occurred during transmission.

The bit changes help in identifying potential errors and ensure the reliability of the [[UDP]] transmission by enabling error detection.


### Principles of Reliable Data Transfer
>This section discusses the problem of reliable data transfer in a general context, highlighting its significance in networking. The framework for studying reliable data transfer is presented, focusing on the service abstraction of a reliable channel. [[TCP]] is introduced as an example of a reliable data transfer protocol that provides this service model to Internet applications.

The responsibility of a reliable data transfer protocol is to implement the reliable channel service abstraction, even in the presence of an unreliable lower layer. The lower layer could be an IP network or a link-level protocol, but for simplicity, it is viewed as an unreliable point-to-point channel. The section progressively develops the sender and receiver sides of a reliable data transfer protocol, taking into account different models of the underlying channel, including bit corruption and packet loss.

The interfaces and terminology used in the protocol development are explained, such as rdt_send(), rdt_rcv(), and deliver_data(). The distinction between packets and segments is made, with the understanding that the concepts discussed are applicable to computer networks in general.

Unidirectional data transfer is considered in this section, while acknowledging that both the sending and receiving sides of the protocol need to transmit packets in both directions. Control packets are also exchanged between the sender and receiver sides, in addition to the data packets.

The section concludes by mentioning the use of udt_send() for sending packets in both directions, where udt represents unreliable data transfer.

The problem of implementing reliable data transfer occurs not only at the transport layer, but also at the link layer and the application layer.
- The general problem is thus of central importance to networking.
- if one had to identify a “top-ten” list of fundamentally important problems in all of networking, reliable data transfer would be a candidate to lead the list.

Figure 3.8 illustrates the framework for our study of reliable data transfer:
![[Pasted image 20230513184652.png]]

The upper-layer entities, which could be applications or protocols, interact with the transport layer and rely on it to provide a reliable channel for transferring their data. The term "reliable channel" means that the transport layer protocol ensures that the data sent by the upper-layer entities will be delivered accurately and in the correct order to the receiving end. 

This service abstraction of a reliable channel allows the upper-layer entities to operate under the assumption that their data will be transmitted without errors, loss, or duplication, regardless of the potential unreliability of the underlying network. This helps the upper layers (shields them) from the complexity and challenges of dealing with network issues in the lower-layer. E.G, packet loss, corruption of bits, or reordering of packets etc. 
Luckly [[TCP]] provides exactly this. 
The challenges lies in that the layer below the reliable transfer protocol may be unreliable. As known, [[TCP]] is a reliable data transfer protocol, that is implemented on top of an unreliable (IP) end-to-end network layer. There are luckly implemented protocol mechanisms that handles when underlying channels corrupt bits or lose entire packets. We'll assume that packets arrive in order, since an underlying channel will not reorder packets, but rather lose them. 
The figure 3.8 (b) illustrates the interfaces for our data transfer protocol. 
- The sending side of the data transfer protocol will be invoked from above by a call to ``rdt_send()``.
- It will pass the data to bedelivered to the upper layer at the receiving side. (Here ``rdt`` stands for reliable data transfer protocol and ``_send ``indicates that the sending side of ``rdt`` is being called.
- On the receiving side, ``rdt_rcv()`` will be called when a packet arrives from the receiving side of the channel.
- When the ``rdt`` protocol wants to deliver data to the upper layer, it will do so by calling ``deliver_data()``.
- In the following, we use the terminology “packet” rather than transport-layer “segment.”
	- Because the theory developed in this section applies to computer networks in general and not just to the Internet transport layer, the generic term “packet” is perhaps more appropriate here.
- In this section, we consider only the case of **unidirectional data transfer**, that is, data transfer from the sending to the receiving side
- The case of reliable bidirectional(that is, full-duplex) data transfer is conceptually no more difficult but considerably more tedious to explain.
- Although we consider only unidirectional data transfer, it is important to note that the sending and receiving sides of our protocol will nonetheless need to transmit packets in both directions, as indicated in Figure 3.8.
- In addition to exchanging packets containing the data to be transferred, the sending and receiving sides of rdt will also need to exchange control packets back and forth. Both the send and receive sides of ``rdt`` send packets to the other side by a call to ``udt_send()`` (where udt stands for unreliable data transfer).

![[Pasted image 20230513190915.png]]

#### Building a Reliable Data Transfer Protocol

> We now take a look through a series of protocols, where each one become more complex and arrives at a flawless reliable data transfer protocol. 

###### **Reliable Data Transfer over a Perfectly Reliable Channel: rdt1.0**
The simplest case, is one where the underlying channel is completely reliable. The protocol ``rtd1.0`` is trivial. The **finite-state machine (FSM)** definitions for the ``rdt1.0`` sender and receiver are shown in the picture below.
![[Pasted image 20230513192053.png]]
- the (a) FSM defines the operation of the sender, while the (b) FSM defines the operation of the receiver. 
- note that there are seperate FSM's for the sender and the receiver. 
	- they each have one state (as illustrated in the picture)
	- the arrows indicate the transition of the protocol from one state to another. 
	- The event causing the transition is shown above the horizontal line labeling the transition, and the actions taken when the event occurs are shown below the horizontal line.
	- When no action is taken on an event, or no event occurs and an action is taken, we’ll use the symbol Λ below or above the horizontal, respectively, to explicitly denote the lack of an action or event.
	- The initial state of the FSM is indicated by the dashed arrow. Although the FSMs in Figure 3.9 have but one state, the FSMs we will see shortly have multiple states, so it will be important to identify the initial state of each FSM.
- The sending side of ``rdt`` simply accepts data from the upper layer via the ``rdt_send(data)`` event, creates a packet containing the data (via the action`` make_pkt(data)``) and sends the packet into the channel.
- In practice, the ``rdt_send(data)`` event would result from a procedure call (for example, to ``rdt_send()``) by the upper-layer application.
- On the receiving side, ``rdt`` receives a packet from the underlying channel via the ``rdt_rcv(packet)`` event, removes the data from the packet (via the action ``extract (packet, data)``) and passes the data up to the upper layer (via the action ``deliver_data(data)``).
- In practice, the ``rdt_rcv(packet)`` event would result from a procedure call (for example, to ``rdt_rcv()``) from the lowerlayer protocol.

In this simple protocol, there is no difference between a unit of data and a packet. 
Also, all packet flow is from the sender to receiver; with a perfectly reliable channel there is no need for the receiver side to provide any feedback to the sender since nothing can go wrong! 
Note that we have also assumed that the receiver is able to receive data as fast as the sender happens to send data. Thus, there is no need for the receiver to ask the sender to slow down!


###### Reliable Data Transfer over a Channel with Bit Errors: rdt2.0
A more relalistic model, is one where the underlying channel may cause the bits in a packet to be corrupted. These errors typically occur in the physical components of a network when a packet is transmitted, propegated or buffered. We'll still assume that all packets are received in order they were sent, even if the bits in the packets are corrupted. 

Let's say two humans talk over the phone, and the sender of a message (talker A) says something and the other person (Talker B) responds with "OK" if he understands, and "Please repeat that" if he doesn't understand. This message-dication protocol uses ***positive acknowledgments*** and ***negative acknowlegdements***. These control messages allow the receiver to let the sender know what has been received correctly, and what has been received in error, and thus needs to be repeated. In a computer network setting, such protocols based on retransmissions are called **ARQ(Automatic Repeat reQuest) protocols**

There are fundamentally three additional protocol capabilities, that are required in ARQ protocols to handle the event of bit errors:
- *Error detection:*
	- A mechanism is needed to allow the receiver to detect when bit errors has occured. [[UDP]] uses the internet [[UDP#UDP Header structure:|checksum]] field for this purpose.  In [[Link Layer]] you can read about error-detection and error-correction techniques in details. These help us detect and possibly correct packet bit errors. Here (for now), we only need to know that these techniques require extra bits (beyond the bits of original data to be transferred) be sent from the sender to the receiver.
		- these bits will be gathereed into the packet checksum field of the ``rtd2.0`` data packet.
- *Receiver feedback:*
	- Senders and receivers usually are executing on different end systems seperated by thousands of kilometres (or miles), and the only way for the sender to learn of the receivers view of the world (whether or not a packet was received correctly) is for the receiver to provide explicit feedback to the sender. 
	- The positive (**ACK**) and negative (**NAK**) acknowledgements replies in the message-dictation scenario are examples of such feedback. 
	- The ``rdt2.0`` protocol will similary send ACK and NAK packets back from the receiver to the sender. 
	- In principle, these packets need only be one bit long
		- for example: a value of ``0`` can indicate a NAK and a value of ``1`` could indicate an ACK. 
- *Retransmission:*
	- A packet that is received in error at the receiver will be retransmitted by the sender.

This picture shows a FSM representation of ``rdt2.0``, a data transfer protocol employing error detection, positive acknowledgments, and negative acknowledgments. 
![[Pasted image 20230513201824.png]]
- The send side of ``rdt2.0`` has two states. In the leftmost state, the send-side protocol is waiting for data to be passed down from the upper layer. When the ``rdt_send(data)`` event occurs, the sender will create a packet (sndpkt) containing the data to be sent, along with a packet checksum.
	- for example: as discussed in this [[Transport Layer#UDP Checksum|section]]
- and then send the packet via the ``udt_send(sndpkt)`` operation. In the rightmost state, the sender protocol is waiting for an ACK or a NAK packet from the receiver.
- If an ACK packet is received the sender knows that the most recently transmitted packet has been received correctly and thus the protocol returns to the state of waiting for data from the upper layer.
	- the notation ``rdt_rcv(rcvpkt) && isACK(rcvpkt)`` in the picture (3.10) corresponds to this event. 
- If a NAK is received, the protocol retransmits the last packet and waits for an ACK or NAK to be returned by the receiver in response to the retransmitted data packet.
- It is important to note that when the sender is in the wait-for-ACK-or-NAK state, it cannot get more data from the upper layer; that is, the rdt_send() event can not occur; that will happen only after the sender receives an ACK and leaves this state.
	- Thus, the sender will not send a new piece of data until it is sure that the receiver has correctly received the current packet. Because of this behavior, protocols such as rdt2.0 are known as stop-and-wait protocols.
- The receiver-side FSM for rdt2.0 still has a single state.
- On packet arrival, the receiver replies with either an ACK or a NAK, depending on whether or not the received packet is corrupted. In Figure 3.10, the notation ``rdt_rcv(rcvpkt) && corrupt(rcvpkt)`` corresponds to the event in which a packet is received and is found to be in error.

Protocol ``rdt2.0`` may look as if it works but, unfortunately, it has a fatal flaw.
- We haven’t accounted for the possibility that the ACK or NAK packet could be corrupted.
- Minimally, we will need to add checksum bits to ACK/NAK packets in order to detect such errors. 
- The more difficult question is how the protocol should recover from errors in ACK or NAK packets. The difficulty here is that if an ACK or NAK is corrupted, the sender has no way of knowing whether or not the receiver has correctly received the last piece of transmitted data.

Consider three possibilities for handling corrupted ACKs or NAKs:
1. The first possibility is inspired by a human dictation scenario. If the receiver's reply is not understood by the sender, the sender might ask for clarification. However, if the request for clarification itself gets corrupted, it creates a challenging situation of endless garbled exchanges.
2. The second alternative is to include enough checksum bits in the packets, allowing the sender to not only detect but also recover from bit errors. This approach solves the problem for a channel that corrupts packets but doesn't lose them.
3. The third approach is for the sender to resend the current data packet when it receives a garbled ACK or NAK packet. However, this introduces duplicate packets in the sender-to-receiver channel. The challenge with duplicate packets is that the receiver cannot determine if the ACK or NAK it previously sent was received correctly by the sender, making it difficult to distinguish between new data and retransmissions.
These three approaches highlight different strategies for handling corrupted ACKs or NAKs, each with its own limitations and challenges.

- A simple solution to this new problem, which is adopted in all existing data transfer protocols, including [[TCP]], is to add a new field to the data packet and have the sender its data packets by putting a **Sequence number** into this field. The receiving part then only have to check this **Sequence number** to determine if the packet received is a re-transmission pack.
- For this simple case of a stop-and-wait protocol, a 1-bit sequence number will suffice, since it will allow the receiver to know whether the sender is resending the previously transmitted packet the sequence number of the received packet has the same sequence number as the most recently received packet) or a new packet (the sequence number changes, moving “forward” in modulo-2 arithmetic).
	- Since we are currently assuming a channel that does not lose packets, ACK and NAK packets do not themselves need to indicate the sequence number of the packet they are acknowledging.
	- The sender knows that a received ACK or NAK packet (whether garbled or not) was generated in response to its most recently transmitted data packet.

- The figure 3.11 and 3.12 shom the FSM description for rdt2.1, which is our fixed version of rdt2.0.
- The rdt2.1 sender and receiver FSMS each now have twice as many states as before
	- the protocol state must now reflect whether the packet currently being sent or expected should have a sequence number of 0 or 1. 
	- Note that the actions in those states where a 0-numbered packet is being sent or expected are mirror images of those where a 1-numbered packet is being sent or expected; the only differences have to do with the handling of the sequence number.
- ![[Pasted image 20230519155613.png]]
- Protocol rdt2.1 uses both positive and negative acknowledgements form the receiver to the sender. 
- When an out-of-order packet is received, the receiver sends a positive acknowledgement for the packet it has received.
- When a corrupted packet is received, the receiver sends a negative acknowledgement. We can accomplish the same effect as a NAK if, instead of sending a NAK, we send an ACK for the last correctly received packet.
- ![[Pasted image 20230519155840.png]]
- A sender that receives two ACKs for the same packet (that is, receives duplicate ACKs) knows that the receiver did not correctly receive the packet following the packet that is being ACKed twice.
- Our NAK-free reliable data transfer protocol for a channel with bit errors is rdt2.2, shown in Figures 3.13 and 3.14. One subtle change between rtdt2.1 and rdt2.2 is that the receiver must now include the sequence number of the packet being acknowledged by an ACK message (this is done by including the ACK, 0 or ACK, 1 argument in make_pkt() in the receiver FSM), and the sender must now check the sequence number of the packet being acknowledged by a received ACK message (this is done by including the 0 or 1 argument in isACK() in the sender FSM).

**Reliable Data Transfer over a Lossy Channel with Bit Errors: rdt3.0** 
- 
- ![[Pasted image 20230519160015.png]]
- Suppose now that in addition to corrupting bits, the underlying channel can lose packets as well, a not-uncommon event in today’s computer networks
- Two additional concerns must now be addressed by the protocol: how to detect packet loss and what to do when packet loss occurs. The use of checksumming, sequence numbers, ACK packets, and re-transmissions -- the techniques, already developed in rdt2.2—will allow us to answer the latter concern. Handling the first concern will require adding a new protocol mechanism.
- There are many possible approaches toward dealing with packet loss
- Here, we’ll put the burden of detecting and recovering from lost packets on the sender. Suppose that the sender transmits a data packet and either that packet, or the receiver’s ACK of that packet, gets lost. In either case, no reply is forthcoming at the sender from the receiver.
- If the sender is willing to wait long enough so that it is certain that a packet has been lost, it can simply re-transmit the data packet. You should convince yourself that this protocol does indeed work.
- But how long must the sender wait to be certain that something has been lost? The sender must clearly wait at least as long as a round-trip delay between the sender and receiver (which may include buffering at intermediate routers) plus whatever amount of time is needed to process a packet at the receiver.
- In many networks, this worst-case maximum delay is very difficult even to estimate, much less know with certainty. Moreover, the protocol should ideally recover from packet loss as soon as possible; waiting for a worst-case delay could mean a long wait until error recovery is initiated. 
- The approach thus adopted in practice is for the sender to judiciously choose a time value such that packet loss is likely, although not guaranteed, to have happened. If an ACK is not received within this time, the packet is re-transmitted
	- Note that if a packet experiences a particularly large delay, the sender may retransmit the packet even though neither the data packet nor its ACK have been lost. This introduces the possibility of duplicate data packets in the sender-to-receiver channel. Happily, protocol rdt2.2 already has enough functionality (that is, sequence numbers) to handle the case of duplicate packets.
- ![[Pasted image 20230519160033.png]]
- The sender does not know whether a data packet was lost, an ACK was lost, or if the packet or ACK was simply overly delayed. In all cases, the action is the same: retransmit.
- Implementing a time-based retransmission mechanism requires a countdown timer that can interrupt the sender after a given amount of time has expired. The sender will thus need to be able to (1) start the timer each time a packet (either a first-time packet or a retransmission) is sent, (2) respond to a timer interrupt (taking appropriate actions), and (3) stop the timer.
- The figure 3.15 we see on the picture down below, shows the sender FSM for ``rdt3.0``, a protocol that reliably transfers data over a channel that can corrupt or lose packets. 
- ![[Pasted image 20230523180856.png]]
- Here is the receiver FSM for rtd3.0
- ![[Pasted image 20230523181011.png]]
- Lets now take a look at a protocol that operates with no lost or delayed packets and how it handles lost data packets. The times in this figure moves forward from the top of the diagram toward the bottom of the diagram. 
	- Note: a receive time for a packet is necessarily later than the send time for a packet as a result of transmission and propagation delays.
- Here is the model: ![[Pasted image 20230523181328.png]]
- Here we can see four scenarios:
	- the first scenario is where protocol goes smoothly, and operates with no packet loss.
	- the second scenario is where a packet is lost after the receiver sends ``ACK0`` , we see that there is a timeout, no ``ACK1`` is sent back from the receiver to the sender, and the sender then sends the ``pkt1`` , and picks up on the rest of the protocol. 
	- the thirds scenario is where we lose an ``ACK`` from the receiver, and the sender "times out" waiting for the ``ACK1``. When the sender does not receive the ACK message from the receiver, we resend the packet, assuming it was lost or not confirmed received. After resending the packet, the receiver detects a duplicate and resends the ``ACK1`` , and the rest of the protocol continues as usual.  
	- the fourth scenario is a premature timeout, where sender resends the ``pkt1`` and receives the ``ACK1`` from the receiver, it then alternates the sequence number and sends ``pkt0``, but right after is also receiving the ``ACK1`` again from the last packet. The sender then discards this ``ACK`` knowing its waiting for the ``ACK0`` for the last packet it sent. 
- In the Reliable Data Transfer protocol 3.0 (rdt3.0), the sender uses sequence numbers for each packet it sends and waits for an acknowledgement (ACK) before it sends the next packet. It also uses a timeout mechanism, retransmitting the packet if the ACK isn't received within a certain timeframe.
- ``rdt3.0`` is sometimes known as the **alternating-bit protocol**
	- packet sequence numbers alternates between 0 and 1. 

#### Pipelined Reliable Data Transfer Protocols
Protocol rdt3.0 is a functionally correct protocol, but it is unlikely that anyone would be happy with its performance, particularly in today’s high-speed networks. At the heart of rdt3.0’s performance problem is the fact that it is a stop-and-wait protocol.
To appreciate the performance impact of this stop-and-wait behavior, consider
an idealized case of two hosts, one located on the West Coast of the United States
and the other located on the East Coast, as shown here:
![[Pasted image 20230523184253.png]]
- The speed-of-light round-trip propagation delay between these two end systems, RTT, is approximately 30 milliseconds.
- Suppose that they are connected by a channel with a transmission rate, R, of 1 Gbps (10^9 bits per second).
- With a packet size, L, of 1,000 bytes (8,000 bits) per packet, including both header fields and data, the time needed to actually transmit the packet into the 1 Gbps link is:
- $d_{trans} = \frac L R = \frac{8000 bits}{(10^9 bits/sec)} = 8 microseconds$
- If we take a look at this picture, the sender begins sending the packet at ``t = 0``, then at ``t = L / R = 8 microseconds``, the last but enters the channel at the sender side. 
- The packet then makes its 15-msec cross-country journey, with the last but of the packet emerging at the receiver at ``t = RTT/2 + L/R = 15.008 msec`` 
- Figure: ![[Pasted image 20230523185540.png]]
- Assuming for simplicity that ACK packets are extremely small (so that we can ignore their transmission time) and that the receiver can send an ACK as soon as the last bit of a data packet is received, the ACK emerges back at the sender at 
	- ``t = RTT + L/R = 30.008 msec.``
- At this point, the sender can now transmit the next message. Thus, in 30.008 msec, the sender was sending for only 0.008 msec.
- If we define the utilization of the sender (or the channel) as the fraction of time the sender is actually busy sending bits into the channel, the analysis in Figure 3.18(a) shows that the stop-and-wait protocol has a rather dismal sender utilization, $U_{sender}$  of:
	- $U_{sender}=\frac{L/R}{RTT + L/R}=\frac{.008}{30.008}=0.00027$
	- That is, the sender was busy only 2.7 hundredths of one percent of the time!
	- Viewed another way, the sender was able to send only 1,000 bytes in 30.008 milliseconds, an effective throughput of only 267 kbps—even though a 1 Gbps link was available!
	- Imagine the unhappy network manager who just paid a fortune for a gigabit capacity link but manages to get a throughput of only 267 kilobits per second!
- The solution to this particular performance problem is simple: Rather than operate in a stop-and-wait manner, the sender is allowed to send multiple packets without waiting for acknowledgments. 
Since the many in-transit sender-to-receiver packets can be visualized as filling a pipeline, this technique is known as pipelining. Pipelining has the following consequences for reliable data transfer protocols:
- The range of sequence numbers must be increased, since each in-transit packet (not counting retransmissions) must have a unique sequence number and there may be multiple, in-transit, unacknowledged packets.
- The sender and receiver sides of the protocols may have to buffer more than one packet. Minimally, the sender will have to buffer packets that have been transmitted but not yet acknowledged. Buffering of correctly received packets may also be needed at the receiver, as discussed below.
- The range of sequence numbers needed and the buffering requirements will depend on the manner in which a data transfer protocol responds to lost, corrupted, and overly delayed packets. Two basic approaches toward pipelined error recovery can be identified: Go-Back-N and selective repeat.

#### Go-Back-N (GBN)
The Go-Back-N (GBN) protocol is a sliding window protocol used in networks for error control. It's often used in cases where reliable delivery is required, such as in the Transmission Control Protocol (TCP). The key idea behind GBN is that it allows the sender to transmit multiple packets without waiting for an acknowledgment (ACK), but imposes a limit on the number of such unacknowledged packets.

Here are some important points about GBN:
- **Window Size**: In GBN, the sender maintains a window of packets to be sent. The window size defines the maximum number of packets that can be unacknowledged by the receiver. The window moves forward when the sender receives an ACK from the receiver.
- **Packet Sending**: The sender continuously sends packets until it has exhausted the window size. The sender must then wait until it receives an ACK from the receiver before it can send new packets.
- **Acknowledgment**: When the receiver correctly receives a packet, it sends an ACK back to the sender. The ACK number tells the sender the sequence number of the next packet the receiver expects.
- **Packet Loss or Error**: If a packet is lost or corrupted during transmission, the receiver does not acknowledge receipt of that packet or any packet sent after it. When the sender detects the loss (via a timeout or missing ACK), it resends all packets starting from the lost or corrupted one, hence the name "Go-Back-N".
- **ACK Loss**: If an ACK is lost in transmission, the sender will not be able to advance its window. After a timeout period, the sender will retransmit the packets for which it has not received an ACK, starting from the earliest one in the window.
- **Ordering of packets**: GBN ensures the correct order of packets as the receiver only accepts the packets in the right order and discards any out-of-order packet.

This is a simple, yet powerful protocol that allows for the efficient use of network resources while ensuring reliable delivery. However, its performance can degrade significantly on networks with high error rates, as a single packet loss will result in the retransmission of many packets. It also may not fully utilize the network's capacity if the window size is too small relative to the network's bandwidth-delay product.

In **GBN** protocol, the sender is allowed to transmit multiple packets (when available) without waiting for an acknowledgment, but is constrained to have no more than maximum allowable number, ``N`` , of unacknowledged packets in the pipeline. 

The sender’s view of the range of sequence numbers in a GBN protocol:
![[Pasted image 20230523205052.png]]
- If we define ``base`` to be the sequence number of the oldest unacknowledged packet and ``nextseqnum`` to be the smallest unused sequence number (that is, the sequence number of the next packet to be sent), then four intervals in the range of sequence numbers can be identified.
- Sequence numbers in the interval ``[0,base-1]`` correspond to packets that have already been transmitted and acknowledged. The interval ``[base,nextseqnum-1]`` corresponds to packets that have been sent but not yet acknowledged.
- Sequence numbers in the interval ``[nextseqnum,base+N-1]`` can be used for packets that can be sent immediately, should data arrive from the upper layer.
- Finally, sequence numbers greater than or equal to ``base+N`` cannot be used until an unacknowledged packet currently in the pipeline (specifically, the packet with sequence number base) has been acknowledged.
- As we see from the picture, the range of permissible sequence numbers for transmitted but not yet acknowledged packets can be viewed as a window of size ``N`` over the range of sequence numbers.
- As the protocol operates, this window slides forward over the sequence number space. For this reason, N is often referred to as the window size and the GBN protocol itself as a sliding-window protocol.
- The number of outstanding unacknowledged packets is not unlimited due to flow control, which you can read about in TCP congestion control.
- In practice, a packet’s sequence number is carried in a fixed-length field in the packet header. If k is the number of bits in the packet sequence number field, the range of sequence numbers is thus ``[0,2^k - 1]``.
- With a finite range of sequence numbers, all arithmetic involving sequence numbers must then be done using modulo $2^k$ arithmetic.
- Recall that rdt3.0 had a 1-bit sequence number and a range of sequence numbers of ``[0,1]``.
	- we will explore the consequences of a finite range of sequence numbers further down.
- Figures 3.20 and 3.21 give an extended FSM description of the sender and receiver sides of an ACK-based, NAK-free, GBN protocol:
![[Pasted image 20230523210736.png]]
![[Pasted image 20230523210753.png]]
- We refer to this FSM description as an extended FSM because we have added variables (similar to programming-language variables) for ``base`` and ``nextseqnum``, and added operations on these variables and conditional actions involving these variables.
	- Note: the extended FSM specification is now beginning to look somewhat like a programming-language specification.

**The GBN sender must respond to three types of events:**
- Invocation from above.
	- When ``rdt_send()`` is called from above, the sender first checks to see if the window is full, that is, whether there are ``N`` outstanding, unacknowledged packets.
	- If the window is not full, a packet is created and sent, and variables are appropriately updated.
	- If the window is full, the sender simply returns the data back to the upper layer, an implicit indication that the window is full. The upper layer would presumably then have to try again later.
- Receipt of an ACK.
	- In our GBN protocol, an acknowledgment for a packet with sequence number n will be taken to be a cumulative acknowledgment, indicating that all packets with a sequence number up to and including n have been correctly received at the receiver.
-  A timeout event.
	- The protocol’s name, “Go-Back-N,” is derived from the sender’s behavior in the presence of lost or overly delayed packets.
	- As in the stop-and-wait protocol, a timer will again be used to recover from lost data or acknowledgment packets.
	- If a timeout occurs, the sender resends all packets that have been previously sent but that have not yet been acknowledged.
	- Our sender in Figure 3.20 uses only a single timer, which can be thought of as a timer for the oldest transmitted but not yet acknowledged packet.
	- If an ACK is received but there are still additional transmitted but not yet acknowledged packets, the timer is restarted.
	- If there are no outstanding, unacknowledged packets, the timer is stopped.

The receiver’s actions in GBN are also simple. If a packet with sequence number ``n`` is received correctly and is in order (that is, the data last delivered to the upper layer came from a packet with sequence number ``n - 1``), the receiver sends an ACK for packet ``n`` and delivers the data portion of the packet to the upper layer.
In all other cases, the receiver discards the packet and resends an ACK for the most recently received in-order packet. Note that since packets are delivered one at a time to the upper layer, if packet ``k`` has been received and delivered, then all packets with a sequence number lower than ``k`` have also been delivered. Thus, the use of cumulative acknowledgments is a natural choice for GBN.

In our GBN protocol, the receiver discards out-of-order packets. Although it may seem silly and wasteful to discard a correctly received (but out-of-order) packet, there is some justification for doing so. Recall that the receiver must deliver data in order to the upper layer.

Suppose now that packet n is expected, but packet ``n + 1`` arrives. Because data must be delivered in order, the receiver could buffer (save) packet ``n + 1`` and then deliver this packet to the upper layer after it had later received and delivered packet ``n``.

However, if packet n is lost, both it and packet ``n + 1`` will eventually be retransmitted as a result of the GBN retransmission rule at the sender. Thus, the receiver can simply discard packet ``n + 1``.
The advantage of this approach is the simplicity of receiver buffering—the receiver need not buffer any out-of-order packets. Thus, while the sender must maintain the upper and lower bounds of its window and the position of ``nextseqnum`` within this window, the only piece of information the receiver need maintain is the sequence number of the next in-order packet. 
- This value is held in the variable ``expectedseqnum``, shown in the receiver FSM in Figure 3.21.
- Of course, the disadvantage of throwing away a correctly received packet is that the subsequent retransmission of that packet might be lost or garbled and thus even more retransmissions would be required.
- Figure 3.22 shows the operation of the GBN protocol for the case of a window size of four packets. Because of this window size limitation, the sender sends packets 0 through 3 but then must wait for one or more of these packets to be acknowledged before proceeding.
![[Pasted image 20230523212503.png]]
- As each successive ACK (for example, ``ACK0`` and ``ACK1``) is received, the window slides forward and the sender can transmit one new packet (``pkt4`` and ``pkt5``, respectively).
- On the receiver side, packet 2 is lost and thus packets 3, 4, and 5 are found to be out of order and are discarded.
- Note here that the GBN protocol incorporates almost all of the techniques that we will encounter when we study the reliable data transfer components of TCP
	- These techniques include the use of sequence numbers, cumulative acknowledgments, checksums, and a timeout/retransmit operation.

#### Selective Repeat
When using GBN there are certain scenarios that we encounter that makes it suffer from performance problems. When the window size and bandwidth-delay product are both large, many packets in the pipeline, which means a single packet error can cause GBN to retransmit a large number of packets, many unnecessarily. 
This might cause a pipeline full of retransmitted packets that slow the protocol down. 

Selective-repeat protocols avoid unnecessary retransmissions by having the sender retransmit only those packets that it suspects were received in error (that is, were lost or corrupted) at the receiver.
This individual, as-needed, retransmission will require that the receiver individually acknowledge
correctly received packets. 
- A window size of N will again be used to limit the number of outstanding, unacknowledged packets in the pipeline.
- However, unlike GBN, the sender will have already received ACKs for some of the packets in the window.
- Figure 3.23 shows the SR sender’s view of the sequence number space. Figure 3.24 details the various actions taken by the SR sender.
- 
  ![[Pasted image 20230523213531.png]]
  - The SR receiver will acknowledge a correctly received packet whether or not it is in order.
  - Out-of-order packets are buffered until any missing packets (that is, packets with lower sequence numbers) are received, at which point a batch of packets can be delivered in order to the upper layer.
  - Figure 3.25 itemizes the various actions taken by the SR receiver.
![[Pasted image 20230523213715.png]]
- Figure 3.26 shows an example of SR operation in the presence of lost packets. Note that in Figure 3.26, the receiver initially buffers packets 3, 4, and 5, and delivers them together with packet 2 to the upper layer when packet 2 is finally received.
![[Pasted image 20230523213817.png]]
- It is important to note that in Step 2 in Figure 3.25, the receiver reacknowledges (rather than ignores) already received packets with certain sequence numbers below the current window base.
- Given the sender and receiver sequence number spaces in Figure 3.23, for example, if there is no ACK for packet send_base propagating from the receiver to the sender, the sender will eventually retransmit packet send_base, even though it is clear (to us, not the sender!) that the receiver has already received that packet.
- If the receiver were not to acknowledge this packet, the sender’s window would never move forward!
- This example illustrates an important aspect of SR protocols (and many other protocols as well).
- The sender and receiver will not always have an identical view of what has been received correctly and what has not. For SR protocols, this means that the sender and receiver windows will not always coincide.
- The lack of synchronization between sender and receiver windows has important consequences when we are faced with the reality of a finite range of sequence numbers.
- Consider what could happen, for example, with a finite range of four packet sequence numbers, 0, 1, 2, 3, and a window size of three. Suppose packets 0 through 2 are transmitted and correctly received and acknowledged at the receiver. At this point, the receiver’s window is over the fourth, fifth, and sixth packets, which have sequence numbers 3, 0, and 1, respectively.
- Now consider two scenarios. In the first scenario, shown in Figure 3.27(a), the ACKs for the first three packets are lost and the sender retransmits these packets. The receiver thus next receives a packet with sequence number 0—a copy of the first packet sent.
- In the second scenario, shown in Figure 3.27(b), the ACKs for the first three packets are all delivered correctly. The sender thus moves its window forward and sends the fourth, fifth, and sixth packets, with sequence numbers 3, 0, and 1, respectively. The packet with sequence number 3 is lost, but the packet with sequence number 0 arrives—a packet containing new data.
- ![[Pasted image 20230523215501.png]]
- Now consider the receiver’s viewpoint in Figure 3.27, which has a figurative curtain between the sender and the receiver, since the receiver cannot “see” the actions taken by the sender. All the receiver observes is the sequence of messages it receives from the channel and sends into the channel.
- As far as it is concerned, the two scenarios in Figure 3.27 are identical. There is no way of distinguishing the retransmission of the first packet from an original transmission of the fifth packet.
- Clearly, a window size that is 1 less than the size of the sequence number space won’t work. But how small must the window size be? A problem at the end of the chapter asks you to show that the window size must be less than or equal to half the size of the sequence number space for SR protocols.

Let’s conclude our discussion of reliable data transfer protocols by considering
one remaining assumption in our underlying channel model. Recall that we
have assumed that packets cannot be reordered within the channel between the
sender and receiver. This is generally a reasonable assumption when the sender and
receiver are connected by a single physical wire. However, when the “channel”
connecting the two is a network, packet reordering can occur. One manifestation of
packet reordering is that old copies of a packet with a sequence or acknowledgment
number of x can appear, even though neither the sender’s nor the receiver’s window
contains x. With packet reordering, the channel can be thought of as essentially
buffering packets and spontaneously emitting these packets at any point in
the future.  Because sequence numbers may be reused, some care must be taken to
guard against such duplicate packets. The approach taken in practice is to ensure
that a sequence number is not reused until the sender is “sure” that any previously
sent packets with sequence number x are no longer in the network. This is done
by assuming that a packet cannot “live” in the network for longer than some fixed
maximum amount of time. A maximum packet lifetime of approximately three
minutes is assumed in the TCP extensions for high-speed networks [RFC 7323](https://www.rfc-editor.org/rfc/rfc7323).
``[Sunshine 1978]`` describes a method for using sequence numbers such that reordering
problems can be completely avoided.
![[Pasted image 20230523215850.png]]

## Connection-Oriented Transport: TCP
Now that we have covered the underlying principles of reliable data transfer,
let’s turn to TCP—the Internet’s transport-layer, connection-oriented, reliable
transport protocol. In this section, we’ll see that in order to provide reliable
data transfer, TCP relies on many of the underlying principles discussed in
the previous section, including error detection, retransmissions, cumulative
acknowledgments, timers, and header fields for sequence and acknowledgment
numbers. TCP is defined in RFC 793, RFC 1122, RFC 2018, RFC 5681, and
RFC 7323.

### The TCP Connection
We say that [[TCP]] is **connection-oriented** because before an application process can begin to send data, the two processes must do the handshake. The handshake is a exchange of preliminary segments to each other to establish the parameters of the coming data transfer.

As part of [[TCP]] connection establishment, both sides of the connection will initialize many TCP state variables associated with the TCP connection.
The TCP “connection” is not an end-to-end TDM or FDM circuit as in a circuit-switched
network. Its a logical connection, where the common state reside only in the TCPs two communicating end systems.

Recall that because the [[TCP]] protocol runs only in the end systems and not in the intermediate network elements (routers and link-layer switches), the intermediate network elements do
not maintain [[TCP]] connection state. In fact, the intermediate routers are completely
oblivious to [[TCP]] connections; they see datagrams, not connections.

A TCP connection provides a full-duplex service: If there is a TCP connection between Process A on one host and Process B on another host, then application-layer data can flow from Process A to Process B at the same time as application-layer data flows from Process B to Process A.

A TCP connection is also always point-to-point, that is, between a single sender and a single
receiver. So-called “multicasting” (see the online supplementary materials for this text)—the transfer of data from one sender to many receivers in a single send operation—is not possible with TCP. With TCP, two hosts are company and three are a crowd!

How a TCP connection is established:
- a process running in one host wants to initiate a connection with another process in another host.
- the process that is initiating the connection is called the client process, while the other process is called the server process.
- The client application process first informs the client transport layer that it wants to establish a connection to a process in the server.
	- Python client program does this by issuing the command
	- ``clientSocket.connect((serverName,serverPort))``
	- where ``serverName`` is the name of the server and ``serverPort`` identifies the process on the server.
- [[TCP]] in the client then proceeds to establish a TCP connection with TCP in the server.
- The server responds with a second special TCP segment. 
- and finally the client responds again with a third special segment!
- The first two segments carry no payload, that is, no application-layer data; the third of these segments may carry a payload.
- Because three segments are sent between the two hosts, this connection-establishment procedure is often referred to as a [[TCP|three-way handshake]].
- Once a TCP connection is established, the two application processes can send data to each other.

Now lets consider the sending of data from the client process to the server process. The client process passes a stream of data through the socket(the door). Once the data passes through the door, the data is in the hands of TCP running in the client. 
![[Pasted image 20230523221341.png]]
As shown in Figure 3.28, TCP directs this data to the connection’s send buffer, which is one of the buffers that is set aside during the initial three-way handshake.
From time to time, TCP will grab chunks of data from the send buffer and pass the data to the network layer.
- Interestingly, the TCP specification [RFC 793] is very laid back about specifying when TCP should actually send buffered data, stating that TCP should “send that data in segments at its own convenience.”

The maximum amount of data that can be grabbed and placed in a segment is limited by the maximum segment size (**MSS**).

The MSS is typically set by first determining the length of the largest link-layer frame that can be sent by the local sending host (the so-called maximum transmission unit, MTU), and then setting the MSS to ensure that a TCP segment (when encapsulated in an IP datagram) plus the TCP/IP header length (typically 40 bytes) will fit into a single link-layer frame.
- Both Ethernet and PPP link-layer protocols have an MTU of 1,500 bytes.
- Thus, a typical value of MSS is 1460 bytes

Note that the MSS is the maximum amount of application-layer data in the segment, not the maximum size of the TCP segment including headers. 

TCP pairs each chunk of client data with a TCP header, thereby forming TCP
segments.
- The segments are passed down to the network layer, where they are separately encapsulated within network-layer IP datagrams
- The IP datagrams are then sent into the network. When TCP receives a segment at the other end, the segment’s data is placed in the TCP connection’s receive buffer, as shown in Figure 3.28
- The application reads the stream of data from this buffer. Each side of the connection has its own send buffer and its own receive buffer.

We see from this segment that a TCP connection consists of buffers, variables, and a socket connection to a process in one host, and another set of buffers, variables, and a socket connection to a process in another host. As mentioned earlier, no buffers or variables are allocated to the connection in the network elements (routers, switches, and repeaters) between the hosts.

### TCP Segment Structure
We will take a look at the TCP segment structure.
The TCP segment consists of [[WEB Requests#General Headers|header fields]] and a data field. The data field contains a chunk of application data. The MSS limits the maximum size of a segment’s data field. When TCP sends a large file, such as an image as part of a Web page, it typically breaks the file into chunks of size MSS (except for the last chunk, which will often be less than the MSS).
Interactive applications, however, often transmit data chunks that are smaller than the MSS
- for example, with remote login applications such as Telnet and ssh, the data field in the TCP segment is often only one byte.
- Because the TCP header is typically 20 bytes (12 bytes more than the [[UDP]] header), segments sent by Telnet and ssh may be only 21 bytes in length.
The structure of the TCP segment:
![[Pasted image 20230523222546.png]]
- As with UDP, the header includes source and destination port numbers, which are used for multiplexing/demultiplexing data from/to upper-layer applications.
- Also, as with UDP, the header includes a checksum field.

A TCP segment header also contains the following fields:
- The 32-bit sequence number field and the 32-bit acknowledgment number field are used by the TCP sender and receiver in implementing a reliable data transfer service. 
- The 16-bit receive window field is used for flow control.
- The 4-bit header length field specifies the length of the TCP header in 32-bit words. The TCP header can be of variable length due to the [[TCP]] options field. (Typically, the options field is empty, so that the length of the typical TCP header is 20 bytes.)
- The optional and variable-length options field is used when a sender and receiver negotiate the maximum segment size (MSS) or as a window scaling factor for use in high-speed networks. A time-stamping option is also defined. See RFC 854 and RFC 1323 for additional details.
- The flag field contains 6 bits. The ACK bit is used to indicate that the value carried in the acknowledgment field is valid; that is, the segment contains an acknowledgment for a segment that has been successfully received. The RST, SYN, and FIN bits are used for connection setup and teardown. The CWR and ECE bits are used in explicit congestion notification. Setting the PSH bit indicates that the receiver should pass the data to the upper layer immediately. Finally, the URG bit is used to indicate that there is data in this segment that the sending-side upperlayer entity has marked as “urgent.” The location of the last byte of this urgent data is indicated by the 16-bit urgent data pointer field. TCP must inform the receiving-side upper-layer entity when urgent data exists and pass it a pointer to the end of the urgent data. (In practice, the PSH, URG, and the urgent data pointer are not used. However, we mention these fields for completeness.)

#### Sequence Numbers and Acknowledgment Numbers
Two of the most important fields in the TCP segment header are the sequence number
field and the acknowledgment number field. These fields are a critical part of TCP’s
reliable data transfer service.
But before discussing how these fields are used to provide reliable data transfer, let us first explain what exactly TCP puts in these fields.

TCP views data as an unstructured, but ordered, stream of bytes. TCP’s use of sequence numbers reflects this view in that sequence numbers are over the stream of transmitted bytes and not over the series of transmitted segments. The sequence number for a segment is therefore the byte-stream number of the first byte in the segment.

**Example:**
Suppose that a process in Host A wants to send a stream of data to a process in Host B over a TCP connection. The TCP in Host A will implicitly number each byte in the data stream. Suppose that the data stream consists of a file consisting of 500,000 bytes, that the MSS is 1,000 bytes, and that the first byte of the data stream is numbered 0.

As shown here:
![[Pasted image 20230523223421.png]]
TCP constructs 500 segments out of the data stream. The first segment gets assigned sequence number 0, the second segment gets assigned sequence number 1,000, the third segment gets assigned sequence number 2,000, and so on. Each sequence number is inserted in the sequence number field in the header of the appropriate TCP segment

Now let’s consider acknowledgment numbers. These are a little trickier than
sequence numbers.
- Recall that TCP is full-duplex, so that Host A may be receiving data from Host B while it sends data to Host B (as part of the same TCP connection).
- Each of the segments that arrive from Host B has a sequence number for the data flowing from B to A.
- *The acknowledgment number that Host A puts in its segment is the sequence number of the next byte Host A is expecting from Host B.*

Another example:
- Suppose that Host A has received all bytes numbered 0 through 535 from B and suppose that it is about to send a segment to Host B. Host A is waiting for byte 536 and all the subsequent bytes in Host B’s data stream. So Host A puts 536 in the acknowledgment number field of the segment it sends to B.
And another example:
- suppose that Host A has received one segment from Host B containing bytes 0 through 535 and another segment containing bytes 900 through 1,000. For some reason Host A has not yet received bytes 536 through 899. In this example, Host A is still waiting for byte 536 (and beyond) in order to re-create B’s data stream. Thus, A’s next segment to B will contain 536 in the acknowledgment number field. Because TCP only acknowledges bytes up to the first missing byte in the stream, TCP is said to provide **cumulative acknowledgments**.
This last example also brings up an important but subtle issue:
- Host A received the third segment (bytes 900 through 1,000) before receiving the second segment (bytes 536 through 899). Thus, the third segment arrived out of order.
- The subtle issue is:
	- What does a host do when it receives out-of-order segments in a TCP connection? Interestingly, the TCP RFCs do not impose any rules here and leave the decision up to the programmers implementing a TCP implementation.
- There are basically two choices:
	- either (1) the receiver immediately discards out-of-order segments (which, as we discussed earlier, can simplify receiver design)
	- or (2) the receiver keeps the out-of-order bytes and waits for the missing bytes to fill in the gaps. Clearly, the latter choice is more efficient in terms of network bandwidth, and is the approach taken in practice.
In Figure 3.30, we assumed that the initial sequence number was zero. In truth,
both sides of a TCP connection randomly choose an initial sequence number. This
is done to minimize the possibility that a segment that is still present in the network
from an earlier, already-terminated connection between two hosts is mistaken for a
valid segment in a later connection between these same two hosts (which also happen
to be using the same port numbers as the old connection)


#### Telnet: A Case Study for Sequence and Acknowledgment Numbers
Telnet, defined in RFC 854, is a popular application-layer protocol used for remote
login. It runs over TCP and is designed to work between any pair of hosts. Unlike the
bulk data transfer applications discussed in the [[Application Layer]]. 

Telnet is an interactive application. We discuss a Telnet example here, as it nicely illustrates TCP sequence and acknowledgment numbers. We note that many users now prefer to use the SSH protocol rather than Telnet, since data sent in a Telnet connection (including passwords!)
are not encrypted, making Telnet vulnerable to eavesdropping attacks. 

Suppose Host A initiates a Telnet session with Host B:
- Because Host A initiates the session, it is labeled the client, and Host B is labeled the server.
- Each character typed by the user (at the client) will be sent to the remote host; the remote host will send back a copy of each character, which will be displayed on the Telnet user’s screen.
- This “echo back” is used to ensure that characters seen by the Telnet user have already been received and processed at the remote site.
- Each character thus traverses the network twice between the time the user hits the key and the time the character is displayed on the user’s monitor.
- Now suppose the user types a single letter, ‘C,’ and then grabs a coffee. Let’s examine the TCP segments that are sent between the client and server.
- As shown in Figure 3.31, we suppose the starting sequence numbers are 42 and 79 for the client and server, respectively
![[Pasted image 20230523224600.png]]
- Recall that the sequence number of a segment is the sequence number of the first byte in the data field. Thus, the first segment sent from the client will have sequence number 42; the first segment sent from the server will have sequence number 79
- Recall that the acknowledgment number is the sequence number of the next byte of data that the host is waiting for.
- After the TCP connection is established but before any data is sent, the client is waiting for byte 79 and the server is waiting for byte 42.
- As shown in Figure 3.31, three segments are sent:
	- The first segment is sent from the client to the server, containing the 1-byte ASCII representation of the letter ‘C’ in its data field. This first segment also has 42 in its sequence number field, as we just described. Also, because the client has not yet received any data from the server, this first segment will have 79 in its acknowledgment number field.
	- The second segment is sent from the server to the client. It serves a dual purpose. First it provides an acknowledgment of the data the server has received. By putting 43 in the acknowledgment field, the server is telling the client that it has successfully received everything up through byte 42 and is now waiting for bytes 43 onward.
		- The second purpose of this segment is to echo back the letter ‘C.’ Thus, the second segment has the ASCII representation of ‘C’ in its data field.
		- This second segment has the sequence number 79, the initial sequence number of the server-to-client data flow of this TCP connection, as this is the very first byte of data that the server is sending.
		- Note that the acknowledgment for client-to-server data is carried in a segment carrying server-to-client data; this acknowledgment is said to be piggybacked on the server-to-client data segment.
	- The third segment is sent from the client to the server. Its sole purpose is to acknowledge the data it has received from the server. This segment has an empty data field (that is, the acknowledgment is not being piggybacked with any client-to-server data).The segment has 80 in the acknowledgment number field because the client has received the stream of bytes up through byte sequence number 79 and it is now waiting for bytes 80 onward.
		- You might think it odd that this segment also has a sequence number since the segment contains no data. But because [[TCP]] has a sequence number field, the segment needs to have some sequence number.

### Round-Trip Time Estimation and Timeout
TCP (like our ``rdt`` protocol) uses a timeout/retransmit mechanism to recover from lost segments. Even thou this is a simple concept, we encounter lots of subtle issues when we implement timeout/rentransmit mechanisms in a protocol such as [[TCP]]. 

Some questions:
- how long is the length of these intervals?
- How do we estimate RTT in a protocol implementing these protocols?
- Should a timer be associated with each and every unacknowledged segment?

Lets dive into them!

#### Estimating the Round-Trip Time
We begin by considering how TCP estimates the round-trip time between sender and receiver. We accomplish this as following:
- The sample RTT, denoted ``SampleRTT``, for a segment is the amount of time between when the segment is sent (that is, passed to IP) and when an acknowledgment for the segment is received.
- Instead of measuring a ``SampleRTT`` for every transmitted segment, most TCP implementations take only one ``SampleRTT`` measurement at a time.
- That is, at any point in time, the ``SampleRTT`` is being estimated for only one of the transmitted but currently unacknowledged segments, leading to a new value of ``SampleRTT`` approximately once every RTT
- Also, TCP never computes a ``SampleRTT`` for a segment that has been retransmitted; it only measures ``SampleRTT`` for segments that have been transmitted once. 
- Obviously, the ``SampleRTT`` values will fluctuate from segment to segment due to congestion in the routers and to the varying load on the end systems. Because of this fluctuation, any given ``SampleRTT`` value may be atypical. 
- In order to estimate a typical RTT, it is therefore natural to take some sort of average of the ``SampleRTT`` values. [[TCP]] maintains an average, called ``EstimatedRTT``, of the ``SampleRTT`` values.
- Upon obtaining a new`` SampleRTT``, [[TCP]] updates ``EstimatedRTT`` according to the following formula:
	- ``EstimatedRTT = (1 – α) * EstimatedRTT + α * SampleRTT``
- The formula above is written in the form of a programming-language statement—the new value of ``EstimatedRTT`` is a weighted combination of the previous value of ``EstimatedRTT`` and the new value for ``SampleRTT``. 
- The recommended value of α is α = 0.125 (that is, 1/8) ``[RFC 6298]``, in which case the formula above becomes:
	- ``EstimatedRTT = 0.875 * EstimatedRTT + 0.125 * SampleRTT``
- Note that ``EstimatedRTT`` is a weighted average of the ``SampleRTT`` values. 


#### Setting and Managing the Retransmission Timeout Interval
Given values of ``EstimatedRTT`` and ``DevRTT``, what value should be used for [[TCP]]’s timeout interval? 

Clearly, the interval should be greater than or equal to ``EstimatedRTT``, or unnecessary retransmissions would be sent. But the timeout interval should not be too much larger than ``EstimatedRTT``; otherwise, when a segment is lost, TCP would not quickly retransmit the segment, leading to large data transfer delays.

It is therefore desirable to set the timeout equal to the ``EstimatedRTT`` plus some margin. The margin should be large when there is a lot of fluctuation in the ``SampleRTT`` values; it should be small when there is little fluctuation. The value of ``DevRTT`` should thus come into play here. All of these considerations are taken into account in TCP’s method for determining the retransmission timeout interval:
- ``TimeoutInterval = EstimatedRTT + 4 * DevRTT `` 
An initial ``TimeoutInterval`` value of 1 second is recommended. 
When a timeout occurs, the value of ``TimeoutInterval`` is doubled to avoid a premature timeout occurring for a subsequent segment that will soon be acknowledged. However, as soon as a segment is received and ``EstimatedRTT`` is updated, the ``TimeoutInterval`` is again computed using the formula above.
![[Pasted image 20230523231005.png]]



### Reliable Data Transfer

>TCP implements rdt on top of IP

As we recall, we remember that the Internet’s network-layer service (IP service) is unreliable. IP does
not guarantee datagram delivery, does not guarantee in-order delivery of datagrams,
and does not guarantee the integrity of the data in the datagrams. With IP service, datagrams can overflow router buffers and never reach their destination, datagrams can arrive out of order, and bits in the datagram can get corrupted (flipped from 0 to 1 and vice versa).
Because transport-layer segments are carried across the network by IP datagrams, transport-layer segments can suffer from these problems as well.

TCP creates a reliable data transfer service on top of IP’s unreliable besteffort service. TCP’s reliable data transfer service ensures that the data stream that a process reads out of its TCP receive buffer is uncorrupted, without gaps, without duplication, and in sequence; that is, the byte stream is exactly the same byte stream that was sent by the end system on the other side of the connection.

In our earlier development of reliable data transfer techniques, it was conceptually easiest to assume that an individual timer is associated with each transmitted but not yet acknowledged segment. While this is great in theory, timer management can require considerable overhead. Thus, the recommended TCP timer management procedures ``[RFC 6298]`` use only a single retransmission timer, even if there are multiple transmitted but not yet acknowledged segments. The TCP protocol described in this section follows this single-timer recommendation.

We will look at how [[TCP]] provides reliable data transfer in two incremental steps:

Step 1: Timeout-Based Retransmission:
- If a timer expires (timeout event), TCP assumes that the previously sent segment was lost and retransmits it. The segment with the smallest sequence number among the not-yet-acknowledged segments is retransmitted.
- Upon retransmission, TCP restarts the timer to account for potential future timeouts.

Step 2: Duplicate Acknowledgment-Based Retransmission:
- When an acknowledgment (ACK) segment is received from the receiver, TCP compares the ACK value (denoted as y) with its SendBase variable, which represents the sequence number of the oldest unacknowledged byte.
- If y > SendBase, it means that the receiver is acknowledging one or more previously unacknowledged segments. TCP updates its SendBase variable accordingly.
- If there are still not-yet-acknowledged segments after updating SendBase, TCP restarts the timer to ensure timely retransmission.

These steps allow TCP to recover from lost segments and ensure reliable data transfer by retransmitting lost segments based on timeouts or duplicate acknowledgments. The code snippet you provided demonstrates a simplified TCP sender implementation that follows these steps.

**TCP timer management**
It uses only a single retransmission timer, even if there are multiple transmitted but not yet acknowledged segments.

Major events related to data transmission
- Data received from the application
- Timer timeout
- ACK receipt

**Actions after data received from the application**
- TCP (eventually) encapsulates the data in a segment, and passes the segment to IP.
- If the timer is not running, TCP starts the timer.

**Actions after Timer timeout**
- TCP retransmit the segment that caused the timeout.
- TCP then restarts the timer.
- 
#### Fast Retransmit
Fast Retransmit is a technique used by TCP to mitigate the delay caused by timeout-triggered retransmissions. Instead of waiting for the timeout period to expire, the sender can detect packet loss earlier by observing duplicate ACKs. A duplicate ACK is an acknowledgment that acknowledges a segment the sender has already received an acknowledgment for. When the sender receives three duplicate ACKs for the same data, it assumes that the following segment has been lost. In response, it performs a fast retransmit by retransmitting the missing segment before its timer expires

The receiver generates duplicate ACKs when it detects a gap in the data stream, indicating a missing segment. By reacknowledging the last in-order byte of data it has received, the receiver provides feedback to the sender. If the sender receives three duplicate ACKs, it triggers a fast retransmit to recover the lost segment.

#### Go-Back-N or Selective Repeat?
TCP's error-recovery mechanism is best categorized as a hybrid of Go-Back-N (GBN) and Selective Repeat (SR) protocols.

At first glance, TCP may appear to resemble a GBN-style protocol because TCP acknowledgments are cumulative and out-of-order segments are not individually acknowledged by the receiver. TCP only needs to maintain the smallest sequence number of an unacknowledged byte (SendBase) and the sequence number of the next byte to be sent (NextSeqNum), similar to GBN.

However, there are notable differences between TCP and Go-Back-N. TCP implementations often buffer correctly received but out-of-order segments, which is not typical in GBN. Additionally, in scenarios where a sequence of segments (1, 2, ..., N) is sent by the sender and an acknowledgment for packet n (where n is not equal to N) gets lost, TCP would retransmit at most one segment, specifically segment n. In contrast, Go-Back-N would retransmit all subsequent packets (n + 1, n + 2, ..., N).

The proposed modification to TCP called selective acknowledgment allows the receiver to acknowledge out-of-order segments selectively rather than cumulatively acknowledging only the last correctly received in-order segment. When combined with selective retransmission, where the retransmission of already selectively acknowledged segments is skipped, TCP exhibits characteristics similar to a generic Selective Repeat protocol (SR).

Hence, TCP's error-recovery mechanism can be considered a hybrid of GBN and SR protocols, leveraging aspects from both to optimize its performance in different scenarios.


### Flow Control
