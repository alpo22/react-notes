## Testing a custom hook

> Make a fake component that uses the custom hook to gain access to it.

```javascript

import React from 'react';
import { render, act} from '@testing-library/react`;
import userCounter from './hooks/use-counter';  // has `count` in state, and `increment` and `decrement` functions which modify it

test('...', () => {
  let result;
  
  function FakeComponent() {
    result = useCounter();
    return null;
  }
  
  render(<FakeComponent />);
  expect(result.count).toBe(0);
  act(() => result.increment());    // must be wrapped in `act` since it changes state
  expect(result.count).toBe(1);
});

