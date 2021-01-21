## Prop Collections

> Return commonly-used props for a component that uses this custom hook.

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
    
    // Switch.js
    function Switch() {
      const {on, switchProps} = useSwitch();
      return <button {...switchProps}>{on ? "On" : "Off"}</button>;
    }
