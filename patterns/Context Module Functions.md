## Context Module Functions

> If we expose the `dispatch` function and the consumer will need to call it multiple times to accomplish something, instead expose a function that itself does the multiple dispatches.

E.g. in a "File Uploader" component the state changes from "pending", to "uploading", to "complete" or "error".  Instead of relying on the consumer to call:

```
disaptch({type: 'pending'});
disaptch({type: 'uploading', data: fileData})
  .then(() => {
    dispatch({type: 'complete'});
  })
  .catch((e) => {
    dispatch({type: 'error', data: e});
  });
```

we can have them just call:
```
upload(dispatch, fileData);
```
and we handle all the "dispatching" correctly, internally in our component. This sounds more like basic programming pricinciples (DRY) and a better API for the consumer.
