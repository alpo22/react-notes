## useSomething (Custom Hook)

>A Custom Hook is a function with state that doesn't render anything. They allow you to:
> 1) reuse stateful logic (every time you use one, all state and effects inside it are fully isolated), or
> 2) isolate concerns


```javascript
// useMovies.js
const useMovies = (query = null) => {
  const [movies, setMovies] = React.useState([]);
  const [q, setQuery] = React.useState(query)

  React.useEffect(() => {
    fetch(`/api/movies?q=${q}`)
    .then(setMovies)
  }, [q, apikey])

  return [movies, setQuery];
}

export default useMovies;
```

A custom hook can contain its own state, logic, and you can use other hooks (like `useEffect`) in them.  You can re-use them as many times as you want in the same component, and each use will have its own state.  It is like a custom component that does not render anything. It must be named like:  `useWhatever`.

They can also be used to keep your code cleaner by abstracting state/effects. If your code has a number of `React.useState()` back to back, this may be a flag to use a custom hook instead.

A good example would be a custom hook that makes async calls, as it would have its own state (status, responseValue, error): https://usehooks.com/useAsync/.

Other examples could be: useDebounce, useKeyPress, useOnOutsideClick.
