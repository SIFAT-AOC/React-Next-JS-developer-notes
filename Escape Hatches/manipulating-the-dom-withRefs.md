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



# React Refs Examples and Best Practices

## Focusing a Text Input

In this example, clicking the button will focus the input:

1. Declare `inputRef` with the `useRef` Hook.
2. Pass it as `<input ref={inputRef}>`. This tells React to put this `<input>`’s DOM node into `inputRef.current`.
3. In the `handleClick` function, read the input DOM node from `inputRef.current` and call `focus()` on it with `inputRef.current.focus()`.
4. Pass the `handleClick` event handler to `<button>` with `onClick`.

## Scrolling to an Element

You can have more than a single ref in a component. In this example, there is a carousel of three images. Each button centers an image by calling the browser `scrollIntoView()` method on the corresponding DOM node:

```javascript
// Example code for a carousel
// ...

<button onClick={() => scrollIntoView(imageRef)}>Center Image</button>

```
In the above examples, there is a predefined number of refs. However, sometimes you might need a ref to each item in the list, and you don’t know how many you will have. Something like this wouldn’t work:

```javascript
 <ul>
  {items.map((item) => {
    // Doesn't work!
    const ref = useRef(null);
    return <li ref={ref} />;
  })}
</ul>

```
## Important Considerations

This is because Hooks must only be called at the top-level of your component. One possible way around this is to get a single ref to their parent element and then use DOM manipulation methods like querySelectorAll to “find” the individual child nodes from it. However, this is brittle and can break if your DOM structure changes.

Another solution is to pass a function to the ref attribute. This is called a ref callback. React will call your ref callback with the DOM node when it’s time to set the ref and with null when it’s time to clear it. This lets you maintain your array or a Map and access any ref by its index or some kind of ID.


In React, every update is split into two phases: render and commit.
Avoid accessing refs during rendering. Refs holding DOM nodes will be null during the first render as the DOM nodes have not yet been created.
React sets ref.current during the commit. It sets affected ref.current values to null before updating the DOM and immediately sets them to the corresponding DOM nodes after updating the DOM.
Use refs for non-destructive actions like focusing, scrolling, or measuring DOM elements.
A component doesn’t expose its DOM nodes by default. Use forwardRef to expose a DOM node by passing the second ref argument down to a specific node.
Avoid changing DOM nodes managed by React. If you do modify DOM nodes managed by React, modify parts that React has no reason to update.
