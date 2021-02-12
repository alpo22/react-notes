## Mock an API

Can use `msw` (https://testing-library.com/docs/react-testing-library/example-intro/) but I think `fetch-mock` is simpler (https://www.npmjs.com/package/fetch-mock) -- at least for GETs, haven't tried for POSTs.

I built a Paprika component to make `fetch-mock` even easier to use:

```javascript
import React from "react";
import { useMockEndpoints } from "@paprika/mock-endpoints";

const endpoints = [
  {
    "url": "/players",
    "response": [
      { "id": 1, "name": "Wayne Gretzky", "number": 99 },
      { "id": 2, "name": "Gordie Howe", "number": 4 },
      { "id": 3, "name": "Sydney Crosby", "number": 87 },
      { "id": 4, "name": "Mario Lemieux", "number": 66 }
    ]
  }
];

export default function Story() {
  const [response, setResponse] = React.useState("");

  const { endpointsAreMocked } = useMockEndpoints(endpoints);
  if (!endpointsAreMocked) return null;

  function fetchPlayers() {
    fetch("/players")
      .then(res => res.json())
      .then(data => setResponse(data));
  }

  return (
    <>
      <p>Click on one of the buttons below to hit the mock API endpoint:</p>
      <button type="button" onClick={fetchPlayers}>
        Fetch Players
      </button>
      <br />
      <br />
      <xmp>{JSON.stringify(response)}</xmp>
    </>
  );
}
```
