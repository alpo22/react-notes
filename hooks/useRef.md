## useRef

>Use to access DOM.

The standard React ref (to access DOM element). This is an easier way to get the content of an input than using 'state' and 'onChange'.

They are also handy for keeping any mutable value around -- like an instance variable in a class.

    const inputRef = useRef();
    //access its value with `inputRef.current.value`
    ...
    <input ref={inputRef} />
