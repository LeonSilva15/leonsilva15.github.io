---
layout: post
title: React Hooks Quick Glance
date: 2024-01-22
---
# React Hooks

Nowadays everyone is into React and so many projects has picked it as its frontend library, making us to learn a lot of stuff to keep up with the newer projects. Here's a quick reference to React Hooks I wrote as reference to work in react projects.

### Why
The motivation to use React Hooks is present when we need to work with dynamic data, react to some web components' life cycle, or when interacting with the DOM elements; so, if we are missing these points, we can skip the hooks usage.

Prior to **React 16.8** we had to use classes to use certain React features, but now we can use the React Hooks in our function components.

Currently there are 10 main React Hooks.

### useState
> useState is a React Hook that lets you add a state variable to your component.

```js
const [state, setState] = useState(initialState)
```

This hook handles the state of a component, it is composed of two parts, the `state` and the `method` that updates it.

![useState](/assets/2024-01-22/useState.png "useState")

> [react.dev - useState](https://react.dev/reference/react/useState)

### useEffect
> useEffect is a React Hook that lets you synchronize a component with an external system.

```js
useEffect(setup, dependencies?)
```

In the past, when working with classes, we had to use the life cycle events, specifically: `componentDidMount`, `componentDidUpdate` and `componentWillUnmount`. Now we can use the `useEffect` hook to run something when the component is mounted, updated or will unmount.

* `componentDidMount`: the code inside every `useEffect` method.
* `componentDidUpdate`: when any of the attributes in the second parameter array of the `useEffect` hook is updated.
* `componentWillUnmount`: the code returned by the `useEffect` method.

![useEffect](/assets/2024-01-22/useEffect.png "useEffect")

> [react.dev - useEffect](https://react.dev/reference/react/useEffect)

### useContext
> useContext is a React Hook that lets you read and subscribe to context from your component.

```js
const value = useContext(SomeContext)
```

This is used to share data without passing it as `props`.
This can share data through the components tree.

We use the context providers as a wrap component to share the same data inside this scope.
We can consume this context data in any child component, no matter how deep it is in the components tree.
The context consumes the nearest parent provider.

![useContext](/assets/2024-01-22/useContext.png "useContext")
> [react.dev - useContext](https://react.dev/reference/react/useContext)

### useRef
> useRef is a React Hook that lets you reference a value that’s not needed for rendering.

```js
const ref = useRef(initialValue)
```

This hook updates data but **doesn’t re-render** anything. This is normally used to reference html elements and link them to react components.

![useRef](/assets/2024-01-22/useRef.png "useRef")

> [react.dev - useRef](https://react.dev/reference/react/useRef)

### useReducer
> useReducer is a React Hook that lets you add a reducer to your component.

```js
const [state, dispatch] = useReducer(reducer, initialArg, init?)
```

This one works similar to useState, the only difference is that instead of directly updating the value, it dispatches and action that indicates how to update the value.
It uses a reducer method that receives the current state and the dispatched action with the “type” (mandatory, string) and the “payload” (optional, any).

![useReducer](/assets/2024-01-22/useReducer.png "useReducer")

> [react.dev - useReducer](https://react.dev/reference/react/useReducer)

### useMemo
> useMemo is a React Hook that lets you cache the result of a calculation between re-renders.

```js
const cachedValue = useMemo(calculateValue, dependencies)
```

Caches the result of function call. This should only be used for expensive computations. This only caches values.
In the examle below, changing the theme doesn't recalculates the memoized value, only modifying the todos or the tab will run the recalculation.

![useMemo](/assets/2024-01-22/useMemo.png "useMemo")

> [react.dev - useMemo](https://react.dev/reference/react/useMemo)

### useCallback
> useCallback is a React Hook that lets you cache a function definition between re-renders.

```js
const cachedFn = useCallback(fn, dependencies)
```

This one works as the useMemo hook but caches an entire function. A common use case is when passing to a list of components a prop made of a function, to avoid recalculating the method, we only process it once and send the memoized version.

![useCallback](/assets/2024-01-22/useCallback.png "useCallback")

> [react.dev - useCallback](https://react.dev/reference/react/useCallback)

### useImperativeHandle
> useImperativeHandle is a React Hook that lets you customize the handle exposed as a ref.

```js
useImperativeHandle(ref, createHandle, dependencies?)
```

Used only in rare cases, this allows us to expose native DOM elements through references. Commonly used when creating a reusable components library.

![useImperativeHandle MyInput.js](/assets/2024-01-22/useImperativeHandle_1.png "useImperativeHandle MyInput.js")
![useImperativeHandle App.js](/assets/2024-01-22/useImperativeHandle_2.png "useImperativeHandle App.js")

> [react.dev - useImperativeHandle](https://react.dev/reference/react/useImperativeHandle)

### useLayoutEffect
> useLayoutEffect is a version of useEffect that fires before the browser repaints the screen.

```js
useLayoutEffect(setup, dependencies?)
```

This is another rare hook; it works like the useEffect hook but takes effect after rendering but before displaying to screen. Some cases might include calculating mouse or scroll position right before rendering.

![useLayoutEffect](/assets/2024-01-22/useLayoutEffect.png "useLayoutEffect")

> [react.dev - useLayoutEffect](https://react.dev/reference/react/useLayoutEffect)

### useDebugValue
> useDebugValue is a React Hook that lets you add a label to a custom Hook in React DevTools.

```js
useDebugValue(value, format?)
```

When working with custom hooks, we can add this hook inside of our custom hook to display our data in the react developer tools.

![useDebugValue](/assets/2024-01-22/useDebugValue.png "useDebugValue")

> [react.dev - useDebugValue](https://react.dev/reference/react/useDebugValue)

---
More in [react.dev](https://react.dev/reference/react/hooks).
