### Example of UseEffect synchronizing 
## React Effects Playground

This React playground demonstrates the behavior of `useEffect` in different scenarios.

```jsx
import { useState, useEffect } from 'react';

function Playground() {
  const [text, setText] = useState('a');

  useEffect(() => {
    function onTimeout() {
      console.log('⏰ ' + text);
    }

    console.log('🔵 Schedule "' + text + '" log');
    const timeoutId = setTimeout(onTimeout, 3000);

    return () => {
      console.log('🟡 Cancel "' + text + '" log');
      clearTimeout(timeoutId);
    };
  }, [text]);

  return (
    <>
      <label>
        What to log:{' '}
        <input
          value={text}
          onChange={(e) => setText(e.target.value)}
        />
      </label>
      <h1>{text}</h1>
    </>
  );
}

export default function App() {
  const [show, setShow] = useState(false);
  return (
    <>
      <button onClick={() => setShow(!show)}>
        {show ? 'Unmount' : 'Mount'} the component
      </button>
      {show && <hr />}
      {show && <Playground />}
    </>
  );
}
```
### Observations and Experiments:
Initial Logs:

1 . Press "Mount the component" to see initial logs: Schedule "a" log, Cancel "a" log, and Schedule "a" log again.
Fast Input Typing:

2 . Edit the input to say "abc" quickly. Observe Schedule/Cancel pairs indicating cleanup. React cleans up the previous Effect before the next one.
Unmount Component:

3 . Type into the input and then press "Unmount the component". Notice how unmounting cleans up the last render’s Effect, preventing the last timeout from firing.
No Cleanup:

4 . Comment out the cleanup function in the useEffect. Type "abcde" quickly. Expect to see a sequence of logs (a, ab, abc, abcd, and abcde) after three seconds. Each Effect captures the text value from its corresponding render.

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
