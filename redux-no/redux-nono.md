# Redux の全体像の確認

[https://codesandbox.io/s/pyx1lrjkjx](https://codesandbox.io/s/pyx1lrjkjx)

## index.js

* store の作成 \(reducerを用いる\)
* Provider で App をラッピングする
* Provider に store を渡す

```javascript
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

## reducer.js

* state を更新するための関数である reducer を作成する
* 現在の state と action を元に、新しい state を作成し

  更新する

* 初期値を与えることと、default の場合を忘れずに

```javascript
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

## App.js

* メインのコンポーネント
* connect で redux の store と React Component を結びつける
* state, dispatch がコンポーネントの props に渡される

```javascript
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

