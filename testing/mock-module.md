## Mocking a module

> Mock complex (or third-party) modules that interfere with your tests simplicity.

```javascript
import React from 'react';
import { render, screen } from '@testing-library/react';
import App from './App';

jest.mock('./NestedComplexComponentWithinApp', () => () => (<div>Hello World</div>));

test('renders', () => {
  render(<App/>);
  expect(screen.textContent).toMatch('Hello World');
});
