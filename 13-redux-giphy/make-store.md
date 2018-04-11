# store を作る

## store の準備

https://codesandbox.io/s/0q54o9lxw0

以下を dependencies に追加する

- redux
- react-redux
- redux-thunk

### index.js

```js
import React from "react";
import { render } from "react-dom";

import App from "./App";

import { createStore } from "redux";

import { Provider } from "react-redux";

// まだ rootReducer がないのでエラーになる
const store = createStore(rootReducer);

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
);
```

### App.js
```js
import React from "react";

const App = () => {
  return <div>App</div>;
};

export default App;
```

## reducer の作成
https://codesandbox.io/s/mq63n3m9oj

### reducers/imageUrls.js

取得した画像用URLのための reducer

```js
const initialState = [1, 2, 3, 4, 5];

const imageUrls = (state = initialState, action) => {
  switch (action.type) {
    case "RECEIVE_DATA":
      return "data";

    default:
      return state;
  }
};

export default imageUrls;
```

### reducers/index.js

複数の reducer を combineReducers でまとめ上げるためのファイル

```js
import { combineReducers } from "redux";

import imageUrls from "./imageUrls";

export default combineReducers({ imageUrls });

```

### index.js

combineReducers でまとめ上げた reducer を import して、createStore に与える

```js
import rootReducer from "./reducers";
const store = createStore(rootReducer);

//　正常に動いているか確認
console.log(store.getState());
```