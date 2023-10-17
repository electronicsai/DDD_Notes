## Chapter 5. Entities

### Big Picture
- We design a domain concept as an Entity when we care about its individuality. An Entity is a unique thing and is capable of being changed continuously over a long period of time. It is the unique identity and mutability characteristics that set Entities apart from Value Objects. 
- We should strive to model using Value Objects instead of Entities wherever possible.
- Entity’s design should be biased toward serving as a Value container rather than a child Entity container.
- Entities should have methods expressing their rich behaviors, which allows to avoid creation of an Anemic Domain Model, but static methods are a sign to create a Domain Service. Entity methods should also implement coarse-grained validations that express deep business knowledge which belongs only to the model.
- How to opt between an Entity and a Value Object? Ask whether that object must itself change over time and persist its unique identity (Entity), or whether it can be completely replaced when change is necessary (Value Object).

### Unique Identity 
- In the early stages of designing an Entity, we purposely focus only on those primary attributes and behaviors that are central to its unique identity, as well as those useful for querying it, and we purposely ignore all other attributes and behaviors until we settle on the primary ones.
An Entity’s unique identity may or may not also be practical for finding or matching.
- In most cases unique identity must be protected from modification, remaining stable throughout the lifetime of the Entity to which it is assigned. Value Objects can serve as holders of unique identity. They are immutable, which ensures identity stability, and any behavior specific to the kind of identity is centralized. 
- Identity generation can occur either early, as part of the object’s construction, or late, as part of its persistence. There are some problems related to late Id allocation.
- If your ORM tool wants to deal with object identity on its own terms, preferring  the database’s native type, such as a numeric sequence, but the domain requires another kind of identity, it is going to cause an undesirable conflict. To cure this, we need to use two identities. One of the identities is designed for the domain model and adheres to the requirements of the domain. The other is for ORM and is known as a surrogate identity.

### Identity Creation Strategies
- The user provides one or more original unique values as input to the application. The application must ensure that they are unique.
- The application internally generates an identity using an algorithm that ensures uniqueness.
- The application relies on a persistence store, such as a database, to generate a unique identity.
- Another Bounded Context (system or application) has already determined the unique identity. 






