# Separate contexts

Split state into multiple logical contexts (i.e. reducers) instead of just one. That way, only one section will re-render when it changes.

Bad:
```
<MyContext>
  <Form />
  <Grid />
</MyContext>
```

Good:
```
<FormContext>
  <Form />
</FormContext>
<GridContext>
  <Grid />
</GridContext>
```
