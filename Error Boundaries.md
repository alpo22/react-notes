## Error Boundaries

>These are Components that catch errors in any of their descendants.

A Component becomes an  `Error Boundary Component`  if it uses one of:

-   `static getDerivedStateFromError(error)`  - for changing state
-   `componentDidCatch()`  - for logging (like to a service)

A few caveats:
- it must be a class component, not a function component
- it will not work if the error is thrown in an event handler, so throw the error in a hook 

For example https://codepen.io/alpo22/pen/QWEmVzg?editors=001:
```
class MyErrorBoundary extends React.Component {
  state = {
    errorString: null
  }

  static getDerivedStateFromError(error) {
    return { errorString: error.message };
  }

  render() {
    if (this.state.errorString) {
      // render custom fallback UI
      return <p style={{color: 'red'}}>{this.state.errorString}</p>;
    }
    return this.props.children;
  }
};

function Section() {
  const [count, setCount] = React.useState(0);
  
  React.useEffect(() => {
    if (count > 0) {
      throw new Error(`Kablooey!`);    
    }
  }, [count]);
  
  return (
    <>
      <h1>Section</h1>
      <button onClick={() => { setCount(oldCount => oldCount+1); }}>+</button>
    </>
  );
}

function App() {
  return (
    <table border="1" cellpadding="10">
      <tr>
        <td>
          <MyErrorBoundary>
            <Section />
          </MyErrorBoundary>
        </td>
        <td>
          <MyErrorBoundary>
            <Section />
          </MyErrorBoundary>
        </td>
      </tr>
    </table>
  );
}
```
