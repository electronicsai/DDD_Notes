# Chapter 3. Context Maps

## Big Picture
- Context Map drawing illustrates how the existing Bounded Contexts in the solution space are related to one another through integration.
- A Context Map is not an Enterprise Architecture or system topology diagram.
- The more detailed way to express Context Maps is as the source code implementations of the integrations. You can find more on the implementation details in Chapter 13 - Integrating Bounded Contexts.
- Other project teams can refer to your team’s Context Map, but they should also create their own Maps if they are implementing DDD.

## Drawing Context Maps
- A Context Map captures the existing terrain. First, you should map the present, not the imagined future. If the landscape will change as your current project progresses, you can update the Map at that time.
- Creating a graphical Context Map need not be complicated. Your first option is always hand-drawn diagrams where whiteboards and dry-erase markers rule.
- Besides boundaries, relationships, and translations, we may want to include other items such as Modules, significant Aggregates, perhaps how teams are allocated, and any other information relevant to the Contexts.
- By drawing a Context Map early, when the project is started, you will be forced to think carefully about your relationships with all other projects you depend on. These projects may be other Bounded Contexts or even a Big Ball of Mud.
- Upstream models have influences on downstream models, as activities on a river that occur upstream tend to have impacts on populations downstream, whether positive or negative.