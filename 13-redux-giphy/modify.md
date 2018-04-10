# 改善

## 小さな修正

### reducers/imageUrls.js

```js
// 初期値を空に
const initialState = [];
```

### APIs/giphyAPI.js

```js
const giphyApi = word => {
  const search = word;
  const key = "V6AU97qCSCYVmbIC5UDppEiVM1xnuO9E";
  // 表示数を増やす
  const limit = 10;
  const url = `https://api.giphy.com/v1/gifs/search?q=${search}&api_key=${key}&limit=${limit}`;

  return axios.get(url);
};
```

## ロード状況をボタンに表示する

https://codesandbox.io/s/l4j8zj4poz

### reducers/buttonText.js

新たな reducer を作る

```js
const initialState = "Find Your GIFs";

const imageUrls = (state = initialState, action) => {
  switch (action.type) {
    case "START_REQUEST":
      return "Wait...";

    case "RECEIVE_DATA":
      return initialState;

    default:
      return state;
  }
};

export default imageUrls;

```

### actions/getUrls.js

```js
import giphyAPI from "../APIs/giphyAPI";

// リクエスト開始用のアクションを作成するクリエイター
const startRequest = () => {
  return {
    type: "START_REQUEST"
  };
};

const receiveData = data => {
  return {
    type: "RECEIVE_DATA",
    payload: data
  };
};

const getUrls = word => {
  return dispatch => {
    // リクエスト直前に実行
    dispatch(startRequest());
    giphyAPI(word).then(res => {
      const data = res.data.data;
      const imageUrlList = data.map(item => item.images.downsized.url);
      dispatch(receiveData(imageUrlList));
    });
  };
};

export default getUrls;

```