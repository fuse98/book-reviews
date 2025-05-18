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
