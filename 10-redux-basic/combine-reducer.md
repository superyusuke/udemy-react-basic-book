# Combine Reducer

https://codesandbox.io/s/913nzp83rr


## Reducer を一つにまとめる

複数の state を管理しやすくするために、reducer を複数用意し、ツリー状に紐付けましょう。そのためには combineReducer を用います。

![](/assets/redux.004.jpeg)

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