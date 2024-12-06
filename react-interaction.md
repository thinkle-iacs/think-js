# Events and State

As we have seen so far, React components let you describe what the user interface (UI) should look like based on some data. However, up until now, our examples have been static. The UI we rendered did not change in response to user input or data changes.

Real web applications need to respond to user actions and update what's displayed. For example, when you click a button, text might change, or a new element might appear. To handle these sorts of changes, React provides two core concepts:

1. **State**: A way to keep track of changing data inside a component.
2. **Events**: A way to listen for and respond to user inputs (like clicks, typing, and other interactions).

Fundamentally, the React model is based on the idea that a GUI program is a cycle (called the React Lifecycle): 

1. There is some initial state (the data that drives a program).
2.  User inputs cause the state to change (events).
3.  State changes cause the UI to update (rendering).
4.  (repeat)

We’ll start by exploring what "state" is, then learn how to handle events, and finally combine them to build an interactive example.

## State

**State** is data managed by a React component that can change over time. When state changes, the component re-renders, updating the UI to match the new data. State is what makes React dynamic.

> Managing state in web applications is complex business. You can think of "state" as the *current value of all the variables that matter*.
> 
>  State also is important in the real world. For example, the state of a light switch is simple --  either "on" or "off" -- but the state of a lightboard in a theater is more complex, with many possible states (e.g. flood, spot, strobe, etc.). 
> 
> The state of a baseball game could be represented on a box score, with many variables like runs, hits, and errors. But if we were representing a video game, we might add many more variables like player health, score, and level.
> 
> The more complex the system, the more complex the state, and debugging state-related issues is a big part of programming.

The React library provides a special `useState` hook (a hook is a function that lets you "hook" into the React lifecycle) to handle state within a functional component. The `useState` hook returns two things:

1. The current value of the state variable.
2. A function to update that value.

We can “destructure” these two values using array syntax, so typically
you'll see a call like this:

```jsx
const [count, setCount] = useState(0);
```

Or, abstractly:
```jsx
const [VALUE, SETTER] = useState(INITIAL_VALUE);
```

This means:
- `count` is our state variable (initially set to 0).
- `setCount` is a function that updates `count`.

Counterintuitively, we use `const` for the value of the state even though we expect it to change. That is because we are not allowed to set the value of a special "state" variable with the assignment operator `=`. Instead, we use the `setCount` function to update the value.

What's really happening is each time we run the setter function (e.g. `setCount`), React schedules a re-render of the component with the new state value. So, each time our component function runs, `count` will have the most recent value and that value will not change while our UI renders: so we think of it as *constant* from the perspective of the function.

We could rewrite our initial "hello world" function using state like this:

```jsx
import React, { useState } from 'react';
const HelloWorld = () => {
  const [count, setCount] = useState(0);
  return <h1>Hello, World! {count}</h1>;
};
```

Because `setCount` is never called in the system above, the value of `count` will always be `0`. You might try adding a call to `setCount` such as `setCount(count + 1)` to change the value, but in practice, that will lead to an infinite render loop. What we actually need to update the count is a way to update the count in response to a user input: that's where events come in!

## Events
**Events** are user inputs that we can "listen" for in the browser, like the user clicking, typing or scrolling. The "listener" pattern is common in programming: we set up a function to run when an event occurs.

In React, we can listen for events by passing a function to an event handler prop on a JSX element. For example, we might write:

```jsx
<button onClick={doSomething}>Click me</button>
```
or
```jsx
<input onChange={handleChange} />
```

In these examples, `doSomething` and `handleChange` are *functions* that will be called whenever the user clicks the button or types in the input field, respectively.

Here is a simple event listener that uses `window.alert` to show you when a function runs

{% include codepen.html id="ogvbKEK" %}



## A Click Counter

Let's put these concepts together to build a simple click counter. We'll use state to keep track of the number of times a button is clicked, and an event to update that state.

```jsx
const ClickCounter = () => {
    const [count, setCount] = useState(0);
    const handleClick = () => setCount(count + 1);
    return (
        <div>
            <h1>Click Counter</h1>
            <button onClick={handleClick}>Click me</button>
            <p>You clicked {count} times</p>
        </div>
    );
};
```

{% include codepen.html id="xbKZvdm" %}

## Mutable Datatypes and State

React decides when to re-render a component by comparing the current state to the previous state. If the state has changed, React will re-render the component. That means that it is easy to make mistakes if you use mutable datatypes (like arrays or objects) for state. As you will recall, if you change an array in place, the array itself has not actually changed, so React will not re-render the component.

Here's an anti-example of a common mistake:

```jsx
const [cats, setCats] = useState(["🐱"]);
const addCat = () => {
    cats.push("🐱");
    // This won't work, *even if we call setCats*
    // because the array itself has not changed!
    setCats(cats);
  };
```

{% include codepen.html id="LEPNPpp" %}


A good pattern is to always make a copy of a list before you make changes. You can copy a list using
the spread operator like this `const newCats = [...cats]` or by using the `slice` method like this `const newCats = cats.slice()`.

Here is a corrected example:

```jsx
const [cats, setCats] = useState(["🐱"]);
const addCat = () => {
    const newCats = cats.slice(); // copy the array!
    newCats.push("🐱");    
    setCats(newCats);
  };
```

Here is the full working code:

{% include codepen.html id="ByBKBKJ" %}
