# Chapter 4. Architecture

### Big Picture
- DDD doesn’t require the use of any specific architecture.
- The most suitable architecture for DDD is Hexagonal Architecture. 

### Architecture Design Rules
1. User Interface
    - The User Interface is to contain only code that addresses user view and request concerns. It must not contain domain/business logic. 
    - The kinds of validation found in the User Interface are not the kinds that belong in the domain model (only). 
    - If the User Interface components use objects from the domain model, it is generally limited to rendering its data to the UI.

2. Application 
    - The Application Services are the direct clients of the domain model, though themselves possessing no business logic.
    - Application Services remain very lightweight and thin, coordinating operations performed against domain objects, such as Aggregates. They are the primary means of expressing use cases on the model. 
    - An Application Service may also use a Domain Service to fulfill some domain-specific task designed as a stateless operation. 
    - Application Services may control persistence transactions and security. They may also be in charge of storing, forwarding, publishing and otherwise dealing with Events.

3. Infrastructure
    - Infrastructure Services implement all the technical components and frameworks that provide low-level services for the application. We want to reject any notion of coupling core domain model objects to Infrastructure.

4. Domain
    - Domain Layer houses all of the business logic, including the Domain Model and Domain Services.

### Use Case Examples For Application Services
- A common function of an Application Service is to accept parameters from the User Interface, use a Repository to obtain an Aggregate instance, and then execute a command operation on it.
- When a new Aggregate must be created, an Application Service would use a Factory or the Aggregate’s constructor to instantiate it and then use the corresponding Repository to persist it. 
- Since the Application Layer is the direct client of the Domain, it depends on Domain interfaces and indirectly accesses Repository and any technical Domain Service implementation classes provided by Infrastructure. 
