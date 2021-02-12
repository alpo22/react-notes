## Testing with context

> A component may require context to render.

Can do it in one of two ways:

### Simply add the context
```javascript
test('...', () => {
  render(<ThemeProvider><Nav /></ThemeProvider);
  ...
});

```

### Provide the context in a wrapper
```javascript
test('...', () => {
  function MyWrapper({children}) {
    return <ThemeProvider>{children}</ThemeProvider>;
  }
  
  render(<Nav />, { wrapper: MyWrapper });
  ...
});
```

Dodds suggests making your own `render`, which first wraps everything with a wrapper like this. So all your components have all your providers.
