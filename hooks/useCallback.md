## useCallback

> Memoize a function.

Memoizes a function (memoization is caching the result of an expensive function call). Functions inside a Component are re-created on every re-render, but you don't want that when:
  - the function is a dependency in a hook (e.g. `useEffect(() => {...}, [myFunction])`)
  - your component is wrapped in a `React.memo()` and accepts a callback prop (e.g. `React.memo(SomeComponent, myFunction)`)

Prevents a function from being created on every single render, which can prevent a component from re-rendering.

For example: I have a `<ToDoList>` component, with 50 `<ToDoItem>` children. The `<ToDoList>` holds the state of the `<ToDoItem>`s (if they are selected). To each `<ToDoItem>` I pass down the `onChangeIsSelected` function. Clicking a `<ToDoItem>` will call this function, which will change the parent `<ToDoList>`'s state, which will make it re-render.
As-is, all of the `ToDoItem`s would also re-render (since their parent's state changed).  To try and solve that, you'd wrap the `ToDoItem` in `React.memo`, but that wouldn't stop them from re-rendering (because the `onChangeIsSelected` prop passed into each would be different on every re-render of `ToDoList`).
To solve this we need to use both  `React.memo` *and* `useCallback`.

It has the same API as `useEffect`:

    const someFunction = React.useCallback(() => {
      //...
    }, []);

    function ToDoList() {
        const [items, setItems] = React.useState(Array(50).fill(false));

        function toggleClick(i) {
          //toggle items[i] and update state
        }
        
        return items.map((item, i) => <Item isChecked={item} onClick={() => toggleClick(i)}
    }
    
    function Item({isChecked, onClick) {
      return <input type="checkbox" checked={isChecked} onChange={onClick} />;
    }
