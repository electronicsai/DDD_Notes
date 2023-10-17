## Chapter 12. Repositories.

### Big Picture
- Repository is a collection-oriented or persistence-oriented storage for Aggregates. Strictly speaking, only Aggregates have Repositories. Generally speaking, there is a one-to-one relationship between an Aggregate type and a Repository. Every persistent Aggregate type will have a Repository. 
- Remember, Aggregate is not a class implementation, it is a transactional consistency boundary around Entities and Value Objects. When we query for an Aggregate using its Repository, we access all the Aggregate’s objects (Entities and Values) through the Aggregate Root Entity, which sits on top of the hierarchy. 
- Collection-oriented Repositories very closely mimic a collection, simulating at least some of its standard interface, and do not have a save() method.
- Persistence-Oriented Repositories are save-based and mimic a database.
 
### Collection-Oriented Repositories
- Collection-Oriented Repositories very closely mimic a collection, simulating at least some of its standard interface. 
- Implementation of a Collection-Oriented Repository requires some specific capabilities of the underlying persistence mechanism such as tracking changes in objects.

### Persistence-Oriented Repositories
- For times when a collection-oriented style doesn’t work, you will need to employ a persistence-oriented, save-based Repository.
- Persistence-Oriented Repositories do not have add() and addAll() methods. Instead they have save() and saveAll().
- When using a persistence-oriented style, Aggregate instances must be saved both when they are created and when they are modified.
- Persistence-Oriented Repositories are sometimes called Aggregate Stores or Aggregate-Oriented Databases for their simplicity of working with Aggregates.

### Repository Design
- Sometimes when two or more Aggregate types share an object hierarchy, the types may share a single Repository. 
- Do not mistake methods that are beneficial to place on Repositories for those that are best placed under the control of Domain Services.
- It may at times be advantageous to query Aggregate parts out of the Repository without directly accessing the Root itself. However, you wouldn’t design a Repository to provide access to parts that the Aggregate Root would not otherwise allow access to by way of navigation.
- Repository might in some cases answer a Value Object rather than an Aggregate instance. This is called a Use Case Optimal Query Pattern.
- If you find that you must create many finder methods supporting use case optimal queries on multiple Repositories, it’s probably a code smell. 
- The domain model and its encompassing Domain Layer is never the correct place to manage transactions. A common architectural approach to facilitating transactions on behalf of persistence aspects of the domain model is to manage them in the Application Layer.
- The transaction may be managed declaratively or explicitly by developer code.
