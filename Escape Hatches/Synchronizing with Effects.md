### Understanding React Effects

- **Unlike events, Effects are caused by rendering itself rather than a particular interaction.**
- Effects enable synchronization between a component and external systems (e.g., third-party APIs, network requests, etc.).
- By default, Effects run after every render, including the initial one.
- React skips the Effect if all its dependencies have the same values as during the last render.
- You can’t manually choose dependencies; they are determined by the code inside the Effect.
- An empty dependency array ([]) corresponds to the component “mounting,” i.e., being added to the screen.
- In Strict Mode (development only!), React mounts components twice to stress-test Effects and identify potential issues.
- If an Effect breaks due to remounting, a cleanup function needs to be implemented.
- React calls the cleanup function before the Effect runs next time and during the component unmounting.

Remember these points while working with React Effects to ensure smooth and efficient synchronization with external systems.
