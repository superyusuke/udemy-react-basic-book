# Redux の全体像の確認

https://codesandbox.io/s/pyx1lrjkjx

### index.js

- store の作成 (reducerを用いる)
- Provider で App をラッピングする
- Provider に store を渡す


```js
import React from "react";
import { render } from "react-dom";

import { createStore } from "redux";
import reducer from "./reducer";

// React Component に store を渡すために、
// Provider でラッピングする
import { Provider } from "react-redux";

import App from "./App";

// reducer を与えて、store を作る
const store = createStore(reducer);

// Provider でラップした上で、
// store を渡す
render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
);

```

### reducer.js

```js
// 現在の state と受け取った action の内容から
// 新しい state を作成し、
// state を更新するための関数
const reducer = (state = 0, action) => {
  switch (action.type) {
    case "PLUS":
      return state + action.payload.num;

    case "MINUS":
      return state - action.payload.num;

    default:
      return state;
  }
};

export default reducer;

```





