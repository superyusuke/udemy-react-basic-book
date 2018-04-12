# Action creator

https://codesandbox.io/s/013mn57x20

## 単にアクションを作成し返すだけの関数

Action Creator は、単にアクションを作成し、返すだけの関数です。これを `dispatch(actionCreator())` と使用することで、アクションを作成し、dispatch します。

### actions/index.js

```js
// 単にアクションを返すだけのファンクション
export const plus = num => {
  return { type: "PLUS", payload: { num: num } };
};

export const minus = num => {
  return { type: "MINUS", payload: { num: num } };
};

```

### containers/App.js

```js
import App from "../components/App";
import { connect } from "react-redux";

// action creator を読み込む
import { minus, plus } from "../actions";

const mapStateToProps = state => {
  return {
    number: state
  };
};

// action creator を使用
const mapDispatchToProps = dispatch => {
  return {
    plus: num => {
      dispatch(plus(num));
    },
    minus: num => {
      dispatch(minus(num));
    }
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(App);

```