## React.memo (not _React.useMemo_) 

> Cache a component.  This is not useMemo.

Memoize a Component (memoization is caching the result of an expensive function call, and a component is just a function).
Wrap a Component with `React.memo()` and it wont re-render if its parent re-renders, unless its own props have changed.

