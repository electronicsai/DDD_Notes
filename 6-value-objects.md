## Chapter 6. Value Objects

### Big Picture
- When you care only about the attributes of an element of the model, classify it as a Value Object. Make it express the meaning of the attributes it conveys and give it related functionality. 
- Treat the Value Object as immutable. Don’t give it any identity and avoid the design complexities necessary to maintain Entities.
- Strive to model using Value Objects instead of Entities wherever possible. Value types that measure, quantify, or describe things are easier to create, test, use, optimize, and maintain. Value Objects may be nested into each other to achieve design goals. Examples of objects that are commonly modeled as Values are numbers; text strings; dates; times; more detailed objects such as a person’s full name composed of first, middle, last name, and title attributes; and others such as currency, colors, phone numbers, and postal addresses.
- Value Objects aren't always held as references by Entities. They may be designed as independent objects. For example, Domain Services may return standalone Value Objects.
- Whole Value should be created in one operation. You must not allow the attributes of a Value instance to be populated after construction, as if to build up the Whole Value piece by piece.
- Only the primary constructor(s) use self-delegation to set properties/attributes. No other methods shall self-delegate to setter methods. Since all setter methods in a Value Object are always private scope, there is no opportunity for attributes to be exposed to mutation by consumers.

### Value Characteristics
- It measures, quantifies, or describes a thing in the domain.
- It can be maintained as immutable — an object that is a Value is unchangeable after it has been created.
- It models a conceptual whole by composing related attributes as an integral unit — each attribute contributes an important part to a whole that collectively the attributes describe. Taken apart from the others, each of the attributes fails to provide a cohesive meaning.
- It is completely replaceable when the measurement or description changes —  an immutable Value should be held as a reference by an Entity as long as its constant state describes the currently correct Whole Value. If that is no longer true, the entire Value is completely replaced with a new Value that does represent the currently correct whole.
- It can be compared with others using Value equality — equality is determined by comparing the types of both objects and then their attributes.
- It supplies its collaborators with Side-Effect-Free Behavior — after the object has been instantiated and initialized by means of construction, none of its methods, whether public or hidden, will from that time forward cause its state to change.

### Storing Value Objects in a Database
- Value Objects can be easily persisted in a database with a basic idea to persist each of the attributes of the Value Object in separate columns of the row where its parent Entity is stored.
- A straightforward approach to persisting a collection of Values in a database is to treat the Value type as an entity ONLY in the database model. We are dealing with an entity, but only from the data model perspective. In the domain model it is clearly a Value Object.

