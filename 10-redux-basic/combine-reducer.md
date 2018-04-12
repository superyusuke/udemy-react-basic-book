# Combine Reducer

https://codesandbox.io/s/913nzp83rr


## Reducer を一つにまとめる

複数の state を管理しやすくするために、reducer を複数用意し、ツリー状に紐付けましょう。そのためには combineReducer を用います。

![](/assets/redux.004.jpeg)

### reducer.num.js

reducer ディレクトリの中に移動させます。

### reducer/day.js

```js
const day = (state = "test day 2018", action) => {
  switch (action.type) {
    default:
      return state;
  }
};

export default day;
````

### reducer/title.js

```js
const title = (state = "test title", action) => {
  switch (action.type) {
    default:
      return state;
  }
};

export default title;

```


### reducers/index.js

複数の reducer をまとめあげます。

```js
import { combineReducers } from "redux";

// reducer を読み込む
import number from "./number";
import title from "./title";
import day from "./day";

// combineReducer で
// 一つの Reducer にまとめる
export default combineReducers({
  number,
  title,
  day
});

```
### index.js

```js
import React from "react";
import { render } from "react-dom";

import { createStore } from "redux";

// まとめ上げた reducer を import する
// 名前が変わっているので注意
import rootReducer from "./reducers";

import { Provider } from "react-redux";

import App from "./containers/App";

// 名前を変更しています
const store = createStore(rootReducer);

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
);

```


### containers/App.js

```js
import App from "../components/App";
import { connect } from "react-redux";

import { minus, plus } from "../actions";

// 渡す state を増やす
// state.プロパティ名 という形で、
// 一本化された　state にアクセスします
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
    }
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(App);

```

### components/App.js

```js
import React from "react";

// connect されたものを受け取る
const App = ({ number, day, title, plus, minus }) => (
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
  </div>
);

export default App;

```