# Chapter 2. Domains, Subdomains and Bounded Contexts

## Big Picture
- The whole Domain of the organization is composed of Subdomains (Core, Supporting, Generic).
- Domain Model is a software model of the Subdomain you are working in. Developing a Domain Model is actually one way that we focus on only one specific Subdomain of the whole business Domain. 
- Bounded Context is an explicit boundary within which a Domain Model exists.

## Core Domain, Supporting and Generic Subdomains
- A Core Domain is a part of the business Domain that is of primary importance to the success of the organization. Strategically speaking, the business must excel with its Core Domain.
- Sometimes a Bounded Context is created or acquired to support the business. If it models some aspect of the business that is essential, yet not Core, it is a Supporting Subdomain.
- If a Bounded Context captures nothing special to the business, yet is required for the overall business solution, it is a Generic Subdomain. Being Supporting or Generic doesn’t mean unimportant.
- It is a desirable goal to align all of the Domain’s Subdomains (Core, Supporting, Generic) one-to-one with Bounded Contexts.

## Problem and Solution Space
- Real world Domains have both a problem space and a solution space. 
- The problem space enables us to think of a strategic business challenge to be solved. It is the parts of the Domain that need to be developed to deliver a new Core Domain. Assessing the problem space involves examining Subdomains that already exist and those that are needed. Thus, your problem space is the combination of the Core Domain and the Subdomains it must use.
- The solution space focuses on how we will implement the software to solve the problem of the business challenge. It is one or more Bounded Contexts, a set of specific software models. The Bounded Context is used to realize a solution as software.

## Making Sense of Bounded Contexts
- A Bounded Context is an explicit boundary within which a domain model exists. Inside the boundary all terms and phrases of the Ubiquitous Language have specific meaning, and the model reflects the Language with exactness.
- A Bounded Context does not necessarily encompass only the domain model. Bounded Context often marks off a system, an application, or a business service. When the model drives the creation of a persistence database schema, the database schema will live inside the boundary. When there are User Interface views that render the model and drive execution of its behavior, these are also inside the Bounded Context. However, this does not mean that we model the Domain in the user interface, causing domain model anemia. We want to reject any temptation to drag domain concepts that belong in the model into other areas of the system.