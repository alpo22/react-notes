## Basic Compound Components

> Compound components is a pattern in which components are used together such that they share an implicit state that lets them communicate with each other in the background, like `<select>` and `<option>`.

The idea is to use better composition; that is, instead of writing it like this:

    <Tabs options={["First", "Second", "Third"]} />

Do it like this:

    <Tabs>
      <Tab title="First" />
      <Tab title="Second" />
      <Tab title="Third" />
    </Tabs>

Doing it this way allows: easily re-ordering the `<Tab>`s, adding/removing `<Tab>`s, changing props, etc.

Using `React.Children.map` and `React.cloneElement`, `<Tabs>` can add an `onClick()` and `isActive` prop to each child `<Tab>`:


    function Tabs({children}) {
      const [activeTabIndex, setActiveTabIndex] = React.useState(0);
      
      return React.Children.map(children, (child, i) =>
	    React.cloneElement(child, {
	      isActive: activeTabIndex === i,
	      onClick: () => { setActiveTabIndex(i);
	    }
	  });
    }


But what if there is a tab that is not  a _direct_ child?  The above wouldn't work...

## Flexible Compound Components

The above solution would not work if any of the `<Tab>` components were not a direct child of `<Tabs>`:

    <Tabs>
      <Tab title="First" />
      <Tab title="Second" />
      <div className="tab--admin">
	    <Tab title="Third" />
	  </div>
    </Tabs>
    
The solution is to share context from `<Tabs>` and consume it in `<Tab>`:
- create a  `React.createContext`  
- add the provider in  `<Tabs>`. and consuming the context in the `<Tab>` component.

Like this:

    const TabsContext = React.createContext();

    function Tabs({children}) {
        const [activeTabTitle, setActiveTabTitle] = React.useState('');
            
      return (
          <TabsContext.Provider value={{activeTabTitle, setActiveTabTitle}}>
            {children}
          </TabsContext.Provider>
      );
    }

    function Tab({children, title}) {
      const c = useContext(TabsContext);
      
      return (
        <button
          onClick={() => c.setActiveTabTitle(title)}
          disabled={c.activeTabTitle === title}
        >
          {title}
        </button>);
    }
