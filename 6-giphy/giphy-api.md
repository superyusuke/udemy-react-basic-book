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

## React App に組み込む

```js
import React from "react";
import { render } from "react-dom";

import axios from "axios";

class App extends React.Component {
  constructor() {
    super();
    // image の url のリストを持つ
    this.state = { gifUrlList: [] };
  }

  // コンポーネントがマウントされた時に実行される
  componentDidMount() {
    this.giphyApi();
  }

  render() {
    console.log(this.state.gifUrlList);
    return <div>app</div>;
  }

  // API を叩いて、その結果を state に反映させるメソッド
  giphyApi() {
    // リクエスト先の URL を作る
    const search = "cat";
    const key = "V6AU97qCSCYVmbIC5UDppEiVM1xnuO9E";
    const limit = 3;
    const url = `https://api.giphy.com/v1/gifs/search?q=${search}&api_key=${key}&limit=${limit}`;

    // axios でリクエストをする
    axios.get(url).then(res => {
      const data = res.data.data;
      // 必要な URL の配列を作る
      const imageUrlList = data.map(item => item.images.downsized.url);
      // state を取得した情報を元に変更する
      this.setState({ gifUrlList: imageUrlList });
    });
  }
}

render(<App />, document.getElementById("root"));

```



## React App に組み込む 1