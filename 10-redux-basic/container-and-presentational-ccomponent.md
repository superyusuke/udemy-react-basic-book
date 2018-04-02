# Container Component と Presentational Component

参考翻訳記事

http://better-than-i-was-yesterday.com/presentational-and-container-components/

コード

https://codesandbox.io/s/o5rok9m2y9

## ロジックと見た目を切り分ける



### components/App.js

```js
import React from "react";

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

export default App;

```

### containers/App.js


```js
import App from "../components/App";
import { connect } from "react-redux";

const mapStateToProps = state => {
  return {
    number: state
  };
};

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

export default connect(mapStateToProps, mapDispatchToProps)(App);

```
