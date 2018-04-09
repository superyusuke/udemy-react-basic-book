# store を作る

## 動画 1

```js
import React from "react";
import { render } from "react-dom";

import App from "./App";

import { createStore } from "redux";

import { Provider } from "react-redux";

const store = createStore(rootReducer);

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
);
```