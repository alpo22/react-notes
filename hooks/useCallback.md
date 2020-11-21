## useCallback

> Memoize (cache) a callback function that is passed to child components so the children do not re-render when the parent re-renders (unless the functions dependencies change).

    const handleToggleIsChecked = React.useCallback(
      (itemId) => {
        //...
      },
      [items]
    );
  
Every time a component's state changes, it re-renders.  If a component declared a function that was passed down to a child component, whenever the parent re-rendered, the child would also re-render -- even if it used `React.memo()`.

#### Use Case 1:

Imagine you have a `ToDoList` app which holds all the state.  At the top of this app is a Form component where you can type in a new item, and beneath is a list of all the Items. Something like this:

    <ToDoListApp>
      state = newItemText, items;

      function handleToggleIsChecked(id) { ... }
  
      <AddItemForm text={} onChangeText={} onSubmit={} />

      <Item isChecked={} onToggleIsChecked={handleToggleIsChecked} text={} />
      <Item isChecked={} onToggleIsChecked={handleToggleIsChecked} text={} />
      <Item isChecked={} onToggleIsChecked={handleToggleIsChecked} text={} />
    </ToDoListApp>

When you type in the text for a new item, each time you press a key, the `ToDoList` app's state changes, so it re-renders itself and all of its children. If you had 20 Items in your list, every single one of them would re-render with each keypress, which is not ideal.

To fix that, you have to do two things:

1) wrap the `Item` component in `React.memo()` so it only re-renders when its state or props have changed -- not its parent's state.
2) wrap `handleToggleIsChecked` in `React.useCallback()` so it does not get redefined each time the `ToDoListApp`'s state changes (i.e. each keypress)

A working example can be seen here: https://codesandbox.io/s/frosty-voice-b9je8?file=/src/ToDoList.js:762-1036

#### Use Case 2:

You'd also want to use this for a function that is a dependency in a hook:

    useEffect(() => {...}, [myFunction])`)

Imagine your effect caused a state change. That would cause the component to re-render, which would redefine the function, which would fire the useEffect hook, which would cause the component to re-render, which would redefined the function, ... infintely looping.

