## Getting a ref to the node

To access a DOM node managed by React, you can use the `useRef` Hook. Here's how you can do it:

1. Import the `useRef` Hook from the `react` package:
    ```javascript
    import { useRef } from 'react';
    ```

2. Declare a ref inside your component using the `useRef` Hook:
    ```javascript
    const myRef = useRef(null);
    ```

3. Pass your ref as the `ref` attribute to the JSX tag for which you want to get the DOM node:
    ```jsx
    <div ref={myRef}>
    ```

The `useRef` Hook returns an object with a single property called `current`. Initially, `myRef.current` will be `null`. When React creates a DOM node for the `<div>`, React will put a reference to this node into `myRef.current`. You can then access this DOM node from your event handlers and use the built-in browser APIs defined on it.

For example, you can use the `scrollIntoView` method to scroll the DOM node into view:
Getting a ref to the node 
To access a DOM node managed by React, first, import the useRef Hook:

import { useRef } from 'react';
Then, use it to declare a ref inside your component:

const myRef = useRef(null);
Finally, pass your ref as the ref attribute to the JSX tag for which you want to get the DOM node:

<div ref={myRef}>
The useRef Hook returns an object with a single property called current. Initially, myRef.current will be null. When React creates a DOM node for this <div>, React will put a reference to this node into myRef.current. You can then access this DOM node from your event handlers and use the built-in browser APIs defined on it.

// You can use any browser APIs, for example:
myRef.current.scrollIntoView();