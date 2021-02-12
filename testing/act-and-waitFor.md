## act
The `act` warning comes up when some component's state changes unexpectedly (i.e. outside of the React stack, eg. when you set state in a `setTimeout` or `setInterval`).

Wrap the test code that is changing the state in `act(() => { ... }` and it will go away.

Kent Dodds has lots of video examples here: https://kentcdodds.com/blog/fix-the-not-wrapped-in-act-warning (the text is below the videos).

```javascript
import {render, screen, act} from '@testing-library/react';

it('some test', () => {
  ...
  await act(() => {
    // the thing that is changing state goes here
  });
});

```

## waitFor
It's also possible that your component (or one of the libraries within your component) is using a timeout before rendering something.  If the test relies on that something, you could see this error (an example is the Paprika Modal, which I think has a timeout before appearing on screen).  You can tell your test to `waitFor` that element to appear:

```javascript
// this has an `act` warning
expect(screen.queryAllByTestId('raw-button').length).toEqual(1);
  
// this works
await waitFor(() => {
  expect(screen.queryAllByTestId('raw-button').length).toEqual(1);
});
```
