## Prop Collections

> In a custom hook, add a property that contains props the consumer would want to apply to their Component that uses the hook.

    function useSwitchHook() {
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
    
    function Switch() {
      const {on, switchProps} = useSwitchHook();
      return <button {...switchProps}>{on ? "On" : "Off"}</button>;
    }
