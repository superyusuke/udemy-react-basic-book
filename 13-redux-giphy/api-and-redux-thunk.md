# GiphyAPI を叩くメソッドの作成と Redux-thunk を使った非同期処理

## GiphyAPI を叩くメソッドの作成

https://codesandbox.io/s/k30no82zo5

### APIs/giphyAPI.js

```js
import axios from "axios";

const giphyApi = word => {
  const search = word;
  const key = "V6AU97qCSCYVmbIC5UDppEiVM1xnuO9E";
  const limit = 3;
  const url = `https://api.giphy.com/v1/gifs/search?q=${search}&api_key=${key}&limit=${limit}`;

  return axios.get(url);
};

export default giphyApi;

```

### index.js

作ったメソッドを仮に実行する

```js
// 仮に実行する
import giphyAPI from "./APIs/giphyAPI";

giphyAPI("cat").then(res => {
  console.log(res.data);
});

```

## redux-thunk を適用する

### index.js

```js
// applyMiddleware を新たに読み込む
import { createStore, applyMiddleware } from "redux";
// redux-thunk も読み込む
import thunk from "redux-thunk";

// middleWare 用の配列を作成する
const middleWares = [thunk];

// store に適用する
const store = createStore(rootReducer, applyMiddleware(...middleWares));

```

## actio を作る

### reducers/imageUrls.js

```js
const initialState = [1, 2, 3, 4, 5];

const imageUrls = (state = initialState, action) => {
  switch (action.type) {
    // action.payload に data が乗ってくる
    case "RECEIVE_DATA":
      return action.payload;

    default:
      return state;
  }
};

export default imageUrls;

```