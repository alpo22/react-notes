## useState

> Save a value and re-render Component when it changes.

Set and retrieve state. Changing state causes a re-render of the component and any children.

    const [name, setName] = useState('');
    
    return (
      <input value={name} onChange={e => setName(e.target.value)}
    );


