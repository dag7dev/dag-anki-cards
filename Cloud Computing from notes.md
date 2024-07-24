---
date_created: 2024-07-19
date_modified: 2024-07-20
document_type: note
tags:
  - note
---
TARGET DECK: Cloud Computing from Notes
START
Basic
What is Cloud Computing?
Back:
Cloud computing is a model for enabling **ubiquitous** , convenient, on- demand network access
to a shared pool of configurable computing resources (e.g., networks, servers, storage, applica-
tions, and services) that can be rapidly provisioned and released with minimal management
effort or service provider interaction.

Ubiquitous = server and data can be located anywhere and accessed from anywhere. Users should not care where it is, or the physical details underneath the service they’re using.

Only the geographical location can be important to improve performances of services, locating them near the final user of the application.

Essential characteristics:
- On-demand self-service: no technical intervention on hardware should be required
- Resource pooling and Rapid Elasticity
<!--ID: 1721488489601-->
END

---

START
Basic
What does mulyi-tenancy means?
Back:
Multi-tenancy (users are tenants): applying this concept to cloud computing, we see that
users must have their own view of the hardware they are using; typically sand-boxed inside
VMs, sharing the same hardware.
<!--ID: 1721488489603-->
END

---


START
Basic
What are the basic characteristics?
Back:
The characteristics are:
- Scalability / Elasticity (the degree to which a system is able to react to workload changes
    during execution, provisioning and de-provisioning resources automatically)
- Isolation
- Availability from a wide range of locations, generally on the Internet, using standard pro-
    tocols
- Recovery from failures of the underlying hardware
- Metered Usage of their resources
<!--ID: 1721488489605-->
END

---

START
Basic
What are the three main cloud architectures?
Back:
- **SaaS** : end-user applications
- **PaaS** : the runtime for the applications is sold (Google AppEngine -> you deploy a docker image on it)
- **IaaS** : the whole virtualized server and low-level resources are sold (EC2)
<!--ID: 1721488489607-->
END

---

START
Basic
The cloud provider is responsible for? What about the customer?
Back:
Cloud provider must guarantee **Security of the cloud**, by regulating **physical security of the**
**servers** in data centers, mantaining the **hardware infrastructure** by **replacing broken compo-**
**nents and upgrading** them when necessary, but also on the software side it needs to **audit the**
**security of the system** (isolation on virtualization, scalability, orchestration, etc). Finally, also the
network infrastructure must be mantained by the Cloud provider.

On the other hand, the customer has responsibilities for **Security in the cloud**. In the case of
IaaS, he needs to **patch the system and run system upgrades**, but also setting up **firewall** rules
and managing access to the VPS, such as **regulating SSH keys** and **user roles**.
<!--ID: 1721488489609-->
END

---

START
Basic
Deployment models
Back:
- **Public** cloud: accessible from a provider by all users around the world, without particular
    requirements
- **Private** cloud: on-premise cloud architecture, where the entire underlying physical re-
    sources are owned by a customer. Generally used by important companies, which want a
    better and more reserved service
- **Hybrid** Cloud
<!--ID: 1721488489611-->
END

---

START
Basic
Cloud roles: what they are, what they do
Back:
- Cloud **Provider** : an entity responsible for making a service (SaaS, PaaS, IaaS) available to
    interested third parties
- Cloud **Consumer** : an entity that mantains a business relationship, using services, with a
    Cloud Provider
- Cloud **Auditor** : an independent entity that assesses performances and security of cloud
    implementations
- Cloud **Broker** (informally "aggregator") : an entity that manages delivery of cloud services, negotiating between
    cloud Providers and Customers - it may also aggregate different existing services to pro-
    vide a new one
- Cloud **Carrier** : an intermediary that provides connectivity of cloud services from Providers
    to Customers - it may have a second SLA with the Provider
<!--ID: 1721488489613-->
END

---

START
Basic
Parallel vs Distributed: what's the difference, paradigms...
Back:
A parallel execution follows some principles:
- **Homogeneity**: tasks are all the same type
- **Locality**: generally on the same physical location
- **Parallelize on Data**, Process or **Master-slaves architecture**

A parallel computing application can follow these paradigms:
- **SIMD**: Single-Instruction Multiple-Data (as in GPUs)
- **MISD**: Multiple-Instruction Single-Data
- **MIMD**: Multiple-Instruction Multiple-Data (shared memory)

On the other hand, Distributed computing is when we run a process on multiple hosts con-
nected via network, and they coordinate only by _passing messages_ between each other.
The computation is divided between units, executed in different units (like CPUs, servers,
and so on).

In Distributed systems, the final application uses a framework that abstracts all the com-
plexity of the operations (Middleware), talking to the operating system and hardware via IPC
primitives.

It’s _introducing utilization models for remotely provisioning scalable and measured
resources_.
<!--ID: 1721488489615-->
END

---

START
Basic
Architectural styles: software
Back:
An example is _batch execution_ or also the _map-reduce_ paradigm, which is a subset of _pipe and
filter_ architecture; where we split data across nodes, apply the mapping, shuffle based on the
key and finally the reduce step to get the final result.

In general, _components have their own life_ : they are independent and handle communica-
tion with others via messages or some form of IPC. They can also be **event-based** , where the
messages are essentially events, stored inside of a queue, via a pub-sub paradigm.
<!--ID: 1721488489617-->
END

---

START
Basic
Architectural styles: definition
Back:
Architectural styles are the way in which we determine how different components are built and
relate each other, also introducing constraints. (Software + System)
<!--ID: 1721488489619-->
END

---

START
Basic
Architectural styles: system
Back:
Client-server or Peer-to-Peer, because they handle how major software components should be
built and behave.

In the Client-Server world, we have the _multi-tier model_ :
- **2-tier** : suitable for small sized software because it suffers from scalability, but it’s also the
    easiest one; the tiers are Client (presentation) and Server (business logic + data)

- **3-tier** : we split business logic and data into 2 distinct layers, allowing the Data layer to
    be independent from the Business Logic implementation - but also the Logic tier can be
    stateless and now replicated

- **N-tier** : additional tiers can be introduced as needed to improve scalability and maintain-
    ability given by the decoupling of various components; here the extreme situation is Mi-
    croservices architecture

As in Peer-to-Peer architecture, all hosts (called Peers) are both servers and clients, making
this solution perfect for distributed systems with no central authority. It also has no bottleneck
components, so it can scale as much as we want in theory.
<!--ID: 1721488489621-->
END

---

START
Basic
What IPC are? Provide some examples and talk about RPC in general
Back:
IPC stands for "Inter-Process Communication".

To communicate, they need to use _IPC_ technologies. They can vary from message queues,
to events or more sophisticated forms of communications such as Distributed Objects, Web
Services (XML-RPC, gRPC, ...) or RPC (Remote Procedure Call) in general.
They can communicate, after defining the protocol, in a point-to-point way, or using more
standard Pub-Sub and Request-Reply communication models.

### RPC

Generally, in RPC we have an **RPC-server and RPC-client, that communicate via the network**.
They handle all of that via an RPC library, which is in charge of marshalling and unmarshalling
parameters to send and corresponding return values.
The software engineer still has to design the API to expose, and wheter to use a platform
dependent solution (RPyC) or not (XML-RPC).
<!--ID: 1721488489623-->
END

---

START
Basic
Service Oriented Applications
Back:
An application consists of aggregated services, each encapsulating specific functionalities with corresponding software components.

Key Points:
- **Explicit Boundaries**: Services have minimal interfaces to simplify interaction and encourage reusability.
- **Autonomy**: Services are independent, manage their own failures, and handle replicas.
- **Shared Schema and Contracts**: Services understand interactions and available services formally.
- **Compatibility**: Managed by policy expressions.
<!--ID: 1721488489624-->
END

---

START
Basic
How does the registration work?
Back:
We have the following steps when calling a service:

1. The _Provider_ registers itself to a _Registry_
2. A _Consumer_ discovers a service requesting it to the Registry
3. The Registry provides to the Client the Binding Information to call the service
4. Consumer establishes a connection with the Provider (protocol is dependent on the im-
    plementation and choices made by the software engineer)
5. Finally, the Consumer can actually use the service it wanted

Since we want to incentive re-usability, these 3 actors may be owned by different organiza-
tions. A single component can also act as multiple actors.
<!--ID: 1721488489626-->
END

---

START
Basic
Orchestration vs. Choreography
Back:
In _Orchestration_ we have a single central Composite Service (the Orchestrator). It combines
thedifferentfunctionalitiesprovidedbysingleservices,managingtheirinteraction. Anexample
is providing a workflow combining different services.

In _Choreography_ every service knows what are other actors and how to interact with them
without the need of a central authority. An example an authentication mechanism where a
service is responsible for validation authentication, and maybe another provides Authorization
policies.

**Web Services** are SOA and can be **SOAP** and **REST**.
REST provides a 1-to-1 mapping between a resource and its path in the
URL, and actions must be indicated by the HTTP method. They also need to be stateless in
principle.
<!--ID: 1721488489628-->
END

---

START
Basic
What does 'Microservices' mean? Describe pros and cons too.
Back:
It’s an architecture where various components are ideally **atomic, decoupled, independently**
**deployable and stateless**. It allows to move faster during development and better react to scal-
ing necessities: **we can just rewrite a single micro-service with a critical functionality in another**
**newer technology**, or to deploy multiple instances of an essential feature of the whole system.
Scalability can happen across different dimensions:

- **X** scaling (horizontally): clone and duplicate the whole system
- **Y** scaling (vertically): scale by doing functional decomposition and duplicate single pieces
    = microservices
- **Z** scaling (data partitioning): split data across different parts of the whole application by
    similar things, such as customer IDs in multi-tenancy replicated applications


Pros :
- Having **small independent parts** of the application **improves CI/CD pipelines** and better
    agility
- Independent scalability, **duplicating only necessary services** and saving resources other-
    wise assigned to unnecessary replicas of other services
- **Fault-tolerance** is relegated to a part of the system and not to it as a whole
- Better **adoption of new technologies** to only **specific small parts of the system**

Cons :
- **Splitting between the right services** is challenging
- Developing a distributed system **is more complex**
<!--ID: 1721488489630-->
END

---

START
Basic
Are microservices SOA? Why?
Back:
Microservices are not Service Oriented Architecture. They differ in:
- **Communication** : SOA is more heavy while MS use lightweight protocols such as gRPC or
    REST, vs Enterprise Service Bus in SOA, which is much more complex and exposes a single
    point of failure
- **Data** : SOA tipically have a single shared data source, while MS can have a data source for
    each service
- **Size** : SOA have big components and MS should be as small as possible
<!--ID: 1721488489632-->
END

---

START
Basic
Virtualization
Back:
Usually, applications invoke APIs of the libraries, which then are responsible for calling the Op-
erating system calls, finally executing privileged instructions on the CPU. For unprivileged ones,
an application or a library may directly call them to the hardware.
Historically, 4 rings existed: from _Ring 3_ (User mode) to _Ring 0_ (Kernel or Supervisor mode).
Nowadays, the intermediate _Ring 1_ and _Ring 2_ are unused.

The **Hyper-visor** , as the name says, it works on top of the Supervisor mode. Its goal is to
emulate a CPU and its state for guest OS. The privileged instructions on the virtual CPU will
still be executed in privileged mode, requiring Supervisor/Kernel mode. This is true especially
in modern Intel-VT and AMD-V instruction sets.

There are two types of hypervisors:
1. **Type 1 Hypervisor (Bare Metal Hypervisor):**
    - directly on the physical hardware of the host system.
    - No underlying operating system is required.
    - Manages the hardware resources and allows multiple guest operating systems to run
       directly on the host hardware.
    - Provides better performance and efficiency because it operates closer to the hardware
       layer.
    - Examples include VMware vSphere/ESXi, Microsoft Hyper-V (when installed on bare
       metal), and Xen.
2. **Type 2 Hypervisor (Hosted Hypervisor):**
    - on top of a host operating system.
    - Requires a pre-existing operating system, such as Windows, Linux, or macOS.
    - Guest operating systems run as processes within the host operating system.
    - Generally used for development, testing, or running VMs on personal computers rather
       than in enterprise environments.
    - Examples include VMware Workstation, Oracle VirtualBox, and Parallels Desktop.
<!--ID: 1721488489633-->
END

---

START
Basic
Pros of virtualization
Back:
- **security** : since the VM Manager controls and filters the activity of
	the guest, it can also **block harmful operations from being executed on the real host system**.
	Also, it can prevent the guest from accessing some resources, such as network interfaces or
	sensible devices.
	It can virtualize some resources from different physical ones. It is possible to:
	- **Share** : a single physical resource can be shared across different virtualized environments
	- **Aggregate** : simulate a bigger virtual resource by the union of multiple physical ones
	- **Emulate** : emulate a different hardware
	- **Isolate** : a physical resource can be isolated from the rest of the system for a safer execution environment

- **portable** , because it abstracts away the underlying hardware: inter-
	preted code runtimes, VM images stored as .ova, a Docker container.
	There are different types of virtualization:
	- **Full** virtualization: the VM Manager (VMM) hides to the Guest OS that is being virtualized,
	    and scans the instructions running non-critical instructions on the real hardware, while
	    emulating others via _Binary translation_ :
		**-** _Statically_ , converting all the code on the target architecture ahead-of-time
		**-** _Dinamically_ , translating code only when necessary; this way re-execution of instruc-
		    tions make the code faster (as in many languages such as in the JVM)
	- **Hardware assisted** virtualization, with Intel-VT or AMD-V, much more efficient because
	provided by the CPU instruction set: some sensitive instructions are called in user mode,
	while others are trapped and emulated
	- **Paravirtualization** ,on top of Hardware-assisted virtualization, but the Host OS must
	provide an intelligent compiler to replace the nonvirtualizable OS instructions by hyper-
	calls (KVM or Hyper-V do that)
<!--ID: 1721488489635-->
END

---

START
Basic
What autonomic computing is?
Back:
The goal of autonomic computing is to create self-managing computer systems capable of au-
tomatically carrying out tasks necessary for their operation, such as configuration, optimization,
healing, and protection, without human intervention.

The properties to reach autonomic computing are:

- Self- **Configuration** : systems can automatically configure themselves based on changes in
    their environment or workload
- Self- **Optimization** : systems continuously optimize their performance to achieve the best
    possible efficiency and resource utilization
- Self- **Healing** : systems detect and diagnose problems, then take corrective action to re-
    cover from failures or errors without human intervention
- Self- **Protection** : systems have built-in mechanisms to defend against security threats and
    adapt to changing security conditions autonomously

An example of _Self-Configuration_ can be such that a service automatically recognizes the
addition of a new component in a network and it’s ready to use.
<!--ID: 1721488489637-->
END

---

START
Basic
What is MAPE-K Cycle?
Back:
The MAPE-K cycle is a framework used in the context of autonomic computing and self-managing
systems to describe a _closed-loop control system_ for managing and improving system perfor-
mance.

1. **Monitor** : Collects data on system behavior and environment (health state, performance).
2. **Analyze** : Identifiespatterns, anomalies, andoptimizationopportunities(dataaggregation
    and prediction).
3. **Plan** : Formulates actions to address issues or optimize performance, putting the system
    in a desired state (ECA, goal based, utility function).
4. **Execute** : Execute the selected action to take (allocate resources, shutdown VM, ...).
5. **Knowledge** : Captures and utilizes system knowledge for continuous improvement.
<!--ID: 1721488489640-->
END

---

START
Basic
Tell the classification of categories of policies for an autonomic manager.
Back:
Classification of categories of policies for an Autonomic _Manager_. This way, we define high-
level objectives, making them actual actions on the system:

- **E** vent- **C** ondition- **A** ction (ECA) policies are the simplest ones, e.g. if response time of a Webserver > 2s, increase number of instances;
- **Goal** policies: we specify the goal to reach, but not explicitly _how_ to reach it - it’s like in
    Declarative programming in SQL where we say what we want but not how _(the planning)_.
    If a goal is impossible, what’s the best undesirable situation to be in?
- **Utility** function: given a state, return a value indicating _how much_ it is desirable - it is hard
    to define, because it may be multidimensional and requires a quantification of goodness
<!--ID: 1721488489641-->
END

---

START
Basic
Monitoring: what is? how? Kinds?
Back:
We must observe the system state in order to make decisions. System state can be directly
measured or inferred from existing properties (called _metrics_ ). The application may be required
to include some _sensors_ that essentially allow to collect some metrics necessary to reconstruct
the state.

Monitoring can be:
- **Passive** : observing without interfering with the system but from data already made avail-
    able from the system itself - such as reading logs
       **-** What to collect? What importance to give to each metric?
- **Active** : calling the system, such as sending pings, special HTTP requests, and so on -
    thereby generating a bit of overhead on the called system
       **-** How frequent to measure data?
       **-** Must reduce interference as much as possible, but still be accurate
<!--ID: 1721488489643-->
END

---

START
Basic
Describe the model driven approach
Back:
A model describes the state of the system and its evolution, including its requirements and the
goals to reach. The update of the model is done through the sensor data mentioned before.
Using this model, we can decide the best planning to decide system actions to take.
In case the model gets invalidated () we can fallback to ECA rules to repair the system.
The architecture of the system can be described with Graphs, or Queue networks (such as
describing the queues of messages in the application).
The actual technique to plan a strategy can be seen as an _Optimization problem_. Also we
can use Heuristics (things that are generally always considered to be true), and finally Reinforce-
ment Learning can be taken into account.

// AC Adoption Model Levels -> TODO
<!--ID: 1721488489645-->
END

---


START
Basic
Automation vs Autonomic Computing
Back:
Automation is related to the **E** xecute part of the MAPE-K cycle and the Self-* properties dis-
cussed in 3.1.

In fact, the goal of Autonomic Computing is having a system with _almost no_ human inter-
action, depending on the level of automation. On the other hand, _IT Automation_ has the goal
to **reduce** human interaction and costs, reducing human error, but still not removing human
interaction completely.

Examples of Autonomic Computing are ones where we _specify high-level objectives_ :

- Server consolidation, VM migration - objective to maximize resources usage
- Guarantee Service Level Agreements - SLA is a set of objectives to grant
- Manage software/hardware failures - This is an example of _self-healing_

On the other side, IT Automation are tasks that I need to perform, such as:
- Software updates
- Vulnerabilities or bugs fix to deploy
- Application components update and configuration
- Infrastructure nodes configuration
- CI/CD and backups
<!--ID: 1721488489646-->
END

---

START
Basic
What orchestration is?
Back:
Automating a series of individual tasks to work together as a process or workflow. We may
orchestrate on _containers_ , IT (virtual) infrastructure, services.

Container orchestration is related to the management **at runtime** of them:
- Deploy
- Run
- Maintenance (while running, not offline)
Typical **operations** we can perform with an orchestrator are:
- Resource limit control
- Scheduling
- Load balance across containers
- Health Check and Fault tolerance
- Auto-scaling

Kubernetes containers orchestration consists of several sub-tasks:
- Service discovery and load balancing
- Storage automatic bounding
- Automated rollouts and rollbacks if needed
- Secret and configuration management
- Self-healing of containers
- Automatic **bin packing** : fitting containers into physical nodes in order to maximize the
    usage of resources
Kubernetes has some fundamental concepts to know.
<!--ID: 1721488489648-->
END

---

START
Basic
How kubernetes work in short?
Back:
Kubernetes objects are persistent entities that represent the state of the cluster, describing applications, resources, and policies. Each object is a record of intent, with fields for the desired state (**spec**) and the actual state (**status**).

A Pod is the smallest deployable unit in Kubernetes, acting like a logical host and potentially including multiple containers that share network and storage resources. These containers run in a shared context, using Linux namespaces and cgroups.

Nodes are physical machines that run Kubernetes and execute Pods. They can self-register or be manually added. The state of a Node, visible through the Kubernetes API, includes readiness and issues like DiskPressure, MemoryPressure, PIDPressure, and NetworkUnavailable. Nodes also provide information about their total and allocable resources.

The Control Plane runs on a dedicated server or VM, managing the entire cluster. It includes the **kube-apiserver** (the frontend), **etcd** (a key-value store database), **kube-scheduler** (which schedules Pod execution), **kube-controller-manager** (ensuring nodes and jobs run correctly), and **cloud-controller-manager** (managing cloud provider interactions).

Each node runs several components, including the **kubelet**, which manages local pods based on instructions from the API Server, and the **kube-proxy**, which manages network connectivity.
<!--ID: 1721488489650-->
END

---

START
Basic
What are the key methods and considerations for implementing autoscaling in cloud and containerized environments, and how do AWS and Kubernetes differ in their approaches?
Back:
### Autoscaling
Autoscaling adjusts system resources automatically to meet demand. Vertical and horizontal scaling are possible, but horizontal scaling is preferred. Key components of autoscaling are defining _when_ to scale and _how_ to scale.

Types of Autoscaling Algorithms:
- **Threshold-based (Reactive):** Scale out when a metric (e.g., CPU load) exceeds a threshold; scale in when it falls below.
Set lower (L) and upper (U) bounds for metrics. Scale down if metric < L, scale up if metric > U. Utilization (ututut) is measured as the ratio of wanted to available resources. A conservative approach requires multiple violations of a threshold before scaling. Adaptive scaling adjusts the amount of resources based on utilization.

- **Model-based (Reactive):** Use mathematical models (e.g., ML models) to decide actions after a threshold is crossed.

- **Proactive:** Predict future metrics to scale preemptively.


### AWS vs. Kubernetes
AWS offers different autoscaling strategies:
- **Target Tracking:** Automatically adjusts resources to maintain a target metric value.
- **Simple Scaling:** Involves a cooldown period post-scaling.
- **Step Scaling:** Allows immediate scaling actions without a cooldown.

AWS scaling policies include change in capacity, exact capacity, and percent capacity. For example, scaling policies adjust resources based on CPU load metrics with specific percentage adjustments.

Kubernetes scales pods based on CPU load averaged over the last minute. This Horizontal Pod Autoscaling controller determines if additional pods are needed to handle the load.

### Adaptive Model-Driven Autoscaling

A proposed model-driven autoscaling approach can dynamically solve scaling issues using advanced algorithms.

### Online VM Auto-Scaling Algorithms

These algorithms determine the optimal number of VMs for application needs, addressing VM-to-PM (Virtual Machines to Physical Machines) allocation. The aim is to meet SLAs while minimizing physical machine usage.

### Shadow Routing Algorithm

The Shadow Routing Algorithm uses a two-tier queuing system to maintain a shadow queue and make routing and service decisions. It aims to maximize VM utilization by matching new applications to the best available VM type based on current specifications and availability.
<!--ID: 1721488489652-->
END

---



START
Basic
Cloud storage: What does atomicity means?
Back:
Multi-step operation (transaction) that should be completed without interruptions and **all-or-
nothing** :
- we do a _pre-commit_ to allocate resources and do preparatory actions;
- _commit-point_ do operations or abort the process;
- _post-commit_ do irreversible actions by writing on the only copy of an object; to do all these
    steps we keep a lot of _logs_ to reconstruct the state of the system in case of a failure to
    ensure consistency

Also,wecanhave **before-or-after** atomicity: itperformstheconcurrentoperationsinparallel,
but the final result must be the same as if the operations were executed serially; often used to
speed-up transactions in a database.
**Implementations** can be via special CPU instructions, or OS support:

- _Test-and-set_ : write to a memory location and get the old value
- _Compare-and-swap_ : compare contents of a memory location and modify the contents
    only if the old value is the provided one
- Locks, semaphores: create a _critical section_ and put sensitive code inside it
<!--ID: 1721488489654-->
END

---


START
Basic
Cloud storage: What does atomicity means?
Back:
A Storage model is the description of the layout of a data structure in physical storage, like a
Filesystem: it can be _cell storage_ (first type of model with simpler requirements: only before-
or-after atomicity, no failure recovery) or the newest _journal storage_

Using the **Cell storage** model, we logically see the storage as a set of cells of the same size,
where each one containsnbytes (block). It guarantees _Read-Write coherence_ , since we directly
apply the modification of the data in the cell. Still, we have no preparation of the resources to
write on, neither history of previous states.

On the other hand, the more evolved **Journal storage** model (Journaling filesystems), is a
construction upon cell storage, but adding Journaling and a Manager. Here, the first-class cit-
izen is an _object_ (like an entire file), not simply a single cell as in previous model. The _Journal_
keeps track of the history of the objects and the cells, keeping track of all operations. At the cost
of space required for this log, we gain more resilience to failure, the ability to recover and the
possibility to implement all-or-nothing atomicity, too.

END

---

START
Basic
Cloud storage: describe Google File System. How does it work?
Back:
Idea is to build an extremely large filesystem built from thousands of inexpensive commodities,
still with high performance and highly reliable, in a datacenter.

The **access model** of files in the cloud is **Append-only** , instead of writing to random loca-
tions. Also, many applications just do **Sequential reads** , instead of random ones. This approach
massively simplifies the process to guarantee our requirements.

Files are stored in _64MB chunks_ ,a big size, backed by a traditional Linux filesystem, and _repli-
cated on 3 sites_. The use of this big chunks improves the performances for reading big files, and
reduces the metadata needed to store it, also reducing disk fragmentation and the overhead
needed to fetch a single chunk (less chunks to get for a file of the same size).

Remember that a file may be from some GB to even a few TB!
<!--ID: 1721488489656-->
END

---

START
Basic
Cloud storage: GFS Cluster Architecture
Back:
We have a _Master node_ , that contains the metadata for the stored files and information on
where they are stored and replicated. It has a global overview of the cluster state. It updates
the information on update, having always the most up-to-date and consistent information.

To **recover from failures** , the Master keeps a log (journal) of the metadata changes, so that
it is able to rebuild it if failing. This log is replicated and operations are atomically executed. To
make the recovery as fast as possible, we save from time to time the snapshot of the current
state. This is the same logic as SQL databases^2

To **read a file** , the application contacts the Master, which will grant a lease to access the file
on a replica in some chunk server, then the application can directly contact it.

A **file creation** ishandledbytheMasternode, andwhenitcomesto **writing data** (inAppend
mode, since this is the design of GFS):
1. Application contacts the Master which replies with IDs of all chunk servers involved, grant-
    ing a lease only to the primary one
2. Application writes data to the primary chunk server
3. The primary sends writes to the secondaries, which will send ACKs to the primary
4. Finally, the primary ACKs the client application
<!--ID: 1721488489658-->
END

---

START
Basic
Cloud storage: what is HADOOP? How does it work?
Back:
Apache open source Java project, **built to support the Map-Reduce workflows**. As GFS, it is in
fact a meta filesystem that requires another simpler filesystem underneath to work.

The architecture is similar, too:
- A Master ( **NameNode** ) that handles the global state of files and metadata, controlling the
    access to files and logging changes in metadata, also check liveness of DataNodes and
    recover from failures - there can be a few replicas of NameNodes, not to have a single
    point of failure
- Slave nodes ( **DataNode** ) keep the actual data stored and connect to the NameNode for
    orchestration and data retrieval

Replica strategy is different: here we choose to keep **2** replicas in the same rack and only 1
in another physical machine. This still keeps 3 replicas, but has better performances (parallelize
physical disk reads, faster fallback in case of failures of a single disk).
The **write protocol** works in 3 main stages:
1. Pipeline set up:
2. Write pipeline stage:
3. Acknowledgment stage:
<!--ID: 1721488489660-->
END

---

START
Basic
Cloud storage: describe NoSQL
Back:
NoSQL databases are all kinds of databases that the structure of the data is not a relational SQL
(graphs, key-value, document-collection, ...).

The guarantee of **ACID** properties depend on the type of database and its implementations,
but they are more or less relaxed in favor of horizontal scaling.

Cloud applications require to perform **OLTP** (OnLine Transaction Processing) where they
need a huge amount of data in an almost real-time latency. Since having strong consistency, as
in SQL databases, cannot allow us to scale performances to meet these requirements, NoSQL
databases adopt **eventual consistency** , so that data can temporarely be inconsistent across all
its replicas.

Now we can do _Data Partitioning_ more easily, so horizontally scale.
<!--ID: 1721488489662-->
END

---

START
Basic
Cloud storage: describe bigtable
Back:
Developed by Google, to handle simple and flexible data model. A Bigtable is a sparse, dis-
tributed, persistent multidimensional sorted map. It is in fact 3-dimensional (rows×columns
×versions [Timestamps]).

Data is all into one table, with columns that are no more that simple strings. Any kind of data
can be stored, without a fixed structure as in a SQL table, since it is just an **uninterpreted array
of bytes**.

Some columns grouped into **families** and each column can have their own **key**. Families
have to be determined at the time of creating a table.

A whole table consists of a multitude of rows: these rows are lexicographically ordered and
partitioned into **tablets**. Each tablet is stored on a physical server.

Versions are established by the _Timestamp_ it receives. If timestamps are server-side gen-
erated, it is guaranteed to be unique; otherwise client-size timestamps have the guarantee to
be unique based on the application specific implementation. Of course, we need a pruning
system to define how and when to remove older versions.

In BigTable, we use the **SSTable** file format to store a table, and also it has some logs, all
inside the underlying GFS to manage these files.

The BigTable architecture is **Master-Slave** , similar to GFS. The slaves are the _Tablet_ servers.
Each Tablet server may have some _Tablets_ inside of them.

The split of a tablet inside multiple tablets, when it gets too large, is done by the Tablet
servers,nottheMaster. MasterisonlyresponsibleformanagingTabletservers(liveness,failures,
add new ones, _Balance Load_ across tablet server, and so on).

Altering the table schema is possible but must be very rare. Since this change must be prop-
agated to all children (Tablet servers) and only the Master knows the global state of the tablets
allocations, this propagation of the schema is a responsibility of the Master.

Basically, a **Tablet** is an index of the SSTables on the GFS. Splitting one Tablet does not di-
rectly mean that also the underlying SSTable blobs are split on GFS as well.
<!--ID: 1721488489664-->
END

---

START
Basic
SSTable format
Back:
This is the format of the blobs of the BigTable tables, written on disk running GFS.
SSTable = sequence of blocks + block index. To find a block, we do a binary search in the
index (kept in memory) and a seek + read on the block on the disk. We can also load entirely
SSTable in memory, for example if it’s accessed very frequently, but being sure to apply Writes
also immediately on disk in this case.
<!--ID: 1721488489666-->
END

---

START
Basic
Chubby: Google locks service
Back:
Its purpose is to allow clients to synchronize, but in a loosely-coupled distributed systems. This
_loosely-coupled_ characteristicmakesstandardalgorithmslikePaxostooheavytobeused,since
most of the distributed instances of the system won’t be interested at all in syncing.
Also, the applications are _already deployed_ , so we cannot modify the application (imagine
modifying the core code of BigTable, may become a messy pretty soon). The lock system is
based on **files** and directories on the system.
GFS uses Chubby to:

- lock to appoint a GFS master server (like in a Write request to a file)
- use it as a location to store small metadata


Also in BigTable that’s useful for:
- elect a master node, make sure that only one is active at a given time, and allow other
    nodes to identify it
- master discovers the child servers it is responsible for
<!--ID: 1721488489668-->
END

---

START
Basic
DynamoDB
Back:
Informally, "like paxos for distributed services but with databases, peer to peer, and data is memorized as long as the majority have it"

It is NoSQL (Key-Value) so it has an _Eventual consistency data store model_ , to improve per-
formance and availability. On the other hand, ACID SQL DBs have Consistency prioritized at
the cost of having poor availability and performance, which is the opposite choice that NoSQL
databases do in general.
A write request, according to this model, is successful if just a minimum subset of the nodes
can complete successfully this operation - not every node - and generally this isn 2 + 1, so that
we are able to reconstruct the real value since this is the majority of the copies.
The logic of Dynamo’s Data Replication is to have an **optimistic replication** , which may in-
troduce problems, since only the majority of the nodes need to actually have the data to make
the Write successful, there may be a conflict. This conflict can be solved at **read time** , to make
the Write operation _always possible_. The Writes have timestamps and other information to get
at read time the correct value of the "variable" in the datastore. The conflict can be **solved** , if
necessary (based on the application use-case), by the application itself: this makes the con-
sistency requirement optional and up to the final application, and also makes the DB service
much more efficient, without having to worry about it.
The nodes architecture here is **Peer-to-Peer** , without a Master since it’s not necessary, and
it makes it a more efficient service, without the bottleneck that a Master may introduce (as a
single point of failure, but also in terms of load). So, since it’s P2P, it can be heterogeneous, and
be deployed on multiple very different nodes without issues.
The system allows to interact with the data using get(key) (returning one or more objects,
in case of _conflicts_ ) and put(key, context, value)(the _Context_ is an opaque object that encap-
sulates all the necessary metadata to perform the write operation, in a transparent way to the
final application).
<!--ID: 1721488489671-->
END

---

START
Basic
Partitioning
Back:

Partitioning data automatically is crucial to be able to scale when data gets too big to manage
from a single server.
The load balancing is done **hashing** the Key value and keeping the modulus of the final hash
number, so that we can identify the Virtual Node, and then the responsible server.
This technique also limits the impact of the down of a server, which will only affect the keys
that Virtual Nodes was storing at that time.
<!--ID: 1721488489673-->
END

---

START
Basic
Replication
Back:

The idea is that the Physical server is responsible for replicating (3 times in total) the assigned
Virtual nodes.
It does so by replicating it to other 2 nodes, chosen in a clockwise order in the a circular array
shape.
<!--ID: 1721488489675-->
END

---

START
Basic
Data Versioning
Back:

Multiple concurrent requests are possible in this highly available, eventually consistent, dis-
tributed system.
The versioning algorithm is **Vector Clock** (seen in Distributed Systems), where we have a
counter for every node that is involved in the Write requests. This guarantees to always have
the notion of history of the changes in the versions. When aGetoperation comes, we return
to the client all the conflicting versions, and the client’s library will be responsible to do the
reconciliation - using the Vector Clock information available.
<!--ID: 1721488489677-->
END

---

START
Basic
S3 Object Storage
Back:

The objects are in Buckets, in a region.
Permissions handling is done by ACLs (file specific) or global rules to the entire bucket.
The R/W errors handling is done via theETag HTTP Headerin the response, containing the
MD5 of the file. If it does not match, an error occurred and the client must not use received
data.
The opposite is also possible: a client sends the hash in the API request (HTTP PUT), so that
the server can double-check that it is not corrupted.
A write may fail: the client can retry after a while, maybe the service is temporarily unavail-
able.
<!--ID: 1721488489678-->
END

---

START
Basic
Consistency Models
Back:
For PUT and DELETE requests, a strong Read-after-Write consistency is guaranteed. Read-after-
write consistency tightens things up a bit, guaranteeing immediate visibility of new data to all
clients. With read-after-write consistency, a newly created object or file or table row will im-
mediately be visible, without any delays. That means that **PUT is atomic** and the client gets a
successful response only after the data is actually stored and modified in all the relevant places.

Also, for ACLs and object metadata (including tags), we get READ Strong Consistency.
The issue appears when there are multiple PUTs in concurrency with another READ, and
in this case corrupted data may exist and the response will never error out, but may receive
unexpected values (see figures 7 and 8). The requests are ordered by the timestamp of which
the server receives the request, not by the clients. The latest timestamped request wins.
Since there is no support for locking mechanisms, you cannot do a transaction, modifying
multiple keys at the same time.

The **bucket configurations** have a (very) eventual consistency mechanism. When enabling
the bucket versioning (which is an option we really want to be enabled before doing something
disruptive to our data) it is suggested to wait 15 minutes, due to the time necessary for the
propagation and replication of previous rules.
<!--ID: 1721488489680-->
END

---


START
Basic
Misc questions
Back:
1. Big table storage, structure and how datas are indexed
2. Automatiom properties
3. Container technologies
4. How does a client write in hadoop filesystem
5. Services provided by the cloud broker
6. three ways of scaling in microservices
7. do container share resources in pods?

AND

1. Which protocol use hdfs and how does it works (architecture)
2. Hdfs vs Gfs
3. Virtualization (which are the main Three components)
4. How the Hypervisor communicate/allocate additional resources
<!--ID: 1721488489682-->
END