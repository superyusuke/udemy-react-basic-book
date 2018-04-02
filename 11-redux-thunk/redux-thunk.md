# Redux-thunk で非同期にアクションを発行する

## Action Creator の中で非同期処理がうまく書けない…

次のように Action Creator の中でアクションを非同期に返しても、うまくいきません。ですので Redux-thunk をミドルウェアとして使用する必要があります。

actions/index.js

```js
export const asyncMinus = num => {
  setTimeout(() => {
    return { type: "MINUS", payload: { num: num } };
  }, 1000);
};
```

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

### 

actions/index

```js
// (dispatch) => {} という関数を返すようにする
// この中で dispatch(action) をすればよい
export const asyncMinus = num => {
  return dispatch => {
    setTimeout(() => {
      dispatch({ type: "MINUS", payload: { num: num } });
    }, 1000);
  };
};

```