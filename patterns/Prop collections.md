## Prop Collections

> Return commonly-used props for a component that uses this custom hook.

```javascript
// useSwitch.js
function useSwitch() {
  const [on, setOn] = React.useState(false);
  function toggle() {
    setOn(true);
  }
      
  return ({
    on,
    toggle,
    switchProps: {
      'aria-pressed': on,
      onClick: toggle
    }
  };
}
```
```javascript
// Switch.js
function Switch() {
  const {on, switchProps} = useSwitch();
  return <button {...switchProps}>{on ? "On" : "Off"}</button>;
  }
```

I'm not sure I see the benefit of doing this... is it so we can add more to `switchProps` and all consumers would get it?  Is it just neater than:

```javascript
// Switch.js
function Switch() {
  const {on, toggle} = useSwitch();
  return <button onClick={toggle} ariaPressed={on}>{on ? "On" : "Off"}</button>;
  }
```
