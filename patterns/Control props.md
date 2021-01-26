## Control props

> Allow a Component to work either `controlled` (manage state from outside) or `uncontrolled` (manage state from inside). That is: allow the consumer to take _Control_ of the component via _props_.

For example, a `<Tabs>` component that internally keeps track of the active tab:

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
  
  // render the tabs, onClickTab fires `setActiveTabIndex`
  // render the active tab's content
}
```

But what if you want to give the ability of the consumer to programatically change the active tab?  Use the control props pattern, which is to support passing in the state and the way to change it:

```javascript
//Tabs.js
export function Tabs({activeTabIndex, onClickTab}) {  
  const [_activeTabIndex, _setActiveTabIndex] = React.useState(activeTabIndex === undefined ? 0 : );
  
  // render the tabs, onClickTab fires `onClickTab`
  // render the active tab's content
}
```
