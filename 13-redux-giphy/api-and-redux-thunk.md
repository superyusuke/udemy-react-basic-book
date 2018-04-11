# GiphyAPI を叩くメソッドの作成と Redux-thunk を使った非同期処理

## GiphyAPI を叩くメソッドの作成

https://codesandbox.io/s/k30no82zo5

### dependencies の追加

Axios を dependencies に追加する

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

https://codesandbox.io/s/9zx8nrnzjr

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

## action を作る

https://codesandbox.io/s/64rq4lyj23

### actions/getUrls.js

```js
import giphyAPI from "../APIs/giphyAPI";

// 通常の action creator
const receiveData = data => {
  return {
    type: "RECEIVE_DATA",
    payload: data
  };
};

// thunk 用の関数を返す action creator
const getUrls = word => {
  return dispatch => {
    giphyAPI(word).then(res => {
      const data = res.data.data;
      const imageUrlList = data.map(item => item.images.downsized.url);
      dispatch(receiveData(imageUrlList));
    });
  };
};

export default getUrls;

```

### reducers/imageUrls.js

reducer の修正

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

### index.js

仮に実行する。

```js
// 仮に実行
import getUrls from "./actions/getUrls";
store.dispatch(getUrls("cat"));

```

## Search コンポーネントにメソッドを connect する

https://codesandbox.io/s/0or0zq8pvn

### App.js

```js
import React from "react";

import ImageList from "./containers/ImageList";

// components から containers へ変更
import Search from "./containers/Search";

const App = () => {
  return (
    <div>
      App
      <Search />
      <ImageList />
    </div>
  );
};

export default App;

```

### containers/Search.js

```js
import Search from "../components/Search";
import { connect } from "react-redux";

// action を読み込む
import getUrls from "../actions/getUrls";

// action を dhispatch するメソッドを props として渡す
const mapDispatchToProps = dispatch => {
  return {
    getUrls: word => {
      dispatch(getUrls(word));
    }
  };
};

export default connect(null, mapDispatchToProps)(Search);

```

### components/Search.js

```js
handleSubmit = event => {
    // connect で与えられたメソッドを受け取る
    const { getUrls } = this.props;
    event.preventDefault();
    // 使用する
    getUrls(this.state.title);
    this.setState({ title: "" });
  };
```

