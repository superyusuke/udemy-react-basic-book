# Provider と Connect / store を React で使用する準備

![](/assets/redux_provide-connect.png)

## Provider

https://codesandbox.io/s/6xoq10ov73

```js
import React from "react";
import { render } from "react-dom";

import { createStore } from "redux";
import reducer from "./reducer";

import { Provider } from "react-redux";

import App from "./App";

const store = createStore(reducer);

store.subscribe(() => {
  console.log(store.getState());
});

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
);

```