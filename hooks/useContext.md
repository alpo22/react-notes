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
export const LocaleContext = React.createContext();
	
export default function LocaleProvider({children}) {
  const [theme, setTheme] = React.useState('dark');
  const thingsToShare = { theme, setTheme };

  return (
    <LocaleContext.Provider value={thingsToShare}>
      {children}
    </LocaleContext.Provider>
  );
}
```
```javascript
//App.js
import LocaleProvider from './MyContext.js';

function App() {
  return (
    <LocaleProvider>
      <Header />
      <Switch>
        <HomePage />
	...
      </Switch>
      <Footer />
    </LocaleProvider>
  );
}
```
```javascript
//Header.js
import { LocaleContext } from './MyContext.js';

function Header() {
  const context = React.useContext(LocaleContext);
  return <div className={`theme--${context.theme}`}>...</div>;
}
```

Kent Dodds implied this isn't the best use of context; its best use would be for sharing data between the parent `<Tabs>` component and the child `<Tab>` components in a library.

