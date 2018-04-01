# Provider と Connect / store を React で使用する準備

![](/assets/redux_provide-connect.png)

## Provider

https://codesandbox.io/s/6xoq10ov73


index.js

```js
import React from "react";
import { render } from "react-dom";

import { createStore } from "redux";
import reducer from "./reducer";

// React Component に store を渡すために、
// Provider でラッピングする
import { Provider } from "react-redux";

import App from "./App";

const store = createStore(reducer);

store.subscribe(() => {
  console.log(store.getState());
});

// Provider でラップした上で、
// store を渡す
render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
);

```

## connect

https://codesandbox.io/s/qq80yx1lr4

```js
import React from "react";
import { connect } from "react-redux";

// connect されることで、
// props に number, plus, minus が入ってくる
const App = ({ number, plus, minus }) => (
  <div>
    <h2>App {number}</h2>
    <button
      onClick={() => {
        plus(10);
      }}
    >
      + 10
    </button>
    <button
      onClick={() => {
        minus(10);
      }}
    >
      - 10
    </button>
  </div>
);

// number という名前で state をコンポーネントに渡す
const mapStateToProps = state => {
  return {
    number: state
  };
};

// plus と minus という名前で
// action を dispatch するメソッドをコンポーネントに渡す
const mapDispatchToProps = dispatch => {
  return {
    plus: num => {
      dispatch({ type: "PLUS", payload: { num: num } });
    },
    minus: num => {
      dispatch({ type: "MINUS", payload: { num: num } });
    }
  };
};

// connect で App コンポーネントに、
// 「state」 と 「action を dispatchするメソッド」を渡す
export default connect(mapStateToProps, mapDispatchToProps)(App);

```
