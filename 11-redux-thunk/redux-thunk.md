# Redux-thunk で非同期にアクションを発行する

https://codesandbox.io/s/ovv2o75mr5

## Action Creator の中で非同期処理がうまく書けない… Redux-thunk を使う

次のように Action Creator の中でアクションを非同期に返しても、うまくいきません。ですので **「Redux-thunk」** をミドルウェアとして使用する必要があります。


### うまくいかない例

actions/index.js

```js
export const asyncMinus = num => {
  setTimeout(() => {
    return { type: "MINUS", payload: { num: num } };
  }, 1000);
};
```

### index.js で redux-thunk を middleWare として適用する

index.js

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

### 関数を返すアクションクリエイターを作る

#### actions/index.js

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

### コンポーネント、コネクトの修正

#### containers/App.js

```js
import App from "../components/App";
import { connect } from "react-redux";

// 作った action である asyncMinus を読み込む
import { minus, plus, asyncMinus } from "../actions";

const mapStateToProps = state => {
  return {
    number: state.number,
    day: state.day,
    title: state.title
  };
};

const mapDispatchToProps = dispatch => {
  return {
    plus: num => {
      dispatch(plus(num));
    },
    minus: num => {
      dispatch(minus(num));
    },
    asyncMinus: num => {
      // 渡す
      dispatch(asyncMinus(num));
    }
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(App);

```

#### components/App.js

```js
import React from "react";

// asyncMinus を受け取る
const App = ({ number, day, title, plus, minus, asyncMinus }) => (
  <div>
    <h2>
      {title} {number} {day}
    </h2>
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
    <button
      onClick={() => {
        // 実行する
        asyncMinus(10);
      }}
    >
      async - 10
    </button>
  </div>
);

export default App;

```