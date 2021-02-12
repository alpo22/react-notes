```javascript
import * as React from 'react'
import {render, screen, fireEvent, waitForElementToBeRemoved} from '@testing-library/react'
import userEvent from '@testing-library/user-event'
import LoginForm from '../../components/LoginForm'

test('demonstrating lots of things', async () => {
  const handleSubmit = jest.fn()                                            // mock function
  render(<LoginForm onClick={handleSubmit} />)
  
  // screen.debug()                                                         // dump out the current HTML content
  
  const submitButton = screen.getByRole('button', {name: /submit/i})        // get elements
  const usernameInput = screen.getByLabelText(/username/i)
  
  userEvent.type(usernameInput, "joe@gmail.com")                            // type event
  
  fireEvent.click(submitButton)                                             // click event
  expect(handleSubmit).toHaveBeenCalled()                                   // assertion
  
  await waitForElementToBeRemoved(() => screen.getByLabelText(/loading/i))  // wait for element to disappear (made `async` above)
  
  expect(screen.getByText(/hello/i).toBeInTheDocument()
})
