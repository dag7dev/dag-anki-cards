---
date_created: 2024-01-22
date_modified: 2024-01-26
---
TARGET DECK: Distributed Systems
START
Basic
Describe CAP Theorem.
What is CAP Thorem? Give some examples.
Describe it, describe real systems that implement this theorem
Back: 
CAP in CAP Theorem stands for:
- **Consistency**: all clients see the same data at the same time, no matter which node they connect to. For this to happen, whenever data is written to one node, it must be instantly forwarded or replicated to all the other nodes in the system before the write is deemed ‘successful.’

- **Availability**: every request will eventually receive a response

- **Partition Tolerance**: the system must continue to work in case of any failure

At time t-1, the latest write for X is 0.
At time t, A and B cannot communicate with each other anymore.
At time t+1, A receives a write(x, 1)
At time t+2, B receives a read(x)
If B replies with 0, Consistency is lost.
If B replies with an error, Availability is lost.
B cannot reply with 1 because A and B cannot communicate, so it cannot be aware of the latest write.

Examples:
- Banking Systems (CA)
- Stock Exchange (CP)
- Social media (AP)
- Akamai (AP)
- Streaming (AP)

Availability is usually the most important feature for a distributed system.

- Paxos are AP but not C, because they allow different decisions on different sides of the partition.
Tags: cap

END

---

START
Basic
Dai un'implementazione dell'algoritmo di Ben-Or infinita
Back: 
Ben-Or termina sempre: live but not safe!
Da un punto di vista di FLP è asincrono e consenso è impossibile.
È un esempio di come risolvere il problema del consenso in un sistema asincrono.
La probabilità che l'agoritmo sia infinito è infinitesimale.
Infinito significa che nessuno riesce a vedere la maggioranza su un valore, soprattutto se esistono faults.
Tags: benor

END

---

START
Basic
Describe Ben-Or algorithm. Why is it used? Complexity? How many crash failure does it allow?
Back: 
Ben-Or is a decentralized consensus algorithm, which it is not a leader-based algorithm.

In the absence of a leader for tie-breaking, Ben-Or solves only binary input consensus, rather than arbitrary input value consensus. Even then, it employs randomization for achieving progress.

**The rounds are common to all nodes**, and they are traversed in a lock-step fashion by **N-F** nodes in an asynchronous manner, where N is the total number of nodes, and F is the number of faulty nodes. 

So it allows **N-F** crash failures.

Each round has two phases.
1. In the first phase, **each node tries to identify a value supported by a majority in order to propose that for the second phase.**

2. In the second phase, the decision/ratification phase, **a node finalizes its decision if it finds the same value proposed by at least F+1 nodes.**

Upon failure to get a decision in the current round, Ben-Or makes some nodes to change their votes before the next round. 

This helps tilt the system toward a decision, so that it converges to a consensus value in one of the upcoming rounds.  

The complexity of this algorithm is **O(log n)** (say "A Performance Comparison of Algorithms for Byzantine Agreement in Distributed Systems" in case the prof says something).
Tags: benor

END

---

START
Basic
Describe FLP Theorem. Describe FLP components.
Back: 
FLP: Fisher-Lynch-Patrol theorem.

**It is impossible in an ASYNCHRONOUS system to achieve consensus.**

It has three properties which are:
- **Termination** AKA **Liveness**: nodes eventually decide  
- **Agreement** AKA **Safety**: all nodes should decide on the same value
- **Fault Tolerance**: the protocol must be effective in case of node failures

The FLP states that we cannot have all these three conditions in an asynchronous system.

It also states that any consensus protocol in an async system can only have either termination or agreement.
Tags: flp

END

---

START
Basic
Describe how Tor and the Dark Web work
Back: 
When you use Tor:  
- Your connection is encrypted and routed through a series of volunteer-operated servers called nodes: the user contacts a "trusted" node to know the relays of the network and composes a path composed by at least 3 nodes (the first node is called **guard** and it's the only node which knows the sender)  
- Each node in the Tor network only knows the **IP address of the previous and next nodes** in the chain, enhancing user privacy.  
- The final node (**exit node**) connects to the destination server on your behalf, maintaining your anonymity.  
The handshake protocol works using Authenticated Diffie-Hellman, using the public key of the node we’re trying to connect to, also preventing Man-In-The-Middle (MITM) attacks. The key can be provided by trusted directory servers, or in the case of hidden services, it is actually encoded in the domain name itself (.onion v3).
Tags: tor

END

---

START
Basic
Describe why network performance (bandwidth and latency) is reduced when you use Tor

Back: 
1. **Limited Bandwidth of Volunteer Nodes**: Tor relies on volunteers to operate nodes, and these nodes typically have limited bandwidth compared to commercial internet service providers. As a result, the overall bandwidth available for Tor users is constrained by the capacity of the slowest relay in the circuit.
  
2. **Encryption and Decryption Overhead**: The multiple layers of encryption and decryption that occur as data passes through each relay in the Tor network can introduce additional processing overhead. This cryptographic processing contributes to latency, as each relay needs to perform these operations before forwarding the data.
  
3. **Randomized Path Selection** Tor uses a randomized path selection mechanism for routing traffic through its network. While this randomness enhances anonymity, it can result in suboptimal routes, potentially causing delays and increasing latency.  

4. **Exit Node Bottlenecks**: The exit node is the final relay in the Tor network before the traffic reaches its destination on the open internet. The bandwidth of the exit node can be a bottleneck, limiting the overall throughput of the Tor connection.  
5. **UDP Traffic Handling**: Tor is primarily designed for TCP traffic, and handling UDP traffic introduces additional complexities and potential performance issues
Tags: tor

END

---

START
Basic
Descrivi perché un sistema sincrono ha al massimo n-f crash

Back: 
Essendo in sincrono, c'è un idea di randomicità. Anche in BenOr ce li ha in maniera asincrona.
TUtti i nodi briadcastano i valori in un tempo finito, prendi tutti i valori e prendi il minimo. Se c'è un failure non funziona, perché il nodo che fallisce riesce a inviare solo a di nodi il valore. Hai bisogno di almeno 2 round.

Es.
Crash = 1, Round = 2
Se tu hai la sicurezza che c'è un round dove non hai failure, visto che il sistema è sincrono, tutti scelgono lo stesso valore, quindi basta che ne fai f+1.
Il secondo round è proprio quello di recovery.

Se esiste un crash in recovery: NON È POSSIBILE!
Infatti se esistesse non avresti bisogno di fare il round di recovery
Tags: async f-crash crash-failure

END

---

START
Basic
Do you remember fast-paxos? 
1. Are they used in the real life?
2. Why do they exist?
3. Is fast-paxos safe, and why?
4. How it works?
5. How many failures can it tolerates, and why?
Back: 
1. Fast Paxos are the evolution of Paxos. They're **not really used in real life**, because if the system has a big number of values to accept, it is likely to get conflicts. Since in fast paxos we have a coordinator who have an accept-any, conflicts can arise. So we don't use them that much.

2. It is used to achieve consensus on a sequence of values, by managing multiple parallel proposers.

3. Safe means that "nothing bad ever happens", then: only a proposed value can be chosen, only a single value is chosen, only a chosen value may be learnt by a correct learner.
   In fast paxos, if both proposers get a value after accept-any, proposers will vote for different values, so it is impossible to reach a majority. If in future another proposer prepare something more, and A gets only 2 of the trees proposed values; one voted 12, one 19. The two values (12 and 19) come at the same time, so I don't know what to log: I'm stuck

4. Let's suppose we have a thousand of instances of paxos. There are some proposers, one coordinator and some acceptors. The coordinator sends prepare(1_1000, 5) to acceptors and collects promise(1_1000, 5, \_1, \_) from acceptors. Then sends accept-ANY(1_1000, 5, ANY), which means acceptors must accept any value that any proposer sends to them and learn.
We consume above three messages for free, because they are just 3 for 1000 instances. So here, we will have only accept and learn (which is faster): 3 messages (proposer to coordinator, accept, learn) instead of 5 (message from a proposer to a coordinator, **prepare, promise, accept, learn**).

5. Failures can be tolerate if (n-1/3) => we need 2/3 of votes

If we have 3 acceptors in fast paxos, we are not allowed to have exactly 3 acceptors, but this is a bad idea: if there is not a majority, I will take any value
Tags: paxos fast-paxos

END

---

START
Basic
Do you remember paxos? 
1. What is it? How it works?
2. Why it is not against FLP Theorem?
3. Is paxos safe, and why?
4. Is paxos live, and why? How can I make it live?
5. How many failures can it tolerates, and why?
Back: 
1. Paxos is a protocol to achieve consensus in an asynchronous system that allows f crash failures.
It works in this way:
- **prepare**: **proposer** sends **prepare** and it will be sent to **all acceptors**. It has the value of the round.
- **promise**: the **acceptor reply with a promise message** to the same proposer. It has current round number, last voted round, value of last voted round. It says **"I'm not going to participate in any other round round smaller than this"**
- **accept**: when **proposer gets a/2+1 of promises from acceptors**, then it can send a message to the acceptors called **accept**
- **learn**: Learners learn the value for that round. Everybody's happy!

2. FLP theorem says that it is **impossible** for a set of nodes in an **asynchronous** system to **agree on a binary value**, in presence of **any failure**.

The term “impossible” means that regardless of the algorithm, **it is not always possible to find a consensus solution**.  
  
The implication of this theorem is that **it is impossible to have consensus given a distributed system**.

Paxos guarantees to **reach consensus even in the presence of failure**. However, Paxos **does not guarantee that the consensus process will always terminate**. Hence, it does not refute FLP.

3. **Paxos is safe**:
Assume, A acceptors, i round, Q subset of A that sent the promise. |Q| >= n-f

We need to demonstrate that:
- p1. if v is chosen in round i, and v' is chosen in round j, then j != i, then v=v'
- p2. if acceptor accept a vote for r in round i, then no v!=v' can be chosen in rounds j<i.

We use the **induction**.
   * i=1 trivial
   * i > 1: let's assume that P2. is True for rounds <= i.
We have two cases:
1. j=-1, so the acceptors in Q have never voted (so in rounds j+1, ..., i-1 there would not be any value other than v to accept).
Besides, all the acceptors from Q promise that they won't participate in rounds smaller than i.
|A-Q| < n-f : acceptors that didn't promise
So they are the minority. So the protocol is safe.
2. j > 1: The voted value is v. Acceptors in Q have promised that they won't participate in rounds smaller than j+1...i-1 and Q is the majority. In round j someone voted v, because the proof holds for every round < i and j < i, so it was safe to vote v in round j, and it is not possible that in rounds smaller than j something different has been chosen. 

4. **Paxos is not live**: because **you can interlive between prepare and promise**, you promise not to participate in a round smaller than current one, so the previous round can not complete.

If more than one proposer starts off new rounds concurrently, then there is no guarantee that any round completes and a value is chosen.

P sends prepare for round i
A sends accept

Before receiving the acept, the acceptor receives a prepare for round i' > i from another proposer.

Since the acceptors have voted to not to vote for any round before i', the round i cannot be completed.

**It is not guaranteed to terminate**, thus doesn't have the liveness property. This is supported by FLP theorem that states that a protocol can only have two of safety, liveness and fault tolerance.  

5. f is the number of failures, n is the number of nodes, so **f=[(n-1)/2].** **The majority is (n-f).**
Tags: paxos

END

---

START
Basic
How do you find hidden websites? (tor)
Back: 
They can be found on other websites or search engines specialized in that, such as the Hidden  
Wiki, or someone can directly know their onion address.
  
A hidden service registers itself to a directory server, attaching its public key and a set of introduction points.
Tags: tor

END

---

START
Basic
How to connect to a Hidden Service on Tor
Back:
A hidden service registers itself to a directory server, attaching its public key and a set of introduction points.

A client asks the directory service the list of introduction points. The client picks a random node as a rendezvous point, and sends both the point and a random string to the introduction points.

The Hidden Service receives all of that, and if it is ok with that, it contacts the chosen rendezvous point to initiate the connection and finally communicates with the client.

No one knows who is talking to, and also all these links are using a circuit by themselves (a link of 3 or more nodes, randomly picked by the protocol).
Tags: tor

END

---

START
If you use TOR to visit CNN, is that the Dark Web?

Back: 
No. This is just using Tor as a way to protect traffic from the sight of governments, ISPs and many other actors on the Internet. But the CNN is a classic website which is not inside Tor
itself, and will be actually reached by the exit node.

The Dark Web is a way to refer to Hidden Services. They are actually services that are reachable only from Tor, addressed using a .onion domain name. It is a way to protect the site and not only the client who connects to it. It’s the case for sensible or illegal websites that must preserve their identity.
Tags: tor
END

---

START
Basic
How many failures could we have? Describe them.
Back: 
1. Crash Failure
The system works or crashes, nothing malicious happens.

2. Byzantine Failure
It is a condition where components may fail and there is imperfect information on whether a component has failed.
A host is up and running, but it has a bad behavior (bug, malicious...).
Tags: failure

END

---

START
Basic
Safety and liveness (in general + in depths with paxos)
Back: 
- Safety Properties
    - nothing bad happens ever
    - example: mutual exclusion (no more than one process holds a critical resource) 
    - paxos: only a proposed value can be chosen, only a single value can be chosen, only a chosen value may be learnt by a correct learner

- Liveness
    - something good will eventually happens
    - example: no deadlock
    - paxos: paxos is not live: rounds cannot be completed because of multiple promises from acceptors
Tags: definitions properties

END

---

START
Basic
What happens if all the intermediate servers are malicious, are you safe? (TOR)

Back: 
If exit nodes are compromised, together with Guards (initial nodes), traffic correlation is  possible and so the privacy is compromised. Since the same entity can observe both incoming  
and outgoing traffic, it knows both who is sending data and which site is receiving it.  
In the case of only intermediate nodes compromised, they do not know anything about the sender and the receiver, so it is perfectly fine as long as they are not guards or exit nodes.
Tags: tor

END

---


START
Basic
Describe the notion of Proof Of Work in Bitcoin / Bitcoin consensus protocol
Back: 
Bitcoin uses a consensus protocol based on Proof of Work. The nodes agree on one of the latest
blocks in the blockchain, implicitly agreeing on all of the ones before that one. That’s the case because inside the header of a block there is the Hash of the previous one.

Keep going with this hash field for all previous blocks and we can see that all of them are implicitly agreed upon. A miner is a fundamental actor in this context: it spends computational resources to find a random nonce that, inserted in a specific field in the block header, makes the final hash of the block lower than a certain threshold which determines the difficulty of finding the correct nonce, adjusted by the protocol.

Since the header of a block contains the hash of the previous one, after a number of blocks, usually 5, a block is considered finalized because changing its content will invalidate the hash of all the ones that refer to it as the predecessor (directly or indirectly) and so the nonce. Recalculating the nonce in a timely manner is considered infeasible.

Every other node will receive the block from one of the miners (the fastest one for that specific block)
and will proceed validating it: all transactions will be validated and also the correctness of the nonce with respect to the criteria we’ve mentioned earlier.
Tags: bitcoin btc

END


START
Basic
Describe Failure Detectors and their taxonomy

Back: ![[Pasted image 20240122123131.png]]
Tags: failure properties

END

---

START
Basic
Show how to make Paxos live with a failure detector in W
Back: 

**With a weak failure detecture**
By definition a weak failure detector has weak accuracy and weak completeness. Weak accuracy means that there exists at least one process p which is never suspected by any correct process.
That means that the intersection of correct processes is never void; so we can exchange the correct set with each other and elect as coordinator the smallest node id in the intersection. So we will make Paxos live with ONLY a weak failure detector.

**With a strong failure detecture**
A perfect failure detector is a specialization of a Strong failure detector.

A strong failure detector, by definition, is eventually right. In fact, only after a certain time t, every process will know that a process P has crashed some time before.

A perfect FD is also the specialization of a Strong accurate FD.

A strong accurate FD never reports a live process as crashed.

Leader Election: every process elects as a leader the process with the lower ID among the ones which it thinks are alive right now.

The "election" is repeated every time the failure detector changes state.
1. Since eventually the failure detector state will converge, so does the elected leader
2. Having a single alive leader makes Paxos live

Does the common leader exist? Suppose a process picks a process P as its leader.
- Can P be crashed? Yes, but if it is, the FD will eventually change state and report P as crashed, thus changing the elected leader locally. The process repeats for a process Q (ID(Q) > ID(P)). In the worst case, the set of alive processes will contain only myself, so it’s guaranteed that it’s never empty.
-  Can P be considered crashed by someone else? If P is alive, it cannot happen because the FD is strongly accurate, which means that an alive process is never reported as crashed by anyone.
-  Can process 𝑄 pick 𝑃' as leader? 
	-  If ID(P’) > ID(P), that’s impossible for the point above
	- Otherwise, I am considering P’ as crashed. Since FD is strongly accurate, it is actually crashed, so Q will eventually converge to P.
Tags: Paxos failure-detector

END

---

START
Basic
Propose an implementation of a Failure Detector and discuss its properties in a synchronous system
Back: 
Heartbeat protocol, under the assumption that all messages are delivered in time at most ∆𝑡
1. Every process 𝑝, sends to everyone an Alive message every time ∆𝑡
2. Every other process 𝑞 ≠ 𝑝, if it doesn’t receive any Alive message after ∆𝑡 time from 𝑝, then 𝑝 ∈ 𝐷𝑞(σ, 𝑡')

**Strong Completeness**
Under the assumption of a synchronous system in which messages are always delivered in a time bounded way without losing them, it is Strong Complete.

When 𝑝 crashes, no one will ever receive a heartbeat message from it. After time ∆𝑡, other processes will report it as crashes. Also, this action is done by every process, so every process knows about the crash of anyone else

**Strong Accuracy**
Under the same assumption, a process must send the Alive message every fixed amount of time. Since no message is lost, and it is time bound, every process will receive the Alive message from everyone before it can be considered crashed. So no one ever reports an alive process as crashed.

Unfortunately, in an asynchronous system, messages can be lost and are not time bound.

Tags: failure-detector

END

---

START
Basic
Describe briefly the Bit-Torrent system
Back: 
BitTorrent is a peer-to-peer system used to distribute files efficiently all over the world.
When a user wants to download a certain file, first of all he must get a Torrent file, which is a descriptor
that contains many information about the file to download, including:
- URL of the Tracker (= server that keeps info about the community at a global state level)
- Name, length and hash of each part of the file, usually 256KB each;
	- Splitting the file into several small parts is used to improve parallelism
	- Having their hash is used to avoid Pollution (having wrong parts of the file circulating around the network)
	- Newer versions use a Merkle tree to verify the hash of the parts of the file: this way, the data integrity of a single chunk can be verified using a logarithmic number of hashes, with respect to the total number of chunks.
		- Still, we have pollution if an entire wrong Torrent file is got by the user
Then, the Tracker returns a list of some peers who have the file ready to be uploaded.

**Which parts of the file should I download first?**
1. The **Rarest first** may be an approach, because it improves the redundancy of a rare part of the file and also it’s safer to abort a download as soon as possible because of a part of a file is missing instead of realizing it only at the end of the process
2. **Randomly**: parts to download are chosen in a random way

**End-game mode**
At the very end of the download, in this mode, a piece of the file may be too slow to download because of several reasons, such as low bandwidth of the peer who is uploading.

In End-game mode, the remaining part is splitted more times and its download is parallelized, downloading from multiple peers.

**Choking for Peers**
In order to avoid saturating some peers and to stimulate a collaborative approach, where one peer also uploads and does not just perform downloads, **unchoking algorithms are used**.
First, a peer A unchokes B randomly, otherwise a new member of the network would have no chances to download anything and so it won’t be able to upload either.

Another algorithm is **Tit for Tat**: A unchokes B if and only if B starts uploading other pieces to A (that A
needs, of course).

"A" should not unchoke too many peers otherwise it’ll have no bandwidth left to download what it
actually needs.

**Node types**
1. Tracker: has the list of the seeds who are sharing the file.
2. Seeder: have the entire file and are only distributing it.
3. Leecher: downloads the file and becomes a seed when the download is over.
4. Free-riders: downloads the file without uploading after.
Tags: bittorrent

END

---

START
Basic
Describe briefly the Akamai system
Back: 
The idea behind Akamai is to serve static content on a website from a server geographically near the user who requests that content.
The implementation is based on the following steps:
-  A website which wants to adopt this system will change the URL of the static content such as images to a URL managed by Akamai. cnn.com/static/image1.jpg may become something like cnn.static.akamai.com/image1.jpg
-  A browser receives that URL and has to resolve cnn.static.akamai.com in a real IP address, using DNS
- The authoritative server responsible for the \*.static.akamai.com domains will return the IP of the server(s) near the user, so that the latency will be lower when actually downloading the file and showing it to the final user in the webpage

This system loses Consistency (in the context of the CAP theorem), which is not so important in systems like CDNs.
Tags: akamai cdn

END

---

START
Basic
What is Atomic/Sequential Consistency. Describe the difference between Sequential consistency and Atomic consistency.
Back: 
In Shared-Memory systems there are several types of possible memory consistency, each one of them with different properties and that can be implemented in different ways.

Two of them are the Atomic Consistency (aka Linearizability) and the Sequential Consistency.

Specifically:
-  Atomic Consistency: in this type of consistency the properties are:
	1. Any read to a location must return the value written by the most recent write as per a global time reference
	2. All operations appear to be executed atomically
	3. All processes see the same sequence of reads and writes
	In this type of consistency every read and write can be saw as a sequence of <invocation, response> and so given a sequence SEQ of <inv, resp> it is said that SEQ is linearizable if exists a SEQ’ of adjacent pairs <inv, resp> such that:
	1. For any variable v, the projection of SEQ’ on v (called SEQ’v) is such that every read returns the most recent write
	2. If the resp of OP1 occurred before the invocation of OP2 then OP1 appears before OP2 in SEQ’
	This means that with this type of consistency we try to find a sequence of operations SEQ’ that is the de-overlapped version of SEQ that is needed to let every process have the same vision of the events.
	The Linearizability can be implemented thanks to Total Order Broadcast
- Sequential Consistency: this is a weaker version of consistency wrt Linearizability in which the result of the computation is as if all the operations were executed in SOME order. The internal order of each process must be respected.
	
	Sequential Consistency is always possible when there is Linearizability (by respecting the same order) and it can be implemented with the Total Order Broadcast (without the broadcast of the reads)
Tags: DSM

END

---

START
Basic
Describe how a CDN works
Back: 
A Content Delivery Network is a system which is used to improve the performance of serving static contents in different geographical locations.
It is a system that, from the point of view of a website’s owner, improves the speed of the loading of the page, in a much cheaper way than renting servers geographically distributed.
A CDN works by storing and caching different static contents, distributing across the globe if they are heavily requested by users, and load balancing the requests.
Also, it can improve the performance of the dynamic content because many requests for static content don’t need to be sent to the actual origin server because they are already cached by the CDN, so that it has more computational resources to compute dynamic content.
Some CDNs also offer the possibility to serve dynamic content executing small scripts on edge servers, located near the final user.
Tags: CDN

END

---

START
Basic
Describe how the DNS system works
Back: 
Domain Name System is a hierarchical and distributed naming system used for translating
human-friendly domain names into IP addresses.
1. The user enters a URL, so the client must resolve the domain name into an IP address (di.uniroma1.it)
2. The local DNS resolver receives the request and replies with the records associated, if it already has them in cache
3. Otherwise, the root DNS server is involved. It stores information about the TLDs servers, such as .com, .it and so on (.it)
4. The TLD DNS server will respond with the IP of the authoritative nameserver for the requested domain (.uniroma1.it)
5. The request is sent by the client to the authoritative nameserver, which will finally reply with the IP address(es) for the requested domain.

It can also reply with other information, based on the type of requested DNS records, such as A -> IPv4 address to visit, AAA -> IPv6 address, CNAME -> alias domain name, TXT -> text with various possible meanings, and so on.
Tags: DNS

END

---

START
Basic
Describe the four ways in which we can simulate a strong failure
detector using a weak one
Back: 
θ to  P
In this case we have that in the θ there is only a single process that detects the crashed process and so we need some information sharing.

Consider the following algorithm in which every process P do the following:
	initially: output = Ø
	when p changes:
		suspectsp <- Dp
		send(p, suspectsp) to everybody
	when msg is received by (p, Sp)
		output = (ouptputp U Sq) - {q}
	Broadcast the info so that everyone knows everything
Tags: failure-detector weak-failure-detector

END

---

START
Basic
Pump & Dump in cryptos
Back: 
In an unregulated market such as cryptocurrencies, market manipulation techniques are possible.

Doing that on the stock market or other regulated markets is illegal.
The scheme involves artificially inflating the price of a coin (pump) and then quickly selling it as soon as possible, making its price drastically drop (dump).

The coordination of the pump action is usually conducted on Telegram or other privacy-oriented messaging systems by a team of people. Since they are the ones who perform the manipulation, they
decide the coin to Pump. This way they can (and will) buy a huge amount of that coin, slowly from time to time to remain hidden from the public.

At a precise moment, they will release the name of the coin to pump to the members of the Telegram channel who will instantly buy large amounts of it, making the price go up.

The administrators, who bought the coin a long time before, will be the first ones to sell and the ones who make the greatest profit. Unfortunately, members are almost always the ones who get scammed because it’s nearly impossible to sell right before the dump. Remember that the pump and dump may last for only very few minutes.

The members are acquired by stimulating the FOMO of the public and saying that everyone will earn a lot of money because only the outsiders will lose everything, which is false but members do not know that until they experience it first-hand.

DeFi and Dex:
- **DeFi**: decentralized finance, smart contracts support the creation of it
- **Dex**: exchange market that executes as smart contracts

New coins can be created easily, as smart contracts that implement **liquidity pools**: two values, one listed and one not listed. 

Other concepts:
- rug pull: at a some point, the owner of a smart contract (liquidity pool) closes the contract and gets all the money 
- sniper bots: bots that allow you to buy at the lowest price possible
Tags: seminars cryptos

END

---

START
Basic
How many processes do I need to tolerate f faults?
Back: 

|       | crash faults | byzantine faults (no signature) | Byzantine faults with signature |
| ----- | ------------ | ------------------------------- | ------------------------------- |
| synch | f+1          | 3f+1                            | 2f+1                            |
| async | 2f+1 (paxos) | 3f+1                            | 3f+1                            | 

**Safety: not reliabness**

In fact, FLP theorem says that consensus is impossible in async system in presence of any fault.
Tags: paxos failures

END

---

START
Basic
Talk about privacy on the internet: analysis of Wifi Beacons in crowds, VPN IPv6 leak, user
IP identification in cellular networks, browser fingerprint, privacy on social networks.

Back: 
**Crowd analysis**
According to the 802.11 standard, a WIFI access point can announce its presence by broadcasting Beacon Frames containing network configuration parameters such as SSID (a string that identifies a WIFI AP in a human-readable form ‘home network’). On the client side, it can scan for WIFI AP in two ways: Active send a probe request to discover networks, Passive listen for beacons and decide which to connect to.
To further improve this mechanism a PNL (preferred network list) is kept by the OS.
It is possible to collect those beacons to get some information about the device owner.
A possible usage of the collected information is to create a graph-structured “social network”, where nodes are smartphones and edges are common Access Points. The key idea is that people connected in the real world are also connected in this network.
Another possible usage of those collected packets is to connect the smartphone owner to the specific location where the owner lives: this is done by searching the home network SSID in the Wigle Database. Since home networks usually have an SSID like “TIM-xxxxxx” the SSID (structured like that) is unique and points to a unique location.

**VPN IPv6 leak**
In operative systems, the IPv4 stack and the IPv6 stacks are separated and only the needed one is used. By testing 14 commercial VPNs the researchers discovered that most of them (10/14) were vulnerable to IPv6 leak: when the user is connected to a VPN and sends data through the IPv6 stack, the data are instead sent in clear and not through the VPN, the result is that the user of the VPN is not protected.
Almost all the VPNs tested (13/14) were also found to be vulnerable to DNS Hijacking: when the user is connected to a VPN and makes some DNS queries, they are intercepted and manipulated.
This is a big security issue because an attacker can redirect the user to some malicious websites to steal credentials or to make some scams. This means that the user types, for example, “paypal.com” and the DNS server redirects it to a malicious clone of it. The browser shows a warning to the user (the red lock icon), but a lot of users ignore it.


**User IP identification in cellular networks**

By looking at the Round-Trip-Time it is possible to know if a target smartphone is sleeping, since it'd have a longer RTT than active smartphones. To get the IP address of the target the attacker can send a message to wake up the device using one of the popular messaging apps widely used, and then ping all the smartphones in the network (this means that the attacker will send millions of pings): the smartphone with the lowest RTT is the one the attacker is looking for. By performing this attack several times (within 20 messages) is it possible in 80% of the cases to correctly identify the smartphone's address, which can then be localized.
Tags: seminars

END

---

START
Basic
What 2FA Commit is?

There is a coordinator and participants. The coordinator sends a message to all participants to vote as vote-req. When the participants receive this message sends back to coordinator the vote which can yes or no.
If the vote is no, then the participnats know the final outcome of the decision (abort).
Commit happens iff when all engaged processes agree on "yes": if only one of them say "no" it must be aborted.

If the final vote is "yes", then the state is "uncertain": on coordinator side, if all the votes are "yes" then the final decision is commit. Otherwise, abort.

In a real world examples, there is a time out in each request: if time out expires, then something might be wrong, then **abort**.

Back: 
Tags: 2fa

END

---

START
Basic
In 2FA, when you're stucked?
Back: 
In 2FA Commit you are stucked if you vote YES and you wait for the final decision that never happens.
1st scenario: 
- coordinator sends voteREQ
- anybody vote yes
- coordinator fails
- all of them are blocked
2nd scenario:
- voteREQ
- you vote YES
- everyone else but you is dead (you're alone)
Tags: 2fa

END

---

START
Basic
Show that the intersection of two consistent cuts is also a consistent cut.
Back: 
![[Screenshot_20240122_232630.png]]
Tags: properties

END

---

START
Basic
Let's assume a synchronous system. How can I code a failure detector?
Back: 
process p: for each p ping(q)
q is the failure detector

if no reply 2 delta time then Dp <- q
repeat every 2 delta time
In case of false positive, double delta time.
Tags: failure-detector

END

---

START
Basic
Describe Bitcoin and Blockchain. (also describe consensus and PoW)
Back:
Bitcoin is an alternative to cash, nobody knows who you are.
Blockchain is a group of ledgers, containing blocks, containing transactions.
Transactions to be confirmed are put into blocks, these blocks need to be confirmed in order to authorize transactions.

If two solutions are considered valid: the **longest** one will be taken

Miners: work and find values to confirm blocks

Paxos and fast-paxos are not good choices, because they can tolerate crash and failure but not byzantine-crysis, then no malicious user is allowed.

Tags: bitcoin btc

END

---

START
Basic
Show that every consistent global state can be reached by some run.
Back: 
![[Pasted image 20240122232717.png]]
Tags: cut clock

END

---

START
Basic
Show that the Chandy-Lamport Snapshot Protocol builds a consistent global state.

Back: 
The protocol requires that each process, after receiving an initial take snapshot message, sends another take snapshot message to all other processes. This, assuming FIFO communication channels, ensures a consistent snapshot.
Since after the local snapshot is taken, the messages that immediately follow are take snapshot messages, no event that occurs after the snapshot can cause an event that occurred before the snapshot on another process, because the take snapshot message arrives before any subsequent event message due to the channel being FIFO.
Tags: lamport

END

START
Basic
What good is a distributed snapshot when the system was never in the state represented by the distributed snapshot? Give an application of distributed snapshots.
Back: 
It’s not possible to have a global clock among a distributed system, in fact the most important thing in a distributed system is to have the cause-effect relationship between events, because if an event may influence another we must not lose this information. The distributed snapshot, otherwise, helps us to solve Global Predicate Evaluation. The goal of GPE is to determine whether the global state of the system satisfies some predicate. Global predicates are constructed so as to encode system properties of interest in terms of state variables. Examples of distributed system problems where the relevant properties can be encoded as global predicates include deadlock detection, termination detection,
token loss detection, unreachable storage (garbage) collection, checkpointing and restarting, debugging, and in general, monitoring and reconfiguration. In this sense, a solution to GPE can be seen as the core of a generic solution for all these problems; what remains to be done is the formulation of the appropriate predicate and the construction of reactions or notifications to be executed when the predicate is satisfied.
In fact, without a snapshot that builds a consistent global state we could occur in some problems like ghost deadlock, in which a deadlock is detected even if it will never happen in a consistent run. Also keeping the consistent global history will allow the system to recover until the snapshot checkpoint
Tags: snapshot

END

---

START
Basic
Consider a distributed system where every node has its physical clock and all physical clocks are
perfectly synchronized. Give an algorithm to record global state assuming the communication network
is reliable. (Note that your algorithm should be simpler than the Chandy–Lamport algorithm.)
Back: 
This means we have access to a real-time global clock. Assuming message delays are bounded to δ, the monitor process starts the protocol by broadcasting a “take a snapshot” message at time t0 for time t ≥ t0 +δ. At time t, each process sends its snapshot to the monitor, which can reorder the events in increasing timestamp order. Number of messages goes from O(n2), required by the Chandy-Lamport algorithm, to O(n).
Tags: lamport

END

---

START
Basic
Show that, if channels are not FIFO, then Chandy–Lamport snapshot algorithm does not work.
Back:
![[Pasted image 20240122233238.png]]
Tags: lamport

END

---

START
Basic
How many messages are used in Paxos if no message is lost and in the best case? Is it possible to reduce the number of messages without losing tolerance to failures and without changing the number of proposers, acceptors, and learners?
Back: 
In classic Paxos we need 3n - n * l messages:
- n prepare
- n promise
- n accept
- n\*l  learn (where l is the number of learners)

Consider the quorum Paxos needs to get a majority:
Q = n - f and f = n-1/2

If we send the messages only to a majority, the number of messages is reduced at least to 3Q + Q \* l. Fault tolerance is provided by using this number of messages only in one round of Paxos, and then reverting to classic Paxos in case of failures
Tags: paxos

END

---

START
Basic
What is a fork in blockchain

Back: 
A fork is a division in the block chain that it’s verified when two different new blocks are accepted because both got the hash right. In this case, the blockchain keeps working in parallel on both, creating two different chains. The longest chain (the chain with the most effort, which is usually the longest) will be preferred because it will have the updated values. Once the best chain is found, the other is discarded.
Tags: bitcoin btc

END

---

START
Basic
Is blockchain safe? Is it live?
Back: 
![[Pasted image 20240122234558.png]]
Tags: bitcoin btc

END

---

START
Basic
Describe shared memory system
Back: 
Shared memory is an abstraction of a distributed system giving the impression of a monolithic memory. Programmers only use read and write primitives to access the network and do not have to deal with send and receive. To provide programmers with the illusion of a single shared address space, a memory mapping management layer is required to manage the shared virtual memory space.

Advantages:
- simplifies task of programmers
- simplifies passing-by–reference
- exploits locality to reduce communication overhead
- fairly cheap
- no bottleneck due to single memory access
- large virtual main memory
- portability

Disadvantages:
- programmers are not shielded from having to know about various replica consistency
models
- overhead as high as message passing implementation (programmers lose the ability to program their own solution)

There are four broad dimensions along which DSM systems can be classified and implemented:
- data replicated or cached
- remote access via hardware or software
- caching/replica via hardware or software
- DSM controlled by distributed memory system, operating system , language runtime system

Memory coherence is the ability of the system to execute memory operations correctly. There are various consistency models, the following figure represents their hierarchy.
The order is (those above include those below??):
- No consistency model
- Slow memory
- Pipelined RAM (PRAM)
- Causal consistency
- Sequential consistency
- Linearizability / atomic consistency / strict consistency
Tags: DSM

END

---

START
Basic
Telegram exploration: TGDataset

Back:
Telegram’s channels are virtual rooms where only an administrator can write and broadcast messages to the subscribers. A fake channel, to deceive the users, usually has the exact name with slight variations; it attempts to qualify itself as the official miming the original behavior.

The study has the goal to detect real and fake TG channels, to do so were built 2 datasets. The first one **TGDataset** includes 120’000+ channels. This dataset takes a snapshot of the actual telegram ecosystem instead of focusing on one single topic.

Dataset creation: the dataset was built using a python’s wrapper for telegram’s official API, they take the last 3000 messages per channel and their lifetime (the time from the channel creation to his last message); then channels were divided in ‘verified’ and ‘not verified’ using official statistics, so from the verified ones, the fake ones that was claiming to be officials were extracted.

A further analysis of the dataset has highlighted some patterns: Verified channels generally have more subscribers than fake ones, fake channels usually 10% of subscribers of the original one, the original channels send more messages and post more media than fake ones, fake channels are more prone to forward messages from others channels.

The chones feature were: writing style (messages length, emojis, ecc…), temporal features (number of messages sent in month) and external interaction (forwarded messages, external links, ecc…).

In the end the best model found was using an MLP (Multilayer perceptron, not my little pony) classifier with an F1 score of ≈85%.
Tags: seminars

END

---

START
Basic
What atomic commit is. Describe atomic commit. This problem is also known as?
Back: 
Consensus Problem.
1. All processes will reach a decision
2. A process can not change decision after reaching one
3. The commit can be reached only if all the processes vote yes
4. If there are no failures, and all the processes has voted "yes", than the decision must be "commit" (final) 
5. in a system that allows for process to fail, if the failures are repaired and if the process can rollback to the process sequence, then the transaction must get completed
Tags: 2fa consensus

END

---
