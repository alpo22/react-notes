## clicking

```javascript
import { fireEvent } from '@testing-library/react'; // from dom-testing-library, but wrapped in `act`

test('...', () => {
  const myButton = screen.querySelector('button');
  fireEvent.click(myButton);
});

```
