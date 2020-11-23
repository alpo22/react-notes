## useContext

> Make variables global so don't have to drill.

Lets you subscribe to React context without nesting.

```javascript
//MyContext.js
export const LocaleContext = React.createContext();
	
export default function LocaleProvider({children}) {
  const thingsToShare = { name: 'Jamie', setName: () => {}, ...};

  return (
    <LocaleContext.Provider value={thingsToShare}>
      {children}
    </LocaleContext.Provider>
  );
}

//Header.js
import { LocaleContext } from './MyContext.js';

function Header() {
  const context = React.useContext(LocaleContext);
  return <h1>Hello, {context.name}</h1>;
}

//App.js
import LocaleProvider from './MyContext.js';

function App() {
  return (
    <LocaleProvider>
      <Header />
    </LocaleProvider>
  );
}
```
Kent Dodds implied this isn't the best use of context; its best use would be for sharing data between the parent `<Tabs>` component and the child `<Tab>` components in a library.

