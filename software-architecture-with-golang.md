# Software Architecture in Golang

Desing and architect highly sacalable and robust application using Go

By Joytiwswarup Raiturkar


## Chapter 1 Building Big with Go

This chapter explores:
* what is software architecture?
* what are some basic rules and concerns that software architects should keep in mind?
* An introduction of some of the common architectures used.
* A deep explanation of Microservice architecture.
* Introduction to Golang(Skipped)

### What is architecture

Architecture is the shape given to a system by those who build it and shape means:

**Components, Their arrangments and how they communicate** 

Incontrast of architecture, desing often refers to structures an low-level decisions but had important effects on architecture.

In other words architecture is dividing a software to components that *has a specific concern and role plus well defined interfaces and responsibilities* to **manage complexities**

The two key **metrics of assesing component division** are:

* Cohesion: How focused is the components task is. (The more the better)
* Coupling: How dependent components are from each other. (The less the better)

There are many common architectural paradigms like MVC, Microservice, Layering, Actor model, Communicating Sequential Processes and so on. Each have different focueses, advantages and disadvantages.

The key is to have a logical separation of the system so that, when code needs to be written, developers have crisp ideas on what goes where.

### The Architect's role

***The primary responsibility of the architect is
to define a blueprint for what needs to be built and ensure that the rest of the team has
sufficient details to get the job done.***

This is not possible without getting our hands dirty and engage in low-level (and or coding).

In more details the architect should:

**1. Clarify requirements**

1. Funcitonal requirments: The PMs and business owners domain and concerns.
2. Non-Functional requirements: The underlying system requirments like fast software. The non-functional requirements need to be *specific,
measurable,
achievable,
and testable.*

**2.Defining key engineering principles**

Generic guidelines or principles, along with the high-level design, help the team to
make decisions at every stage.

* High-level design: A blue prints of components.
* Code quality attributes: Namings, test coverage, ...
* CI/CD (Really in architecture????)
* A/B testing (Again is this decision that high level and important that it effects every architecture? I don't think so!)

**3. Technology selection**

This comes after the part of reaching a blue print and component division.

**4. Leadership**

The architect should take ownership of the architecture and design meaning:

* Be a leader and not micro manage (Sell the design, not force! e.g Asking developers hard questions)
* Ensure the system being built is compatible with the design
* Coach and mentor developers


### Microservices

The basic concept of a microservice is simple—it's a simple, standalone application that does one thing only and does that one thing well.

The goal is to retain the **_simplicity, isolation, and productivity_** for a very large and complex system.

The book briefly talks about challenges of microservices like:

1. Cost of infrustructure
2. Development complexity for developers
3. Lack of local reasoning for exploring and investigating features and code (some parts of the logic is delivered to another system. This leads to harder tracing of bugs.)

### Go

Some tips and reminders about go syntax, features and phlosophies:

* Receivers can either be pointers (reference) or non-pointers (value).
Pointer references are useful in the same way as normal pass-by-reference
variables, should you want to modify struct, or if the size of struct is
large, and so on. In the previous example of Area(), the c Circle
receiver is passed by value. If we passed it as c * Circle, it would be
pass by reference.

* In Go, code is binned into packages. These packages provide a namespaces for code.


* Go uses a variant of CSP with first-class channels.

  Communicating Sequential Processes (CSP) is a formal language for describing patterns of interaction in concurrent systems.

  CSP promotes the message-passing paradigm of communication, as compared to the shared memory and locks paradigm for communication.


* The Go way of object-orientation is : composition over inheritance.

  For polymorphic behavior, Go uses interfaces and duck typing: "If it looks like a duck and quacks like a duck, it's a duck."

  Duck typing implies that any class that has all of the methods that an interfaces advertises can be said to implement the said interface.


At the end of this chapter writer suggests reading  *"Clean Architecture: A Craftsman's Guide to Software Structure and Design by Robert C.
Martin"* for  a deeper understanding of software architecture.  


## Chapter 2: Packaging Code

This chapters talk about the organization of code in the two levels of:

1. Object-orientation in Go
2. Packages, dependencies and ...


### Contracts

A software contract is a formalized documentation of an interaction with a software
component. Such as *interfaces, APIs and protocols*

Things that they should have:
* Change rarely
* Versioned and backward compatible(as much as possible)
* Include service level agreements(SLAs)

### Object Orientation in Go

Object orientation helps hide the implementation of behaviour behind a similar interface (not necessary the *interface* we know in code but in a more genral way.) and keeping a healthy **Contract**.

Inheritance is feature to reduce code complexity and package similar behaviour into a group under a common interface (Parent).

Inheritance, though useful, has its pitfalls:

*  Often leads to a hierarchy of classes, and sometimes the behavior of the final object is spread across the hierarchy

* Super classes can often be fragile, because one little change to a superclass can ripple out and affect many other places 

Inheritance is one type of object orientaiton and an alternative is **composition**.

- Inhertinace = an **_is a_** relationship

- Composition = a **_has a_** relationship

Compositions has this two parts that help create the smae advantages of the inheritance:

* Classes implement an interface—which is the contract the base class offers.
* Functionality reuse happens through having references to objects, rather than
deriving from classes.

The book states that:

`Building objects and references through compositions allows you to delay the
creation of objects until and unless they are needed`

But to be fare this is also  achivable in an inheritance world (lazy objects). Plus one of the (or maybe the only thing) the book has to say against inheritance is the scattering logic and behaviour across different classes while this is also the case in composition as well where the different components implement the scattered behaviour.

**TIP**

One uses pointer recievers in the two following senarios:
1. Wanting to actually modify the reciever.
2. The struct is very large and a deep copy(Which is used every time a method with non-pointer reciever is called) is expensive.

**TIP**

Slices and maps act as references, so even passing them as value will allow mutation of the objects.


#### Polymorphism

Go enables polymorphism by **interface**s

#### Embedding

Embedding is a mechanism to allow the ability to borrow pieces from different structs and interfaces. It is the equivalent of multiple inheritance with non-virtual members.

Let's call Base, struct embedded into a Derived struct. Like normal (public/protected) subclassing, the fields and methods of the Base class are directly available in the Derived struct. Internally, a hidden/anonymous field is created with the name of the base struct.

Base fields and methods can be shadowed, if redefined in the derived class. Once shadowed, the only way to access the base member is to use the hidden field named as the base-struct-name.


Because it is like the multi inheritance, the **_dimond of death_** problem is possible and is resolved by the compile errors when this ambiguity occures.


### Packaging and modules

Here the book is very out of touch from the latest trends of doing things(go mod) and talks about workspaces!

Some good points are:

Important thing when writing internal modules as common code between prijects are:
* The configuration for the code should be externalized
* This code should as far as possible, not handle errors on its own. It should translate library events into something meaningful related to the contract and emit them


Book refers to **_table driven tests_** and **_subtest_** to run them concurrrently.


--- 

And finally a good gneral role of thumb:


**Every technique/recommendation has a context, and when the recommendation is applied blindly, it can lead to developer frustration and, ultimately, lack of quality.**

## Chapter 3: Design Patterns

A design pattern is a description of a problem and a template of how to solve it.

Design patterns can be roughly categorized into three areas:
* Creational
* Structural
* Behavioral

Two important things to keep in mind of each class and component are:
* Responsibility assignment
* Dependency management


**Once for all: SOLID**

- **S**ingle responsibility principle: One class should have one, and only one, responsibility.
- **O**pen-Closed principle: You should be able to extend a class's behavior without modifying it.
- **L**iskuv Substitution principle: The interface should be able to suffice for all structs that implement that interface
- **I**nterface Segrigation principle: Many client-specific interfaces are better than one general-purpose interface.
- **D**ependency inversion principle: Depend on abstractions, not on concretions.


### Creational Design Patterns

* **Factory method**: Simple helper method to create objects
* **Builder**: When some logic is needed in creation of the objects
* **Abstract factory**: When we want to create a group of related objects with different variations  
* **Singleton**: Anti-pattern do not use (Introduces a global variable to the system).


### Structural Design Patterns
In software engineering, structural design patterns help delineate **_clean relationships_**
between objects and simplify design.

* **Adaptor**: An adaptor between a client that uses an interface and an Adaptee with an old or incompatible interface.
* **Bridge**: ??
* **Composite**
* **Decorator**
* **Proxy**: A proxy is essentially a class functioning as an interface to something else.
* **Facade**: Simplifies multiple interfaces into a simple one

### Behavioural Design Patterns

Behavioral design patterns are design patterns that identify communication patterns
among objects and provide solution templates for specific situations.

* **Command**: When an object is used to represent
a request (or actions) and encapsulate all information needed to process the same.
* **Chain of Responsibility**: ??
* **Mediator**: ?? difference with adaptor?
* **Memento**: capturing and storing the current state of an object so that it
can be restored later on in a smooth manner(Undo)
* **Observer**: one entity (subject) with state and several others (observers)
that are interested in that state
* **Visitor**: we want to do different things with elements (nodes) of an aggregate (array, tree, list, and so on).
* **Strategy**: allow the user to change the algorithm used
without changing the rest of the code. This is done with encapsulating the input and output of the algorithms into an interface.
* **Template method**: A variation of the strategy pattern where the algorithm is broken to some steps and the steps are implemented differently
* **State**: Change behaviour based on different state of an object.


## Chapter 4: Scaling Applications

Enabling propper(efficient) reactions to the changing pace of workload in a matter that hold up to the SLAs.

Scalability depends on the following (and more):
* Algorithems
* DataStructures
* Threading model
* Local state


Another three important matters descused in this chapters are:
* Bottlenecks
* Different options on how systems can be scaled
* Scaling deployments

### Algorithems

Book talks about space and time complexity. And then talks about some general algorithms.

#### Distributed Algorithems

Some conditions make a problem hard to solve by reaching efficiency on algorithem alone. One must use the advantages deviding your workload on multiple machines. Some of these conditions are:

**Sometimes, the dataset is so large that it cannot fit into the memory or disk of a single
machine**

Developing this is quite complex and has some tricky parts:
* Automatic parallelization
* Communication and coordination
* Distribution
* Optimization for network and disk access

**Concept of Google's ReduceMap is introduced but I could ont capture the idea in the first read**



### DataStructures

Each action on different data structures have different time order. E.g: Worst time of binary search in BST vs Red/Black tree.
This can predict the performnace impact of operations when loading data

#### Probablistic data structures


These algorithems are best when the exact value for the query is not important but query is  for a huge number of elements and is some aggregated query(count, min, max ...). Example:
* **Reservoir sampling is an algorithm/data structure that enables these types of queries.**
* **An alternative data structure is called count-min sketch**
* (Personal take): **Bloom Filter**


The way of storing data on database effect scalability:
* complexity modeling of algorithms and data structures mentioned
previously, having a large number of elements may make searching for a
particular element inefficient. (Like queries without indexes in most DBs)
* There are a lot of concurrent updates of the database. Typically, most databases
err on the side of safety. This means some clients are locked while updates or
reads are happening for another client.

### Scalibility Bottlenecks
Scalability bottlenecks are those system aspects that serialize (or choke) parallel
operations.

To demonstrate scalability bottlenecks and their solution two examples are given:
* **C10K Problem**: Old web servers could not handle more than 10k concurrent conections. Solution: **eventing model**

* **The Thundering Herd problem**



### Personal Idea
To use a bloom filter thingy for each complex query and save them in a persistance way. Each event passes these filters and updates them and aat the same time tells if this filter satisfies their request.


