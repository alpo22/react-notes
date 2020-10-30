## useSomething

>A component that has nothing to render.

A custom hook can contain its own state, logic, and you can use other hooks (like `useEffect`) in them.  You can re-use them as many times as you want in the same component.  It is like a custom component that does not render anything. It must be named like:  `useWhatever`.

A good example would be a custom hook that makes async calls, as it would have its own state (status, responseValue, error): https://usehooks.com/useAsync/.

Other examples could be: useDebounce, useKeyPress, useOnOutsideClick.

