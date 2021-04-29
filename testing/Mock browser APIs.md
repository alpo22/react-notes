## Mock browser APIs

Our tests run via Node, and some `window` functions are not available in Node's simulated DOM environment (jsdom). So we have to supply them:


```javascript
beforeAll(() => {
  window.navigator.geolocation = {
    getCurrentPosition: () => ({ coords: {
      latitude: 35,
      longitude: 139
    }})
  }
});
```


You can also just temporarily mock them:

```javascript
  it("should show error state if it cannot parse the typing string", () => {
    const spy = jest.spyOn(console, "warn").mockImplementation(() => {}); // suppress a momentjs warning

    // test code goes here

    spy.mockRestore();
  });
```
