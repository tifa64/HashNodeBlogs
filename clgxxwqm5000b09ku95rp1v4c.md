---
title: "How to use a React state immediatley after dispatch()"
datePublished: Wed Apr 26 2023 16:58:22 GMT+0000 (Coordinated Universal Time)
cuid: clgxxwqm5000b09ku95rp1v4c
slug: how-to-use-a-react-state-immediatley-after-dispatch
tags: reactjs, redux, redux-toolkit, reacthooks

---

Redux is a powerful state manager but its good to know its side effects.

Recently I encountered an issue where I needed to use a state right after dispatching an action that updates it using redux-toolkit.

### Problem

When an action is dispatched in Redux, the store is updated asynchronously, which means that the updated state may not be immediately available in the component that dispatched the action.

### Solution

Use a reference to the state using `useRef` hook and leverage `useEffect` which makes use of the fact that the component will re-render after the state is changed.

Inside the `useEffect` you can update the ref and use that ref from now on.

### Code

```typescript
import { useRef, useEffect } from 'react';
import { useDispatch, useSelector } from 'react-redux';
import { increment } from './counterSlice'; // assuming you have a counterSlice that contains an "increment" action

function Counter() {
  const count = useSelector((state) => state.counter.value);
  const dispatch = useDispatch();
  const counterRef = useRef(count); // create a mutable reference to the initial count value

  useEffect(() => {
    counterRef.current = count; // update the reference when count changes
  }, [count]);

  const handleIncrement = () => {
    dispatch(increment());
    const updatedCount = counterRef.current; // use the updated value from the reference
    someFunction(updatedCount); // pass the updated count value to another function
  };

  return (
    <div>
      <h1>Count: {count}</h1>
      <button onClick={handleIncrement}>Increment</button>
    </div>
  );
}

export default Counter;
```