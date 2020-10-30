## useEffect

> Run code on render.

If the dependencies are omitted, it runs after every render.
If the dependencies are an empty array, it only runs on mount.
Otherwise, it runs whenever one of the dependencies in the array changes.

    React.useEffect((
      window.title = "This happens only once onMount, since the dependencies is an empty array.";
    ) => []);

