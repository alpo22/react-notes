## Error Boundaries

>These are Components that catch errors in any of their descendants.

A Component becomes an  `Error Boundary Component`  if it uses one of:

-   `static getDerivedStateFromError(error)`  - for changing state
-   `componentDidCatch()`  - for logging (like to a service)

For example:

```
function MyErrorBoundary({children}) {
  const [error, setError] = React.useState('');
  
  static function getDerivedStateFromError(error) {
    setError(error);
  }
  
  return error ? <ErrorDisplay error={error} /> : children;
}

function App() {
  return (
    <MyErrorBoundary>
      <FancyApp />
    </MyErrorBoundary>
  );
}
```
