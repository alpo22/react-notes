```javascript
import * as React from 'react'
import {render, screen, fireEvent} from '@testing-library/react'
import userEvent from '@testing-library/user-event'
import LoginForm from '../../components/LoginForm'

test('demonstrating lots of things', () => {
  const handleSubmit = jest.fn()                                      // mock function
  render(<LoginForm onClick={handleSubmit} />)
  
  const submitButton = screen.getByRole('button', {name: /submit/i})  // get elements
  const usernameInput = screen.getByLabelText(/username/i)
  
  userEvent.type(usernameInput, "joe@gmail.com")                      // type
  
  fireEvent.click(submitButton)                                       // click event
  expect(handleSubmit).toHaveBeenCalled()                             // assertion
  
  await waitForElementToBeRemoved(() => screen.getByText(/spinner/))  // wait for element to disappear
  
})
