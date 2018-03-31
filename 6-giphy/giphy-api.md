# Giphy API を叩いて Gif 画像を表示する App を作る

## Giphy API の Key を取得する

https://developers.giphy.com/

- アカウントを作成する
- API Key を取得する

## Giphy API をたたく

### 問い合わせ先の URL

```js
const search = "cat";
const key = "V6AU97qCSCYVmbIC5UDppEiVM1xnuO9E";
const limit = 3;

const url = `https://api.giphy.com/v1/gifs/search?q=${search}&api_key=${key}&limit=${limit}`;

```

### axios でリクエストをし、得た情報を DOM に反映させる

https://codesandbox.io/s/ylyn217wv

```js
import axios from "axios";

const search = "cat";
const key = "V6AU97qCSCYVmbIC5UDppEiVM1xnuO9E";
const limit = 3;

const url = `https://api.giphy.com/v1/gifs/search?q=${search}&api_key=${key}&limit=${limit}`;

axios.get(url).then(res => {
  console.log(res.data);
  const data = res.data.data;
  const imageUrl = data[0].images.downsized.url;
  console.log(imageUrl);

  const img = document.createElement("img");
  img.src = imageUrl;
  document.body.appendChild(img);
});
```

## React App に組み込む 1