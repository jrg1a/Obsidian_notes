> Network applications are the raisons d’être of a computer network—if we couldn’t conceive of any useful applications, there wouldn’t be any need for networking infrastructure and protocols to support them.

### Principles of Network Applications
- At the core of network application development is writing programs that run on different end systems and communicate with each other over the network.
- For example:
	- in the Web application there are two distinct programs that communicate with each other: the browser program running in the user’s host (desktop, laptop, tablet, smartphone, and so on); and the Web server program running in the Web server host.
- Network-core devices do not function at the application layer but instead function at lower layer, specifically at the network layer and below
---
### Network Application Architectures
- The network architecture is fixed and provides a set of services to applications, from a developers perspective.
- There are two predominant architectural paradigms used in modern network applications:
	- The client-server architecture.
		- There is an always-on host, called the server, which services requests from many other hosts, called clients.
		- E.g., a website
	- Peer-to-peer architecture (P2P).
		- There is minimal (or no) reliance on dedicated servers in data centers. Instead the application exploits direct communication between pairs of intermittently connected hosts, called peers.
		- The peers are not owned by the service provider, but are instead desktops and laptops controlled by users, with most of the peers residing in homes, universities, and offices.
		- Example of a popular P2P application is the file-sharing application BitTorrent.
		- P2P architectures are cost effective!
		- However, P2P applications face challenges of security, performance, and reliability due to their highly decentralised structure.
![[Pasted image 20230511225712.png]]

---
### Processes Communicating

- Processes is the way computers communicate with each other
- Client Server Processes:
	- A network application consist of pairs of processes that send messages to each other over a network. For example in the Web application a client browser process exchanges messages with a Web server process.
	- In [[Application Layer#Peer-to-Peer File Distrubution|P2P]] file-sharing system, a file is transferred from a process in one peer to a process in another peer.
	- browser = client process
	- web server = server process
	- in P2P, one process can act as server and client at the same time.

###### *The interface Between the Process and the Computer Network*
- Most applications consist of pairs of communicating processes, with the two processes in each pair sending messages to each other.
- Messages sent between two processes needs to go though the underlying network
- Messages is sent and received through a socket
- In a house analogy, the socket can be view as the door of the house, where one needs to shove the message out their door, and it then gets transported, and arrives at the receivers house and through the receivers door.
![[Pasted image 20230511232105.png]]
- As we see in the picture above: a socket is the interface between the application layer and the [[Transport Layer]] within a host. It is also referred to as the **Application Programming Interface([[CRUD API|API]])** between the application and network, since the socket is the programming interface with which network applications are built. 
- The application developer has control of everything on the application-layer side of the socket but has little control of the transport-layer side of the socket. The only control that the application developer has on the transport-layer side is 
	1. the choice of transport protocol  
	2. perhaps the ability to fix a few transport-layer parameters such as maximum buffer and maximum segment sizes.

###### *Addressing Processes*
- In order for a process running on one host to send packets to a process running on another host, the receiving process needs an address. 
- To identify the receiving process, we need two pieces of informations
	1. the address of the host
	2. an identifier that specifies the receiving process in the destination host
- The Host is identified by the **[[IP address]]** 
- The sender needs to identify the receiving process (the socket) running in the host.

---
### Transport Services Available to Applications

- Recall that a socket is the interface between the application process and the transport layer protocol.
- The application at the sending side pushes messages through the socket. At the other side of the socket, the transport-layer protocol has the responsibility of getting the messages to the socket of the receiving process.
- Many networks, including the Internet, provide more than one [[Transport Layer]] protocol. When you develop an application, you must choose one of the available transport-layer protocols.
- We can broadly classify the possible services along four dimensions: [[#*Reliable Data Transfer*| Reliable Data Transfer]], [[#*Throughput*|Throughput]], [[#*Timing*|Timing]], and [[#*Security*|Security]].

###### *Reliable Data Transfer*
- Packets can get lost within a computer network. For example, a packet can overflow a buffer in a router, or can be discarded by a host or router after having some of its bits corrupted.
- To support these applications, something has to be done to guarantee that the data sent by one end of the application is delivered correctly and completely to the other end of the application.
- A protocol provides such a guaranteed data delivery service is called a reliable data transfer. 
- One important service that a transport-layer protocol can potentially provide to an application is process-to-process reliable data transfer.
	- Sending process can just pass its data into the socket and know with complete confidence that the data will arrive without errors at the receiving process
-  No reliable data transfer protocol = data that may never arrive
	- might be acceptable for *loss-tolerant applications* such as multimedia applications
		- video
		- audio
		- might cause a small glitch in audio or video

###### *Throughput*
- The rate at which the sending process can deliver bits to the receiving process.
- Because of different applications on the network path will be sharing bandwidth along the network path, the available [[Physical Layer#Throughput|throughput]] can fluctuate with time. 
- Another natural service that a transport-layer protocol could provide, is guaranteed available throughput at some specified rate.
	- With such a service, the application could request a guaranteed throughput of r bits/sec, and the transport protocol would then ensure that the available throughput is always at least r bits/sec
- While bandwidth-sensitive applications have specific throughput requirements, elastic applications can make use of as much, or as little, throughput as happens to be available.
	- Electronic mail, file transfer and web transfers are all elastic applications. 

###### *Timing*
- As with throughput guarantees, timing guarantees can come in many shapes and forms.
- An example guarantee might be that every bit that the sender pumps into the socket arrives at the receiver’s socket no more than 100 msec later.
- This applies to interactive real-time applications, such as:
	- internet telephony, virtual environments, teleconferencing, and multiplayer games
	- these all require tight timing constraints

###### *Security*
- A transport protocol can provide an application with one or more security services.
- A transport protocol can encrypt all data transmitted by the sending process, and in the receiving host, the transport-layer protocol can decrypt the data before delivering the data to the receiving process.
- Such service would provide confidentiality between the two processes.
- Other security services in addition to confidentiality: including data integrity and end-point authentication.

---
### Transport Services Provided by the Internet

- The internet makes two transport protocols available to applications, [[UDP]] and [[TCP]].
- Which one that is chosen is based on what needed for the specific application. 

###### TCP
- The service model includes a connection-oriented service and a reliable data transfer service.
- When an application invokes [[TCP]] as its transport protocol, the application receives both of these services from [[TCP]].
	- Connection-oriented service
		- [[TCP]] makes the client and host exchanges transport-layer control information with each other **before** the application-level messages is exchanged. 
		- Three way handshake procedure alerts the client and the server for incoming packet stream. 
		- [[TCP ]]connection is said to exist between the sockets of the two processes.
		- The connection is a full-duplex connection in that the two processes can send messages to each other over the connection at the same time.
		- When communication has ended, it tears down the connection. 
	- [[Application Layer#*Reliable Data Transfer*|Reliable Data Transfer Service]]
		- The communicating processes can rely on [[TCP]] to deliver all data sent without error and in the proper order.
		- When one side of the application passes a stream of bytes into a socket, it can count on [[TCP]] to deliver the same stream of bytes to the receiving socket, with no missing or duplicate bytes.
		- [[TCP]] also includes a congestion-control mechanism.
			- The [[TCP ]]congestion-control mechanism throttles a sending process (client or server) when the network is congested between sender and receiver. 

###### UDP
- [[UDP]] is a no-frills, lightweight transport protocol, providing minimal services.
- It is connectionless, so there is no handshaking before the two processes start to communicate.
- [[UDP]] provides an unreliable data transfer service, meaning when a process sends a message into a [[UDP]] socket, it provides no guarantee that the message will ever reach the receiving process. 
- Messages that arrive might also arrive out of order. 
- [[UDP]] does not come with a congestion-control mechanism, so the sending side of UDP can pump data into the layer below (network layer) at any rate it pleases.
---
### Application-Layer Protocols
- An application layer protocol defines how an app processes, running and different end systems, and  pass messages to each other. 
- An application-layer protcol define:
	- Types of messages exchanged, e.g. request and response messages. 
	- Syntax of the various message types, such as the fields in messages and how the fields are delineated. 
	- Semenatics of the fields, the meaning of the information in the fields
	- The rules for determining when and how a process sends messages and responds to messages.
- Some protocols are specified in RFC's and are therefore in the public domain.
- One of these is HTTP (HyperText Transfer Protocol) which is defined in the RFC 7230. 
- Many other application-layer protocols are proprietary and intentionally not available in the public domain. For example, Skype uses proprietary application-layer protocols.
- It is important to distinguish between *network applications* and *application-layer protocols*!
	- An application-layer protocol is only one piece of a network application
- The Web is a client-server application that allows users to obtain documents from Web servers on demand. The Web application consists of many components, including a standard for document formats (that is, HTML), Web browsers (for example, Chrome and Microsoft Internet Explorer), Web servers (for example, Apache and Microsoft servers), and an application-layer protocol.
---
### The Web and HTTP
- The Web was the first Internet application that caught the general public’s eye.
- Hyperlinks and search engines
- Forms, JavaScript, video, and many other devices enable us to interact with pages and sites.
- The Web and its protocols serve as a platform for YouTube, Web-based e-mail (such as Gmail), and most mobile Internet applications, including Instagram and Google Maps.

###### Overview of HTTP
- The HyperText Transfer Protocol (HTTP), the Web’s application-layer protocol, is at the heart of the Web.
	- defined in [RFC 1945], [RFC 7230], and  [RFC 7540]
- HTTP is implemented in two programs: a client program and a server program. The client program and server program, executing on different end systems, talk to each other by exchanging HTTP messages.
- HTTP defines the structure of these messages and how the client and server exchange the messages. 
- Most Web pages consist of a base HTML file and several referenced objects.
- if a Web page contains HTML text and five JPEG images, then the Web page hassix objects: the base HTML file plus the five images. The base HTML file references the other objects in the page with the objects’ URLs. Each URL has two components: the hostname of the server that houses the object and the object’s path name. For example, the URL
	- http://www.someSchool.edu/someDepartment/picture.gif  
	  has www.someSchool.edu for a hostname and /someDepartment/picture.
 - HTTP defines how Web clients request Web pages from Web servers and how servers transfer Web pages to clients.
 - When a user requests a Web page (for example, clicks on a hyperlink), the browser sends HTTP request messages for the objects in the page to the server. The server receives the requests and responds with HTTP response messages that contain the objects.
  ![[Pasted image 20230512121333.png]]
- HTTP uses TCP as its underlying transport protocol (rather than running on top of UDP). The HTTP client first initiates a [[TCP]] connection with the server. Once the connection is established, the browser and the server processes access TCP through their socket interfaces.
- The client sends HTTP [[WEB Requests|request]] messages into its socket interface and receives HTTP response messages from its socket interface. Similarly, the HTTP server receives request messages from its socket interface and sends response messages into its socket interface.
- Once the client sends a message into its socket interface, the message is out of the client’s hands and is “in the hands” of TCP.
- HTTP need not worry about lost data or the details of how TCP recovers from loss or reordering of data within the network.
- It is important to note that the server sends requested files to clients without storing any state information about the client. If a particular client asks for the same object twice in a period of a few seconds, the server does not respond by saying that it just served the object to the client; instead, the server resends the object, as it has completely forgotten what it did earlier.
- AKA, an HTTP server maintains no information about the clients, HTTP is said to be a **stateless protocol**.

###### Non-Persistent and Persisten Connections
- In several internet applications, the client and server needs to  communicate for an extended period of time. Then the server and client requests and responds to a lot between each other. 
- When a client-server that is dependent on a series of request may be made back-to-back, periodically at regular intervals or inetermittently, the application developer needs to choose if either each request/response pair be sent over a separate TCP connection or should all their corresponding reponses be sent over the same TCP connection.
- HTTP, which can use both non-persistent connections and persistent connections.
- Although HTTP uses persistent connections in its default mode, HTTP clients and servers can be configured to use non-persistent connections instead.
- Advantages and disadvantages of persistent connections:
- **HTTP with Non-Persistent Connections**
	- Refer to a method of establishing a connection between a client (such as a web browser) and a server, where each request and response is sent over a separate connection.
	- When a client initiates an HTTP request using a non-persistent connection, it establishes a TCP (Transmission Control Protocol) connection with the server, sends the request, and waits for the server's response. Once the server sends the response, the connection is closed. Subsequently, if the client needs to fetch additional resources (such as images, stylesheets, or scripts) to render the web page, it repeats the process of establishing a new connection for each resource.
	- Non-persistent connections have certain advantages and disadvantages. On the positive side, they are relatively simple to implement and can save server resources since the connections are short-lived. However, establishing and tearing down connections for every request can introduce latency and overhead due to the TCP handshake and connection setup process.
- **HTTP with Persisten Connections**
	- Persistent connections, also known as keep-alive connections, are an enhancement to HTTP that allows multiple requests and responses to be sent over the same TCP connection.
	- With persistent connections, when a client initiates an HTTP request, it establishes a TCP connection with the server, sends the request, and waits for the server's response. However, instead of closing the connection immediately, the connection remains open for subsequent requests. The client can send multiple requests over the same connection without the need to establish new connections for each request.
	- Benefits: Reduces the overhead of establishing and tearing down connections, leading to improved performance and reduced latency.
	- allows for pipelining, where the client can send multiple requests without waiting for the corresponding responses. This can further enhance efficiency by overlapping request and response transmission
	- To indicate the use of persistent connections, the client includes the [[WEB Requests#Request Headers|"Connection: keep-alive"]] header in its request.
	- The server can either accept or reject the persistent connection request by including the [[WEB Requests#Response Headers|"Connection: close"]]  or [[WEB Requests#Request Headers|"Connection: keep-alive"]]  header in its response, respectively
	- Persistent connections have become the default behavior in modern HTTP implementations, as they provide significant performance benefits by reducing the overhead associated with connection establishment.
- In summary, non-persistent connections in HTTP involve establishing a separate connection for each request and response, while persistent connections allow multiple requests and responses to be sent over the same connection, leading to improved performance and reduced latency.
![[Pasted image 20230512125425.png]]
- The first two parts of the three-way handshake take one RTT. After completing the first two parts of the handshake, the client sends the HTTP request message combined with the third part of the three-way handshake (the acknowledgment) into the TCP connection. Once the request message arrives at the server, the server sends the HTML file into the TCP connection. This HTTP request/response eats up another RTT. Thus, roughly, the total response time is two RTTs plus the transmission time at the server of the HTML file.
- With HTTP/1.1 persistent connections, the server leaves the TCP connection open after sending a response. Subsequent requests and responses between the same client and server can be sent over the same connection.


###### HTTP Message Format
- The HTTP (Hypertext Transfer Protocol) message format is a standardized structure used for communication between clients and servers.
- It consists of two types of messages: the request message, sent by the client to the server, and the response message, sent by the server back to the client.
###### HTTP Request Message
-  HTTP request message example:
![[Pasted image 20230512125520.png]]
- The first line of an HTTP request message is called the request line.
- The subsequent lines are called the header lines.
- The request line has three fields: the method field, the URL field, and the HTTP version field.
- The method field can take on several different values, including [[WEB Requests#Request Methods|GET]], [[WEB Requests#Request Methods|POST]], [[WEB Requests#Request Methods|HEAD]], [[WEB Requests#Request Methods|PUT]], and [[WEB Requests#Request Methods|DELETE]].
- The great majority of HTTP request messages use the [[WEB Requests#Request Methods|GET]] method, and its used when the browser requests an object, with the requested object identified in the URL field. 
- In this example, the browser is requesting the object `/somedir/page.html`.
	- The browser implements version HTTP/1.1.
	- The header line Host: www.someschool.edu specifies the host on which the object resides.
	- the information provided by the host header line is required by Web proxy caches
	- By including the `Connection: close` header line, the browser is telling the server that it doesn’t want to bother with persistent connections; it wants the server to close the connection after sending the requested object.
	- The `User-agent`: header line specifies the user agent, that is, the browser type that is making the request to the server. Here the user agent is Mozilla/5.0, a Firefox browser.
		- The server can actually send different versions of the same object to different types of user agents.
	- Finally, the `Accept-language: header` indicates that the user prefers to receive a French version of the object, if such an object exists on the server; otherwise, the server should send its default version.
		- This header is just one of many content negotiation headers available in HTTP.
- **General format of a request message**. 
- ![[Pasted image 20230512140940.png]]
- After the header lines (and the additional carriage return and line feed) there is an “entity body.”
- The entity body is empty with the  [[GET|GET]] method, but is used with the [[WEB Requests#Request Methods|POST]] method.
- An HTTP client often uses the [[WEB Requests#Request Methods|POST]] method when the user fills out a form, like when a user provides search words to a search engine.
- With a [[WEB Requests#Request Methods|POST]] message, the user is still requesting a Web page from the server, but the specific contents of the Web page depend on what the user entered into the form fields.
- If the value of the method field is [[POST|POST]], then the entity body contains what the user entered into the form fields.
- A request generated with a form does not necessarily have to use the [[WEB Requests#Request Methods|POST]] method.
- HTML forms often use the [[WEB Requests#Request Methods|GET]] method and include the inputted data (in the form fields) in the requested URL.
- if a form uses the [[WEB Requests#Request Methods|GET]] method, has two fields, and the inputs to the two fields are monkeys and bananas, then the URL will have the structure 
  www.somesite.com/animalsearch?monkeys&bananas.
- The [[WEB Requests#Request Methods|HEAD]] method is similar to the [[WEB Requests#Request Methods|GET]]  method.
- When a server receives a request with the `HEAD method`, it responds with an HTTP message but it leaves out he requested object.
	- *Funfact:* Application developers often use the ``HEAD`` method for debugging.
- The [[WEB Requests#Request Methods|PUT]] method is often used in conjunction with Web publishing tools. It allows a user to upload an object to a specific path (directory) on a specific Web server.
	- Its also used by applications that need to upload objects to Web servers.
- The [[WEB Requests#Request Methods|DELETE]] method allows a user, or an application, to delete an object on a Web server.
###### HTTP Response Message
- An HTTP response message is sent by the server in response to a client's request. It contains the requested resource or information about the outcome of the request. A response message consists of the following components.
	- Status Line
	- Reponse Headers
	- Response Body
- Example of a typical HTTP response message. 
- ![[Pasted image 20230512143537.png]]
- This example has an initial status line, six header lines, and then the entity body.
- The entity body contains the "meat" of the message, the requested object (data). 
- The status line has three fields: the protocol version field, a status code, and a corresponding status message
- In this example:
	- The status line indicates that the server is using HTTP/1.1 and that everything is OK
	- The server uses the ``Connection: close`` header line to tell the client that it is going to close the TCP connection after sending the message.
	- The ``Date:`` header line indicates the time and date when the HTTP response was created and sent by the server.
		- **NB!** This is not the time when the object was created or last modified; it is the time when the server retrieves the object from its file system, inserts the object into the response message, and sends the response message.
	- The ``Server:`` header line indicates that the message was generated by an Apache Web server; it is analogous to the ``User-agent:`` header line in the HTTP request message.
	- The ``Last-Modified:`` header line indicates the time and date when the object was created or last modified.
		- This header is critical for object caching, both in the local client and in network cache servers (also known as proxy servers).
	- ``Content-Length:`` header line indicates the number of bytes in the object being sent.
		- The header line indicates that the object in the entity body is HTML text. (The object type is officially indicated by the ``Content-Type: header`` and not by the file extension.)
- General format of a response message.
- ![[Pasted image 20230512150652.png]]
- The status code and associated phrase indicate the result of the request. Some common status codes and associated phrases include:
	- ``200 OK:`` Request succeeded and the information is returned in the response.
	- ``301 Moved Permanently:`` Requested object has been permanently moved; the new URL is specified in Location: header of the response message. The client software will automatically retrieve the new URL.
	- ``400 Bad Request:`` This is a generic error code indicating that the request could not be understood by the server.
	- ``404 Not Found:`` The requested document does not exist on this server.
	- ``505 HTTP Version Not Supported:`` The requested HTTP protocol version is not supported by the server
- Example of an HTTP response message using telnet. 
- ![[Pasted image 20230512151321.png]]

###### User-Server Interaction: Cookies
- Mentioned above that an HTTP server is stateless.
- Cookies, defined in [RFC 6265], allow sites to keep track of users. Most major commercial Web sites use cookies today.
![[Pasted image 20230512151954.png]]
- Cookie technology has four components:
	1. cookie header line in the HTTP response message
	2. a cookie header line in the HTTP request message
	3. a cookie file kept on the user’s end system and managed by the user’s browser
	4. a back-end database at the Web site
- When a user connects to a web server for the first time, the server creates a unique identification number and creates an entry in its back-end database that is indexed by the identification number. 
- The server responds the client with a [[WEB Requests|HTTP response]] and a ``Set-cookie:``  header, which contains the identification numbers. E.G., `Set-cookie: 1678`
- When the client browser receives the HTTP response message, it sees the ``Set-cookie:`` , and then appends a line to the special cookie file that it manages.
	- This line includes the hostname of the server and the identification number in the ``Set-cookie:`` header.
- The clients cookie file gets consulted by the browser when the client keeps browsing and seding request on the web site, for each request the idenfitication number for the site is retrieved when the browser consults the file and puts the cookie header line in the HTTP request. 
- Each HTTP request to the Amazon Server includes the header line `Cookie: 1678`
- *Cookies can be used to identify a user.*
- During the subsequent sessions, the browser passes a cookie header to the server, thereby identifying the user to the server. Cookies can thus be used to create a user session layer on top of stateless HTTP.
- It's important to note that while cookies offer convenience and functionality, they also raise privacy concerns. Some users may disable or clear cookies to protect their privacy or prevent tracking.
- To address privacy concerns, newer standards and regulations like the General Data Protection Regulation (GDPR) in the European Union require websites to inform users about the use of cookies and provide options for consent and control over their data.
- Overall, cookies play a crucial role in user-server interaction by enabling personalized experiences, session management, and data tracking, but their use should align with privacy regulations and user preferences.

###### Web Caching
- A web cache - also called proxy server, is a network entity that satisfies HTTP requests on the behalf of an origin Web server. 
- The Web cache has its own disk storage and keeps copies of recently requested objects in this storage.
- A user’s browser can be configured so that all of the user’s HTTP requests are first directed to the Web cache [RFC 7234].
- Once a browser is configured, each browser request for an object is first directed to the Web cache.
- As an example, a browser is requesting the object:
  http://www.someschool.edu/campus.gif.
- Here is what happens:
	1. The browser establishes a TCP connection to the Web cache and sends an HTTP  request for the object to the Web cache.
	2. The Web cache checks to see if it has a copy of the object stored locally. If it does, the Web cache returns the object within an HTTP response message to the client browser.
	3. If the Web cache does not have the object, the Web cache opens a TCP connection to the origin server, that is, to www.someschool.edu. The Web cache then sends an HTTP request for the object into the cache-to-server [[TCP]] connection. After receiving this request, the origin server sends the object within an HTTP response to the Web cache.
	4. When the Web cache receives the object, it stores a copy in its local storage and sends a copy, within an HTTP response message, to the client browser (over the existing TCP connection between the client browser and the Web cache).
- A cache is both a server and a client at the same time.
- When it receives requests from and sends responses to a browser, it is a server. When it sends requests to and receives responses from an origin server, it is a client.
- Typically a Web cache is purchased and installed by an ISP.
- Web caching has seen deployment in the Internet for two reasons.
	- a Web cache can substantially reduce the response time for a client request, particularly if the bottleneck bandwidth between the client and the origin server is much less than the bottleneck bandwidth between the client and the cache.
	- Second, Web caches can substantially reduce traffic on an institution’s access link to the Internet. By reducing traffic, the institution (for example, a company or a university) does not have to upgrade bandwidth as quickly, thereby reducing costs.
- Web caches can substantially reduce Web traffic in the Internet as a whole, thereby improving performance for all applications.

- Example: 
- This figure shows two networks—the institutional network and the rest of the public Internet. The institutional network is a high-speed LAN. A router in the institutional network and a router in the Internet are connected by a 15 Mbps link. The origin servers are attached to the Internet but are located all over the globe. Suppose that the average object size is 1 Mbits and that the average request rate from the institution’s browsers to the origin servers is 15 requests per second. Suppose that the HTTP request messages are negligibly small and thus create no traffic in the networks or in the access link (from institutional router to Internet router). Also suppose that the amount of time it takes from when the router on the Internet side of the access link in Figure 2.12 forwards an HTTP request (within an IP datagram) until it receives the response (typically within many IP datagrams) is two seconds on average. Informally, we refer to this last delay as the “Internet delay.” The total response time—that is, the time from the browser’s request of an object until its receipt of the object—is the sum of the LAN delay, the access delay (that is, the delay between the two routers), and the Internet delay. Let’s now do a very crude calculation to estimate this delay. The traffic intensity on the LAN is:
	- (15 requests/sec) * (1 Mbits/request)/(100 Mbps) = 0.15
- Whereas the traffic intensity on the access link (from the Internet router to institution router) is
	- (15 requests/sec) * (1 Mbits/request)/(15 Mbps) = 1
- A traffic intensity of 0.15 on a LAN typically results in, at most, tens of milliseconds of delay; hence, we can neglect the LAN delay.
- ![[Pasted image 20230512160216.png]]
- However, as the traffic intensity approaches 1 (as is the case of the access link in Figure 2.12), the delay on a link becomes very large and grows without bound. Thus, the average response time to satisfy requests is going to be on the order of minutes, if not more, which is unacceptable for the institution’s users. We need to do something.
- One possible solution is to increase the access rate from 15 Mbps to, say, 100 Mbps.
	- This will lower the traffic intensity on the access link to 0.15, which translates to negligible delays between the two routers. In this case, the total response time will roughly be two seconds, that is, the Internet delay. But this solution also means that the institution must upgrade its access link from 15 Mbps to 100 Mbps, a costly proposition.
- Now consider the alternative solution of not upgrading the access link but instead installing a Web cache in the institutional network. 
- ![[Pasted image 20230512160603.png]]
- Hit rates—the fraction of requests that are satisfied by a cache— typically range from 0.2 to 0.7 in practice.
- let’s suppose that the cache provides a hit rate of 0.4 for this institution.
	- Because the clients and the cache are connected to the same high-speed LAN, 40 percent of the requests will be satisfied almost immediately, say, within 10 milliseconds, by the cache.
- Nevertheless, the remaining 60 percent of the requests still need to be satisfied by the origin servers. But with only 60 percent of the requested objects passing through the access link, the traffic intensity on the access link is reduced from 1.0 to 0.6.
- A traffic intensity less than 0.8 corresponds to a small delay, say, tens of milliseconds, on a 15 Mbps link. This delay is negligible compared with the two-second Internet delay. Given these considerations, average delay therefore is:
	- 0.4 * (0.01 seconds) + 0.6 * (2.01 seconds)
	- which is just slightly greater than 1.2 seconds. Thus, this second solution provides an even lower response time than the first solution, and it doesn’t require the institution to upgrade its link to the Internet.
- Through the use of Content Distribution Networks (CDNs), Web caches are increasingly playing an important role in the Internet.
- A CDN company installs many geographically distributed caches throughout the Internet, thereby localizing much of the traffic.
- There are shared CDNs (such as Akamai and Limelight) and dedicated CDNs (such as Google and Netflix).
- How it works:
	- Caching at the Client-side (Browser Cache): When a user visits a website, the browser stores certain resources (such as HTML pages, images, CSS files, and JavaScript) in its local cache. If the user revisits the same website or navigates to a different page within the same website, the browser checks its cache before making a request to the server. If the requested resource is found in the cache and has not expired, the browser retrieves it from the cache instead of fetching it from the server. This reduces the load on the server and improves the page load time for the user.
	- Caching at the Network Level: Internet Service Providers (ISPs) and network intermediaries can implement caching mechanisms to store frequently accessed web content closer to the user. These caches are typically located at the ISP's servers or within the network infrastructure. When a user requests a resource, the cache checks if it has a fresh copy of that resource. If available, it serves the resource directly to the user, eliminating the need to retrieve it from the original server. Network-level caching helps reduce latency and bandwidth consumption, especially for popular and static resources.
	- Content Delivery Networks (CDNs): CDNs are distributed networks of servers located in various geographical locations. They store cached copies of web content, such as images, videos, and static files, closer to the end users. When a user requests a resource from a website that utilizes a CDN, the CDN automatically routes the request to the nearest server in its network. If the requested resource is present in the CDN's cache, it delivers the cached content directly to the user. CDNs improve performance by reducing latency and offloading traffic from the origin server.
- In summary, web caching optimizes web browsing by storing frequently accessed resources closer to users, resulting in faster page load times, reduced bandwidth usage, and improved scalability. Client-side caching, network-level caching, and CDNs all play important roles in enhancing web performance and efficiency.

**The conditional Get**
- Although caching can reduce user-perceived response times, it introduces a new problem:
	- the copy of an object residing in the cache may be stale. In other words, the object housed in the Web server may have been modified since the copy was cached at the client.
- HTTP has a mechanism that allows a cache to verify that its objects are up to date. This mechanism is called the conditional GET[RFC 7232].
- An HTTP request message is a so-called conditional GET message if (1) the request message uses the GET method and (2) the request message includes an If-Modified-Since: header line.
- To illustrate how the conditional [[GET]] operates, let’s walk through an example. 
	- First, on the behalf of a requesting browser, a proxy cache sends a request message to a Web server:
	- ![[Pasted image 20230512163830.png]]
	- Second, the Web server sends a response message with the requested object to the cache:
	- ![[Pasted image 20230512164014.png]]
	- The cache forwards the object to the requesting browser but also caches the object locally. Importantly, the cache also stores the last-modified date along with the object.
	- Third, one week later, another browser requests the same object via the cache, and the object is still in the cache. Since this object may have been modified at the Web server in the past week, the cache performs an up-to-date check by issuing a conditional GET. Specifically, the cache sends:
	- ![[Pasted image 20230512164128.png]]
	- Note that the value of the If-modified-since: header line is exactly equalto the value of the Last-Modified: header line that was sent by the server one week ago. This conditional GET is telling the server to send the object only if the object has been modified since the specified date.
	- Suppose the object has not been modified since 9 Sep 2015 09:23:24. Then, fourth, the Web server sends a response message to the cache:
	- ![[Pasted image 20230512164927.png]]
	- We see that in response to the conditional GET, the Web server still sends a response message but does not include the requested object in the response message.
		- This would only waste bandwidth and increase userperceived response time, particularly if the object is large.
		- Note that this last response message has 304 Not Modified in the status line, which tells the cache that it can go ahead and forward its (the proxy cache’s) cached copy of the object to the requesting browser.

###### HTTP/2 
- HTTP/2 [RFC 7540], standardized in 2015, was the first new version of HTTP since HTTP/1.1, which was standardized in 1997.
- Since standardization, HTTP/2 has taken off, with over 40% of the top 10 million websites supporting HTTP/2 in 2020.
- The primary goals for HTTP/2 are to:
	- reduce perceived latency by enabling requests and response multiplexing over a single TCP connection
	- provide request prioritization and server push, and provide efficient compression of HTTP header fields.
	- HTTP/2 does not change HTTP methods, status codes, URLs, or header fields.
		- Instead, HTTP/2 changes how the data is formatted and transported between the client and server.
- Performance and Efficiency:
	- HTTP/2 was designed with performance improvements in mind compared to HTTP/1.1. Some key features of HTTP/2 that enhance performance include:
		- Multiplexing: HTTP/2 supports multiplexing, allowing multiple requests and responses to be sent concurrently over a single connection. This eliminates the need for multiple connections, reducing latency and improving efficiency.
		- Server Push: HTTP/2 introduces server push, which enables the server to proactively send additional resources to the client without waiting for a separate request. This can improve page load times by reducing the round trips required for resource fetching.
		- Header Compression: HTTP/2 utilizes header compression techniques to reduce the overhead associated with sending header data. This helps optimize network utilization and improve efficiency.
		- Binary Protocol: While HTTP/1.1 uses text-based headers, HTTP/2 employs a binary protocol, which is more compact and efficient for data transmission.
	- Connection Handling: HTTP/1.1 uses persistent connections, where multiple requests and responses can be sent over a single connection. However, each request/response pair is processed sequentially, and the server cannot send a response until it receives the entire request.
- In contrast, HTTP/2 supports multiplexing, allowing multiple requests and responses to be interleaved on a single connection. This allows for more efficient use of network resources and reduces the number of round trips required for data transmission.
	- Header Compression:
		- HTTP/1.1 sends headers as plain text for each request and response. This can introduce redundancy and overhead, especially when sending large headers or making multiple requests.
- HTTP/2 addresses this issue by introducing header compression, which significantly reduces the size of header data by using a technique called Huffman encoding. This helps minimize bandwidth consumption and improves overall efficiency.
	- Backward Compatibility:
		- HTTP/2 is backward compatible with HTTP/1.1. This means that if a client or server does not support HTTP/2, the communication can still fall back to using HTTP/1.1. This ensures interoperability and allows gradual adoption of HTTP/2 without requiring an immediate upgrade of all systems.
- Overall, HTTP/2 offers improved performance, multiplexing, server push, header compression, and a binary protocol compared to HTTP/1.1. These enhancements result in faster and more efficient web communication, reducing latency and improving the overall browsing experience.
- HTTP/2 addresses the issue of Head-of-Line (HOL) blocking, which refers to a situation where the delivery of a resource is delayed due to the sequential nature of HTTP/1.1's request-response mechanism.
- HOL blocking occurs when a large resource or a slow response is encountered, blocking subsequent requests from being processed until the previous request is fully completed.
- HTTP/2 solves HOL blocking through the following mechanisms:
	- Multiplexing: One of the key features of HTTP/2 is [[Transport Layer#Multiplexing and Demultiplexing|multiplexing]], which allows multiple requests and responses to be sent concurrently over a single TCP connection.
	- The HTTP/2 solution for HOL blocking is to break each message into small frames, and interleave the request and response messages on the same TCP connection.
- As a result, multiple requests and responses can be interleaved and sent in parallel over the same connection. This eliminates the need for a strict request-response order, reducing the chances of HOL blocking.
	- Stream Prioritization: HTTP/2 introduces the concept of stream prioritization, where each stream is assigned a priority level. The client can assign relative weights or dependencies to different streams, indicating the order of importance for resource delivery.


---
### Electronic Mail in the Internet
- E-mail is an asynchronous communication medium—people send and read messages when it is convenient for them, without having to coordinate with other people’s schedules.
- Modern e-mail has many powerful features, including messages with attachments, hyperlinks, HTMLformatted text, and embedded photos.
- Application-layer protocols that are at the heart of Internet e-mail.
- Figure 2.14 presents a high-level view of the Internet mail system:
![[Pasted image 20230512170532.png]]
- it has three major components: user agents, mail servers, and the Simple Mail Transfer Protocol (SMTP).
- Mail servers form the core of the e-mail infrastructure. Each recipient, such as Bob, has a mailbox located in one of the mail servers. Bob’s mailbox manages and maintains the messages that have been sent to him.
- If server can't deliver the mail, the mail will be put in a message queue, and attempts to transfer the message at a later time, usually often every 30 minutes. 
	- if there is no success after several days, the server removes the message and notifies the sender with an e-mail message.
- SMTP is the principal application-layer protocol for Internet electronic mail. 
- It uses the reliable data transfer service of TCP to transfer mail from the sender’s mail server to the recipient’s mail server
	- it acts both as an client and a server

###### SMTP
- SMTP, defined in RFC 5321, is at the heart of Internet electronic mail. 
- SMTP (Simple Mail Transfer Protocol) is a widely used protocol for sending and receiving email messages over the Internet. It is primarily responsible for the transfer and delivery of email from the sender's mail server to the recipient's mail server.
- The Key aspects of the SMTP protocol:
	- Connection Establishment:
		- SMTP operates on the traditional client-server model. To send an email, the client (also known as the mail user agent or MUA) initiates a TCP connection with the server (mail transfer agent or MTA) on port 25. This connection is used for communication throughout the email transfer process
	- SMTP Commands and Responses:
		- SMTP communication involves a series of commands and responses exchanged between the client and server. The client sends commands to the server, and the server responds accordingly. Some common SMTP commands include:
			- ``HELO/EHLO:`` The client initiates the conversation with the server by sending the HELO (or EHLO for extended features) command, followed by the domain name of the client.
			- ``MAIL FROM:`` The client identifies the sender of the email by providing the sender's email address.
			- ``RCPT TO:`` The client specifies the recipient(s) of the email by providing their email addresses. Multiple recipients can be specified.
			- ``DATA:`` The client indicates that it is ready to send the email content. The actual email content, including the message body and headers, is sent after this command
			- ``QUIT:`` The client terminates the SMTP session and closes the connection.
		- The server responds to each command with a three-digit status code and an optional message. For example, a response starting with "250" indicates success, while "550" signifies a permanent failure.
	- Message Routing:
		- SMTP servers use various mechanisms to route email messages. When a client sends an email, the server first performs domain name resolution to determine the recipient's mail server. It then establishes a connection with the recipient's server and transfers the email using the SMTP commands mentioned earlier.
	- Relaying and Spam Prevention:
		- SMTP servers often employ measures to prevent unauthorized relaying of email messages, which could be exploited for spamming. These measures include authentication, IP-based restrictions, and verification of sender domains to ensure that only authorized users can send email through the server.
	- SMTP Extensions:
		- SMTP supports extensions that provide additional features and capabilities. Some common extensions include:
		- SMTP Authentication (AUTH): Allows clients to authenticate with the server using various mechanisms, such as username/password or digital certificates.    
		- STARTTLS: Enables encryption of the SMTP connection using Transport Layer Security (TLS) or Secure Sockets Layer (SSL).    
		- Delivery Status Notifications (DSN): Provides notifications to the sender about the delivery status of an email message.
- SMTP is a fundamental protocol for email communication, providing a standardized method for sending and receiving messages across different mail servers. While it primarily handles the transfer of email between servers, other protocols like POP3 and IMAP are used for email retrieval by clients.
- ![[Pasted image 20230512171843.png]]
- Example of transcript messages exchanged between an SMTP client (C) and an SMTP server(S). The host name for the client is ``crepes.fr``, and ``hamburger.edu`` for the server
- 
``S: 220 hamburger.edu``
``C: HELO crepes.fr``
``S: 250 Hello crepes.fr, pleased to meet you``
``C: MAIL FROM: <alice@crepes.fr>``
``S: 250 alice@crepes.fr ... Sender ok``
``C: RCPT TO: <bob@hamburger.edu>``
``S: 250 bob@hamburger.edu ... Recipient ok``
``C: DATA``
``S: 354 Enter mail, end with ”.” on a line by itself``
``C: Do you like ketchup?``
``C: How about pickles?``
``C: .``
``S: 250 Message accepted for delivery``
``C: QUIT``
``S: 221 hamburger.edu closing connection``

### DNS
The Internet’s Directory Service
- Identifier for a host is its hostname, such as www.google.com are mnemonic. 
- For the internet to know the host location within the internet, we identify hosts by [[IP address|IP addresses]]. 
	- An IP address consists of four bytes and has a rigid hierarchical structure.
	- An IP address looks like 121.7.106.83, where each period separates one of the bytes expressed in decimal notation from 0 to 255.
	- An IP address is hierarchical because as we scan the address from left to right

###### Services Provided by DNS
- There are two ways to identify a host:
	- by a hostname
	- by an [[IP address]]
- In order for routers (that prefere fixed-length, hierarchically strucutred IP addresses) to understand where the domain is located on the internet, we need a translator from mnemonic hostnames to IP addresses.
	- This is the main task of the Internet’s domain name system (DNS).
- The DNS is:
	- distributed database implemented in a hierarchy of DNS servers.
	- an application-layer protocol that allows hosts to query the distributed database. The DNS servers are often UNIX machines running the Berkeley Internet Name Domain (BIND) software [BIND 2020]. The DNS protocol runs over UDP and uses port 53.
- DNS is commonly employed by other application-layer protocols, including HTTP and SMTP, to translate user-supplied hostnames to IP addresses.
- DNS provides a few other important services in addition to translating hostnames to IP addresses:
	- Host aliasing: a technique used in DNS to assign multiple hostnames to a single IP address. It allows a server or network device to be accessed using multiple domain names, providing flexibility and convenience in network configurations
	- Mail server aliasing: a practice that allows multiple email addresses to be associated with a single mailbox or mail server. It provides flexibility in managing email communications and offers several benefits.
	- Load distribution: also known as load balancing, is a technique used to distribute network traffic evenly across multiple servers or resources. It aims to optimize resource utilization, improve performance, and ensure high availability by preventing any single server or resource from becoming overwhelmed with excessive traffic.
###### Overview of How DNS Works
- DNS (Domain Name System) is a hierarchical and distributed system that translates domain names into IP addresses, enabling the identification and communication of devices on a network. Here's an overview of how DNS works:
- Applications, such as web browsers or mail clients, invoke the client side of DNS to translate hostnames to IP addresses using functions like gethostbyname().
- DNS queries and replies are sent within UDP datagrams to port 53.
- DNS is a complex system consisting of distributed DNS servers and an application-layer protocol for communication.
- A centralized design for DNS with a single server is not suitable due to the risks of a single point of failure, high traffic volume, distant centralized database, and maintenance challenges.
- DNS is distributed by design to overcome the limitations of a centralized approach.
- Distributed DNS involves multiple DNS servers distributed globally to handle queries efficiently and reduce delays.
- DNS servers store records for different hosts, forming a distributed database that can scale with the vast number of hosts on the Internet.
- DNS is an example of how distributed databases can be implemented in the Internet.

###### A Distributed, Hierarchical Database
- DNS servers are organized in a distributed and hierarchical manner to handle the scale of the DNS system.
- The three classes of DNS servers are:
	- Root DNS servers: There are more than 1000 instances worldwide, serving as copies of 13 root servers managed by 12 organizations. They provide IP addresses of TLD servers.
	- Top-level domain (TLD) servers: Each TLD, such as com, org, edu, has its own server or server cluster maintained by organizations like Verisign and Educause. They provide IP addresses for authoritative DNS servers.
	- Authoritative DNS servers: Organizations with publicly accessible hosts (e.g., web servers) on the Internet maintain their own authoritative DNS servers or use a service provider. These servers house DNS records mapping hostnames to IP addresses.
- Local DNS servers, belonging to ISPs, play a crucial role in DNS architecture. They are not part of the hierarchy but act as proxies for DNS queries from hosts connected to the ISP.
- Local DNS servers are typically "close to" the host, either on the same LAN for institutional ISPs or separated by a few routers for residential ISPs.
- When a host makes a DNS query, it is sent to the local DNS server, which then forwards the query into the DNS server hierarchy for resolution.
- DNS servers are organized in a hierarchy, including root DNS servers, TLD DNS servers, and authoritative DNS servers. They form a distributed and hierarchical system.
- Local DNS servers, belonging to ISPs (residential or institutional), are not strictly part of the DNS hierarchy but are central to the DNS architecture.
- Each ISP provides one or more local DNS servers to its hosts, typically through DHCP.
- The local DNS server is "close to" the host, either on the same LAN for institutional ISPs or separated by a few routers for residential ISPs.
- When a host makes a DNS query, it is sent to the local DNS server, which acts as a proxy, forwarding the query into the DNS server hierarchy.
- The DNS query process involves recursive queries and iterative queries.
	- Recursive queries: The initial query from the host to the local DNS server is recursive, as the local DNS server obtains the mapping on behalf of the host.
	- Iterative queries: Subsequent queries between DNS servers are iterative, as the replies are directly returned to the local DNS server.
- DNS messages, including queries and replies, are exchanged between DNS servers to resolve the requested mappings.
- Caching plays a role in reducing query traffic, as DNS servers store resolved mappings for a certain period, reducing the need for repeated queries.

**DNS Caching** 
- DNS caching is a crucial feature of the DNS system used to improve performance and reduce DNS message traffic.
- DNS caching exploits the idea of storing mappings from DNS replies in local memory to avoid repeated queries.
- When a DNS server receives a DNS reply containing a hostname-to-IP address mapping, it can cache the information.
- Cached mappings allow DNS servers to provide the desired IP address for a hostname, even if they are not authoritative for that hostname.
- Cached information is not permanent and is discarded after a certain period, often set to two days.
- DNS servers can cache IP addresses of TLD servers, allowing them to bypass root DNS servers in subsequent queries.
- Caching greatly reduces the reliance on root servers for DNS queries, as most queries can be resolved using cached information.
- DNS caching improves delay performance by enabling faster responses and reduces the number of DNS messages traveling across the Internet.

###### DNS Records and Message
- DNS servers store resource records (RRs) that contain information such as hostname-to-IP address mappings.
- A resource record is a four-tuple with fields: Name, Value, Type, and TTL (time to live)
- The TTL field determines when a resource record should be removed from a cache.
- Different types of resource records include:
	- Type=A: Name is a hostname, and Value is the IP address for the hostname, providing a hostname-to-IP address mapping.
	- Type=NS: Name is a domain, and Value is the hostname of an authoritative DNS server that knows how to obtain IP addresses for hosts in the domain. Used for routing DNS queries.
	- Type=CNAME: Value is a canonical hostname for the alias hostname Name, providing the canonical name for a hostname.
	- Type=MX: Value is the canonical name of a mail server with an alias hostname Name, allowing mail server hostnames to have simple aliases.
- DNS clients query for specific types of resource records to obtain information. For example, MX records for mail server canonical names and CNAME records for canonical names of alias hostnames.
- If a DNS server is authoritative for a hostname, it contains a Type A record for that hostname. If it is not authoritative, it contains a Type NS record for the domain including the hostname and a Type A record providing the IP address of the DNS server.
- Resource records allow DNS servers to map hostnames to IP addresses and facilitate the resolution of DNS queries.

**DNS Messages**
- DNS messages consist of query and reply messages, both having the same format.
- The header section of a DNS message contains several fields, including:
	- Query identifier: A 16-bit number that matches replies with sent queries.
	- Flags: Various 1-bit flags indicating query/reply, authoritative server status, recursion-desired, and recursion-available.
	- Number-of fields: Indicate the occurrence of data sections that follow the header.
- The question section in a query message contains information about the query, including the name being queried and the type of question being asked (e.g., Type A or Type MX).
- In a reply message from a DNS server, the answer section contains resource records (RRs) for the queried name. Each RR includes the Type, Value, and TTL.
- The authority section contains records of other authoritative servers, providing additional information.
- The additional section contains helpful records, such as Type A records providing IP addresses for canonical hostnames.
- The nslookup program allows users to send DNS queries directly from their hosts to DNS servers. It is available on most Windows and UNIX platforms and displays the records included in the reply.
- Web-based tools and websites also provide the capability to perform remote nslookup queries.
- The DNS Wireshark lab mentioned in the text allows for further exploration of DNS in detail.
- This information explains the structure and semantics of DNS query and reply messages, the fields within the messages, the purpose of different sections, and the availability of tools like nslookup for sending DNS queries.

**Inserting Records into the DNS Database**
- When registering a domain name, such as networkutopia.com, with a registrar, you provide the registrar with the names and IP addresses of your primary and secondary authoritative DNS servers.
- Registrars verify the uniqueness of the domain name, enter it into the DNS database, and collect fees for their services.
- Prior to 1999, Network Solutions had a monopoly on domain name registration, but now there are many accredited registrars competing for customers.
- The registrar ensures that Type NS and Type A records for the authoritative DNS servers are entered into the TLD (Top-Level Domain) com servers.
- Authoritative DNS servers contain resource records (RRs) for the registered domain, including Type NS and Type A records.
- Additional resource records, such as Type A for the Web server ([www.networkutopia.com](http://www.networkutopia.com)) and Type MX for the mail server (mail.networkutopia.com), need to be entered into the authoritative DNS servers.
- The DNS database can be configured statically or dynamically using DNS protocol updates.
- Once the domain registration and DNS configuration are completed, users can access the website ([www.networkutopia.com](http://www.networkutopia.com)) and send emails to the domain's mail server (mail.networkutopia.com).
- When a user, such as Alice in Australia, wants to view the webpage, her host sends a DNS query to her local DNS server, which contacts a TLD com server.
- The TLD com server replies with the Type NS and Type A resource records, providing the IP address of the Web server.
- The local DNS server sends a query to the IP address of the authoritative DNS server (e.g., 212.212.212.1) for the Type A record of [www.networkutopia.com](http://www.networkutopia.com), obtaining the IP address of the desired Web server.
- Alice's browser can now establish a TCP connection with the Web server's IP address (e.g., 212.212.71.4) and send an HTTP request.
- This information highlights the process of registering a domain name, entering records into the DNS database, the role of registrars, the interaction between DNS servers, and the resolution of domain names to IP addresses for accessing webpages. It emphasizes the complexity behind web surfing and the underlying mechanisms of DNS.
- ---

### Peer-to-Peer File Distrubution
- Client-server architectures rely on always-on infrastructure servers, while P2P architectures involve intermittent connections between peers.
- P2P file distribution allows peers to redistribute portions of the file they have received, reducing the burden on the server and utilizing peer-to-peer communication.
- BitTorrent is the most popular P2P file distribution protocol, with multiple independent BitTorrent clients conforming to the protocol.
- P2P architectures exhibit self-scalability, where the distribution time for a fixed set of peers increases linearly with the number of peers.
- A quantitative model compares client-server and P2P architectures for file distribution.
- In the client-server architecture, the server must transmit one copy of the file to each peer, resulting in a minimum distribution time of NF/us, where NF is the file size and us is the server's upload rate.
- The minimum distribution time in the client-server architecture is also influenced by the download rate of the peer with the lowest download rate, dmin.
- The lower bound on the distribution time in the client-server architecture is given by Dcs = max(NF/us, F/dmin).
- The distribution time in the client-server architecture increases linearly with the number of peers, N.
- P2P architectures offer potential advantages in scalability as the distribution time does not increase linearly with the number of peers.
- The specific example highlights the scalability challenges faced by client-server architectures and the potential benefits of P2P architectures in file distribution.
- In a P2P architecture, each peer can assist in distributing the file, redistributing the data it has received to other peers.
- Calculating the distribution time in a P2P architecture is more complex than in a client-server architecture.
- The minimum distribution time in P2P depends on how peers distribute portions of the file to each other.
- Observations for the minimum distribution time in P2P include: the server must send each bit of the file at least once, the peer with the lowest download rate has a minimum distribution time of F/dmin, and the total upload capacity of the system cannot exceed utotal.
- The minimum distribution time in P2P, denoted by DP2P, is obtained by combining these observations.
- Equation 2.2 provides a lower bound for the minimum distribution time in P2P architecture.
- In reality, where file chunks are redistributed, Equation 2.2 serves as a good approximation of the actual minimum distribution time.
- The comparison in Figure 2.23 shows that the minimum distribution time for P2P architecture is always less than that of the client-server architecture.
- The minimum distribution time in P2P architecture is less than one hour for any number of peers, indicating self-scalability.
- P2P architecture scalability is due to peers being both redistributors and consumers of bits.
- P2P architectures offer advantages in terms of minimal distribution time and self-scaling capabilities compared to client-server architectures for file distribution.
- ![[Pasted image 20230512181411.png]]


**BitTorrent**
- BitTorrent is a popular P2P protocol for file distribution.
- In BitTorrent, a collection of peers participating in the distribution of a file is called a torrent.
- Peers in a torrent download equal-size chunks of the file from each other.
- When a peer joins a torrent, it registers with a tracker, which keeps track of participating peers.
- The tracker randomly selects a subset of peers and provides their IP addresses to the new peer.
- The new peer establishes TCP connections with these neighboring peers.
- Peers in a torrent have subsets of chunks from the file, and they periodically exchange lists of chunks they have.
- The rarest first technique is used to prioritize requesting the rarest chunks from neighbors, aiming to equalize the number of copies of each chunk in the torrent.
- BitTorrent uses a trading algorithm where peers prioritize trading with neighbors who are supplying data at the highest rate.
- Peers periodically select four top uploaders and one optimistically unchoked peer to exchange chunks with.
- Random neighbor selection allows new peers to get chunks and facilitates finding compatible trading partners.
- Other neighboring peers are "choked" and do not receive chunks from a peer.
- BitTorrent has additional mechanisms such as mini-chunks, pipelining, random first selection, endgame mode, and anti-snubbing.
- The trading incentive mechanism in BitTorrent is referred to as tit-for-tat, which encourages reciprocal sharing.
- BitTorrent's tit-for-tat incentive scheme has been shown to be effective, despite some circumvention attempts.
- BitTorrent is widely used, with millions of simultaneous peers actively sharing files in hundreds of thousands of torrents.
- Distributed Hash Tables (DHTs) are another application of P2P, where a simple database is distributed over peers in a P2P system.
- DHTs have been implemented in BitTorrent and have been extensively researched.
---
### Video Streaming and Content Distribution Networks

By many estimates, streaming video—including Netflix, YouTube and Amazon
Prime—account for about 80% of Internet traffic in 2020 [Cisco 2020]. This section
we will provide an overview of how popular video streaming services are implemented
in today’s Internet. We will see they are implemented using application-level
protocols and servers that function in some ways like a cache.

###### Internet Video
- Internet video streaming involves sending requests to servers to view prerecorded videos on demand.
- Video is a sequence of images displayed at a constant rate, typically 24 or 30 images per second.
- Uncompressed digital video consists of pixels encoded into bits to represent luminance and color.
- Video can be compressed to trade off video quality with bit rate.
- Compression algorithms can compress video to any desired bit rate.
- Compressed Internet video ranges from 100 kbps for low-quality video to over 4 Mbps for streaming high-definition movies.
- High-definition 4K streaming envisions a bitrate of more than 10 Mbps.
- Video streaming at high bit rates can result in significant traffic and storage requirements.
- Average end-to-end throughput is the most important performance measure for streaming video, ensuring the network can provide a throughput at least as large as the video's bit rate.
- Multiple versions of the same video can be created at different quality levels using compression.
- Different versions of the video can be offered at rates such as 300 kbps, 1 Mbps, and 3 Mbps.
- Users can choose the version of the video based on their available bandwidth, with higher-speed connections opting for higher quality versions and slower connections opting for lower quality versions.

###### HTTP Streaming and DASH
- Internet video companies distribute multi-Mbps streams to millions of users daily.
- Building a single massive data center to stream videos directly to clients worldwide has drawbacks, including potential throughput limitations, wasted network bandwidth, and single point of failure.
- Content Distribution Networks (CDNs) are used to distribute video data to users worldwide.
- CDNs manage servers in multiple geographically distributed locations and store copies of videos.
- CDNs aim to direct user requests to the closest CDN location for better user experience.
- CDNs can be private (owned by the content provider) or third-party (distributing content on behalf of multiple providers).
- CDNs can adopt different server placement philosophies: "Enter Deep" by deploying server clusters in access ISPs worldwide, or "Bring Home" by building large clusters at a smaller number of sites.
- CDNs replicate content across their clusters but may not place a copy of every video in each cluster.
- CDNs use a pull strategy, where a cluster retrieves a requested video if it's not stored locally and streams it to the client while storing a copy locally.
- Web caching is employed to remove videos from a cluster's storage that are not frequently requested when the storage becomes full.

**CDN Operation**
- CDNs use DNS to intercept and redirect user requests for specific videos.
- When a user clicks on a video link, their host sends a DNS query for the corresponding URL.
- The user's Local DNS Server (LDNS) relays the DNS query to the authoritative DNS server for the content provider.
- The content provider's authoritative DNS server returns a hostname in the CDN's domain instead of an IP address.
- The DNS query enters the CDN's private DNS infrastructure, and the user's LDNS sends a second query for the CDN hostname.
- The CDN's DNS system returns the IP addresses of a CDN content server to the LDNS, specifying the server from which the client will receive the content.
- The LDNS forwards the IP address of the content-serving CDN node to the user's host.
- The client establishes a direct TCP connection with the content server using the provided IP address.
- The client issues an HTTP GET request for the video, and if Dynamic Adaptive Streaming over HTTP (DASH) is used, the server sends a manifest file with URLs for different versions of the video.
- The client dynamically selects and requests video chunks from the different versions based on its capabilities and available bandwidth.

**Cluster Selection Strategies:**
CDNs employ various cluster selection strategies to direct clients to server clusters or data centers within the CDN. Some common approaches include:
- Geographical proximity: Assigning clients to the cluster that is geographically closest to their location. This is determined by mapping the client's LDNS IP address to a geographic location using commercial geo-location databases. While this strategy works well for many clients, it may not always result in the best network path or account for variations in delay and available bandwidth.
- Real-time measurements: CDNs periodically perform measurements of delay and loss performance between their clusters and clients. This can involve sending probes (e.g., ping messages or DNS queries) from clusters to LDNS servers worldwide. This approach allows CDNs to dynamically determine the best cluster for a client based on current traffic conditions. However, some LDNS servers may be configured to not respond to such probes.

***Case Study: Netflix and YouTube***

*Netflix:*
as a leading online movies and TV series provider, has two major components for video distribution: the Amazon cloud and its private CDN infrastructure.
- Content ingestion: Netflix receives studio master versions of movies and uploads them to hosts in the Amazon cloud for processing.
- Content processing: The Amazon cloud creates various formats and bit rates suitable for different client video players.
- Uploading versions to CDN: Once all versions of a movie are created, the Amazon cloud uploads them to Netflix's CDN.

- Initially, Netflix used third-party CDNs for video distribution, but it later built its own private CDN. Netflix's CDN includes server racks in Internet Exchange Points (IXPs) and within residential ISPs. The racks in IXPs contain the entire Netflix streaming video library, while ISP locations house selected popular videos. Netflix uses push-caching to populate its CDN servers during off-peak hours.

- When a user selects a movie to play, Netflix's software determines which CDN server has a copy of the movie and selects the best server based on the client's ISP or nearby IXP. Netflix sends the client the specific server's IP address and a manifest file with URLs for different versions of the movie. The client and CDN server interact using a proprietary version of DASH for adaptive streaming.

- Netflix's architecture embodies key principles such as adaptive streaming and CDN distribution. Their private CDN allows direct communication between the client and CDN servers, eliminating the need for DNS redirect. Additionally, Netflix uses push caching instead of pull caching for content delivery.

*YouTube:*
as the world's largest video-sharing site, handles an enormous amount of video content with billions of daily views. YouTube uses CDN technology extensively for video distribution, similar to Netflix. Here are some key aspects of YouTube's operation:

CDN Usage:
- YouTube utilizes its own private CDN infrastructure, consisting of server clusters deployed in numerous Internet Exchange Points (IXPs) and Internet Service Provider (ISP) locations.
- Videos are distributed from these CDN locations as well as directly from Google's large data centers.
- Google employs pull caching, where CDN servers retrieve videos dynamically during cache misses, as described in Section 2.2.5 of the text.
- DNS redirect is also used to direct clients to the appropriate cluster. Generally, the cluster selection strategy aims to minimize the Round Trip Time (RTT) between the client and cluster. However, load balancing considerations may occasionally direct the client to a more distant cluster.

Video Streaming and Formats:
- YouTube employs HTTP streaming for video delivery. It offers a limited number of different versions for each video, with varying bit rates and quality levels.
- Unlike Netflix, YouTube does not use adaptive streaming techniques like DASH. Instead, users manually select the desired version based on their preferences.
- YouTube implements the use of HTTP byte range requests to limit the transmitted data flow after prefetching a target amount of video. This helps conserve bandwidth and server resources, reducing unnecessary repositioning or early termination.

Video Upload and Processing:

- YouTube receives millions of video uploads daily from content creators. These uploads occur over HTTP from the client to the server.
- Upon receiving a video, YouTube processes it within Google's data centers. The video is converted to a YouTube-compatible format and multiple versions are created at different bit rates.

Overall, YouTube's video distribution infrastructure, leveraging its private CDN and data centers, allows for efficient delivery of a vast amount of user-generated content to viewers worldwide.


### Application Layer Protocol requests:

Here is a collection of diverse protocols implemented in the Application layer, and how a captured TCP stream in Wireshark would look like. 


#### FTP ( File Transfer Protocol)
Capture in Wireshark
```sql
220 Service ready for new user.
USER anonymous
331 User name okay, need password.
PASS guest
230 User logged in, proceed.
PWD
257 "/"
QUIT
221 Service closing control connection.
```
Briefly and in your own words, answer the following questions.
1. What layer does this protocol belong to?
2. What services does this protocol provide?
3. Provide a short explanation of the line that begins with 'PASS'. Note: This question is not about TCP but about the protocol whose messages are being exchanged.
   
**Solution:**
1. This belong to the application layer
2. FTP, File Transfer Protocol is a standard internet protocol that transmits files from one host to another over a TCP-based network. FTP is built on a client-server architecture. 
3. The PASS line is the respons the server gets for requesting authorization from the user, and receiving the password, which in this example is guest, for the user anonymous.


#### DNS (Domain Name System)
Capture in Wireshark:
```css
;; ->>HEADER<<- opcode: QUERY, status: NOERROR, id: 12345
;; flags: qr rd ra; QUERY: 1, ANSWER: 1, AUTHORITY: 0, ADDITIONAL: 0

;; QUESTION SECTION:
;www.example.com.        IN    A

;; ANSWER SECTION:
www.example.com.    1234    IN    A    192.0.2.42

```
Briefly and in your own words, answer the following questions.
1. What layer does this protocol belong to?
2. What services does this protocol provide?
3. Provide a short explanation of the line that begins with ';; ANSWER SECTION'. Note: This question is not about TCP but about the protocol whose messages are being exchanged.

**Solution:**
1. Application layer
2. DNS is the protocol that translates human-friendly domain names into their corresponding IP addresses. This makes it easier for user on the web to browse websites, without having to remember a the IP address numbers to get to their correct location.
3. the ;;ANSWER SECTION, is where the DNS response message to the user who sent the DNS query, and tells the user what the IP address of that requested domain is.


#### DHCP(Dynamic Host Configuration Protocol)
Capture in Wireshark:
```yaml
Message type: Boot Request (1)
Hardware type: Ethernet
Hardware address length: 6
Hops: 0
Transaction ID: 0x3903F326
Seconds elapsed: 0
Bootp flags: 0x0000 (Unicast)
Client IP address: 0.0.0.0
Your (client) IP address: 0.0.0.0
Next server IP address: 0.0.0.0
Relay agent IP address: 0.0.0.0
```
Briefly and in your own words, answer the following questions.
1. What layer does this protocol belong to?
2. What services does this protocol provide?
3. Provide a short explanation of the line that begins with 'Transaction ID'. Note: This question is not about TCP but about the protocol whose messages are being exchanged.

**Solution:**
1. Application Layer
2. DHCP is a network management protocol used to automate the process of configuring devices on IP networks. It assigns IP-addresses, subnet mask, default gateways, and other parameters. 
3. the `Transaction ID` line refers to an identifies which is unique for each DHCP transaction, which in this example is a client obtaining an IP address from the DHCP server.


#### Telnet
Capture in Wireshark:
```sql
Trying 192.0.2.23...
Connected to 192.0.2.23.
Escape character is '^]'.
Username: test
Password: test
Last login: Mon Sep 13 09:55:00 from 192.0.2.42
test@ubuntu:~$
```
Briefly and in your own words, answer the following questions.
1. What layer does this protocol belong to?
2. What services does this protocol provide?
3. Provide a short explanation of the line that begins with 'Last login'. Note: This question is not about TCP but about the protocol whose messages are being exchanged.

**Solution:**
1. Application Layer
2. Telnet is a text-based interface for remote communication with another device over a network. This allows for a user of one machine, to log into another over the network and execute commands or manage services. 
3. the last login line provides the user information about the last successful login to the system. As you can see, date, month, time and IP.


### SSH (Secure Shell)
Capture in Wireshark:
```
SSH-2.0-OpenSSH_7.9
SSH-2.0-OpenSSH_7.9
KEXINIT
KEXINIT
KEXDH_REPLY
NEWKEYS
SERVICE_REQUEST
SERVICE_ACCEPT
USERAUTH_REQUEST
USERAUTH_SUCCESS
CHANNEL_OPEN
CHANNEL_OPEN_CONFIRMATION
```
Briefly and in your own words, answer the following questions.
1. What layer does this protocol belong to?
2. What services does this protocol provide?
3. Provide a short explanation of the line that begins with 'USERAUTH_SUCCESS'. Note: This question is not about TCP but about the protocol whose messages are being exchanged.

**Solution:**
1. Application Layer
2. SSH(Secure Shell) is a protocol that provides secure channel over a unsecured network, where it can be used to handle network operations such as executing commands, manage files, and config  etc. on a remote server.  SSH uses encryption to secure the data that is being transmitted over the channel. 
3. the USER_AUTH_SUCESS line indicates that the authentication process was successful, and that the client has provided the correct credentials, and can access the server. 


### SMTP (Simple Mail Transfer Protocol)
Capture in Wireshark:
```sql
220 smtp.example.com ESMTP Postfix
EHLO alice.example.com
250-smtp.example.com
MAIL FROM:<alice@example.com>
250 2.1.0 Ok
RCPT TO:<bob@example.com>
250 2.1.5 Ok
DATA
354 End data with <CR><LF>.<CR><LF>
Subject: Hello Bob
Hi Bob, How are you?
.
250 2.0.0 Ok: queued as C1F40C0548
QUIT
221 2.0.0 Bye
```
Briefly and in your own words, answer the following questions.
1. What layer does this protocol belong to?
2. What services does this protocol provide?
3. Provide a short explanation of the line that begins with 'DATA'. Note: This question is not about TCP but about the protocol whose messages are being exchanged.

**Solution:**
1. Application Layer
2. SMPT (Simple Mail Transfer Protocol) is a protocol that is responsible for email transmission over the internet, between two host. Its responsible for sending, receiving and relaying outgoing mail between senders and receivers.
3. The `DATA` line signals to the server that this is the start of the message body, which then the server responds on the line after, initiating an invitation to transmit the actual content of the message.


### HTTP (Hypertext Transfer Protocol
Capture in Wireshark:
```HTTP
GET / HTTP/1.1
Host: www.example.com
User-Agent: Mozilla/5.0
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: en-US,en;q=0.5
Accept-Encoding: gzip, deflate
Connection: keep-alive
```
Briefly and in your own words, answer the following questions.
1. What layer does this protocol belong to?
2. What services does this protocol provide?
3. Provide a short explanation of the line that begins with 'GET'. Note: This question is not about TCP but about the protocol whose messages are being exchanged.

**Solution:**
1. Application Layer
2. HTTP, Hyperlinks, Hypermedia, web server - browser, fundamental structure, etc
3. GET request, is a method in HTTP, where it request data from a specified resource. In this case it is requesting the root document, and its indicated that its using HTTP1.1 version. 

### SNMP (Simple Network Management Protocol)
Capture in Wireshark:
```HTTP
SNMPv2-MIB::sysDescr.0 = STRING: Linux 3.10.0-957.27.2.el7.x86_64 #1 SMP Mon Jul 29 17:46:05 UTC 2019 x86_64
SNMPv2-MIB::sysObjectID.0 = OID: NET-SNMP-MIB::netSnmpAgentOIDs.10
DISMAN-EVENT-MIB::sysUpTimeInstance = Timeticks: (20848400) 2 days, 10:01:24.00
SNMPv2-MIB::sysContact.0 = STRING: Root <root@localhost> (configure /etc/snmp/snmp.local.conf)
SNMPv2-MIB::sysName.0 = STRING: localhost.localdomain
```
Briefly and in your own words, answer the following questions.
1. What layer does this protocol belong to?
2. What services does this protocol provide?
3. Provide a short explanation of the line that begins with 'SNMPv2-MIB::sys# Assistant will generate the rest of the questions based on the user's request

**Solution:**
1. Application Layer
2. The SNMP protocol provides network management services, that allows admins to manage and monitor network devices, collect data about their performance and status, and do configs.
3. The line mentioned is describing the system which the SNMP agent is running. We can see its running Linux and its kernel version.

### RTP (Real-time Transport Protocol)
Capture:
```yaml
RTP
[Stream setup by SDP (frame 284)]
10.. .... = Version: RFC 1889 Version (2)
..0. .... = Padding: False
...0 .... = Extension: False
.... 0000 = Contributing source identifiers count: 0
0... .... = Marker: False
Payload type: ITU-T G.711 PCMU (0)
Sequence number: 0
[Extended sequence number: 0]
Timestamp: 12345
Synchronization Source identifier: 0x12345678 (305419896)
```
Briefly and in your own words, answer the following questions.
1. What layer does this protocol belong to?
2. What services does this protocol provide? 

**Solution:**
1. Application
2. The RTP (Real-Time Transport Protocol) provides services for real-time transmissions of multimedia data, such as video and audio, over IP networks. Commonly used in VoIP etc. 

### SIP (Session Initiation Protocol)
Capture in Wireshark:
```HTTP
INVITE sip:bob@biloxi.com SIP/2.0
Via: SIP/2.0/UDP pc33.atlanta.com;branch=z9hG4bKhjhs8ass877
Max-Forwards: 70
To: Bob <sip:bob@biloxi.com>
From: Alice <sip:alice@atlanta.com>;tag=1928301774
Call-ID: a84b4c76e66710
CSeq: 314159 INVITE
Contact: <sip:alice@pc33.atlanta.com>
Content-Type: application/sdp
Content-Length: 142
```
Briefly and in your own words, answer the following questions.
1. What layer does this protocol belong to?
2. What services does this protocol provide?
3. Provide a short explanation of the line that begins with 'INVITE sip:[bob@biloxi.com](mailto:bob@biloxi.com)'.

**Solution:**
1. Application Layer
2. The Session Initiation Protocol provides services for initiating, modifying, and terminating multimedia sessions such as voice and video calls over IP network.  It handles setup, manages, and teardown, allowing real-time communication between two people.
3. The line is a request message, an INVITE request that is used to initiate a session with the email in the line. Its sent to the client, and we can see its using SIP 2.0.


### DHCP (Dynamic Host Configuration Protocol)
Capture in Wireshark:
```HTTP
DHCP Discover - Transaction ID 0x3d307674
DHCP Offer - Transaction ID 0x3d307674
DHCP Request - Transaction ID 0x3d307674
DHCP ACK - Transaction ID 0x3d307674
```
Briefly and in your own words, answer the following questions.
1. What layer does this protocol belong to?
2. What services does this protocol provide?
3. Provide a short explanation of the line that begins with 'DHCP Discover'.

**Solution:**
1. Application
2. the Dynamic Host Configuration Protocol (DHCP) provides services for dynamically assigning IP addresses, along with other parameters, to the devices in a network. It manages and provides the devices on a network subnet mask, IP addresses, gateways, dns server addresses, etc.
3. the line represent a broadcast request to discover DHCP servers available on the network.

### NTP (Network Time Protocol)
Capture in Wireshark:
```Css
NTP Version 4, client
NTP Version 4, server
```
Briefly and in your own words, answer the following questions.
1. What layer does this protocol belong to?
2. What services does this protocol provide?
3. Provide a short explanation of the line that begins with 'NTP Version 4, client'

**Solution:**
1. Application
2. the Network Time Protocol provides the service to synchronize the clocks of network devices, allowing them to obtain accurate time information from reference time source. 
3. The line that begins with 'NTP Version 4, client' represents an NTP message indicating that the device is operating as an NTP client. In NTP, the client initiates time synchronization by sending requests to NTP servers to obtain accurate time information. The NTP client uses this information to adjust its own clock to align with the reference time provided by the NTP server.