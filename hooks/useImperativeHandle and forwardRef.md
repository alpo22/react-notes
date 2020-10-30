## useImperativeHandle

> Expose a Component's inner functions so can call them

Allows you to pass in a `ref` to a component, then in the component you can expose some of its functions by adding them to that ref, so the parent can call them.
E.g. you have a `<Textarea>` component, and elsewhere on the screen there is a button that when clicked makes the `<Textarea>` scroll to its top.
Used rarely, pairs with `forwardRef`.
https://reactjs.org/docs/hooks-reference.html#useimperativehandle


### forwardRef
Allows component to take a `ref` as a prop and pass it down further to its child.
Simple example: https://gist.github.com/jamesreggio/142215754ad06f375bd87657c6227ed8
Not sure why you couldnt just pass down the ref as a prop though, call it `myRef`...

