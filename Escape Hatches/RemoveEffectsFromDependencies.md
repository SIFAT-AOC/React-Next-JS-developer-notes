### Dependencies should always match the code.
When you’re not happy with your dependencies, what you need to edit is the code.
Suppressing the linter leads to very confusing bugs, and you should always avoid it.
To remove a dependency, you need to “prove” to the linter that it’s not necessary.
If some code should run in response to a specific interaction, move that code to an event handler.
If different parts of your Effect should re-run for different reasons, split it into several Effects.
If you want to update some state based on the previous state, pass an updater function.
If you want to read the latest value without “reacting” it, extract an Effect Event from your Effect.
In JavaScript, objects and functions are considered different if they were created at different times.
Try to avoid object and function dependencies. Move them outside the component or inside the Effect.
