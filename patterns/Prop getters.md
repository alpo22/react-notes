## Prop Getters

> In a custom hook, allow the consumer to provide props that get _combined_ with the hook's.

    function useToggle() {
      const [on, setOn] = React.useState(false)
      const toggle = () => setOn(!on)

      function getTogglerProps(requestedPropsObject) {
        return {
          ...requestedPropsObject,
          onClick: () => {
            requestedPropsObject.onClick && requestedPropsObject.onClick()
            toggle()
          },
        }
      }

      return {on, toggle, getTogglerProps}
    }

    function App() {
      const {on, getTogglerProps} = useToggle()
      return (
        <div>
          <Switch {...getTogglerProps({on})} />
          <hr />
          <button
            {...getTogglerProps({
              'aria-label': 'custom-button',
              onClick: () => console.info('onButtonClick'),
              id: 'custom-button-id',
            })}
          >
            {on ? 'on' : 'off'}
          </button>
        </div>
      )
    }
