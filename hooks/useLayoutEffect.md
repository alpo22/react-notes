## useLayoutEffect

> Run code on render but before browser updates.

Similar to `useEffect`, except that this is fired BEFORE the updated DOM has been re-painted -- while `useEffect` is fired AFTER the updated DOM has been re-painted.

You will use `useEffect` 99% of the time, but you may want to use this one when:
- working on an animation/scrolling and there is some flickering/delay
- making observable changes to the DOM
- you want to be sure that the effect runs first
