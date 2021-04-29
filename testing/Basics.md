```javascript
import * as React from 'react'
import {render, screen, waitForElementToBeRemoved} from '@testing-library/react'
import { within } from '@testing-library/dom';
import userEvent from '@testing-library/user-event'
import LoginForm from '../../components/LoginForm'

test('demonstrating lots of things', async () => {
  const handleSubmit = jest.fn()                                                 // mock function
  render(<LoginForm onClick={handleSubmit} />)
  
  // screen.debug()                                                              // dump out the current HTML content
  
  const submitButton = screen.getByRole('button', {name: /submit/i})             // get elements
  const usernameInput = screen.getByLabelText(/username/i)
  
  userEvent.type(usernameInput, "joe@gmail.com")                                 // type event
  userEvent.click(submitButton)                                                  // click event
  
  expect(handleSubmit).toHaveBeenCalled()                                        // assertion
  
  await waitForElementToBeRemoved(() => screen.getByLabelText(/loading/i))       // wait for element to disappear (made `async` above)
  
  expect(screen.getByText(/hello/i)).toBeInTheDocument()
  // expect(screen.getByLabelText('my checkbox label')).toHaveAttribute('checked', '');
  // expect(screen.findByText('future content'));                                // wait for 'future content' text to appear in the doc

  expect(screen.queryByRole('button')).not.toBeInTheDocument()                   // use `queryBy` when checking if NOT in the document
  expect(within(screen.getByRole('dialog')).getByText(...)).toBeInTheDocument(); // drill down the DOM
})
```

There is also a `rerender` function (returned by `render()`) which allows you to re-render the SAME instance of a component, but with new props.
