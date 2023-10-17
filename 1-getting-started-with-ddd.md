# Chapter 1. Getting Started with DDD

## Big Picture
- DDD is about discussion, listening, understanding, discovery and business value, all in effort to centralize knowledge about an important business area.
- Domain experts are the people who know the most about some high-priority area of the business. Domain experts are also going to have to listen to you as a software developer. You are on the team just as they are.
- There is no need for translation between business people and techies. DDD puts domain experts and developers on level ground. There should be literally ZERO translations and only ONE shared Ubiquitous Language for each Bounded Context. Find the domain experts. Listen. Learn. Design in code.
- Domain model is a software model of the very specific business domain you are working in. Using DDD you never try to model the whole business enterprise with a large, single domain model.
- DDD is not about creating a real-world model, as in trying to mimic reality.

## Why I Should Do DDD
- Put domain experts and developers on a level playing field, which produces software that makes perfect sense to the business, not just the coders. That “makes sense to the business” thing means investing in the business by making software that is as close as possible to what the business leaders and experts would create if they were the coders.
- You can actually teach the business more about itself. No domain expert, no C-level manager, no one, ever knows every single thing about the business. With DDD, everybody learns because everybody contributes to discovery discussions.
- There are zero translations between the domain experts, the software developers, and the software.

## How DDD Helps
- DDD brings domain experts and software developers together in order to develop software that reflects the mental model of the business experts. This does not mean that effort is spent on modeling the “real world.” Rather, DDD delivers a model that is the most useful to the business. The Ubiquitous Language is developed with full team agreement, is spoken, and is directly captured in the model of the software. It is worth reiterating that the team is composed of both domain experts and software developers. It’s never “us and them.” It’s always us.
- DDD addresses the strategic initiatives of the business. It helps define the best inter-team organizational relationships and provides early-warning systems for recognizing when a given relationship could cause software and even project failure.
- DDD meets the real technical demands of the software by using tactical design modeling tools to analyze and develop the executable software deliverables. These tactical design tools allow developers to produce software that is a correct codification of the domain experts’ mental model, is highly testable, is less error prone (a provable statement), performs to service-level agreements (SLAs), is scalable, and allows for distributed computing.

## Where to Apply DDD
- Primarily DDD needs to be used in the areas that are most valuable to the domain. Do not use DDD in invaluable areas, because it makes the solution more complex, not simpler. You don’t invest in what can be easily replaced. You invest in the nontrivial, the more complex stuff, the most valuable and important stuff that promises to return the greatest dividends.
- Domain experts cannot help where there is complex code, because they are not programmers.

## Business Value Delivered by DDD
- The organization gains a useful model of its domain. We don’t over-model, we focus on the Core Domain. Our focus should be on what distinguishes our business from others. A refined, precise definition and understanding of the business is developed.
- Domain experts contribute to software design.
- A better user experience is gained. When the user experience is designed to follow the contours of the underlying expert model, users are led to correct conclusions.
- Clean boundaries are placed around pure models.
- Enterprise architecture is better organized.
- Agile, iterative, continuous modeling is used. DDD is not a heavyweight, high-ceremony design and development process. DDD is about carefully refining the mental model of domain experts into a useful model for the business.
- New tools, both strategic and tactical, are employed.

## Ubiquitous Language
- Ubiquitous Language is a shared language developed by the team - a team composed of both domain experts and software developers. The language is more centered on how the business thinks and operates. The Language is not just a bunch of business jargon being forced on developers. It's a real Language created by the whole team. The team must speak the Language openly.
- The use of the word ubiquitous is not an attempt to describe some kind of enterprise-wide, company-wide, or worldwide, universal domain language.
There is one Ubiquitous Language per Bounded Context. The Language is ubiquitous only within the team that is working on the project that develops in an isolated Bounded Context.
- On a single project that develops a single Bounded Context, there are always one or more additional isolated Bounded Contexts with which it integrates using Context Maps. Each of the multiple Bounded Contexts that integrate has its own Ubiquitous Language, even though some terms of each may overlap.
- Both the software and the tests that verify the model's adherence to the tenets of the domain capture and adhere to this Language, the same one spoken by the team.

## Anemia and Memory Loss
- Anemic domain model is a model composed of objects (just dumb data holders) that do not have any additional behavior except for getters and setters.
- Anemic domain model leads to memory loss (loss of understanding of what the object is intended to be) because objects do not have any behavior.
- To avoid memory loss, all domain objects such as Aggregates, Entities and Value Objects should have methods, expressing their rich behaviors.