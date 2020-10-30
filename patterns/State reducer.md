# State reducer

> Make the component more flexible by giving the consumer the option to provide state control logic.

Allow the consumer to provide the `reducer` so they can control the component's state as they want.  Additionally export the reducer and constants (types) so the consumer can override whichever actions they want.

An example of inversion of control could be for a `Popover` component that has an `alignment` prop that accepts one of "left" or "right". It is inevitable that consumers would request "top", "bottom", "left edge", "centre", etc. Instead, allow the `alignment` prop to also accept a function (that would calculate position).


