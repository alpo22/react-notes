## useReducer

> Set state when order matters.

Same as `useState`, but need it when you will be setting states back-to-back and you want to guarantee the order in which they are set, i.e. one of your states relies on another one of your states.

Since it is hard to know in advance if you'll need this, maybe it's best to use them on non-trivial code.


    import React from "react";
    
    function App() {
      const myReducer = (state, action) => {
        switch (action.type) {
          case "DEC":  return {...state, count: state.count - 1};
          case "INC":  return {...state, count: state.count + 1};
          default:
            throw new Error(`Unexpected action ${action.type}`);
        }
      };
    
      const [state, dispatch] = React.useReducer(myReducer, {count: 0});
    
      return (
        <div>
          Count: {state.count}<br />
          <button onClick={() => dispatch("DEC")}>-</button>
          <button onClick={() => dispatch("INC")}>+</button>
        </div>
      );
    }



