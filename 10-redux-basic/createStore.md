# createStore

## store を作る

https://codesandbox.io/s/p5o5wjx4vq

store を作っていきます。

![](/assets/redux_createStore.png)

```js
import { createStore } from "redux";

// reducer を定義する
// state の初期値を 0 にしている
const reducer = (state = 0, action) => {
  switch (action.type) {
    case "PLUS_ONE":
      return state + 1;

    case "MINUS_ONE":
      return state - 1;

    // 初期値を設定するためにも必要
    default:
      return state;
  }
};

// createStore を使って store を作る
// その際に reducer を紐づける
const store = createStore(reducer);

// store が変更された際に実行する内容を登録する
store.subscribe(() => {
  // store.getState() で state を取得できる
  console.log(store.getState());
});

// action を dispatch する
store.dispatch({ type: "PLUS_ONE" });
store.dispatch({ type: "PLUS_ONE" });

store.dispatch({ type: "MINUS_ONE" });
store.dispatch({ type: "MINUS_ONE" });
```

## reducer を別ファイルに切り出し、また payload も活用する

## reducer.js に切り出す

reducer.js

```js
const reducer = (state = 0, action) => {
  switch (action.type) {
    case "PLUS":
      // aciton.payload を活用
      return state + action.payload.num;

    case "MINUS":
      return state - action.payload.num;

    default:
      return state;
  }
};

export default reducer;

```


index.js

```js
import { createStore } from "redux";
import reducer from "./reducer";

const store = createStore(reducer);

store.subscribe(() => {
  console.log(store.getState());
});

// action に type だけではなく、
// payload など他のプロパティも持たせることで、
// reducer の中で使用できる
store.dispatch({ type: "PLUS", payload: { num: 1 } });
store.dispatch({ type: "PLUS", payload: { num: 10 } });

store.dispatch({ type: "MINUS", payload: { num: 1 } });
store.dispatch({ type: "MINUS", payload: { num: 10 } });
```


