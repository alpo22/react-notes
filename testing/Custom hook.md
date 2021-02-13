## Testing a custom hook

> Won't often need to do this; you'll test the component that _uses_ the custom hook.

Most terse way is by using `renderHook`:

```javascript
import { renderHook, act} from '@testing-library/react`;
import userCounter from './hooks/use-counter';  // has `count` in state, and `increment` and `decrement` functions which modify it

test('...', () => {
  let { result } = renderHook(useCounter);
  expect(result.current.count).toBe(0);
  act(() => result.current.increment());        // must be wrapped in `act` since it changes state
  expect(result.current.count).toBe(1);
});
```

Alternatively can be accomplished by making a fake component that uses the custom hook to gain access to it.

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
  act(() => result.increment());                // must be wrapped in `act` since it changes state
  expect(result.count).toBe(1);
});
```
