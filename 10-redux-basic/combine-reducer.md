# Combine Reducer

https://codesandbox.io/s/913nzp83rr

![](/assets/redux.004.jpeg)

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