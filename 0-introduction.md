# Introduction

## Big Picture
- Tactical Design (DDD-Lite) incorporates DDD details such as ValueObjects, Entities, Aggregates, Repositories, Services and so on.
- Strategic Design allows one to get a high view of the DDD methodology and includes tenets such as Bounded Contexts, Context Maps, Ubiquitous Language and others.
- Scrum and Agile methodologies should not be used as a substitute for careful design. Scrum was never meant to stand in place of design.
- Developers should think of how the backlog tasks affect the application domain model.
- A Ubiquitous Language is applicable only within a single Bounded Context. Context Maps show the relationships between Bounded Context.
- Whichever way the software models are designed tactically, strategically they reflect the following: a clean Ubiquitous Language modeled in an explicitly Bounded Context.

## Strategic Modeling
- DDD strategic design patterns are Ubiquitous Language, Bounded Context, Context Maps, Core Domain and Generic/Supporting Subdomains. Strategic design patterns offer a high level view of the domain.
- A Bounded Context is a conceptual boundary where a domain model is applicable. It provides a context for the Ubiquitous Language that is spoken by the team and expressed in its carefully designed software model.
- Bounded Contexts talk to each other through Context Maps. Context Maps are used to understand the project terrain.
- Tactically and strategically designed domain models should be architecture independent. A powerful architectural style for hosting a Bounded Context is Hexagonal, which can be used to facilitate other styles such as REST, Event-Driven and others.

## Tactical Modeling
- DDD-Lite is a set of DDD tactical design patterns such as Value Object, Entity, Aggregate, Repository, Service. Practicing DDD-Lite leads to the construction of inferior domain models. We model tactically inside a Bounded Context using DDD’s building block patterns.
- One of the most important tactical design patterns is Aggregate. An Aggregate is composed of either a single Entity (Aggregate Root), or a cluster of Entities and Value Objects, which must remain transactionally consistent throughout the Aggregate’s lifetime. An instance of an Aggregate is persisted using Repository and later searched for within and retrieved from it. Each Aggregate has its own transactional consistency boundary. Aggregates should not be designed only according to the natural hierarchy of objects in the Domain.
- Stateless Domain Services are inside the domain model to perform business operations that don’t naturally fit as an operation on Entities or Value Objects. Domain Services carry out domain-specific operations, which may involve multiple domain objects.
- Domain Events are used to indicate the occurrence of significant happenings in the domain. When Domain Events capture occurrences that are a result of some Aggregate command operation, the Aggregate itself publishes the Event.