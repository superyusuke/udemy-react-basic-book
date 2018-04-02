# Redux-thunk で非同期にアクションを発行する

### index.js で middleWare を適用する

```js
import React from "react";
import { render } from "react-dom";

// store に middleWare を適用するための関数
// applyMiddleware を import する
import { createStore, applyMiddleware } from "redux";
import rootReducer from "./reducers";

import { Provider } from "react-redux";

import App from "./containers/App";

// redux-thunk
import thunk from "redux-thunk";

// 後々複数の middleWare を適用できるように配列に入れる
const middleWares = [thunk];

// createStore の第二引数に、
// applyMiddleware() を使って、middleWare を適用する
const store = createStore(rootReducer, applyMiddleware(...middleWares));

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
);

```