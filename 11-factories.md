## Chapter 11. Factories.

### Big Picture
- The primary motivation for using Factories is to shift the responsibility for creating instances of complex objects and Aggregates to a separate object, which may itself have no responsibility in the domain model but is still part of the domain design. Create entire Aggregates as a piece, enforcing their invariants.
- An Aggregate Root that provides a Factory Method for producing instances of another Aggregate type (or inner parts) will have the primary responsibility of providing its main Aggregate behavior, the Factory Method being just one of those. 
- Factory methods for aggregates can be placed either on Aggregates or Domain Services. Placing a carefully designed Factory Method on specific Aggregate Roots can ensure that domain objects are created correctly. Also simplifies clients, requiring them to pass only basic parameters, often Value Objects only, by hiding the construction details from them.
- One case where you would find an Abstract Factory of great benefit is when creating objects of different types in a class hierarchy, which is a classic use. The client is required to pass in only some basic parameters from which the Factory can determine the concrete type that must be created.
