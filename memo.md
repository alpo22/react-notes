## React.memo (not _React.useMemo_) 

> Memoize (cache) a component so it won't re-render unless its props or state change (it will not re-render just because its parent did).

Imagine two components on a page: a Form and a Graph.  We do not want the Graph to re-render every time a key is pressed in the Form, so we would make the Graph component use `React.memo()`.

#### Example

    import React from "react";

    const MyComponent = React.memo(() => {
       //...
    });

    export default MyComponent;
