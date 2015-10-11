#SWEN90007 Software Design and Architecture

# Week 1 - Lecture 1

### Enterprise System

**Common properties of enterprise system**

* Persistent data
* A lot of data
* Concurrent access
* Many user interfaces
* Build on business logic
* Integrate with other enterprise systems

### Architecture

A software architecture is a high-level view of a software system’s components, how those components behave, how they relate to each other, and how they relate to their environment, for the purpose of achieving their stated functionality.


# Week 1 - Lecture 2


### Principle

**SOLID Principle**

* Single Responsibility Principle
* Open Closed Principle
* Liskov Substitution Principle
* Interface Segregation Principle

###Patterns

* template solution
* not invented but discovered
* communication device

###Layer

**Three-layer Architecture**

* Presentation layer
* Domain layer
* Data source layer

**Pros**
	
* Understandability
* Substitution
* re-use
	
**Cons**
	
* Change
* Performance

###Transaction

**ACID property**

* Atomicity
* Consistency
* Isolation
* Durability

## Week 2 - Lecture 3

### Web Presentation Patterns

* Model View Controller (MVC)
* Model View Presenter (MVP)

### Input Controller

**Page Controller**

* Each page has its own controller
	* e.g extract information from a POST control
	* decide which domain layer to sent it to

**Pros**

* Ease of understanding
* Simplicity
* One to one mapping


**Cons**

* Duplication of logic
* Complex logic in the controller
* Extensibility: less extensible

**Front Controller**

* Front command implements generic code

**Pros**

* less redundant code
* gain flexibility
* change easier

**Cons**

* Dse
* lose flaxibility

###View

**Template view**

* dynamic html is hard to code

**Pros**

* Simple

**Cons**

* Reduced maintainability
* Promotes bad design practises
* Challenging to test

* mixed code in html
	* low testability
	* low mantainability 

**Transform view**

* separate data from presentation
	* e.g XSLT or XML

**Pros**

* Portability
* Encapsulation
* Improved Testability
* 
* multiple views


**Cons**

* Programming Complexity

* Overload
* loos kind of gross

#Week 2 - Lecture 4
	
**Two Step View**

**Step 1:** domain oriented format -> presentation format

**Step 2:** presentation format -> Html

**Pros**

* output formats
* maintainability(change)

**Cons**

* Overhead
* Implementation complesity

###Application Controller

* Centralised application flow

Pro


Cons 
complex for simple flow(overhead)

##Sessions

Three solutions

* Client
* Server
* Database

###Client

Store session safe locally ->send back forth

**Pros**

* scale 
* server clustering

**Cons**

* security!
* lose information on concurrent data
* message scales
* dependent client system

###Server

Store session in memory or dy
each session has a session ID

**Pros**

**Cons**

* clustering
* failover
* memory /disk

###Database

Server side but in a database


## Week 3 - Chapter 2

##Domain Layer

###Transaction script

* Collocation where each script handles one "requirement"
* CRUD
* scripts should not interrupt each other

####Pros

* Few business rule (Simplicity)
* Transaction boundaries are clear
* one-to-one mapping

####Cons

* not much re-usability
* refactoring
* scale(Scalability)
* Duplication

### Domain logic

Object model that contains data and behaviour (rules)

* object: business object
* method: business rule

#### Pros

* distributed implementation
* re-use (re-usability)
* managing domain complexity

#### Cons

* complexity
* overhead

###Comparison

####Transaction script

* Single rules
* unlikely to change

####Domain logic

* experience in domain modelling
* likely to change
* non-trivial business rules

### Table module pattern

Blend domain logic and transaction script

* One object per table
* Tie behaviour to table instance

####Pros

* simple mapping(Simplicity)
* less duplication


####Cons

* Scalability
* more coupled => maintainability

##Week 3

### Service Layer

* boundary for the application
* lay on top of the domain layer

#### Domain Fasade

#### its own layer (Operation script)

* domain-specific behaviour
* application-specific behaviour

####Pros

* Single entry-point
* one-to-one mapping(Maintainability)
* Customisable(reusable)
* Extensible
* Multiple clients

####Cons

* Complexity
* Operation grouping (non-trivial)

##Week 4-1 - Chapter 3

## Data-source layer -- Architecture Design

###Object-relational Mapping(ORM)

* architectural patterns
	
	how the domain layer and data-source layer interact with each other
	
* behavioural patterns

	how data is loaded from and stored into the underlying database
	
* structural patterns

	how the domain model can be mapped to tables in the database

###Table data gateway

* single object per table

####Pros

* Precise/simple mapping
* Compatibility(table module)

####Cons

* RecordSet/ResultSet(Incompatibility(domain model))

###Row data gateway

* single object per row(that we have queried)
	* tie code to this

####Pros

* Type safely
* Simplifies domain layer -> transaction script share code in gateway
* Precise mapping

####Cons

* Boiler plate code
* Database coupling
* Incompatibility(domain model)

###Active record

* row data gateway + domain logic

####Pros

* high cohesion
* + all row data gateway

####Cons

* combine business logic in data source logic(tight coupling)

###Data mapper

* set of mapper that move objects between two layer

####Pros

* loose coupling
* type safety
* separation of concerns

####Cons

* one change => three change (complexity)
	* instance of mediator 

###Comparison

Table data mapping |	one-to-one mapping

Run data mapping	  | one-to-one mapping

Active record

##Week 4-2 - Chapter 4

##Data source - behavioural patterns

How to efficiently load and store 

* **Concurrency**
* **Performance:** load large collection, change some, write back

###Unit of work

####Four lists

* new
* clean
* dirty
* deleted

####Pros

* Simple
* Efficiency

####Cons

* Forgetfulness
* cannot transfer accuss threads
* Developer know how to get object

###Identity map

Due to prevent routes being duplicated across objects

* in memory map for database ID to or in memory object

## Week 5-1 Chapter 5

###Lazy load

## Week 5-2 Chapter 5

### Embedded value

map on class field to a table of end class

### Single table inheritance

* type
* null values

####Cons

* Simplicity
* 

### Class table inheritance

* maps attribute to table
* each instance over multiple table

### Concrete table inheritance

* map abstract attributes to all table
* unique ids across table

##Week 6 - Chapter 8

##Concurrency

* Multiple patterns
* Problems
	* Inconstant read
	* Interference or data race 
	* Deadlock

### AA

#### transactianal resource e.g.DBMS

* transactions:
	* request tranaction
	* long transaction
	* late transaction

#### Aims

* maintaining integraty
* supportory liveness 

### Optimistic offline lock

### Pessimistic offline lock

long transaction pattern

####Pros

* No work/data lost

####Cons

* Low lieness

##Week 7-1 - Chapter 11

##Performance

###when ?

* requirements performance goal
* design
* testing (performance)
* implementation
* deployment

###Bell's principle

###Pipelining

* latency: amount of time to execute a task
* throughput: amount of tasks estimate a given time(bandwidth)

###Caching

Temporary storage of data in a faster 


##Week 9-1 - Chapter 12

###Parterns

####File Transfer

###File Transfer

Using files to transfer information

####Pros

* Simple

####Cons

* Inefficient (File I/O)
* Timing
* Synchronisation
* File Format(Format Incompatibility)

###Shared database

Application read/write to a shared database and can use as a communication mechanism

####Pros

* Transaction
* Data consistancy
* Timeliness

####Cons

* Performance overhead
* Couples systems via/to the database
* not support in some application(Implementation complexity)

###Remote Procedure Invocation

Use remote procedure calls, to transfer information

####Pros

* Synchronous
* functionality sharing
* encapsulation

####Cons

* Performance overhead
* highly coupled
* Synchronous

###Messaging

Use send/receive message to share information
generalisation at RPI


##Week 10-1 - Chapter 13
 
##Messaging

* Channels: 
* Messages: packet of data
* Router: may go through serval channels
* Meesage Translator: Reformat messages.
* Endpoint: Interfacing between message system. 


###Chanel Type

Application use preditec message 

####Design decision

* One-to-one vs one-to-many
* dealing with undeliverable message
* integration of non-messaging clients.
* messaging as a communication backbone.

###One to one channel(Point-to-point channel)

one sender, multiple listener, one receiver.

####load balancing

###Publish-Subscrible Channel

sender broadcast a publish interface 

Observer pattern

###Datatype Channel

###Invalid Message Channel

###Dead Letter Channel



