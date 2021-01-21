## Context Module Functions

> If our component uses context and a reducer and makes asynchronous UI updates, and the consumer will need to call it multiple times to accomplish something, expose a function that accepts the `dispatch` function as a prop, which itself does the multiple dispatches.

E.g. in a "File Uploader" component the state changes from "pending", to "uploading", to "complete"/"error".  Instead of relying on the consumer to have this code:

```
onUpload() {
  disaptch({type: 'pending'});
  disaptch({type: 'uploading', data: fileData})
    .then(() => {
      dispatch({type: 'complete'});
    })
    .catch((e) => {
      dispatch({type: 'error', data: e});
  });
}
```

they can have this code:
```
onUpload() {
  upload(dispatch, fileData);
}
```
and we handle all the "dispatching" in internally in our component. This sounds more like basic programming pricinciples (DRY) and a better API for the consumer.
