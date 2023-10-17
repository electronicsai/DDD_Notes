## Chapter 8. Domain Events

### Big Picture
- Use a Domain Event to capture an occurrence of something that happened in the domain that domain experts care about.
- Model information about activity in the domain as a series of discrete events. Represent each event as a domain object.
- When Events are delivered to interested parties, in either local or foreign systems, they are generally used to facilitate eventual consistency. It can eliminate the need for two-phase commits (global transactions) and support of the rules of Aggregates.
- Domain Event Publishers: Aggregates (Aggregate’s Root Entity or other Entities), Domain Services.
- Domain Event Subscribers: Application Services, and sometimes Domain Services.
- If Domain Events are correctly designed, they will rarely if ever carry entire objects as part of their state, but rather unique identities of foreign Aggregates. The Event should have some limited amount of command parameters and/or Aggregate state that will convey enough meaning to allow subscribing Bounded Contexts to react correctly.
- When modeling Events, name them and their properties according to the Ubiquitous Language in the Bounded Context where they originate. An Event is usually designed as immutable.
- When publishing Events from Aggregates, it is important that the Event name reflects the past nature of the occurrence. Not every Aggregate command results in an Event being produced.
- Remember, the Application Service controls the transaction. Don’t use the Event notification to modify a second Aggregate instance. That breaks a rule of thumb to modify one Aggregate instance per transaction.
- Using Domain Events allows any number of your enterprise systems to be designed as autonomous services and systems. Term autonomous represents a coarse-grained business service, possibly thought of as a system or application, that operates largely independent of other such “services” in the enterprise.
- Prefer asynchronous messaging over RPC and RESTful API to achieve a greater degree of independence between systems.

### Eventual Consistency 
- The changes in one model that influence changes in one or more other models, depending on the traffic to individual systems and the effects they have on others, may make the system as a whole never be fully consistent at any one instant in time.
- The use of any messaging mechanism between Bounded Contexts requires that we adopt a commitment to eventual consistency. It can’t be fought
- Eventual consistency is required to ensure that when the model’s changes are persisted, Event delivery is also guaranteed, and that if an Event is delivered through messaging, it indicates a true situation reflected by the model that published it. If either of these is out of lockstep with the other, it will lead to incorrect states in one or more interdependent models.
- Using the Event Store based approach, discussed in detail in chapter 8, is a straightforward way to facilitate eventual consistency.  

### Publishing Domain Events inside a Bounded Context
- One of the simplest and most effective ways to publish Domain Events without coupling to components outside the domain model is to create a lightweight Observer (GoF Pattern). All registered subscribers execute in the same process space with the publisher and run on the same thread. When an Event is published, each subscriber is notified synchronously, one by one. This also implies that all subscribers are running within the same transaction, perhaps controlled by an Application Service that is the direct client of the domain model.

### Publishing Domain Events to Outside of a Bounded Context
- One of the ways for remote Bounded Contexts to become aware of Events that occur in your Bounded Context is to apply an enterprise messaging mechanism, generally classed as middleware. The use of any messaging mechanism between Bounded Contexts requires that we adopt a commitment to eventual consistency. 
- The second way is to make use of RESTful resources. Here autonomous systems are the interested parties that reach out to the publishing system, requesting all Event notifications that they have not previously consumed.




