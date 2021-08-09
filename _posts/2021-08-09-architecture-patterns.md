---
layout: post
title: "Architecture Patterns"
date: 2021-08-09
tags: design
---

## Software Architecture
* The organization of the system;
* Different components vis-à-vis their functions;
* How the components interact with each other.
    
## How to choose
* The software is easy to maintain;
* Business stakeholders can understand it easily;
* Good software architectures are usable over the long-term;
* Such architecture patterns are flexible, adaptable, and extensible;
* It should facilitate scalability;
* The team can easily add features, moreover, the system performance doesn’t diminish due to this;
* There is no repetition of the code;
* The system can be refactored easily.
    
## 1. Layered pattern

### About
* Most common architecture pattern
* N-tier architecture
* Divided into units - layers
* Usualy four:
  * Presentation layer (handles user interface)
  * Application layer
  * Business Logic layer
  * Data Access layer 

### Usage
* Usually used in building general desktop applications, relatively simple web apps.
* Good choice fo sitautions with very tight budget and time constraints.

### Pros
* Maintaining the software is easy since the tiers are segregated.
* Development teams find it easy to manage the software infrastructure, therefore, it’s easy to develop large-scale web and cloud-hosted apps.
* lower layer can be used by different higher layers.
* Layers make standartization easier.

### Cons
* Not universally aplicable
* The code can become too large.
* A considerable part of the code only passes data between layers instead of executing any business logic, which can adversely impact performance.
* Certain layers may have to be skipped in certain situations.
    
## 2. Client-server pattern

### About
* Main components - client (service requester) and server (service provider)
* Communicate over a network on separate hardware

### Usage
* Online applications

### Pros
* Ease of modelling a set of services
* Clients access data from a server using authorized access, which improves the sharing of data.
* Accessing a service is via a ‘user interface’ (UI), therefore, there’s no need to run terminal sessions or command prompts.
* Client-server applications can be built irrespective of the platform or technology stack.
* This is a distributed model with specific responsibilities for each component, which makes maintenance easier.

### Cons
* Server can be a performance bottleneck and a single point of failure
* Complex and costly to change decisions where to locate the functionality - client or server

## 3. Master-slave pattern

### About
* Two components:
  * Master - distributes the work among identical slave components and computes a final result from the results which slaves return.
  * Slaves - work in parallel.

### Usage
* Useful when clients make multiple instances of the same request which need simultaneous handling. 
* Database replications, where master database is regarded as the authoritative source and slave databases are synchronized to it.
* Monitoring applications used in electrical energy systems.

### Pros
* The accuracy in which the execution of a service is delegated to different slaves with different implementations.
* Applications read from slaves without any impact on the master.
* Taking a slave offline and the later synchronization with the master requires no downtime.

### Cons
* Can be applied only to a problem that can be decomposed.
* This pattern doesn’t support automated fail-over systems since a slave needs to be manually promoted to a master if the original master fails.
* Writing data is possible in the master only.
* Failure of a master typically requires downtime and restart, moreover, data loss can happen in such cases.
* The latency in master-slave communication could be a problem.
* Slaves are isolated.

## 4. Pipe-filter pattern

### About
* Single event triggers a sequence of processing steps each performing a specific function
* Pipes and filters divides a larger processing task into a sequence of smaller independent processing steps (filters) connected by channels (pipes)

### Usage
* Often used in compilers
* Workflows in bioinformatics.

### Pros
* There are repetitive steps such as reading the source code, parsing, generating code, etc. These can be easily organized as separate filters.
* Each filter can perform its’ processing in parallel if the data input is arranged as streams using pipes - concurrent processing.
* It’s a resilient model since the pipeline can reschedule the work and assign to another instance of that filter.
* Easy to add filters.

### Cons
* This pattern is complex.
* Data loss between filters is possible in case of failures unless you use a reliable infrastructure.
* Efficiency is limited by the slowest filter process.
* Data transformation overhead when moving from one process to another.

## 5. Broker pattern

### About
* Distributed systems with decoupled components which can interact with each other by remote service invocations
* Broker component is responsible for the coordination of communication among coponents
* Server publishes their capabilities to a broker
* Clients request a service from a broker
* Broker redirects a client to a suitable service from its registry

### Usage
* Provision of different services independent of each other.
* Message broker software as ActiveNQ, Kafka, RabbitMQ, JBoss

### Pros
* Allows dynamic change, addition, deletion and relocation of objects and it makes distribution transparent to the developer.
* Developers face no constraints due to the distributed environment, they simply use a broker.
* This pattern helps using object-oriented technology in a distributed environment.

### Cons
* Requires standardization of service descriptions.

## 6. Peer-to-peer pattern

### About
* Individual components (peers).
* May function both as client (requesting services from other peers) and server (providing services to other peers).
* Peer may act as client, server or both and can change its role dynamically in time.
* Supports decentralized computing.

### Usage
* File-sharing networks.
* Multimedia protocols P2PTV, PDTV.
* Cryptocurrency.

### Pros
* Highly robust in the failure of any given node.
* Highly scalable in terms of resources and computing power.

### Cons
* No guarantee about quality of service as nodes cooperate voluntarily.
* Security is difficult to guarantee.
* System performance depends on the number of nodes.

## 7. Event-bus pattern

### About
* Distributed system that can service asynchronously arriving messages associated with high volume of events.
* Four major components:
  * Event source - publish messages to particular channel on an event bus.
  * Event listener - subscribe to particular channels.
  * Channel.
  * Event bus.

### Usage
* Android development, e-commerce applications and notification services.

### Pros
* This pattern helps developers handle complexity.
* New publishers, subscribers and connections can be added easily.
* This is an extensible architecture, new functionalities will only require a new type of events.
* Effective for highly distributed applications.

### Cons
* Scalability might be a problem for this pattern as all messages travel through the same bus.
* Testing of interdependent components is an elaborate process.
* If different components handle the same event require complex treatment to error-handling.
* Some amount of messaging overhead is typical of this pattern.

## 8. Model-view-controller pattern

### About
* Application functionality separated into three components.
  * Model: Core functionality and data.
  * View: Displays information to the user - more than one view can be defined.
  * Controller: Handles the input from the user.

### Usage
* Web frameworks (Django and Rails).

### Pros
* Using this model expedites the development.
* Development teams can present multiple views to users.
* Changes to the UI is common in web applications, however, the MVC pattern doesn’t need changes for it.
* The model doesn’t format data before presenting to users, therefore, you can use this pattern with any interface.

### Cons
* With this pattern, the code has new layers, making it harder to navigate the code.
* There is typically a learning curve for this pattern, and developers need to know multiple technologies.
* Increases complexity. May lead to many unecessary updates for user actions.

## 9. Blackboard pattern

### About
* Useful for problems with no deterministic solution strategies are known
* Three main components:
  * Blackboard - structured global memory containing objects from the solution space
  * Knowledge Source - specialized modules with thei own representation
  * Controller - selects, configures and executes modules
* Flow:
  * Data Input Stream -> Blackboard
  * Blackboard Notifies Controller
  * Contoller Enrolls Knowledge Source
  * Knowledge Source Updates Blackboard (with new data objects)
* Components look for particular data on the blackboard and finds these by pattern matching with existing knowledge source

### Usage
* Speech recognition, protein structure identification and sonar signals interpretation

### Pros
* Extending the structure of the data space is easy.
* Easy to add new applications.
* The pattern facilitates experiments.
* You can reuse the knowledge resources like algorithms.

### Cons
* Modifying the structure of the data space is hard as all applications are affected.
* May need synchronization and access control.
* An intermediate arrangement. Ultimately, you will need to arrive at a suitable architecture pattern, however, you don’t have certainty that you will find the right answer.
* All communication within the system happens via the blackboard, therefore, the application can’t handle parallel processing.
* Testing can be hard.

## 10. Interpreter pattern

### About
* You implement an interface that aids in interpreting given contexts in a programming language.
* The pattern uses a hierarchy of expressions.
* It also uses a tree structure, which contains the expressions.
* A parser, external to the pattern, generates the tree structure for evaluating the expressions.

### Usage
* Grammar of programming languages

### Pros
* Highly dynamic behavior is possible.
* Good for end user programability.
* Enhances flexibility as replacing interpeted program is easy.

### Cons
* Performance may be an issue as interpreted language is slower.

## 11. Microservices pattern

### About
* Solves monolit too big problem
* Each service is independently deployable and scalable and has its own API boundary
* Different services can be written in different program languages, manage their own databases and developed by different teams
* Suitable for use cases with extensive data pipeline

### Usage
* Works best for teams looking to re-write their monolithic applications to a more sustainable pattern.
* Works best for applications with immense and rapidly growing data systems.

### Pros
* Microservices are independently deployable and allow for more team autonomy.
* Microservices are independently scalable.
* Microservices reduce downtime through fault isolation.
* The smaller codebase enables teams to more easily understand the code, making it simpler to maintain.

### Cons
* Microservices create different types of complexity than monolithic applications for development teams.
* Interface control is even more critical.
* Up-front costs may be higher with microservices.

## 12. Microkernel pattern

### About
* Separated into a minimal functional core and extended functionality (plug-ins).
* Core system consists of general business logic with no custom code for exceptional cases or complex conditional processes.
* Plug-ins are a set of independent components that assist the core by providing specialized processing additional features via custom code.
* Microkernel serves as a socket for these plug-ins to extend its functionality and power.

### Usage
* Applications that require or are concerned with the separation between low-level functionalities and higher-level functionalities.
* Since the microkernel pattern provides extensibility, scalability, and portability, it is best used for enterprise applications.
* It is best suited for development teams that are spread out.

### Pros
* Microkernel architecture is small and isolated therefore it can function better.
* Microkernels are secure because only those components are included that disrupt the functionality of the system otherwise.
* The expansion of the system is more accessible, so it can be added to the system application without disturbing the Kernel.
* Microkernels are modular, and the different modules can be replaced, reloaded, modified without even touching the Kernel.
* Fewer system crashes when compared with monolithic systems.
* Microkernel interface helps you to enforce a more modular system structure.
* Without recompiling, add new features
* Server malfunction is also isolated as any other user program's malfunction.
* Microkernel system is flexible, so different strategies and APIs, implemented by different servers, which can coexist in the system.
* Increased security and stability will result in a decreased amount of code which runs on kernel mode 

### Cons
* Providing services in a microkernel system are expensive compared to the normal monolithic system.
* Context switch or a function call needed when the drivers are implemented as procedures or processes, respectively.
* The performance of a microkernel system can be indifferent and may lead to some problems. 

## 13. Space-Based pattern

### About
* Handles the case of many concurrent users when the database reaches its peak capability.
* A tuple space is an implementation of the associative memory paradigm for parallel/distributed computing. It provides a repository of tuples that can be accessed concurrently.
* Components:
  * Processing Unit (PU) The Processing Unit typically contains the application modules, along with an in-memory data grid and an optional asynchronous persistent store for failover. It also contains a replication engine that is used by the virtualized middleware to replicate data changes made by one processing unit to other active PUs.
  * Messaging Grid The messaging grid, manages input request and session information. When a request comes into the virtualized middleware component, the messaging-grid component determines which active processing components are available to receive the request and forwards the request to one of those processing units.
  * Data Grid The data-grid component is perhaps the most important and crucial component in this pattern. The data grid interacts with the data replication engine in each processing unit to manage the data replication between processing units when data updates occur.
  * Processing Grid The processing grid, is an optional component within the virtualized middleware that manages distributed request processing when there are multiple processing units, each handling a portion of the application. It mediates and orchestrates the request between those two processing units.
  * Deployment Manager The deployment-manager component manages the dynamic startup and shutdown of processing units based on load conditions. This component continually monitors response times and user loads, and starts up new processing units when load increases, and shuts down processing units when the load decreases.

### Usage
* For applications and software systems that work under a heavy load of users that access or write to the database concurrently.
* For applications that need to address and solve scalability and concurrency issues.
* It is best suited for e-commerce or social website development.

### Pros
* Good architecture choice for smaller web-based applications with variable load.
* Makes straightforward to address Non Functional Requirements (NFRs) such as near-linear scalability, high availability, low latency, and high throughput. 

### Cons
* Complex and expensive pattern to implement.
* Not well suited for traditional large-scale relational database applications with large amounts of operational data. 


## References
* <https://en.wikipedia.org/wiki/Architectural_pattern>
* [10 Common Software Architectural Patterns in a nutshell](https://towardsdatascience.com/10-common-software-architectural-patterns-in-a-nutshell-a0b47a1e9013)
* [10 Most Popular Software Architectural Patterns](https://nix-united.com/blog/10-common-software-architectural-patterns-part-1/)
* [5 Common Software Architecture Patterns and When To Use Them](https://blog.crowdbotics.com/5-common-software-architecture-patterns-and-when-to-use-them/)
* [Space-Based Architecture](https://www.slideshare.net/SureshPatidar2/spacebased-architecture)
* [Microkernel in Operating System: Architecture, Advantages](https://www.guru99.com/microkernel-in-operating-systems.html)
* [Microservices Advantages and Disadvantages: Everything You Need to Know](https://solace.com/blog/microservices-advantages-and-disadvantages/)
