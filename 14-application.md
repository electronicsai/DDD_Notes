## Chapter 14. Application.

### Bounded Context Architecture
An Application consists of multiple Bounded Contexts. A Bounded Context’s layers hierarchy is as follows:
- User Interface, API
- Application Services, Infrastructure Services
- Domain Model (Domain Services and Domain Objects)

Layer Responsibilities:
- User Interface and API present concepts of the domain model and allow the user to perform various actions on the model.
- Application Services coordinate use case tasks, manage transactions, and assert necessary security authorizations. Infrastructure Services provide enterprise platform-specific infrastructural support and will include the facilities of a component container, application management, messaging, and database.
- Domain Model is the heart of an application. We should strive to push all business domain logic into the Domain Model, whether that be in Aggregates, Entities, Value Objects, or Domain Services.

### Rendering Domain Objects onto the User Interface
The user interface will often need to render properties of multiple Aggregate instances. This is despite the fact that in most cases a user should be performing a state-mutating task that is to be applied to just one instance of a single type of Aggregate.
1. Render Aggregate Instances from the Data Transfer Object:
    - How It Works: The Application Service will use Repositories to read the necessary Aggregate instances and then delegate to a DTO Assembler to map the attributes of the DTO. DTO Assembler will directly access every part of the Aggregates that it needs to build the DTO. The user interface component accesses each individual DTO attribute and renders it onto the view. 
    - The DTO is designed to hold the entire number of attributes that need to be displayed in a view.
    - Your Aggregates will need to be designed so that DTO Assemblers can query for necessary data. Think carefully about how to reveal state without revealing too much about the internal shape or structure of the Aggregates. Try to eliminate a client’s coupling to all internal parts of an Aggregate. 
    - To work around the problem of tight coupling between the model and its clients, you may choose to design Mediator (aka Double-Dispatch and Callback) interfaces to which the Aggregate publishes its internal state. The trick is to not wed the Mediator’s interface to any sort of view specification, but to keep it focused on rendering Aggregate states of interest.

2. Render Aggregate Instances from the Domain Payload Object:
    - How It Works: The Application Service uses Repositories to retrieve the necessary Aggregate instances and then instantiates the DPO to hold references to each. The presentation components ask the DPO object for the Aggregate instance references, and then ask the Aggregates for viewable attributes.
    - The idea is to gather multiple whole Aggregate instances for view rendition into a single Domain Payload Object. The DPOs tend to be much easier to design and have a smaller memory footprint compared to DTOs.
    - DPO is designed to contain references to whole Aggregate instances, not individual attributes. Clusters of Aggregate instances can be transferred between logical tiers or layers by a simple Payload container object.
    - There are a few potential negative consequences to consider. Because of the similarity to DTOs, this approach also requires Aggregates to provide a means to read their state. To avoid tightly coupling the user interface to the model, the same Mediator, Double-Dispatch, or Aggregate Root query interface, suggested previously for use by DTO Assemblers, may be employed here as well.

3. Rendering Aggregate Instances using the Use Case Optimal Repository Queries:
    - How It Works: The use case optimal query uses a Repository to dynamically place the results into a Value Object specifically designed to address the needs of the use case. The custom use case optimal Value Object is then consumed directly by the view renderer.
    - You design a Value Object, not a DTO, because the query is domain specific, not application specific (as are DTOs). 
    - This is where you design your Repository with finder query methods that compose a custom object as a superset of one or more Aggregate instances.
    - The use case optimal query uses a Repository against the unified domain model persistence store rather than a raw database (such as SQL) query against a separate query/read store.

### State Representations of Aggregate Instances 
- If your application provides REST-based resources these will need to produce state representations of domain objects for clients. It is very important to create representations that are based on use case, not on Aggregate instances. It may be more accurate to think of a set of RESTful resources as a separate model in their own right. 
- Resist the temptation to produce representations that are a one-to-one reflection of your domain model Aggregate states, possibly with links to navigate to deeper states. Otherwise your clients will have to understand your domain model as well as the Aggregates themselves. Clients will have to be fully aware of subtleties in behaviors and state transitions, and you will lose all benefits of abstraction.
- What will you do if your application must support multiple, disparate clients? This may include an RIA, a graphical thick client, REST-based services, and messaging too. You probably also consider various test drivers as being different client types. You may design your Application Services to accept Data Transformer, where each client specifies the Data Transformer type. The Application Service would double-dispatch on the Data Transformer parameter, which would produce the required data format.

### Application Services
- Application Services are responsible for task coordination of use case flows, one service method per flow. When using an ACID database, the Application Services also control Repository transactions, ensuring that model state transitions are atomically persisted. Security is also commonly cared for by Application Services.
- Application Services are allowed to directly interact with Infrastructure Services such as Repository and manage its transactions.
- It is a mistake to consider Application Services to be the same as Domain Services. They are not. Application Services do not contain any business logic and should be kept thin.
- Single Application Service may make use of multiple Domain Services, and is a port of the Bounded Context.
- Sometimes the Application Services are designed to completely shield the user interface from all such domain knowledge and this way it’s prohibited to use Value Objects, Aggregates in Application Services’ method signatures. Doing so, the Application Service method signatures use only primitive types (int, long, double), strings and possibly DTOs. 

### Infrastructure
- The job of the infrastructure is to provide technical capabilities for other parts of your application. 
- Infrastructure works out very well if its components depend on the interfaces from the User Interface, Application Services, and Domain Model that require special technical capabilities. 
- You would use the infrastructure to implement interfaces that require use of messaging, repositories, password hashers, etc. If there are special user interface components that feature generated graphical charts, maps, and the like, these would also be implemented in the infrastructure.