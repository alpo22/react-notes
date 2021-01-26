## Control props

> Allow a Component to work either `controlled` (manage state from outside) or `uncontrolled` (manage state from inside), by accepting optional props with the initial state and the handler to change them. That is: allow the consumer to take _Control_ of the component via _props_.

For example, a `<Tabs>` component that internally keeps track of the active tab (uncontrolled):

```javascript
<Tabs>
  <Tab title="Tab 1">Contents of tab 1</Tab>
  <Tab title="Tab 2">Contents of tab 2</Tab>
  <Tab title="Tab 3">Contents of tab 3</Tab>
</Tabs>
```
```javascript
//Tabs.js
export function Tabs() {
  const [activeTabIndex, setActiveTabIndex] = React.useState(0);
  
  // render the tabs. when a tab is clicked, fire `setActiveTabIndex`
  // render tab[activeTabIndex]'s content
}
```

Using the `Control props` pattern this component can made to _also_ support being controlled, which would give the consumer the ability to externally change the active tab if they wanted to:

```javascript
//Tabs.js
export function Tabs({activeTabIndex, onClickTab}) {  
  const [_activeTabIndex, _setActiveTabIndex] = React.useState(activeTabIndex === undefined ? 0 : activeTabIndex);
  
  // render the tabs. when a tab is clicked, if activeTabIndex === undefined, fire _setActiveTabIndex. else, fire onClickTab
  // render tab[_activeTabIndex]'s content
}
```

The important thing here is that the props are not mandatory - the component works with or without them.
