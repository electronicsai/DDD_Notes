## Chapter 13. Integrating Bounded Contexts

### Big Picture
- There are always multiple Bounded Contexts in any project of significance, and two or more of those Bounded Contexts will need to integrate.
- Context Maps have two primary forms. One form is a simple drawing that is used to illustrate the kinds of relationships that exist between any two or more Bounded Contexts. The second and far more concrete form is the code that actually implements those relationships.
- Where possible use Value Objects to model concepts in the downstream Bounded Context when objects from the upstream Bounded Context flow in.
- The consuming Bounded Context should be interested only in the data properties and should never be tempted to use functionality that is part of a different model. This principle can be implemented using Events.
- It’s true that Generic and Supporting Subdomains will sometimes lack all the extras associated with a full application, and that’s fine.

### Approaches to Integrate Bounded Contexts
1. Via RPC
    - One Bounded Context exposes an application programming interface (API), and another Bounded Context uses that API via remote procedure calls (RPCs).

2. Via Domain Events and a Messaging Mechanism
    - One of the ways that DDD can be leveraged to make systems autonomous is through the use of Domain Events. As Events occur, they are published to interested parties by means of a messaging mechanism.
    - A message-based approach to integration can allow any one system to achieve a higher degree of autonomy from systems it depends on. As long as the messaging infrastructure remains operational, messages can be sent and delivered even when any one system is unavailable.
    - The consuming Bounded Context should be interested only in the data properties and should never be tempted to use functionality that is part of a different model. Any necessary calculations or processing should be performed by the producing Bounded Context and provided as enriching Event data attributes.

3. Using RESTful API
    - The RESTful service provider must be directly interacted with whenever a resource is operated on, this style does not permit clients to be completely autonomous. If the REST-based Bounded Context becomes unavailable for some reason, dependent client Bounded Contexts will be unable to carry out necessary integration operations during any downtime.
