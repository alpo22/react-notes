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
