## useContext

> Context provides a way to pass data through the component tree without having to pass props down manually at every level.

Imagine you have an app structured like this:

```javascript
<App>
  <Header />
  <Switch>
    <HomePage />
    <AboutUsPage />
    <SettingsPage>
      ...
      <DisplayTab>
        ...
        <ThemePicker />
      </DisplayTab>
    </SettingsPage>
    ...
  </Switch>
  <Footer />
</App>
```

and the `<App />` holds the state of the component, including a `theme` setting. Each page needs to know which `theme` is active, and the `ThemePicker` component also lets you change that setting.

Without context, the `App` component would need to pass `theme` to all of its children explicitly (`Header`, `HomePage`, `AboutUsPage`, `SettingsPage`, `Footer`). The `SettingsPage` would have to pass that down to `DisplayTab`, which would have to pass it down to `ThemePicker`.  The same would be true for the `setTheme()` function, being drilled down to `ThemePicker`.

With context, this drilling can be avoided and whatever is added to context becomes globally available to all _descendants_ of the provider:

```javascript
//MyContext.js
export const ThemeContext = React.createContext();
	
export default function ThemeProvider({children}) {
  const [theme, setTheme] = React.useState('dark');
  const thingsToShare = { theme, setTheme };

  return (
    <ThemeContext.Provider value={thingsToShare}>
      {children}
    </ThemeContext.Provider>
  );
}
```
```javascript
//App.js
import ThemeProvider from './MyContext.js';

function App() {
  return (
    <ThemeProvider>
      <Header />
      <Switch>
        <HomePage />
	...
      </Switch>
      <Footer />
    </ThemeProvider>
  );
}
```
```javascript
//Header.js
import { ThemeContext } from './MyContext.js';

function Header() {
  const context = React.useContext(ThemeContext);
  return <div className={`theme--${context.theme}`}>...</div>;
}
```

Kent Dodds implied this isn't the best use of context; its best use would be for sharing data between the parent `<Tabs>` component and the child `<Tab>` components in a library.

### A simpler example
```javascript
// Context.js
import React from "react";

const MyContext = React.createContext({});

export default MyContext;
```

```javascript
// Parent.js
import React from "react";
import Context from "./Context";

export function Parent() {
  const thingsToExpose = { name: "Jamie", gender: "M" };
  
  return (
    <Context.Provider value={thingsToExpose}>
      <Child />
    </Context.Provider>
  );
}
```

```javascript
// Child.js
import React from "react";
import Context from "./Context";

export function Child() {
  const _context = React.useContext(Context);
  return <h1>Hello {_context.name}</h1>
}
```

### Re-renders

Changing the state in a provider will cause all of the children to re-render, which can be problematic in big apps.
Here are some ways to attempt to stop the re-renders: https://github.com/facebook/react/issues/15156#issuecomment-474590693
