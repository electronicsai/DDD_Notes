## Chapter 10. Aggregate

### Big Picture
- Aggregate is a cluster of Entities and Value Objects with transactional consistency boundary. 
- Aggregates are chiefly about consistency boundaries and not driven by a desire to design object graphs. Aggregate is synonymous with transactional consistency boundary. 
- Aggregate is not a distinct class implementation or domain object, it is a transactional consistency boundary around Entities and Value Objects. 
- Aggregate publishing an Event means that the Aggregate’s Root Entity or other Entities have published an Event.
- Each Aggregate has a globally unique identity that is associated with the Root Entity.
- An invariant is a business rule that must always be transactionally consistent. When trying to discover the Aggregates in a Bounded Context, we must understand the model’s true invariants. Only with that knowledge can we determine which objects should be clustered into a given Aggregate. 
- Limiting modification to one Aggregate instance per transaction is a rule of thumb and should be the goal in most cases. User interface should concentrate each request to execute a single command on just one Aggregate instance.
- Dependency injection of a Repository or Domain Service into an Aggregate should generally be viewed as harmful. 
- In an Application Service method preferably dependent objects are looked up before an Aggregate command method is invoked, and then passed in to it. 

### Aggregate Design Rules
1. Design Small Aggregates
    - When designing Aggregates, we may desire a compositional structure that allows for traversal through deep object graphs, but that is NOT the motivation of the pattern.
    - Limit the Aggregate to just the Root Entity (Aggregate Root) and a minimal number of attributes and/or Value-typed properties. 
    - Choose to model contained Aggregate parts as Value Objects rather than Entities whenever possible.
    - The correct minimum is however many are necessary (those that must be consistent with others, even if domain experts don’t specify them as rules) and no more.
    - The consistency boundary (Aggregate) logically asserts that everything inside adheres to a specific set of business invariant rules no matter what operations are performed. The consistency of everything outside this boundary is irrelevant to the Aggregate. 
    - Smaller Aggregates not only perform and scale better, they are also biased toward transactional success, meaning that conflicts preventing a commit are rare.

2. Reference Other Aggregates by Identity
    - One Aggregate may hold references to the Root of other Aggregates. However, we must keep in mind that this does not place the referenced Aggregate inside the consistency boundary of the one referencing it. Both the referencing Aggregate and the referenced Aggregate must not be modified in the same transaction. Only one or the other may be modified in a single transaction.
    - Prefer references to external Aggregates only by their globally unique identity by holding these references in dedicated Value Objects, not by holding a direct object reference (or “pointer”).
    - Use a Repository or Domain Service to look up dependent objects ahead of invoking the Aggregate behavior. A client Application Service may control this, then dispatch to the Aggregate. Having an Application Service resolve dependencies frees the Aggregate from relying on either a Repository or a Domain Service.

3. Use Transactional Consistency Inside the Boundary
    - A properly designed Aggregate is one that can be modified in any way required by the business with its invariants completely consistent within a single transaction. 
    - A properly designed Bounded Context modifies only one Aggregate instance per transaction in all cases. We cannot correctly reason on Aggregate design without applying transactional analysis.
    - Limiting modification to one Aggregate instance per transaction is a rule of thumb and should be the goal in most cases.
    - The fact that Aggregates must be designed with a consistency focus implies that the user interface should concentrate each request to execute a single command on just one Aggregate instance.

4. Use Eventual Consistency Outside the Boundary
    - This rule bears heavily on what we must do to achieve model consistency when multiple Aggregates must be affected by a single client request.
    - If executing a command on one Aggregate instance requires that additional business rules execute on one or more other Aggregates, use eventual consistency. The key idea is that an aggregate command method publishes a Domain Event that is in time delivered to one or more asynchronous subscribers. Each of these subscribers then retrieves a different yet corresponding Aggregate instance and executes its behavior based on it. Each of the subscribers executes in a separate transaction, obeying the rule of Aggregates to modify just one instance per transaction.

### Reasons To Break The Rules
1. User Interface Convenience 
    - Sometimes user interfaces, as a convenience, allow users to define the common characteristics of many things (Aggregates) at once in order to create batches of them. 
    - It doesn’t cause a problem with managing invariants, since it would not matter whether these Aggregates were created one at a time or in batch.

2. Lack Of Technical Mechanism
    - Eventual consistency requires the use of some kind of out-of-band processing capability, such as messaging, timers, or background threads.
    - If the project you are working on has no provision for any such mechanism, there may be some compromises.

3. Global Transactions
    - This influence is considered to be the effects of legacy technologies and enterprise policies. One such might be the need to strictly adhere to the use of global, two-phase commit transactions.
    - Even if you must use a global transaction, you should try not to modify multiple Aggregate instances at once in your local Bounded Context.

4. Query Performance 
    - There may be times when it’s best to hold direct object references to other Aggregates. This could be used to ease Repository query performance issues.
    - These must be weighed carefully in the light of potential size and overall performance trade-off implications. 

### Real World Cases with Aggregates
1. On one project for the financial derivatives sector, Niclas Hedhman reported that his team was able to design approximately 70 percent of all Aggregates with just a Root Entity containing some Value-typed properties. The remaining 30 percent had just two to three total Entities. This doesn’t indicate that all domain models will have a 70/30 split. It does indicate that a high percentage of Aggregates can be limited to a single Entity, the Root.
