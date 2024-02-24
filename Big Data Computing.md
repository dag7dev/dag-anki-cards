# Big Data Computing - Flashcards (De Sensi)

TARGET DECK: Big Data Computing
START
Basic
Introduction:  
Back: 
a buzzword that describes 5 V words
- value, volume, variety, velocity, veracity

They means:
- **Value**: extracting knowledge from data is extremely valuable
- **Volume**: very large amount of data (orders of TB or PB)
- **Variety**: different formats of data: structured (relational tables), semistructured (JSON files), and unstructured (text/audio/video)
- **Velocity**: insane speed at which data is generated (e.g., Twitter stream)
- **Veracity**: reliability of the data used to drive decision processes
<!--ID: 1708701022738-->
END

---
START
Basic
Introduction: scale up vs. scale down
Back: 
Datacenters have two main options:
1. scale up: so buy wait for a faster CPU and faster Disk
	1. waiting is not an option
	2. buying same
2. scale out
	1. more hardware interconnected
	2. flexible: this is good
	3. it brings additional challenges
	4. machine learning is intensive, so we need to have a lot of computational power

Scale out is the only viable solution!
<!--ID: 1708701022740-->
END

---
START
Basic
Introduction: Describe a data center architecture
Back: 
![[Pasted image 20240223005649.png]]
<!--ID: 1708701022741-->
END

---
START
Basic
Packet’s load tolerance: Network latency vs. Troughput vs. Bandwidth
Back: 
## Keep up packets
- **latency**: measures data speed (how quickly does the water in the pipe reaches its destination)
- **throughput**: measures data transmitted and received during a specific time (the water running through the time)
- **bandwidth**: measures capacity (a bigger pipe would mean higher bandwidth)
Example: you can have a 100Gb/s NIC (bandwidth), but can transmit only at 40Gb/s (throughput) because of overheads
<!--ID: 1708701022743-->
END

---
START
Basic
Packet’s load tolerance: network model 
Back: 
|Level|OSI|TCP/IP|Examples|
|---|---|---|---|
|1|physical|same|ethernet|
|2|data link|same|ethernet|
|3|network|same|ip|
|4|transport|same|tcp/udp|
|5|session|-||
|6|presentation|-||
|7|application|same||
<!--ID: 1708701022744-->
END

---
START
Basic
Packet’s load tolerance: sockets
Back: 
Socket is a unix file with basic function that can send and receive “data”.

Characteristics:
- first in 1983
- level of abstraction very useful because nowadays are still used
- it is between **transport and application layer**
<!--ID: 1708701022746-->
END

---
START
Basic
Packet’s load tolerance: Transferring data between NIC and end-Host 
Back: 
- polling: works but waste of cpu (first controllers, then cpu does copy)
- DMA

DMA is a hardware block which without CPU assistance is capable of copying data, eg from peripheral to memory, memory to peripheral, memory to memory or peripheral to peripheral
<!--ID: 1708701022747-->
END

---
START
Basic
Packet’s load tolerance: Notify the end host about network packet reception
Back: 
Using interrupts. The interrupts are some "abruption" in the system caused by peripherals or devices.
<!--ID: 1708701022748-->
END

---
START
Basic
Packet’s load tolerance: livelock vs. deadlock
Back: 
- if CPU gets an interrupt and keeps to be interrupted, this leads to a **livelock**: a state where the system is perfectly able to work but it cannot do any work
- **deadlock**: process waits for some resource to do the work
<!--ID: 1708701022750-->
END

---
START
Basic
Packet’s load tolerance: whats the problem of interrupts "in general"? Describe some mitigations
Back: 
Interrupt would occur each 6ns.
It is not sustainable for the cpu to work in this way, so, some possible alternatives:
1. interrupt coalescing (mix): generate an interrupt every n packets
2. polling: disable interrupts all together, use CPU polling to check for new arrivals
3. hybrid: a mix of these two
	- interrupts -> polling -> interrupts
	- there is a threshold when the rate exceed then switch to polling, then to interrupts

> [!success] Advantages
> - lower cpu utilization
> - higher throughput

> [!error] Disadvantages
> - higher latency
<!--ID: 1708701022751-->
END

---
START
Basic
Packet’s load tolerance: How to build a packet with multiple protocols and headers
Back: 
scatter-gather DMA operations

Scatter-gather DMA (Direct Memory Access) is a technique used in computer systems to enhance the efficiency of data transfers between devices and memory without involving the CPU directly. Traditional DMA transfers involve moving contiguous blocks of data between a device and memory. However, in scatter-gather DMA, the data to be transferred is scattered in non-contiguous memory locations and then gathered at the destination.

Here's a brief explanation of the terms:

1. **Scatter:**
    
    - In the context of DMA, "scatter" refers to the process of spreading the source data across different non-contiguous memory locations.
    - This can be useful when the data to be transferred is not stored in a contiguous block in memory.
2. **Gather:**
    
    - "Gather" refers to the process of collecting the scattered data from its various non-contiguous locations and assembling it into a contiguous block at the destination.

The scatter-gather DMA capability is particularly beneficial in scenarios where data is fragmented or scattered across memory, and the transfer operation involves non-contiguous blocks. This approach can be more flexible and efficient compared to traditional DMA when dealing with tasks such as network packet processing, file I/O, or data streaming, where the data is not necessarily stored in a sequential manner in memory.

Operating systems and device drivers use scatter-gather DMA to specify a list of memory descriptors or pointers to non-contiguous memory regions. The DMA controller then uses this information to transfer data directly between the device and the scattered memory locations, reducing the involvement of the CPU and improving overall system performance.
<!--ID: 1708701022753-->
END

---
START
Basic
Packet’s load tolerance: NIC techniques to receive data efficiently, TSO, LRO/GRO
Back: 
NIC support for segmentation offload, TSO, LRO/GRO, and checksum generation + Jumbo Frames
### NIC Support for Segmentation, TSO, LRO/GRO:

**Segmentation Offload (TSO - TCP Segmentation Offload):** NICs (Network Interface Cards) that support TSO can offload the task of dividing large TCP packets into smaller ones to the hardware. This reduces the CPU overhead and improves overall network performance.

**Large Receive Offload (LRO) / Generic Receive Offload (GRO):** LRO and GRO are features that allow NICs to combine multiple smaller incoming packets into a larger one before passing them to the operating system. This helps in reducing CPU utilization and enhancing network efficiency by processing fewer, larger packets.

### NIC Support for Checksum Generation:

NICs can offload the task of calculating checksums for packets to improve performance. This involves the **calculation of checksums for data integrity** at the hardware level instead of relying on the CPU to perform these computations. This offloading helps in reducing the processing burden on the CPU, contributing to better overall system performance.

### Jumbo Frames

**Jumbo frames** refer to Ethernet frames that exceed the standard maximum frame size (usually 1500 bytes). NICs and network equipment that support jumbo frames allow for the transmission of larger packets, potentially improving network efficiency by reducing overhead associated with transmitting a larger number of smaller frames. However, support for jumbo frames must be consistent across the entire network infrastructure for it to be effective.
<!--ID: 1708701022754-->
END

---
START
Basic
NIC: What TCP Offloading is? What's the difference between stateless and stateful?
Back: 
TCP offload means that **TCP network packets are unpacked from the network card and assembled into larger segments**. This task is usually done by the CPU but can be done to a large extent on hardware with modern network set-ups.

Difference between stateless and stateful
1. **Stateless**
    - **Definition:** Stateless refers to a system or protocol that does not maintain any knowledge or memory of previous interactions. Each transaction is independent, and the system does not store information about the past state.
    - **Example:** The Internet Protocol (IP) is a stateless protocol. Each packet is treated in isolation, without any reference to previous packets.
2. **Stateful**    
    - **Definition:** Stateful refers to a system or protocol that maintains information about the state of previous interactions. The system retains memory of past events, allowing it to understand the context and relationship between different transactions.
    - **Example:** TCP (Transmission Control Protocol) is a stateful protocol. It maintains a connection state, keeping track of the sequence of data sent and received between two devices.
<!--ID: 1708701022755-->
END

---
START
Basic
NIC: what is Multicore Scalability? What's the history?
Back:

The ability of a computer system or software application to efficiently utilize and benefit from multiple processor cores within a multicore processor.

History:
- in the past **pre-2005**, CPU was faster than the network and doubled every month
- in the manycore era (2005 - 2015) -> jumbo frames, interrupts, offloading... **many core scalability efforts!**
- today: performance is delivered by specialization (GPU, TPUs...)
<!--ID: 1708701022757-->
END

---
START
Basic
Multicore: what the problems are with multicore approach?
Back:
- synchronization on common data 
	- coordination or control of the order and timing of execution of multiple threads or processes in a concurrent or parallel computing environment
	- with mutexes and locks you slow down everything
- cache pollution
	- multiple processor cores compete for access to shared cache resources. When multiple cores are accessing and modifying data that resides in shared caches, it can lead to cache pollution.
<!--ID: 1708701022758-->
END
---

START
Basic
Multicore: what does irqbalace Linux does?
Back:
1. Balance interrupt once or periodically (static vs dynamic)
2. Tell which interrupts should go to which CPU (affinity)
3. Tell which CPUs should not handle which interrupts (!affinity)
4. Which interrupts should not be balanced (manual pinning)
<!--ID: 1708701022759-->
END
---

START
Basic
What's the journey of a packet?
Back:
- the cpu0 usually takes charge of the most of interrupts
	- so cpu gets interrupted
- the outgoing NIC packets are in queue
	- when cpu cores try to analyze them, they break (mutex, semaphores....wadda wadda)
- solution? Multi-queue
	- policies
		- random
			- but it lacks cache and it is no connection based management, it means that if using two connections it is a mess
		- receive side scaling
			- packet belonging to the same connection must be processed on the same core
			- a tcp flow (connection) is identified by 4-tuple: src, dst, src_port, dst_port
			- **cache locality**
				- means that the data is available through cache
			- this is a **good solution**
		- RPS
		- RFS
		- XPS

- RSS: Receive Side Scaling - is hardware implemented and hashes some bytes of packets ("hash function over the network and/or transport layer headers-- for example, a 4-tuple hash over IP addresses and TCP ports of a packet"). Implementations are different, some may not filter most useful bytes or may be limited in other ways. This filtering and queue distribution is fast (only several additional cycles are needed in hw to classify packet), but not portable between some network cards or can't be used with tunneled packets or some rare protocols. And sometimes your hardware have no support of number of queues enough to get one queue per logical CPU core.

> RSS should be enabled when latency is a concern or whenever receive interrupt processing forms a bottleneck. Spreading load between CPUs decreases queue length.

- Receive Packet Steering (RPS) "is logically a software implementation of RSS. Being in software, it is necessarily called later in the datapath.". So, this is software alternative to hardware RSS (still parses some bytes to hash them into queue id), when you use hardware without RSS or want to classify based on more complex rule than hw can or have protocol which can't be parsed in HW RSS classifier. But with RPS more CPU resources are used and there is additional inter-CPU traffic.

> RPS has some advantages over RSS: 1) it can be used with any NIC, 2) software filters can easily be added to hash over new protocols, 3) it does not increase hardware device interrupt rate (although it does introduce inter-processor interrupts (IPIs)).

- RFS: Receive Flow Steering is like RSS (software mechanism with more CPU overhead), but it not just hashing into pseudo-random queue id, but takes "into account application locality." (so, packet processing will probably be faster due to good locality). Queues are tracked to be more local to the thread which will process received data, and packets are delivered to correct CPU core.

> The goal of RFS is to increase datacache hitrate by steering kernel processing of packets to the CPU where the application thread consuming the packet is running. RFS relies on the same RPS mechanisms to enqueue packets onto the backlog of another CPU and to wake up that CPU. ... In RFS, packets are not forwarded directly by the value of their hash, but the hash is used as index into a flow lookup table. This table maps flows to the CPUs where those flows are being processed.

- Accelerated RFS - RFS with hw support. (Check your network driver for `ndo_rx_flow_steer`) "Accelerated RFS is to RFS what RSS is to RPS: a hardware-accelerated load balancing mechanism that uses soft state to steer flows based on where the application thread consuming the packets of each flow is running.".

---

Similar method for packet transmitting (but packet is already generated and ready to be send, just select best queue to send it with - and to easier post-processing like freeing skb)

- XPS: Transmit Packet Steering: "a mapping from CPU to hardware queue(s) is recorded. 

> The goal of this mapping is usually to assign queues exclusively to a subset of CPUs, where the transmit completions for these queues are processed on a CPU within this set"
<!--ID: 1708701022761-->
END
---

START
Basic
NIC: What is RDMA? How it works? Advantages and disadvantages
Back:
RDMA stands for Remote Direct Memory Access. It is a networking technology that allows data to be transferred directly from the memory of one computer to the memory of another computer without involving the operating system of either computer. This can significantly reduce latency and CPU overhead, making it a valuable technology for high-performance computing and data center applications.

This is possible through the use of specialized network adapters and switches that support RDMA, as well as the use of protocols such as InfiniBand and RoCE (RDMA over Converged Ethernet). 

Advantages:
- speed: RDMA can provide very low latency and high throughput, making it suitable for applications that require fast data transfers.

Disadvantages:
- complexity: RDMA requires specialized hardware and software support, which can make it more complex to deploy and manage compared to traditional networking technologies.
- price: the cost of RDMA-capable hardware and infrastructure can be higher than standard networking equipment, which may be a barrier to adoption for some organizations.
<!--ID: 1708701022762-->
END
---

START
Basic
What is the idea of RDMA?
Back:
RDMA, or Remote Direct Memory Access, is a networking technology enabling direct data transfer between the memories of two computers without involving their operating systems. This minimizes latency and enhances overall network performance.
<!--ID: 1708701022763-->
END
---

START
Basic
Why does RDMA become possible and what kind of support does it expect from the hardware?

Back:
RDMA becomes feasible due to advancements in networking hardware supporting direct memory access. Hardware support includes features like RDMA-capable network adapters, offloading data transfer tasks from the CPU, reducing reliance on the operating system.
<!--ID: 1708701022765-->
END
---

START
Basic
What is userspace networking and kernel bypassing?

Back:
Userspace networking involves shifting network processing tasks from the operating system kernel to user space, bypassing the traditional kernel stack.

Idea: Let the process manage its networking resources

Kernel bypassing provides applications with more direct control over network resources, leading to reduced latency and improved performance in RDMA implementations.

Idea: Access hardware/NIC resources directly from the user-space
<!--ID: 1708701022766-->
END
---

START
Basic
Explain the relationship between socket programming and RDMA.

Back:
Socket programming is a higher-level networking paradigm involving communication between applications using sockets. 

It has its own programming API, abstractions, and protocols.

RDMA operates at a lower level, allowing direct memory access between systems.

RDMA is independent of the networking technology, and the programming interfaces give to the user (there is a pseudo-standard stack called Open-Fabric Alliance).

Examples of protocol that implements RDMA are InfiniBand and RoCE (RDMA over Converged Ethernet).
<!--ID: 1708701022767-->
END
---

START
Basic
What advantages does RDMA offer?

Back:
RDMA offers several advantages, including low latency, high bandwidth, and reduced CPU overhead. It enables faster data transfer by allowing direct memory access without involving the CPU for data copy operations. This makes RDMA particularly suitable for applications requiring high-performance and low-latency communication.
<!--ID: 1708701022769-->
END
---

START
Basic
What are the (potential) disadvantages of RDMA?

Back:
Potential disadvantages of RDMA include the complexity of implementation, requiring specialized hardware and software support. Not all applications may benefit equally, and compatibility issues, along with the need for RDMA-capable hardware, can be potential drawbacks.
<!--ID: 1708701022770-->
END
---

START
Basic
In what kind of setting should RDMA be used?

Back:
RDMA is well-suited for settings where low latency and high bandwidth are critical, such as in high-performance computing clusters, data centers, and applications where real-time communication is essential.

Ideal settings are where low-latency and high-throughput communication are crucial.

For examples HPC (High Performance Computing), Data Centers, Storage Systems, ML, Telecommunications..
.
<!--ID: 1708701022771-->
END
---

START
Basic
Provide a bit of historical context and explain where today's RDMA networks evolved from.

Back:
- **Direct Memory Access (DMA)**: DMA is a technique that allows peripherals to access the system's memory directly without involving the CPU. This concept has been in use since the early days of computing to enhance data transfer speeds between devices and memory. Early DMA implementations focused on improving I/O performance.

- **InfiniBand Emergence (late 1990s)**: InfiniBand, a high-speed interconnect standard, was introduced in the late 1990s to address the increasing demands of HPC environments. InfiniBand provided low-latency and high-bandwidth communication, making it suitable for clusters and supercomputers. While not initially RDMA-focused, InfiniBand laid the groundwork for RDMA-capable networks.

- **RDMA Consortium (2002)**: The RDMA Consortium was formed in 2002 with the goal of developing and promoting a standardized RDMA technology. Members included industry leaders such as Cisco, IBM, Microsoft, and Intel. This collaboration aimed to define and standardize RDMA specifications for broader industry adoption.

- **Emergence of RDMA Protocols**: As a result of the RDMA Consortium's efforts, various RDMA protocols, such as iWARP (Internet Wide Area RDMA Protocol) and RoCE (RDMA over Converged Ethernet), began to emerge. These protocols facilitated RDMA capabilities over standard Ethernet networks, making the technology more accessible and scalable.

- **Widespread Adoption (2000s-2010s)**: RDMA started gaining broader adoption in various fields, including HPC, data centers, storage, and networking. Its ability to provide low-latency, high-throughput communication became particularly valuable as data-intensive applications and distributed computing environments became more prevalent.

- **Incorporation into Industry Standards (2010s)**: RDMA technologies, especially RoCE, were incorporated into industry standards, making them more widely supported by network equipment vendors. This further facilitated the integration of RDMA capabilities into mainstream networking solutions.

- **Ongoing Developments (Present)**: RDMA continues to evolve with ongoing research and development efforts. Newer technologies and improvements in RDMA protocols aim to enhance performance, scalability, and compatibility with emerging applications in areas such as artificial intelligence, machine learning, and edge computing.
<!--ID: 1708701022772-->
END
---

START
Basic
Describe SmartNIC

Back:
The SmartNIC (Smart Network Interface Card) is a network interface card that offloads network processing tasks from the host CPU to the NIC itself. SmartNICs are designed to accelerate network performance, reduce CPU overhead, and provide additional functionality such as packet processing, security, and monitoring capabilities.

This is because the idle CPU is a waste of resources, so the SmartNIC is a way to offload the CPU from the network processing tasks.

The advantages are:
- lower latency
- lower cpu utilization
- higher throughput

<!--ID: 1708701022774-->
END
---

START
Basic
SmartNIC: on-path vs. off-path

Back:
on-path: the SmartNIC is in the path of the packet, so it can process the packet directly

off-path: the SmartNIC is not in the path of the packet, so it cannot process the packet directly
<!--ID: 1708701022775-->
END
---

START
Basic
Describe SmartNICs' use cases

Back:
There are four cases:
1. Shuffle Offloading
	- mapreduce: pick data and divide it in chunkies and shuffle them

2. Gradient Aggregation
   - every deep learning queue is aggregated and merged into another giant one

3. Key-Value Store
   - redis

4. Distributed File Systems Storage Policies
<!--ID: 1708701022776-->
END
---

START
Basic
Describe Shuffle Offloading highlighting pros and cons

Back:
First use-case

Shuffle Offloading: (mapreduce) 
- Shuffling is the process of data redistribution
  - To make sure each reducer obtains all values associated with the same key.

- It is needed for all of the operations which require grouping    
  - E.g., word count, compute avg. the score for each department
- Spark and Hadoop have different approaches implemented for handling the shuffles.
- problem: smartNIC have limited memory and it is not possible to store all the data
  - offload 1: partition merging -> merge the data from the same partition
  - offload 2: data rearrengement -> wordcount, and transmit the result to the reducer (the reducer will do the final merge)

PROS
- Nicely integrated with Spark
- They consider memory exhaustion of the NIC (not all the papers do it), and address with a simple yet effective solution (spilling)

CONS
- They don’t show what happens when implementing
merging/rearrangement on the host CPU on a dedicated core. They would waste one core, but what about the performance
<!--ID: 1708701022778-->
END

---

START
Basic
Describe Gradient Aggregation highlighting pros and cons

Back:
Second use-case

Gradient Aggregation:
- Gradient aggregation is a key operation in distributed machine learning, where the gradients computed by different workers are aggregated to update the model parameters.

- Parameter server: a distributed system that stores the model parameters and is responsible for aggregating the gradients.
- The parameter server is a bottleneck in distributed machine learning systems, as it needs to handle a large number of gradients and update the model parameters frequently.
  - so we perform an allreduce operation and decentralize the parameter server (every worker sends the gradients to the other workers and then they aggregate the gradients)

PROS:
- Exploit FPGA to do compression in-hardware
- Baseline at 100Gbps, FPGA-based one at 40Gbps, we can expect higher improvements

CONS:
- Small setup (only 6 nodes)
- They use CPUs rather than GPUs (GPUs more common in ML training)
<!--ID: 1708701022779-->
END

---

START

Basic
Describe Key-Value Store

Back:
Third use-case

Key-Value Store:
- Key-value stores are a way to store data in a simple and efficient manner, where each piece of data is associated with a unique key.
- Key-value stores are widely used in distributed systems, databases, and caching systems.
<!--ID: 1708701022780-->
END

---

START
Basic
Describe Storage Policies Offload highlighting pros and cons

Back:
Fourth use-case

Storage Policies Offload:
- Storage policies define the characteristics and behavior of data storage, such as Client request validation, replication and erasure coding.
  - **Client request validation**: a user can define a policy that specifies the conditions under which a client request is considered valid. For example, a policy might require that a client request be signed by a specific user or that it originate from a specific IP address.
  - **Replication**: a policy might specify that data must be replicated across multiple storage devices to ensure fault tolerance and data durability. For example, a policy might require that data be replicated across three different storage devices in the same data center.
  - **Erasure coding**: a policy might specify that data be encoded using erasure coding techniques to provide fault tolerance and data durability. For example, a policy might require that data be encoded using a Reed-Solomon erasure coding scheme with a specific number of parity blocks.

PROS:
- Timely problem, disks are getting faster, network might become the bottleneck
- For erasure-coding, comparison with the most up-to-date solution (TriEC) – (I did not show it in the slides, but generally an important point to check)
- Cycle-accurate simulations

CONS:
- Lack of test on real I/O traces. How large the writes/reads typically are?
<!--ID: 1708701022782-->
END

---

START
Basic
Can we have some processing units to avoid sending data back and forth between the NIC and the host?

Back:
We can have some processing units (general purpose cores, P4
pipelines, FPGA, other) on the NIC.
<!--ID: 1708701022783-->
END

---

START
Basic
What Data centers are?

Back:
Data centers are centralized locations where computing and networking equipment is concentrated for the purpose of collecting, storing, processing, and distributing large amounts of data.

They have racks, each rack has a switch, and each switch has a NIC.
<!--ID: 1708701022785-->
END

---

START
Basic
What is congestion control?

Back:
Congestion control is a set of mechanisms and techniques used to manage and prevent network congestion, ensuring that the network operates efficiently and effectively.

Example scenario:
- two senders want to send packets using one switch
- the switch will have lots of dropped packets
- therefore, while we use congestion control to adjust the sending rate accordingly to our bandwidth
- the sender or the switch needs to check what’s the latency
<!--ID: 1708701022786-->
END

---

START
Basic
What are the approches to detect congestion control?


When **switch** detects congestion, many approaches are available:
- **RED**: switch sets a threshold, then when a packet arrives and it is within the threshold, the switch randomly drops it
- **ECN**: what if we use RED notifying the sender? So here we don't randomly drop packages, rather than we mark them. When the receiver will get the marked packets, it will ask to slow down, preventing the congestion. The problem is that you are going to always reduce as long as you receive marked packages. IT'S SLOW! 
- **DCTCP**: DCTCP uses Explicit Congestion Notification (ECN) to detect congestion in the network. It responds to congestion by reducing the TCP window size more aggressively than traditional TCP, ensuring a more rapid response to network congestion. 
	- This works for TCP, but what about RDMA?
- **PFC**: PFC allows Ethernet switches to pause entire Ethernet flows when congestion is detected, preventing packet loss. This could leads to deadlock.
- **DCQCN**: QCN + DCTCP. DCQCN quantizes the congestion notification to allow finer control over the congestion response. It's especially useful in high-speed networks
- **HPCC**: Adjust flow rates per ACK

When a **sender** detects congestion, only two approaches are available:
- **Swift**: Swift uses a decentralized architecture where nodes collaborate to store and retrieve data, providing high availability and fault tolerance
- **RL-CC**: RL-CC employs reinforcement learning models to dynamically adjust network parameters based on real-time network conditions, maximizing throughput and minimizing latency.
	- Requires substantial training and tuning
<!--ID: 1708701022787-->
END

---

START
Basic
What is the difference between congestion control and load balancing?

Back:
- **Congestion control** is a set of mechanisms and techniques used to manage and prevent network congestion, ensuring that the network operates efficiently and effectively.
- **Load balancing** is the process of distributing network traffic across multiple network links or servers to optimize resource utilization, maximize throughput, minimize response time, and avoid overloading any single resource.
<!--ID: 1708701022788-->
END

---

START
Basic
What are the most used topology in data centers?

Back:
The most important ones are:
- **Fat-tree**: where the switches are organized in a tree-like structure, with multiple paths between any pair of servers. This topology provides high bandwidth and fault tolerance, making it suitable for large-scale data centers. Like a three but we have more links on the roots

- **Hamming-Mesh**: a mesh network with a torus topology, providing multiple paths between any pair of servers. This topology is known for its fault tolerance and scalability.

The others are:
- Ring/1D Torus
	- the usual ring
- Mesh
	- "maglia"
- Torus
	- mesh with edges
- Blocking fat trees
	- same as fat trees but while going from roots to leafs, we reduce bandwidth
- Dragonfly
	- fully connected groups of switches
	- groups are fully connected between them
- Dragonfly+
	- same as dragonfly, but switches are connected with a fat tree
- Jellyfish
	- Let’s drop any structure and use a random graph
- RDCNs
	- Reconfigurable Data Center Networks
<!--ID: 1708701022790-->
END

---

START
Basic
What are the three types of bandwidth?

Back:
- **alltoall**: each process or node communicates with every other process or node
- **allreduce**: combining values from different processes and distributing the result back to all processes. This is often used for tasks like summation or finding the maximum value across distributed data
- **bisection**: dividing a parallel system into two equal halves. It describe network performance.
<!--ID: 1708701022791-->
END

---

START
Basic
Kind of load balancers

Back:
Load balancing helps in improving network performance
- It can be congestion-oblivious or congestion-aware
- It can be done in different parts of the network (centralized, in-network, on host)

- centralized (Hedera, Planck, Fastpass)
- distributed
  - in-network
    - congestion oblivious (ECMP, PacketSpray)
    - congestion aware (CONGA, Hula)
  - host-based
    - congestion oblivious (Presto)
    - congestion aware (mTCP, FlowBender)
<!--ID: 1708701022792-->
END

---

START
Basic
ECMP vs. Random Packet Spraying

Back:

They are both congestion-oblivious load balancing techniques, but they have different approaches to distributing network traffic.

- **ECMP**: Equal-Cost Multi-Path (ECMP) is a routing technique that allows network traffic to be distributed across multiple paths of equal cost. This helps in load balancing and fault tolerance, as traffic can be rerouted in case of link failures. ECMP is commonly used in data center networks to distribute traffic across multiple paths, improving network performance and reliability.

- **Random Packet Spraying**: Random Packet Spraying is a congestion-oblivious load balancing technique that randomly distributes packets across multiple paths in a network. This approach aims to evenly distribute traffic without considering the congestion status of individual paths. While simple and easy to implement, random packet spraying may not be as effective as congestion-aware load balancing techniques in preventing network congestion and optimizing traffic distribution.
<!--ID: 1708701022794-->
END

---

START
Basic
What is the difference between congestion-oblivious and congestion-aware load balancing?

Back:
- **Congestion-oblivious load balancing** techniques distribute network traffic without considering the congestion status of individual paths. They are simple and easy to implement but may not be as effective as congestion-aware techniques in preventing network congestion and optimizing traffic distribution.

- **Congestion-aware load balancing** techniques take into account the congestion status of individual paths and adjust traffic distribution accordingly. These techniques aim to prevent network congestion and optimize traffic distribution based on real-time network conditions, improving overall network performance and reliability.
<!--ID: 1708701022795-->
END

---

START
Basic
What is the difference between centralized and distributed load balancing?

Back:
- **Centralized load balancing** involves a single entity making load balancing decisions for the entire network. This approach can provide a global view of network traffic and resources, allowing for more effective load balancing. However, it may introduce a single point of failure and scalability challenges.
- **Distributed load balancing** distributes load balancing decisions across multiple entities in the network. This approach can improve fault tolerance and scalability but may require more complex coordination and communication among distributed entities.
<!--ID: 1708701022796-->
END

---

START
Basic
What is the difference between in-network and host-based load balancing?

Back:
- **In-network load balancing** involves distributing network traffic within the network infrastructure itself, typically using switches, routers, or other network devices. This approach can improve network performance and scalability by distributing traffic closer to its destination. However, it may require specialized network hardware and protocols to implement effectively.
- **Host-based load balancing** involves distributing network traffic at the host level, typically using software-based load balancing mechanisms. This approach can provide more flexibility and control over traffic distribution but may introduce additional overhead on the host systems.
<!--ID: 1708701022798-->
END

---

START
Basic
CONGA vs. Flowlet - differences, ideas

Back:
- **CONGA**: CONGA (CONgestion-aware load balancinG Algorithm) is a congestion-aware load balancing technique that aims to optimize traffic distribution in data center networks. It uses a centralized controller to monitor network conditions and make load balancing decisions based on congestion status. CONGA aims to prevent network congestion and improve overall network performance by dynamically adjusting traffic distribution based on real-time network conditions.


- **Flowlet**: Flowlet is a load balancing technique that focuses on optimizing the distribution of network flows based on flow characteristics. It aims to reduce the impact of microbursts and improve overall network performance by grouping packets into flowlets and distributing them across multiple paths. Flowlet load balancing can help in reducing congestion and improving network efficiency by smoothing out traffic patterns and reducing the impact of bursty traffic.
  - it works by grouping packets into flowlets and distributing them across multiple paths
<!--ID: 1708701022799-->
END

---

START
Basic
What is the difference between Hedera and Planck?

Back:
- **Hedera**: Hedera is a centralized load balancing technique that uses a global view of network traffic and resources to make load balancing decisions. It aims to optimize traffic distribution and prevent network congestion by dynamically adjusting traffic paths based on real-time network conditions. Hedera uses a centralized controller to monitor network status and make load balancing decisions, providing a global view of network traffic and resources.

- **Planck**: Planck is a distributed load balancing technique that distributes load balancing decisions across multiple entities in the network. It aims to improve fault tolerance and scalability by distributing load balancing decisions across multiple entities, reducing the reliance on a single point of failure. Planck provides a more scalable and fault-tolerant load balancing approach compared to centralized techniques.
<!--ID: 1708701022800-->
END

---

START
Basic
What is FlowBender?

Back:
- FlowBender is a congestion-aware, host-based load balancing technique designed to optimize traffic distribution at the host level.
- It utilizes software-based load balancing mechanisms to dynamically distribute network traffic across multiple paths, enhancing network performance and reliability.
- The technique is geared towards preventing network congestion and optimizing traffic distribution by dynamically adjusting based on real-time network conditions.
- FlowBender works by implementing software-based load balancing mechanisms at the host level, ensuring a responsive approach to traffic distribution.
- This congestion-aware approach allows FlowBender to adapt in real-time, adjusting traffic distribution dynamically according to the current network conditions.
<!--ID: 1708701022802-->
END

---

START
Basic
GPUs vs. TPUs

Back:
- **GPUs**: GPUs (Graphics Processing Units) are specialized hardware designed to accelerate graphics rendering and processing. They are widely used in applications such as gaming, video editing, and scientific computing due to their parallel processing capabilities and high computational performance. In recent years, GPUs have also become popular for accelerating machine learning and deep learning workloads, providing significant performance improvements over traditional CPUs.
- **TPUs**: TPUs (Tensor Processing Units) are custom-designed hardware accelerators developed by Google specifically for machine learning and artificial intelligence workloads. TPUs are optimized for processing tensor operations, which are fundamental to many machine learning algorithms. They are designed to provide high computational performance and energy efficiency for training and inference tasks in machine learning applications.

A tensor is a multidimensional array, and tensor operations are fundamental to many machine learning algorithms, making TPUs well-suited for accelerating machine learning workloads.
<!--ID: 1708701022803-->
END

---

START
Basic
What is CUDA and how it works in a nutshell?

Back:
CUDA is a parallel computing platform and programming model developed by NVIDIA for general-purpose computing on GPUs. It allows software developers to harness the computational power of NVIDIA GPUs to accelerate a wide range of applications, from scientific simulations to deep learning.

In CUDA, the basic unit of execution is a thread, and threads are grouped into blocks. Blocks, in turn, can be organized into a grid. Each block of threads can execute independently, and the threads within a block can communicate and synchronize with each other through shared memory. Additionally, multiple blocks can execute in parallel, allowing for the efficient parallel processing of data.
<!--ID: 1708701022804-->
END

---

START
Basic
What are the main storage forms for big data?

Back:
- **Distributed File Systems**: Distributed file systems are designed to store and manage large volumes of data across multiple nodes in a distributed environment. Examples include Hadoop Distributed File System (HDFS) and Google File System (GFS).
- **NoSQL Databases**: NoSQL databases are designed to handle large volumes of unstructured or semi-structured data. They provide flexible data models and horizontal scalability, making them suitable for big data applications. Examples include Apache Cassandra, MongoDB, and Apache HBase.
- **NewSQL Databases**: NewSQL databases combine the scalability of NoSQL databases with the transactional capabilities of traditional SQL databases. They are designed to handle large-scale data processing and analytics while maintaining ACID (Atomicity, Consistency, Isolation, Durability) properties. Examples include Google Spanner and CockroachDB.
<!--ID: 1708701022805-->
END

---

START
Basic
Describe GFS Architecture

Back:

- Actors
    - **Master Server**: Manages metadata, keeps track of file locations, and handles namespace operations.
    - **Chunk Servers**: Store data in fixed-size chunks (64 MB by default) and manage the actual data storage.
    - **Clients**: Applications or users interacting with the file system.

- Communication
    - **Client-Chunk Server Communication**: Clients communicate directly with chunk servers to read or write data chunks.
    - **Client-Master Communication**: Clients communicate with the master to retrieve metadata, such as file locations and chunk information.
    - **Master-Chunk Server Communication**: Master communicates with chunk servers to manage chunk placement and handle failures.

- Data Flow
    - Data is divided into **fixed-size chunks** and **stored** across **multiple chunk servers** for reliability and parallel access.
    - **Each file is divided into chunks**, and each chunk is replicated across multiple chunk servers for fault tolerance.
    - **The master server keeps metadata**, including file and chunk locations, and manages the overall file system namespace.

- Consistency and Reliability
    - **GFS sacrifices strong consistency for availability and fault tolerance**.
    - Uses a simplified consistency model, allowing for eventual consistency.
    - Replicates data across multiple chunk servers to tolerate node failures.

- Fault Tolerance
    - GFS is designed to **handle server failures gracefully by replicating data across multiple chunk servers**.
    - The master server monitors chunk servers and redistributes data in case of failures.
    - Chunk servers periodically send heartbeats to the master to signal their availability.

- Scalability
    - GFS is **designed for scalability**, allowing it to handle large-scale distributed storage needs.
    - The architecture supports the addition of more chunk servers to accommodate growing data volumes.
<!--ID: 1708701022807-->
END

---

START
Basic
Describe HDFS Architecture

Back:
Hadoop is an open-source framework for distributed storage and processing of large datasets. Hadoop Distributed File System (HDFS) is the primary storage system used by Hadoop.

It is an open source clone of GFS, and it is designed to store and manage large volumes of data across multiple nodes in a distributed environment.

Erasure coding is a method of data protection in which data is broken into fragments, expanded and encoded with redundant data pieces and stored across a set of different locations or storage media.

In the case of HDFS, we use Reed-Solomon code: data is divided into k chunks and stored together with m parity chunk. This allows for the recovery of the original data even if some chunks are lost
<!--ID: 1708701022808-->
END

---

START
Basic
What does ACID means?

Back:
ACID stands for Atomicity, Consistency, Isolation, and Durability. It is a set of properties that guarantee the reliability of database transactions.

- **Atomicity**: Ensures that all operations within a transaction are completed successfully or none of them are. If any part of the transaction fails, the entire transaction is rolled back, leaving the database in its original state.

- **Consistency**: Ensures that the database remains in a consistent state before and after the transaction. All constraints, rules, and relationships are maintained, and the database is not left in an inconsistent state.

- **Isolation**: Ensures that the execution of multiple transactions concurrently does not interfere with each other. Each transaction is isolated from others, and the results of concurrent transactions are consistent with the results of running them sequentially.

- **Durability**: Ensures that once a transaction is committed, its changes are permanent and cannot be lost, even in the event of a system failure. The changes are stored in non-volatile memory and are recoverable.
<!--ID: 1708701022809-->
END


---

START
Basic
Does newsql databases support ACID properties?

Back:
Yes, NewSQL databases are designed to support ACID (Atomicity, Consistency, Isolation, Durability) properties, providing the transactional capabilities of traditional SQL databases while offering horizontal scalability and distributed processing.

Examples: Google Spanner and CockroachDB
<!--ID: 1708701022811-->
END

---

START
Basic
What is noSQL?

Back:
NoSQL (Not Only SQL) is a term used to describe a wide range of database technologies that are designed to handle large volumes of unstructured or semi-structured data.

They enbrace the BASE characteristics (Basically Available, Soft state, Eventual consistency)

- **Basically Available**: The system is always available, even in the presence of network partitions or failures. It sacrifices strong consistency for availability.
- **Soft state**: The state of the system may change over time, even without input. This allows for eventual consistency and flexibility in data storage.
- **Eventual Consistency**: The system will eventually become consistent, even if updates are made to different parts of the system. It does not guarantee immediate consistency but ensures that the system will converge to a consistent state over time.
<!--ID: 1708701022812-->
END

---

START
Basic
Pros and Cons of NoSQL

Back:
- **NoSQL**
- Pros
  - Easy to scale-out
  - Higher performance than SQL data stores for large data
  - Most solutions are either open- source or cheaper than industrial SQL data stores
  - Supports complex data and objects
- Cons
  - No ACID guarantees, less suitable for transactions
  - Lack of standardization (each store has its own querying language)
  - Limited supports for aggregation operations (e.g., sum, average, etc…)
  - No well defined approach for DB design (no common data/storage model), might lead to lock-in
<!--ID: 1708701022813-->
END

---

START
Basic
MapReduce

Back:
MapReduce is a programming model and processing framework for distributed computing on large datasets. It is designed to process and analyze large volumes of data in parallel across a distributed cluster of nodes.

MapReduce: PROs and CONs
- PROs
  - Problems that require many sequential data access (from disk)
  - Large batch jobs (i.e., not interactive nor real time)

- CONs
  - Problems that require random access to data
  - Working with graphs
  - Interdependent data
<!--ID: 1708701022815-->
END

---

START
Basic
What is Spark?

Back:
Spark is a general-purpose distributed data processing engine
which overcomes many of the Hadoop's limitations

- Spark provides a rich ecosystem of services to work on (big)
data through APIs accessible via multiple programming
languages
- Lazy execution avoids frequent and costly disk operations
  - lazy execution means that the operations are not executed until the data is actually needed
- Spark's **DataFrame** as the main abstraction for playing with
data
	- DataFrame is a distributed collection of data organized into named columns
<!--ID: 1708701022816-->
END

---

START
Basic
Narrow vs. Wide transformations

Back:
- **Narrow transformations**: Narrow transformations are those where each input partition contributes to at most one output partition. They can be executed in parallel without shuffling data across the network. Examples include map, filter, and union operations.

- **Wide transformations**: Wide transformations are those where each input partition can contribute to multiple output partitions. They require shuffling data across the network and can be more resource-intensive. Examples include groupByKey, reduceByKey, and join operations.
<!--ID: 1708701022817-->
END

---

START
Basic
What is the difference between RDD and DataFrame?

Back:
- RDD means Resilient Distributed Dataset, and it is the fundamental data structure of Spark. It is an immutable distributed collection of objects. Each dataset in RDD is divided into logical partitions, which may be computed on different nodes of the cluster.

- DataFrame is a distributed collection of data organized into named columns. It is conceptually equivalent to a table in a relational database or a data frame in R/Python, but with richer optimizations under the hood. DataFrames can be constructed from a wide array of sources such as structured data files, tables in Hive, external databases, or existing RDDs.

Both Hadoop and Spark can use RDD-like structures for distributed data processing, but Spark has expanded its capabilities with higher-level abstractions like DataFrames, providing a more SQL-like interface for data manipulation and optimization opportunities through Spark's Catalyst optimizer.
<!--ID: 1708701022819-->
END

---

START
Basic
What is the difference between Hadoop and Spark?

Back:
| Feature           | Hadoop                                                | Spark                                                 |
|-------------------|-------------------------------------------------------|-------------------------------------------------------|
| **Overview**      | Apache Hadoop is for distributed storage and processing of large datasets. | Apache Spark is a fast, general-purpose cluster-computing system for real-time data processing and iterative algorithms. |
| **Processing Model** | Primarily MapReduce programming model.              | DAG processing engine allowing in-memory processing, supporting batch and real-time processing. |
| **Storage**       | Relies on HDFS for distributed storage, breaking data into smaller blocks across nodes. | Introduces RDDs for distributed storage, promoting in-memory computation. |
| **Fault Tolerance** | Achieves fault tolerance through data replication in HDFS. | Implements fault tolerance through lineage information, enabling recovery by recomputing lost data from the original source. |
<!--ID: 1708701022820-->
END

# Big Data Computing - Flashcards 2 (Tolomei)
START
Basic
Vertical vs. Horizontal Scale

Back:
- **Vertical**: very large number of input data points
- **Horizontal**: very large representation of input data points

Example:
- Vertical: find 42 in a list of 1 billion numbers
- Horizontal: find a doge in a list of images
<!--ID: 1708789812484-->
END

---

START
Basic
Whar does similarity means? What are the types of similarity?

Back:
Similarity is a measure of how alike two data objects are.

There is no single definition of similarity that is suitable for all data types and applications. The choice of similarity measure depends on the nature of the data and the specific problem being addressed.

Types of similarity:
- **Cosine Similarity**: Measures the cosine of the angle between two vectors, providing a measure of similarity between two non-zero vectors.
- **Euclidean Distance**: Measures the straight-line distance between two points in a multi-dimensional space, providing a measure of similarity based on spatial proximity.
- **Jaccard Similarity**: Measures the similarity between two sets by comparing the intersection and union of the sets, providing a measure of similarity based on shared elements.
<!--ID: 1708789812486-->
END

---

START
Basic
What is an Euclidean Norm (L2 norm)?

Back:
The Euclidean norm, also known as the L2 norm, is a measure of the magnitude of a vector in a multi-dimensional space. It is calculated as the square root of the sum of the squares of the vector's components.

The formula is:
$$ ||x|| = sqrt((x_1)^2 + (x_2)^2 + ... + (x_n)^2) = sqrt(x \cdot x) $$

Where x is a vector with n components.

We use this norm to calculate the distance between two points in a multi-dimensional space.
<!--ID: 1708789812488-->
END

---

START
Basic
What is the Cosine Similarity?

Back:
A measure of similarity between two non-zero vectors of an inner product space that measures the cosine of the angle between them.

It ranges from -1 to 1, where -1 indicates exactly opposite, 1 indicates exactly the same, and 0 indicates orthogonality.

It captures the **orientation** of the vectors, not the magnitude.

The formula is:
$$ cos(\theta) = \frac{A \cdot B}{||A|| \cdot ||B||} $$

Where A and B are two vectors.
<!--ID: 1708789812489-->
END

---

START
Basic
What is the Jaccard Index (Coefficient)?

Back:
The Jaccard index, also known as the Jaccard similarity coefficient, is a measure of similarity between two sample sets. It is defined as the size of the intersection of the sets divided by the size of the union of the sets.

The formula is:
$$ J(A, B) = \frac{|A \cap B|}{|A \cup B|} = \frac{|A \cap B|}{|A| + |B| - |A \cap B|} $$

Where A and B are two sets.

It is used to compare the similarity and diversity of sample sets, particularly in the context of data analysis and data mining.
<!--ID: 1708789812491-->
END

---

START
Basic
What is clustering?

Back:
Clustering is the process of grouping a set of data points into subsets, or clusters, based on the similarity between the data points within each cluster.

It is a **fundamental technique in unsupervised learning** and is used to identify patterns and structures in data.

Clustering algorithms aim to partition data points into clusters such that points within the same cluster are more similar to each other than to those in other clusters.
(high-intra-cluster similarity)
<!--ID: 1708789812493-->
END

---

START
Basic
What are the issues of clustering?

Back:
- **object representation**: data points may be in a very high-dimensional space
- **distance measure**: the choice of the distance measure is crucial (e.g., Euclidean distance, cosine similarity, etc.)
- **number of clusters**: how many clusters should we have?

Example: in **text document clustering**, how we can group documents that have the same topic? The key issues are two: how to represent the documents and how to measure the similarity between them.

In this specific example, we could have different representations of words (a set of words, a bag of words, a bag of N-Grams...)
  
<!--ID: 1708789812494-->
END

---

START
Basic
What is the difference among a set of words, a bag of words and a bag of n-grams? How to calculate them? How they works?

Back:
- **Set of words**: a set of words is a collection of unique words in a document. It does not consider the frequency of words, only their presence or absence. We keep track of the words that are present in the document and its multiplicity, by using a dictionary. **We use Jaccard similarity to compare two sets of words.**
- **Bag of words**: a bag of words is a collection of words in a document, along with their frequency of occurrence. It is calculated by counting the frequency of each word in the document. It has vocabulary and a weighting scheme. It then counts the frequency of each word in the document, and put them in a vector. This approach has two main limitations: it has high dimensionality and it does not consider the order of the words. We use euclidean distance to compare two bags of words.
- **Bag of N-Grams**: a bag of N-Grams is a collection of sequences of N words in a document. It is calculated by counting the frequency of each sequence of N words in the document. It is a generalization of the bag of words, and it is used to capture the local context of words in a document. For example, if N=2, we have bigrams, if N=3, we have trigrams, and so on. The idea is to take two or more words and put them in a vector. We use cosine similarity to compare two bags of N-Grams.
<!--ID: 1708789812496-->
END 

---

START
Basic
What is the curse of dimensionality?

Back:
The curse of dimensionality refers to the phenomenon where the feature space becomes increasingly sparse as the dimensionality of the data increases.

Examples:
- **Distance-based algorithms**: as the number of dimensions increases, the distance between points becomes less meaningful, and the notion of proximity becomes less reliable.
- **Data sparsity**: as the number of dimensions increases, the amount of data required to fill the space grows exponentially, making it difficult to obtain representative samples.
<!--ID: 1708789812498-->
END

---

START
Basic
What is the manifold hypothesis?

Back:
The manifold hypothesis suggests that high-dimensional data often lies on a lower-dimensional manifold embedded within the high-dimensional space.

Basically we are doing a so-called **reduction of dimensionality**

We can reduce the dimensionality of the data by projecting it onto the lower-dimensional manifold, preserving the essential structure and relationships within the data.

Example:
- **Handwritten digits**: the data points representing handwritten digits in a high-dimensional space (e.g., pixel values) may lie on a lower-dimensional manifold corresponding to the variations in writing style and digit shape.
This is achieved by using techniques like PCA, t-SNE, and UMAP.
<!--ID: 1708789812499-->
END

---

START
Basic
Taxonomy of clustering algorithms (General Overview)

Back:
Clustering algorithms can be broadly categorized into the following types based on their underlying principles and approaches:
- **Partitioning Algorithms**: These algorithms partition the data into a predefined number of clusters. Examples include K-means, K-medoids, and CLARA.
- **Hierarchical Algorithms**: These algorithms create a tree of clusters, where each node represents a cluster and the parent-child relationships represent the inclusion of clusters.
- **Density-Based Algorithms**: These algorithms identify clusters as dense regions of data points separated by low-density regions. Examples include DBSCAN and OPTICS.
- **Grid-Based Algorithms**: These algorithms partition the data space into a finite number of cells to form a grid structure, and then group the cells to form clusters. Examples include STING and CLIQUE.
- **Model-Based Algorithms**: These algorithms assume that the data is generated by a mixture of underlying probability distributions and use statistical models to identify clusters. Examples include Gaussian Mixture Models and Hidden Markov Models.
<!--ID: 1708789812501-->
END

---

START
Basic
Tell me more about partitioning

Back:
The general idea of partitioning is to divide the data into a predefined number of clusters, where each data point belongs to exactly one cluster.

It is NP-hard to find the optimal partitioning, because we have to try all the possible combinations of clusters, and this is not feasible for large datasets as the number of possible combinations grows exponentially with the number of data points.

Therefore we use heuristics to find a good partitioning, and the most famous algorithms are K-means, K-medoids, and K-Means++.
<!--ID: 1708789812502-->
END

---

START
Basic
What is LLoyd's algorithm?

Back:
Lloyd's algorithm is the most famous algorithm for K-means clustering. It is an iterative algorithm that partitions a dataset into K clusters by minimizing the sum of squared distances between data points and their respective cluster centroids.

A centroid is the mean of the data points in a cluster, and the algorithm iteratively updates the centroids and reassigns data points to the nearest centroid until convergence.

It is divided into two steps:
- **Assignment step**: each data point is assigned to the nearest centroid.
- **Update step**: the centroids are updated to the mean of the data points assigned to each cluster.

LLoyd algorithm, is good because it approximate the solution.
<!--ID: 1708789812504-->
END

---

START
Basic
What is the K-means algorithm?

Back:
K-means is a popular partitioning algorithm used for clustering data into K clusters. It is based on the principle of minimizing the sum of squared distances between data points and their respective cluster centroids.

The basic idea is constructing K clusters so that the total intra-cluster variation (or total within-cluster sum of square) is minimized (SSD).

The LLoyd's algorithm is the most famous algorithm for K-means clustering.
It is an iterative algorithm that partitions a dataset into K clusters by minimizing the sum of squared distances between data points and their respective cluster centroids.

A centroid is the mean of the data points in a cluster, and the algorithm iteratively updates the centroids and reassigns data points to the nearest centroid until convergence.

The algorithm for solving k-means works as follows:
1. Initialize K centroids randomly.
2. Assign each data point to the closest centroid.
3. Update the centroids to the mean of the data points assigned to each cluster.
4. Repeat steps 2 and 3 until convergence (stopping criterion is met, e.g. centroids do not change significantly between iterations).
5. The algorithm converges when the centroids do not change significantly between iterations.
6. The final clusters are formed based on the converged centroids.
7. The algorithm is sensitive to the initial choice of centroids, and different initializations can lead to different results.

The LLoyd's algorithm takes O(R * K * N * d) time, where R is the number of iterations, K is the number of clusters, N is the number of data points, and d is the dimensionality of the data.
<!--ID: 1708789812505-->
END

---

START
Basic
Seed's selection in K-means

Back:
Since we randomly initialize the centroids, the final clusters can be different based on the initial choice of centroids.

For this reason, we execute the algorithm multiple times with different initializations and select the best result based on a predefined criterion (e.g., the lowest sum of squared distances).

As an alternative, we can use the K-means++ algorithm, which is a method for choosing the initial values (or "seeds") for the K-means clustering algorithm.
<!--ID: 1708789812507-->
END

---

START
Basic
What is the K-means++ algorithm?

Back:
K-means++ is a method for choosing the initial values (or "seeds") for the K-means clustering algorithm.

The key idea is to select the i-th centroid as the farthest data point to any other already selected centroid.

The algorithm works as follows:
1. Choose the first centroid randomly from the data points.
2. For each data point, calculate the distance to the nearest centroid already chosen.
3. Select the next centroid from the data points with probability proportional to the square of the distance to the nearest centroid already chosen.
4. Repeat steps 2 and 3 until K centroids are chosen, then run the K-means algorithm with these initial centroids.

Clusters obtained using K-means++ are O(log k) WORSE than the optimal solution.
<!--ID: 1708789812508-->
END

---

START
Basic
What is the K-medoids algorithm?  

Back:
K-medoids is a partitioning algorithm similar to K-means, but it uses medoids instead of centroids.

A medoid is the closest object to any other point in the cluster.

It is computationally more expensive than K-means, but it is more robust to noise and outliers.

---

START
Basic
Measures of cluster quality

Back:
There are several measures of cluster quality that can be used to evaluate the performance of clustering algorithms and the quality of the resulting clusters.

Some common measures include:
- **Internal Evalution**: clustering is evaluated based on the data alone, without reference to external information.
  - **Silhouette Score**: measures how similar an object is to its own cluster compared to other clusters.
  - **Davies-Bouldin Index**: measures the average similarity between each cluster and its most similar cluster.
  - **Dunn Index**: measures the compactness and separation of clusters.
- **External Evaluation**: clustering is evaluated based on data that was not used to create the clusters, yet pre-classified. It usually requires human intervention to label the data.
  - **Rand Index**: measures the similarity between two data clusterings. It considers all pairs of objects and counts the number of pairs that are either in the same cluster or in different clusters in both the predicted and true clusterings. (Confusion matrix)
<!--ID: 1708789812510-->
END

---

START
Basic
What is the difference between precision, recall, f-measure?

Back:
- **Precision**: measures the proportion of true positive predictions among all positive predictions. It is calculated as the number of true positive predictions divided by the sum of true positive and false positive predictions.
- **Recall**: measures the proportion of true positive predictions among all actual positive instances. It is calculated as the number of true positive predictions divided by the sum of true positive and false negative predictions.
- **F-measure**: is the harmonic mean of precision and recall, providing a single score that balances both measures. It is calculated as 2 * (precision * recall) / (precision + recall). A higher F-measure indicates a better balance between precision and recall.

All of these measures are used to evaluate the performance of classification algorithms and the quality of the resulting predictions, more specifically:
- **Precision**: measures the ability of the classifier to avoid false positives.
- **Recall**: measures the ability of the classifier to identify all positive instances.
- **F-measure**: provides a single score that balances precision and recall, providing a more comprehensive evaluation of the classifier's performance.
<!--ID: 1708789812511-->
END

---

START
Basic
What is PCA?

Back:
PCA stands for Principal Component Analysis, and it is a dimensionality reduction technique used to reduce the number of dimensions in a dataset while preserving the essential structure and relationships within the data.

PCA defines a set of principal components as follow:
- The first principal component is the direction in which the data varies the most.
- The second principal component is the direction in which the data varies the second most, and it is orthogonal to the first principal component.
- And so on...  

We look for the greatest variance in the data, because we want to minimize the chance that two points that are far in the original space are close in the new space.

About the covariance, we want to maximize the variance of the data projected onto the new space, therefore we use the covariance matrix.

We do that by using eigenvalues and eigenvectors.
<!--ID: 1708789812513-->
END

---

START
Basic
Practical issues of PCA

Back:
- Covariance and variance are sensitive to the scale of the data, so it is important to standardize the data before applying PCA.
- If one dimension takes on extremely large values, it will dominate the variance and the other dimensions will be ignored.

---

START
Basic
Reccomender Systems

Back:
We need recommender systems to help users find items that they might like, based on their past preferences and behavior.

Formally a recommender system is:
- set of users U
- set of items I
- user-item utility function, r: U x I -> R 
- set of ratings R totally ordered
- discrete ratings: 1, 2, 3, 4, 5
- continuous ratings: [0, 1]
<!--ID: 1708789812514-->
END

---

START
Basic
What are the three key problems in recommender systems?

Back:
1. **Data collection**: collecting and storing user-item interactions and ratings.
2. **Rating prediction**: predicting the ratings that users would give to items they have not yet interacted with.
3. **Recommendation Evaluation**: evaluating the quality of the recommendations made by the system.

For the first, we can gather information from explicit feedback (e.g., ratings, reviews) and implicit feedback (e.g., clicks, purchases, browsing history).

For the second, we can use collaborative filtering, content-based filtering, and hybrid methods, because we need to manage cold start problems, sparsity, and scalability.

For the third, we can use metrics like RMSE, mean average precision, and recall, serendipity and personalization.
<!--ID: 1708789812516-->
END

---

START
Describe the three main types of recommender systems

Back:
1. **Collaborative Filtering**: Recommends items to users based on the preferences of other users. It can be user-based or item-based.
2. **Content-Based Filtering**: Recommends items to users based on the characteristics of the items and the user's preferences. It uses item features to recommend items similar to those the user has liked in the past. They can be neighborhood-based or model-based or hybrid.
3. **Hybrid Methods**: Combine collaborative filtering and content-based filtering to provide more accurate and diverse recommendations. They can be weighted, mixed, or feature combination.

END

---

START
Basic
How content-based filtering works?

Back:
Core concept: Item/User profiles

Steps:
1. **Item profile creation**: Extract features from items (e.g., keywords, genres, actors for movies) and create a profile for each item.
2. **User profile creation**: Extract preferences from user interactions with items and create a profile for each user.
3. Match user and item profiles: Calculate the similarity between user and item profiles to recommend items to users.
<!--ID: 1708789812517-->
END

---

START
Basic
Do an example of content-based filtering

Back:
Example: items are movies, and movie profile is the list of actors.

Suppose user u has watched 5 movies, each movie represented by 2 actors.

User profile is the mean of item profiles
- 2 movies with actor 1 (1+1)/5
- 3 movies with actor 2 (1+1+1)/5
- then the user have 0.4 actor1 and 0.6 actor2
<!--ID: 1708789812519-->
END

---

START
Basic
Pros and cons of content-based filtering

Back:
PROs
- No need for data on other users: only the user and the items rated by her/him are needed
- No item cold start problem: when the item is new or unpopular (i.e., no one has rated yet) it can still be recommended to users with highest profile similarity
- Explainable recommendations using content features that caused an item to be recommended

CONs
- Finding the appropriate item features is hard
- Overspecialization: never recommends items outside user's profile
- Unable to exploit quality judgments of other users
- Cold start problem for new users: If the user hasn't rated any items, then there's no user profile
- May need to create average profiles and gradually improve them overtime
<!--ID: 1708789812521-->
END

---

START
Basic
Describe collaborative filtering

Back:
Recommend items to users based on the preferences of other users. It can be user-based or item-based.

The three approaches are **neighborhood-based**, **model-based**, and **hybrid**.

In the **neighborhood-based approach**, we use the similarity between users or items to make recommendations. How we can do that? By knowing what users have rated, we can predict what they would rate.

Drawbacks: sparsity (systems performed poorly when the number of items was large), efficiency (the number of computations grows with the number of users and items), and aging (user profiles change over time and the system needs to be updated).
<!--ID: 1708789812522-->
END

---

START
Basic
What is the difference between user-based and item-based collaborative filtering?

Back:
- **User-based**: Recommends items to a user based on the preferences of other users who are similar to that user. It uses the similarity between users to make recommendations.
- **Item-based**: Recommends items to a user based on the preferences of that user for similar items. It uses the similarity between items to make recommendations.

Example: in a movie recommendation system, user-based collaborative filtering would recommend movies to a user based on the preferences of other users who have similar tastes, while item-based collaborative filtering would recommend movies to a user based on the preferences of that user for similar movies.
<!--ID: 1708789812524-->
END

---

START
Basic
What model-based collaborative filtering is?

Back:
Tries to predict ratings by representing both items and users with a number of hidden factors inferred from observed ratings.

They are hidden: latent!

Learning algorithms are used to find the best values for these factors such that they can predict the ratings for items that users have not yet rated.

Two main optimization algorithms are used: **Alternating Least Squares (ALS)** and **Stochastic Gradient Descent (SGD)**.
<!--ID: 1708789812526-->
END

---

START
Basic
SGD vs. ALS

Back:
- **SGD**: Stochastic Gradient Descent is an iterative optimization algorithm used to minimize an objective function. It updates the model parameters by moving in the direction of the steepest descent of the objective function.
- **ALS**: Alternating Least Squares is an optimization algorithm used to solve matrix factorization problems. It alternates between updating the user factors and the item factors, minimizing the squared error between the observed ratings and the predicted ratings. It is commonly used in collaborative filtering and recommendation systems.

Steps for ALS are:
1. Initialize user factors randomly
2. Fix item factors and update user factors
3. Fix user factors and update item factors
4. Repeat steps 2 and 3 until convergence

We prefer ALS becuase it is parallelizable and because of implicit data: the training data is dense and looping over all the data is not feasible.

We need to considera biases too, because the ratings are not only influenced by the user and the item, but also by the context in which the rating was given. (e.g., the time of the day, the device used, etc.)
<!--ID: 1708789812527-->
END

---

START
Basic
What are the problems of collaborative filtering?

Back:
- **Cold Start**: New users and items have no or very few ratings, making it difficult to make accurate recommendations.
- **Scalability**: The number of users and items can be very large, making it computationally expensive to calculate similarities and make recommendations.
- **Sparsity**: The number of items is much larger than the number of ratings, leading to sparse user-item matrices.
<!--ID: 1708789812529-->
END

---

START
 Basic
What is the hybrid approach in recommender systems?

Back:
Hybrid methods combine collaborative filtering and content-based filtering to provide more accurate and diverse recommendations.

Netflix uses this.
<!--ID: 1708789812530-->
END
