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
