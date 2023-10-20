> *Before any network communications can occur, a physical connection to a local network must be established*


When connecting networks, a physical connection could be both a wireless connection using radio waves, or using a cable.

The type of physical connection that is used, is dependent on how the network is setup and its needs.
Wireless connectivity is common in networks for both individuals and businesses, same goes for cables.
The access points are then again wired to other devices outwards in the network.

If you are not connected with an ethernet cable, connecting with a Network Interface Card is possible. The **Network Interface Cards** has an interface for cable and wireless connection on regular laptops (usually), but some devices may not. E.g., an printer may only have a NIC with Ethernet NIC only, and needs to connect to an ethernet port to access the internet and receive printing orders. Other devices such as newer laptops, smartphones and iPads might only contain a WLAN NIC and must use a wireless connection to connect to internet.

The OSI Physical Layer is "made" so that is can transport the bits in a ***data link layer*** frame out and across into the network. 
- This layer accepts a complete frame from the data link layer and encodes it as a series of signals that are transmitted to the local media.

---
## Physical Layer Characteristics
---
### Physical Layer Standards

The protocols and operations of the upper OSI layers are performed using software designed by software engineers and computer scientists. The services and protocols in the TCP/IP suite are defined by the Internet Engineering Task Force (IETF).

The physical layer consists of electronic circuitry, media, and connectors developed by engineers. Therefore, it is appropriate that the standards governing this hardware are defined by the relevant electrical and communications engineering organizations.

There are many different international and national organizations, regulatory government organizations, and private companies involved in establishing and maintaining physical layer standards. For instance, the physical layer hardware, media, encoding, and signaling standards are defined and governed by these standards organizations:
- International Organization for Standardization (ISO)
- Telecommunications Industry Association/Electronic Industries Association (TIA/EIA)
- International Telecommunication Union (ITU)
- American National Standards Institute (ANSI)
- Institute of Electrical and Electronics Engineers (IEEE)
- National telecommunications regulatory authorities including the Federal Communication Commission (FCC) in the USA and the European Telecommunications Standards Institute (ETSI)


In addition to these, there are often regional cabling standards groups such as CSA (Canadian Standards Association), CENELEC (European Committee for Electrotechnical Standardization), and JSA/JIS (Japanese Standards Association), which develop local specifications.
![[Pasted image 20230925171134.png]]

### Physical Components

The physical layer is addressed by these three function areas:
- Physical Components
- Encoding
- Signalling

When talking about physical components in a network, we are referring to electronic hardware devices, media and other connectors that transmit the signals that represent the bits. Components such as NIC, interfaces and connectors, cable materials, and cable design are all specified after a standard that is associated with the physical layer.

### Encoding
When talking about encoding in a network, we are talking about the method encoding, which is a way of converting a stream of bits into a predefined "code". These codes are group of bits that is used to provide a predictable and easy pattern used to represent digital information within a frame.
- Can be similar to Morse code, where a message is encoded using a series of dots and dashes.

**Example:**
Manchester encoding represents a 0 bit by a high to low voltage transition, and a 1 bit is represented as a low to high voltage transition. An example of Manchester encoding is illustrated in the figure. The transition occurs at the middle of each bit period. This type of encoding is used in 10 Mbps Ethernet. Faster data rates require more complex encoding. Manchester encoding is used in older Ethernet standards such as 10BASE-T. Ethernet 100BASE-TX uses 4B/5B encoding and 1000BASE-T uses 8B/10B encoding.
![[Pasted image 20230925172509.png]]

### Signaling

The physical layer is responsible to generate the electrical, optical or wireless signals that is used to represent the 1's and 0's on the media. The way these bits are represented are named/called ***signaling method***. The layer standards is responsible and must define what type of signals that represent which number. This can for example be done in a change of the level of an electric signal or optical pulse, where e.g., an long pulse might represent 1, and a short can represent a 0. 
- this is also similar to Morse Code, where the length of the beep might represent certain things, and short represent others.

Here is some examples:

**Microwave Signals Over Wireless**
![[Pasted image 20230925173155.png]]

**Copper Cable**
![[Pasted image 20230925173230.png]]

**Fiber Optic Cable**
![[Pasted image 20230925173257.png]]

### Bandwidth
When we discuss data transfer, the term "bandwidth" is used to describe the process. This is the capacity at which a medium can carry data. Digital bandwidth is measured in the amount of data that can flow from one place to another given amount of time. 
- Common measures are:
	- kbps
	- Mbps
	- Gbps
Bandwidth is sometimes thought of as the speed that bits travel, however this is not accurate. For example, in both 10Mbps and 100Mbps Ethernet, the bits are sent at the speed of electricity. The difference is the number of bits that are transmitted per second.

A combination of factors determines the practical bandwidth of a network:
- Properties of the physical media
- Technologies chosen for signaling and detecting network signals

#### Bandwidth Terminology
> [[Physical Layer#Latency|Latency]], Throughput, Goodput

##### Latency
Described as the amount of time, including delays for data that is traveling from one point to another.  
In an internetwork, or a network with multiple segments, throughput cannot be faster than the slowest link in the path from source to destination. Even if all, or most, of the segments have high bandwidth, it will only take one segment in the path with low throughput to create a bottleneck in the throughput of the entire network.

##### Throughput
The measure of the transfer of bits across media over a period of time. When describing throughput we usually do not see a match between the bandwidth and the [[Application Layer#*Throughput*|throughput]] in the physical layer implementations. 
- is usually/often lower than bandwidth, due to several different factors influencing the throughput.

*Factors that might interfere:*
- Amount of traffic
- Types of traffic
- A latency between the number of network devices that is encountered when communicating from the source to endpoint/destination.

##### Goodput
A measurement described as the transfer of usable data, over a given period of time. If you eliminate the overhead the different protocols that act and interfere when sending a packet over a network, you get the goodput. 

*Goodput = Throughput - traffic overhead*

List off overhead that is removed for traffic to be considered goodput:
- Session establishment data
- ACK (acknowledgements)
- Encapsulation
- Retransmitted bits

Goodput is **always** lower than throughput, which is also generally lower than the bandwidth. 


**Questions**
#netacad

- What is goodput? :: A measurement described as the transfer of usable data, over a given period of time
- How does the presence of only one segment with low throughput affect the entire network?:: The presence of even one segment with low throughput can create a bottleneck, limiting the throughput of the entire network to the throughput of that segment.
<!--SR:!2023-09-30,3,250-->
- Why is bandwidth not equivalent to the speed at which bits travel? :: Because the speed at which bits travel, such as the speed of electricity in Ethernet, is constant. Bandwidth refers to the number of bits transmitted per second, not their speed.
<!--SR:!2023-09-30,3,250-->
- Define "Latency" in network terminology. :: The amount of time, including delays, it takes for data to travel from one point to another.
- How does latency impact throughput in a multi-segment network? :: Throughput cannot exceed the speed of the slowest link in the path, and any segment with low throughput can create a bottleneck for the entire network.
- Why is Goodput always lower than Throughput? :: Because Goodput only considers usable data, excluding overhead such as session establishment data, ACK, encapsulation, and retransmitted bits.
- List the overhead elements removed to calculate Goodput. :: Session establishment data, ACK (acknowledgements), Encapsulation, Retransmitted bits
- What are the two types of physical connections when connecting networks? :: Both a wireless connection using radio waves and using a cable.
- How are access points connected to other devices in the network? :: The access points are wired to other devices outwards in the network.
- Do all devices have interfaces for both cable and wireless connections? :: No, some devices may only have a NIC with Ethernet NIC, and others might only contain a WLAN NIC.
- Who defines the services and protocols in the TCP/IP suite? :: The Internet Engineering Task Force (IETF) defines the services and protocols in the TCP/IP suite.
- What does the physical layer consist of? :: The physical layer consists of electronic circuitry, media, and connectors.
- What is the role of the OSI Physical Layer in relation to the data link layer frame? :: It accepts a complete frame from the data link layer and encodes it as a series of signals that are transmitted to the local media.
- What are the three function areas addressed by the physical layer? :: Physical Components, Encoding, Signalling
- What are referred to as physical components in a network? :: Electronic hardware devices, media, and other connectors that transmit the signals representing the bits, such as NIC, interfaces and connectors, cable materials, and cable design.
- What is the responsibility of the physical layer in terms of signaling? :: It is responsible to generate the electrical, optical, or wireless signals used to represent the 1's and 0's on the media.
<!--SR:!2023-09-28,1,230-->
- What is a signaling method in the context of the physical layer? :: It is the way the bits are represented, defined by the layer standards, such as a change in the level of an electric signal or optical pulse.
- What does encoding in networks provide? :: It provides a predictable and easy pattern used to represent digital information within a frame by converting a stream of bits into a predefined "code".


---
## Copper Cabling

> Copper cabling is the most common type of cabling used in networks today. Its often used because of the inexpensive nature, where its easy to install, and has low resistance to electrical current. Downsides are limited distance and signal interference.

When data is transmitted on copper cables, it is transported as electrical pulses, where a detector at the network interface of the destination receive that signal and interpret and successfully decode it to match the signal sent.
The problem arrives when the signal needs to travel longer distances, because of the deterioration of the signal during longer travel time.
- We refer to this as **signal attenuation**
- This is regulated by giving all copper media strict distance limitations that is specified by the guiding standards

The timing & voltage values of the electrical pulses sent through a copper wire is also susceptible to interference from two sources:

1. **Electromagnetic Interference (EMI)** or **Radio frequency interference (RFI)**. EMI and RFI signals can corrupt and distort the data signals being carried in copper media (copper cable). There are several potential sources of EMI and RMI that can include radio waves and electromagnetic devices, such as fluorescent lights or electric motors. 
2. **Crosstalk** is a disturbance caused by the electric or magnetic fields of a signal on one wire to the signal in an adjacent wire, more precise wires that lie next to each other. For example in telephone circuits, crosstalk can occur so that the voices from another conversation is heard from the adjacent circuit. Specially when an electrical current flows through a wire, since it creates a small circular magnetic field around the wire, which then can be picked up by an adjacent wire. 


The figure shows how data transmission can be affected by interference.
![[Pasted image 20230927171607.png]]

1. A pure digital signal is transmitted
2. On medium, there is an interference signal
3. The digital signal is corrupted by interference signal
4. The receiving computer reads a changed signal. Notice that a 0 bit is now interpreted as a 1 bit.

**Measures taken when using copper cables**
To counter negative effects of EMI and RFI, some types of copper cables are wrapped in metallic shielding and require proper ground connections.@

To counter the negative effects of crosstalk, some types of copper cables have opposing circuit wire pairs twisted together, which effectively cancels the crosstalk. 

The susceptibility of copper cables to electronic noise can also be limited using these recommendations:
- Selecting the cable type or category most suited to a given networking environment
- Designing a cable infrastructure to avoid known and potential sources of interference in the building structure
- Using cabling techniques that include the proper handling and termination of the cables


### Types of Copper Cabling
> There are three main types of copper media used in networking
![[Pasted image 20230927174350.png]]

#### Unshielded twisted-pair (UTP)
This is the most common cabling used in network media, terminated with RJ-45 connectors, and is used for interconnecting network hosts with intermediary network devices, such as switches and routers.

In LANs, UTP cable consists of four pairs of color-coded wires that have been twisted together and then encased in a flexible plastic sheath that protects from minor physical damage. When we twist the wires, it helps to protect against signal interference from other wires.

![[Pasted image 20230927175119.png]]

#### Shielded twisted-pair (STP)
STP provides better noise protection than UTP cabling. But the downside is that compared to [[Physical Layer#Unshielded twisted-pair (UTP)|UTP]] cable, the STP is significantly more expensive and difficult to install. The STP also uses a [RJ-45](https://no.wikipedia.org/wiki/RJ-45) connector, just like UTP cable. 

STP goes one step further then UTP cable, but both use wire twisting to counter crosstalk, the difference is that STP combines this with the technique of shielding to counter EMI and RFI. The shielded twisted-pair cable are terminated with special shielded STP data connectors. 
If the cable is improperly grounded, the shield can act as an antenna and pick up unwanted signals.

> In networking, terminating a cable means attaching a connector to the end of the cable. This connector allows the cable to be plugged into networking equipment, ensuring proper electrical contact and signal transmission between the cable and the equipment.

The STP cable shown uses four pairs of wires, each wrapped in a foil shield, which are then wrapped in an overall metallic braid or foil.

- What is the difference between UTP cable and STP cable?::Both use twisting wires, but STP uses shielding.

![[Pasted image 20230927181238.png]]


#### Coaxial Cable

> Coaxial cable, or coax for short, gets its name from the fact that there are two conductors that share the same axis

The coaxial cable consist of the following:
- A copper conductor is used to transmit the electronic signals
- A layer of flexible plastic insulation surrounds a copper conductor.
- The insulating material is surrounded in a woven copper braid, or metallic foil, that acts as the second wire in the circuit and as a shield for the inner conductor. This second layer, or shield, also reduces the amount of outside electromagnetic interference.
- The entire cable is covered with a cable jacket to prevent minor physical damage.
There are different types of connectors used with coax cable. The Bayonet Neill–Concelman (BNC), N type, and F type connectors are shown in the figure.

Although UTP cable has essentially replaced coaxial cable in modern Ethernet installations, the coaxial cable design is used in the following situations:
- **Wireless installations**: Coaxial cables attach antennas to wireless devices. The coaxial cable carries radio frequency (RF) energy between the antennas and the radio equipment.
- **Cable internet installations**: Cable service providers provide internet connectivity to their customers by replacing portions of the coaxial cable and supporting amplification elements with fiber-optic cable. However, the wiring inside the customer's premises is still coax cable.
![[Pasted image 20230927182407.png]]

---
## UTP Cabling

> Reasons for going into detail in UTP cabling: UTP is standard for the use in LANs, and it has its advantages and limitations, and we'll look at them deeper, and how we avoid problems

### Properties of UTP Cabling
When we use UTP cable as a network medium, the UTP cable consist of four pairs of color-coded copper wires that have been twisted together and then encased in a flexible plastic sheath. The shear small size gives an advantage when installing new network systems and lines.

As discussed in the [[Physical Layer#Unshielded twisted-pair (UTP)|UTP cable]] section above, we know that UTP does no take use of shielding like [[Physical Layer#Shielded twisted-pair (STP)|STP]] to counter the effects of EFI and RFI. Instead, cable designers have discovered other ways that they can limit the negative effect of crosstalk:
- **Cancellation**: Designers now pair wires in a circuit. When two wires in an electrical circuit are placed close together, their magnetic fields are the exact opposite of each other. Therefore, the two magnetic fields cancel each other and also cancel out any outside EMI and RFI signals.
- **Varying the number of twists per wire pair**: To further enhance the cancellation effect of paired circuit wires, designers vary the number of twists of each wire pair in a cable. UTP cable must follow precise specifications governing how many twists or braids are permitted per meter (3.28 feet) of cable. Notice in the figure that the orange/orange white pair is twisted less than the blue/blue white pair. Each colored pair is twisted a different number of times.

UTP cable relies solely on the cancellation effect produced by the twisted wire pairs to limit signal degradation and effectively provide self-shielding for wire pairs within the network media.
![[Pasted image 20230927184815.png]]

### UTP Cabling standards and Connectors
UTP cabling conforms to the standards established jointly by the TIA/EIA. Specifically, TIA/EIA-568 stipulates the commercial cabling standards for LAN installations and is the standard most commonly used in LAN cabling environments. Some of the elements defined are as follows:
- Cable types
- Cable lengths
- Connectors
- Cable termination
- Methods of testing cable

The electrical characteristics of copper cabling are defined by the Institute of Electrical and Electronics Engineers (IEEE). IEEE rates UTP cabling according to its performance. Cables are placed into categories based on their ability to carry higher bandwidth rates. For example, Category 5 cable is used commonly in 100BASE-TX Fast Ethernet installations. Other categories include Enhanced Category 5 cable, Category 6, and Category 6a.

Cables in higher categories are designed and constructed to support higher data rates. As new gigabit speed Ethernet technologies are being developed and adopted, Category 5e is now the minimally acceptable cable type, with Category 6 being the recommended type for new building installations.

The figure shows three categories of UTP cable:
- Category 3 was originally used for voice communication over voice lines, but later used for data transmission.
- Category 5 and 5e is used for data transmission. Category 5 supports 100Mbps and Category 5e supports 1000 Mbps
- Category 6 has an added separator between each wire pair to support higher speeds. Category 6 supports up to 10 Gbps.
- Category 7 also supports 10 Gbps.
- Category 8 supports 40 Gbps.

Some manufacturers are making cables exceeding the TIA/EIA Category 6a specifications and refer to these as Category 7.
![[Pasted image 20230927185053.png]]

UTP cable is usually terminated with an RJ-45 connector. The TIA/EIA-568 standard describes the wire colour codes to pin assignments (pinouts) for Ethernet cables.

As shown in the figure, the RJ-45 connector is the male component, crimped at the end of the cable.
![[Pasted image 20230927185540.png]]

The socket, shown in the figure, is the female component of a network device, wall, cubicle partition outlet, or patch panel. When terminated improperly, each cable is a potential source of physical layer performance degradation.
![[Pasted image 20230927185606.png]]
This figure shows an example of a badly terminated UTP cable. This bad connector has wires that are exposed, untwisted, and not entirely covered by the sheath.

**Poorly Terminated UTP Cable**
![[Pasted image 20230927185642.png]]
The next figure shows a properly terminated UTP cable. It is a good connector with wires that are untwisted only to the extent necessary to attach the connector.

**Properly Terminated UTP Cable**
![[Pasted image 20230927185721.png]]
**Note**: Improper cable termination can impact transmission performance.


### Straight-through and Crossover UTP Cables
>There are different situations that may require UTP cables to be wired to a different wiring convention than the standard, meaning that the individual wires in the cable have to be connected in a different order onto the pins in the RJ-45 connectors. 

There are two main cable types that are obtained by using specific wiring conventions:
- **Ethernet Straight-through:** the most common type of networking cable, and is used to interconnect a host to a switch, and a switch to a router.
- **Ethernet Crossover:** A cable used to interconnect similar types of devices, such as connecting a switch to a switch, host to a host, or a router to a router. But crossover cables are now considered legacy as NICs use medium-dependant interface crossover (auto-MDIX) to detect cable types and make the internal connection.

***Note:*** Cisco has a rollover cable, that is used to connect a workstation to a router, or a switch console port. 

If we use the wrong cable when using crossover and straight-through cables, it will not damage the devices, but no communication and connection will take place. This is a very common error and should be first on the troubleshoot list if you are experiencing network error where connection and communication does not happen.

### T568A and T658B Standards
![[Pasted image 20230928141351.png]]
Here we can observe the individual wire pairs for the T568A and T568B standards. 

### Cable Types and Standards
> The table shows the UTP cable type, related standards, and typical application of these cables.

| **Cable Type**            | **Standard**                       | **Application**                                                                                             |
| ------------------------- | ---------------------------------- | ----------------------------------------------------------------------------------------------------------- |
| Ethernet Straight-through | Both ends T568A or both ends T568B | Connects a network host to a network device such as a switch or hub                                         |
| Ethernet Crossover        | One end T568A, other end T568B     | Connects two network hosts Connects two network intermediary devices (switch to switch or router to router) |
| Rollover  |   Cisco Proprietary  | Connects a workstation serial port to a router console port, using an adapter  |

---

## Fiber-Optic Cabling
> Fiber-optic cabling is the other type of cabling used in networks. Because it is expensive, it is not as commonly used at the various types of copper cabling. But fiber-optic cabling has certain properties that make it the best option in certain situations, which you will discover in this topic.

### Properties of Fiber-Optic Cabling
A optical fiber cable can transmit data over longer distances and faster than any other network media out there. Fiber cables can transmit signals with less attenuation and is completely immune to EMI and RFI, unlike the copper wires. 
- Is commonly used to interconnect network devices

The Optical Fiber is flexible, but extremely thin, transparent strand of very pure glass, which almost as small as human hair. The bits are encoded on the fiber as light impulses, and the fiber-optic cables acts as a waveguide (or "light pipe") to transmit light between the two ends with minimal loss of signal.

As an analogy, consider an empty paper towel roll with the inside coated like a mirror. It is a thousand meters in length, and a small laser pointer is used to send Morse code signals at the speed of light. Essentially that is how a fiber-optic cable operates, except that it is smaller in diameter and uses sophisticated light technologies.
![[Pasted image 20230928142824.png]]

### Types of Fiber Media
We classify fiber-optic cables into two broadly types:
- Single-mode fiber (SMF)
- Multimode fiber (MMF)

#### *Single-Mode Fiber* 
SMF consists of a small core and uses expensive laser technology to send a single ray of light. It is most popular to use this in long-distance situations where the distance is spanning hundreds of kilometers, such as those required in long haul telephony and cable TV applications
![[Pasted image 20230928143529.png]]

#### *Multimode Fiber*
MMF consists of a larger core compared to SMF, and uses LED emitters to send light pulses through the cable. More specifically, light from an LED enters the multimode fiber at different angles. MMF are popular in LANs because they can be powered by low-cost LEDs. It provides a bandwidth up to 10 Gbps over link lengths of up to 550 meters
![[Pasted image 20230928143832.png]]
One of the highlighted differences between MMF and SMF is the amount of dispersion. 'Dispersion' refers to the spreading out of a light pulse over time. Increased dispersion means increased loss of signal strength. MMF has a greater dispersion than SMF, and thats why MMF can only travel up to 500 meters before signal loss.


#### Single-mode vs multi-mode
Single-mode fibers are suitable for long-distance, high-speed, and high-capacity applications due to their small core diameter and single light mode. In contrast, multimode fibers are more suitable for short-distance, lower-speed, and lower-capacity applications due to their larger core diameter and multiple light modes. The choice between single-mode and multimode fibers depends on the specific requirements of the application, such as distance, speed, capacity, and budget.

Here are the key differences between single-mode and multimode fiber cables:
##### 1. **Mode of Propagation:**
- **Single-mode Fiber:**
    - Transmits only one mode or ray of light directly down the fiber.
- **Multimode Fiber:**
    - Supports the transmission of multiple modes or rays of light, which reflect at different angles within the fiber.

##### 2. **Core Diameter:**
- **Single-mode Fiber:**
    - Has a smaller core diameter, typically around 9 micrometers.
- **Multimode Fiber:**
    - Has a larger core diameter, typically ranging from 50 to 62.5 micrometers.

##### 3. **Distance:**
- **Single-mode Fiber:**
    - Capable of transmitting signals over longer distances, often up to tens or even hundreds of kilometers without amplification.
- **Multimode Fiber:**
    - Suitable for shorter distances, typically up to 2 kilometers, due to modal dispersion.

##### 4. **Data Rate:**
- **Single-mode Fiber:**
    - Can support higher data rates due to the absence of modal dispersion.
- **Multimode Fiber:**
    - Has lower data rates compared to single-mode fibers over long distances.

##### 5. **Cost:**
- **Single-mode Fiber:**
    - Generally more expensive due to the precision required in manufacturing and the need for more expensive transceivers.
- **Multimode Fiber:**
    - Typically less expensive to manufacture and install, with lower-cost transceivers.

##### 6. **Applications:**
- **Single-mode Fiber:**
    - Ideal for long-distance telecommunications, CATV, and high-speed data applications.
- **Multimode Fiber:**
    - Commonly used for short-distance applications such as within buildings, data centers, and LANs.

##### 7. **Wavelengths:**
- **Single-mode Fiber:**
    - Typically operates at 1310 nm or 1550 nm wavelengths.
- **Multimode Fiber:**
    - Typically operates at 850 nm or 1300 nm wavelengths.

##### 8. **Color Code:**
- **Single-mode Fiber:**
    - Usually yellow.
- **Multimode Fiber:**
    - Usually orange or aqua, depending on the type.

### Fiber-Optic Cabling Usage

>Fiber-optic cabling is being used in these four types of industry at the moment:
- **Enterprise Networks**: is used for backbone cabling applications and interconnecting infrastructure devices
- **Fiber-to-the-Home**: used to provide always-on broadband services to homes and small businesses
- **Long-Haul Networks**: used by service providers to connect countries and cities
- **Submarine Cable Networks**: used to provide reliable high-speed, high-capacity solutions capable of surviving harsh undersea environments at up to transoceanic distances. 

### Fiber-Optic Connectors
An optical-fiber connector terminates the end of an optical fiber. A variety of optical-fiber connectors are available. The main differences among the types of connectors are dimensions and methods of coupling. Businesses decide on the types of connectors that will be used, based on their equipment.

**Note**: Some switches and routers have ports that support fiber-optic connectors through a small form-factor pluggable (SFP) transceiver. Search the internet for various types of SFPs.

#### *Straigth-Tip (ST) Connectors*
ST connectors were one of the first connector types used. The connector locks securely with a 'twist-on/twist-off' bayonet-style mechanism.
![[Pasted image 20230928145830.png]]

#### *Subscriber Connector (SC)*
SC connectors are often referred to as the 'square connectors' or 'standard connectors'. They are widely adopted LAN and WAN connectors that uses a push-pull mechanism to ensure positive insertion. The square connectors (SC) are used with both multimode and singe-mode fiber.
![[Pasted image 20230928150708.png]]

#### *Lucent Connector (LC) Simplex Connectors*
LC simplex connectors are a smaller version of the SC connector. These are sometimes called little or local connectors and are quickly growing in popularity due to their smaller size.
![[Pasted image 20230928150817.png]]

#### *Duplex Multimode LC Connectors*
A duplex multimode LC connector is similar to an LC simplex connector, but uses a duplex connector
![[Pasted image 20230928150917.png]]


***Funfact***: Until recently, light could only travel in one direction over optical fiber. Two fibers were required to support the full duplex operation. Therefore, fiber-optic patch cables bundle together two optical fiber cables and terminate them with a pair of standard, single-fiber connectors. Some fiber connectors accept both the transmitting and receiving fibers in a single connector known as a duplex connector, as shown in the Duplex Multimode LC Connector in the figure. BX standards such as 100BASE-BX use different wavelengths for sending and receiving over a single fiber.


### Fiber Patch Cords
> Fiber patch cords are required for interconnecting infrastructure devices. The use of color distinguishes between single-mode and multimode patch cords. A yellow jacket is for single-mode fiber cables and orange (or aqua) for multimode fiber cables.

#### *SC-SC Multimode Patch Cord* 
![[Pasted image 20230928151348.png]]

#### *LC-LC Single-Mode Patch Cord 
![[Pasted image 20230928151506.png]]

#### *ST-LC Multimode Patch Cord*
![[Pasted image 20230928151612.png]]

#### *SC-ST Single-Mode Patch Cord*
![[Pasted image 20230928151954.png]]

**Note**: Fiber cables should be protected with a small plastic cap when not in use.


### Fiber versus Copper
Fiber-optic cables hold numerous advantages over copper cables, such as Unshielded Twisted Pair (UTP) cables, especially in enterprise environments. Here’s a summarized and rephrased comparison of the two:

Fiber-optic cables are predominantly utilized as backbone cabling within enterprise settings, facilitating high-traffic, point-to-point connections between data distribution centers. They are also the preferred choice for connecting buildings within multi-building campuses. Their non-conductive nature and minimal signal loss make them ideal for such applications.

#### Comparison between UTP and Fiber-Optic Cabling:
- **Bandwidth:**
    - UTP supports bandwidths ranging from 10 Mb/s to 10 Gb/s.
    - Fiber-optic cables offer a significantly broader range, from 10 Mb/s to 100 Gb/s.
- **Distance:** 
    - UTP cables are suitable for relatively short distances, between 1 and 100 meters.
    - Fiber-optic cables can cover extensive distances, from 1 to 100,000 meters.
- **Immunity to Interference and Hazards:**
    - UTP has low immunity to Electromagnetic Interference (EMI) and Radio Frequency Interference (RFI) and is susceptible to electrical hazards.
    - Fiber-optic cables are completely immune to EMI, RFI, and electrical hazards, offering high safety and reliability.
- **Cost and Installation:**
    - UTP cabling and connectors are the least expensive and require the lowest level of skills to install, with minimal safety precautions needed.
    - Fiber-optic cabling, on the other hand, is more costly, necessitates advanced installation skills, and requires stringent safety precautions.

In summary, while UTP cabling is cost-effective and easy to install for shorter distances, fiber-optic cabling is superior in terms of bandwidth, distance coverage, and immunity to interferences and hazards, making it well-suited for high-traffic connections and inter-building linkages in enterprise environments.

--- 

## Wireless Media
>You may be reading this using a tablet or a smart phone. This is only possible due to wireless media, which is the third way to connect to the physical layer of a network.

### Properties of Wireless Media
Wireless media carry electromagnetic signals that represent the binary digits of data communications using radio or microwave frequencies.

Wireless media provide the greatest mobility options of all media, and the number of wireless-enabled devices continues to increase. Wireless is now the primary way users connect to home and enterprise networks.

These are some of the limitations of wireless:
- **Coverage area** - Wireless data communication technologies work well in open environments. However, certain construction materials used in buildings and structures, and the local terrain, will limit the effective coverage.
- **Interference** - Wireless is susceptible to interference and can be disrupted by such common devices as household cordless phones, some types of fluorescent lights, microwave ovens, and other wireless communications.
- **Security** - Wireless communication coverage requires no access to a physical strand of media. Therefore, devices and users, not authorized for access to the network, can gain access to the transmission. Network security is a major component of wireless network administration.
- **Shared medium** - WLANs operate in half-duplex, which means only one device can send or receive at a time. The wireless medium is shared amongst all wireless users. Many users accessing the WLAN simultaneously results in reduced bandwidth for each user.

Although wireless is increasing in popularity for desktop connectivity, copper and fiber are the most popular physical layer media for deployment of intermediary network devices, such as routers and switches.



