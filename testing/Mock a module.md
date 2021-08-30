## Mock a module

> Mock complex (or third-party) modules that interfere with your tests simplicity.

#### A local component:

```javascript
import React from 'react';
import { render, screen } from '@testing-library/react';
import App from './App';

jest.mock('./components/SomeComponent', () => () => (<div>Hello World</div>));

test('renders', () => {
  render(<App/>);
  expect(screen.textContent).toMatch('Hello World');
});
```

#### Third-party components

Simply create a `__mocks__` folder beside `node_modules` that matches the import path.  E.g. to mock the `HighChart` component, that is imported like this: `import HighChart from '@acl-services/sriracha-high-chart/dist/HighChart';`, create this folder structure:

```
  __mocks__
    @acl-services
      sriracha-high-chart
        dist
          HighChart.js
  node_modules
  src
  ...
```
