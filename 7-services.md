## Chapter 7. Services

### Big Picture
- A Service in the Domain is a stateless operation that fulfills a domain-specific task.
- Don’t lean too heavily toward modeling a domain concept as a Domain Service. Do not treat Domain Services as a “silver bullet”, because it results in the negative consequences of creating an Anemic Domain Model. Domain logic should be mostly spread across Entities and Value Objects.
- A Domain Service’s interface should be expressed in terms of the Ubiquitous Language of the Bounded Context you’re working on.
- Do not confuse a Domain Service with an Application Service. We don’t want to house business logic in an Application Service, but we do want business logic housed in a Domain Service.
- It's not always necessary for a Domain Service to have a separate interface, but it often should.
- Domain Services are allowed to use Infrastructure Services such Repository, but the responsibility of transaction management should be left to Application Services.

### When to Create a Domain Service
- When the operation you need to perform feels out of place as a method on an Aggregate, Entity or a Value Object. It would be a code smell to design a static method on the class of an Aggregate Root instead.
- When you need to perform a significant business process.
- When you need to transform an Aggregate or Entity from one composition to another.
- When you need to calculate a Value Object requiring input from more than one Aggregate.

# Nontrivial Domain Service Use Cases
- There are times when a Domain Service is concerned with remote invocations on a foreign Bounded Context. 
- Some of the more technical Domain Service implementations may live in Infrastructure. Transformation Services which are used for integration between Bounded Contexts are Domain Services too, but their implementations definitely live in Infrastructure.