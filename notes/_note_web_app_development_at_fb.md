# Hacker Way - Rethinking Web App Development at Facebook
https://www.youtube.com/watch?list=PLb0IAmt7-GS188xDYE-u1ShQmFFGbrk0v&v=nYkdrAPrdcw

- They want to be able to create quality code by default. They have a core set of values such as creating quality, short iteration time (as fast as possible), etc... 

- One problem they found was, MVC doesn't scale. When you add a new feature to the MVC product the complexity just blew up. It became really unpredictable.

- They started to strive to increase predictability.

- Flux : System architecture that uses single directional data flow.

- Action comes into the system. Dispatcher acts like a traffic controller for the system. Store is the data layer that basically updates whenever you get a new action. And views render whenever the store is changed.

- Dispatcher is the main piece that ensures that there are no cascading effects.

- Once an action goes into store you can't throw another one in till the stores finish processing it.

- One lesson they learned while fixing the chat bug is that:
> (on the client side) Use explicit data instead of derived data. 
> Separate data from view state. 

- Again the role of the dispatcher is that it ensures a synchronious processing of actions. It ensures that no new actions are going to get dispatched until stores are done with the existing ones.

- The primary aim is to prevent cascading effects.

- Figuring out a diff is a hard thing. It is better to always re-render.

> Data changing over time is root of all evil.

- It is really hard for human mind to capture the mutations of state happening over time.

- Dijkstra (Daykstra) has a quote for this:
> We should do our utmost to shorten the conceptual gap between the static program and the dynamic process, to make the correspondance between the program and the process as trivial as possible.

- React does it in 90s way actually. It re-renders the whole thing each time the data changes.
- Get same set of inputs for same set of outputs.

> Simplicity is a prerequisite for reliability
