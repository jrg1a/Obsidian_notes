TCP stands for Transmission Control Protocol. It is a connection-oriented protocol that operates at the transport layer of the Internet Protocol Suite. TCP provides reliable, ordered, and error-checked delivery of data between applications over a network.

Here are some key characteristics of TCP:
1.  Connection-oriented: TCP establishes a connection between the sender and receiver before transferring data. This connection is a logical pathway that allows reliable and ordered data transmission.
2.  Reliable delivery: TCP guarantees the reliable delivery of data. It ensures that data sent from one end is received correctly and completely at the other end. It uses acknowledgment mechanisms, retransmission of lost packets, and sequencing of packets to achieve reliable delivery.
3.  Ordered delivery: TCP preserves the order of data packets sent by the sender. The receiver receives the packets in the same order they were sent, allowing the application to reconstruct the original data stream.
4.  Flow control: TCP performs flow control to manage the rate of data transmission between the sender and receiver. It prevents the sender from overwhelming the receiver by dynamically adjusting the amount of data sent based on the receiver's capacity.
5.  Congestion control: TCP includes congestion control mechanisms to prevent network congestion. It monitors the network's congestion levels and adjusts the sending rate to avoid overwhelming the network and causing packet loss.
6.  Full-duplex communication: TCP enables full-duplex communication, allowing simultaneous bidirectional data transfer between the sender and receiver. Both ends can send and receive data at the same time.
7.  Stream-oriented: TCP provides a stream-oriented service, treating data as a continuous stream of bytes rather than individual packets. It segments the stream into manageable chunks called TCP segments for efficient transmission.
8.  Error detection and recovery: TCP uses checksums to detect errors in transmitted data. If errors are detected, TCP requests retransmission of the corrupted segments, ensuring error-free delivery.

TCP is widely used in applications that require reliable and ordered data delivery, such as web browsing, file transfer, email, and remote access. Some notable features and use cases of TCP include:
- Web browsing: When you visit a website, your web browser establishes a TCP connection with the web server to exchange HTTP data, ensuring the reliable delivery of web pages.
- File transfer protocols: TCP is used by file transfer protocols like FTP (File Transfer Protocol) and SFTP (Secure File Transfer Protocol) to transfer files between client and server.
- Email transmission: TCP is used by email protocols like [[Application Layer#SMTP|SMPT]] (Simple Mail Transfer Protocol) and IMAP (Internet Message Access Protocol) to send and receive emails reliably.
- Remote access: TCP is used in protocols like SSH (Secure Shell) and RDP (Remote Desktop Protocol) to establish secure and reliable connections for remote access to servers and systems.

While TCP provides reliability and ordered delivery, it comes with higher overhead compared to [[UDP]]. It involves more complex connection setup and acknowledgment mechanisms, which may introduce additional latency. However, TCP is essential for applications that prioritize data integrity and reliability over speed and latency.

### TCP Socket Programming
- In TCP, unlike [[UDP]], establishing a connection between the client and server is necessary before they can start sending data. This connection is established through a handshake process. One end of the TCP connection is associated with the client socket, and the other end is associated with the server socket. The TCP connection is defined by the client socket address (IP address and port number) and the server socket address.
- Once the TCP connection is established, data can be sent between the client and server by dropping the data into the TCP connection via their respective sockets. In contrast, UDP requires the server to attach a destination address to each packet before sending it.
- In TCP, the client initiates contact with the server. For the server to react to the client's initial contact, it must be running as a process, and it must have a special socket that welcomes the client's initial contact. This special socket is referred to as the "welcoming door." The client program creates a TCP socket and specifies the address of the server's welcoming socket (IP address and port number). The client then initiates a three-way handshake to establish a TCP connection with the server. This handshake is transparent to the client and server programs.
- During the three-way handshake, the client knocks on the server's welcoming door. Upon hearing the knocking, the server creates a new socket, called the connection socket, which is dedicated to that particular client. From the application's perspective, the client's socket and the server's connection socket are directly connected by a pipe. TCP ensures that the bytes sent by the client will be received by the server in the same order.
- In a TCP client-server application, both the client and server processes can send and receive bytes through their respective sockets. TCP provides reliable communication between the client and server processes.
- `TCPClient.py`
```Python
from socket import *
serverName = ’servername’
serverPort = 12000
clientSocket = socket(AF_INET, SOCK_STREAM)
clientSocket.connect((serverName,serverPort))
sentence = input(’Input lowercase sentence:’)
clientSocket.send(sentence.encode())
modifiedSentence = clientSocket.recv(1024)
print(’From Server: ’, modifiedSentence.decode())
clientSocket.close()
```
- `TCPServer.py`
```Python
from socket import *
serverPort = 12000
serverSocket = socket(AF_INET,SOCK_STREAM)
serverSocket.bind((’’,serverPort))
serverSocket.listen(1)
print(’The server is ready to receive’)
while True:
	connectionSocket, addr = serverSocket.accept()
	sentence = connectionSocket.recv(1024).decode()
	capitalizedSentence = sentence.upper()
	connectionSocket.send(capitalizedSentence.encode())
	connectionSocket.close()
```