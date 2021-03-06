# Giphy API を使用して、GIF画像検索する React App の作成

## Giphy API の Key を取得する

[https://developers.giphy.com/](https://developers.giphy.com/)

* アカウントを作成する
* API Key を取得する

## Giphy API をたたく

### 問い合わせ先の URL

```javascript
const search = "cat";
const key = "V6AU97qCSCYVmbIC5UDppEiVM1xnuO9E";
const limit = 3;

const url = `https://api.giphy.com/v1/gifs/search?q=${search}&api_key=${key}&limit=${limit}`;
```

### axios でリクエストをし、得た情報を DOM に反映させる

[https://codesandbox.io/s/ylyn217wv](https://codesandbox.io/s/ylyn217wv)

```javascript
import axios from "axios";

const search = "cat";
const key = "V6AU97qCSCYVmbIC5UDppEiVM1xnuO9E";
const limit = 3;

const url = `https://api.giphy.com/v1/gifs/search?q=${search}&api_key=${key}&limit=${limit}`;

axios.get(url).then(res => {
  console.log(res.data);
  const data = res.data.data;

  // 全てのデータの中から、仮に最初の要素の、gif 用 URL を取り出す
  // この URL が画像を取得する際に必要となるもの
  const imageUrl = data[0].images.downsized.url;
  console.log(imageUrl);

  // img 要素を生成して、body 直下に強引に入れ込む
  const img = document.createElement("img");
  img.src = imageUrl;
  document.body.appendChild(img);
});
```

## React App に組み込む

[https://codesandbox.io/s/x3o73pzz4q](https://codesandbox.io/s/x3o73pzz4q)

```javascript
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

## img 要素をレンダリング

[https://codesandbox.io/s/7mpkvy49w1](https://codesandbox.io/s/7mpkvy49w1)

```javascript
// img 要素のリストを作るメソッド
renderImageList(list) {
  const imageList = list.map(url => {
    return (
      <li>
        <img src={url} />
      </li>
    );
  });

  return <ul>{imageList}</ul>;
}

// 上記メソッドをレンダー内で使用する
render() {
  console.log(this.state.gifUrlList);
  return <div>{this.renderImageList(this.state.gifUrlList)}</div>;
}
```

## 検索窓を作る

[https://codesandbox.io/s/n0ppvpzqm4](https://codesandbox.io/s/n0ppvpzqm4)

### todoApp で作ったコンポーネントを活用して Search コンポーネントを作る

components/Search.js

```javascript
import React from "react";

export class Search extends React.Component {
  constructor(props) {
    super(props);
    this.state = { title: "" };
  }

  render() {
    return (
      <div>
        <h2>Find Your GIF</h2>
        <form onSubmit={this.handleSubmit}>
          <input value={this.state.title} onChange={this.handleChange} />
          <input type="submit" value="Search!!" />
        </form>
      </div>
    );
  }

  handleChange = event => {
    const title = event.target.value;
    this.setState({ title: title });
  };

  handleSubmit = event => {
    event.preventDefault();
    // 受け取ったメソッドを実行し、app の state を変更している
    this.props.search(this.state.title);
    this.setState({ title: "" });
  };
}
```

### Search Component を配置する

```javascript
// addTodo を再利用したコンポーネントを読み込む
import { Search } from "./components/Search";

class App extends React.Component {
  // 省略

  render() {
    // Search コンポーネントを使用する
    return (
      <div>
        <Search search={this.giphyApi} />
        {this.renderImageList(this.state.gifUrlList)}
      </div>
    );
  }
```

### Search コンポーネントにメソッドを渡す

App.js

```javascript
render() {
    // Search コンポーネントにメソッドを渡す
    return (
      <div>
        <Search search={this.giphyApi} />
        {this.renderImageList(this.state.gifUrlList)}
      </div>
    );
  }
```

### Search コンポーネントの中で受け取ったメソッドを実行する

Search.js

```javascript
handleSubmit = event => {
  event.preventDefault();
  // 受け取ったメソッドを実行し、app の state を変更している
  this.props.search(this.state.title);
  this.setState({ title: "" });
};
```

### 検索対象を引数として受け取って使用する

index.js

```javascript
// 検索対象を target という引数で受けて使用する
  giphyApi = target => {
    const search = target;
    const key = "V6AU97qCSCYVmbIC5UDppEiVM1xnuO9E";
    const limit = 10;
    const url = `https://api.giphy.com/v1/gifs/search?q=${search}&api_key=${key}&limit=${limit}`;

    axios.get(url).then(res => {
      const data = res.data.data;
      const imageUrlList = data.map(item => item.images.downsized.url);
      this.setState({ gifUrlList: imageUrlList });
    });
  };
```

## CSS でスタイリング

[https://codesandbox.io/s/8vxy99n28](https://codesandbox.io/s/8vxy99n28)

index.js

```javascript
// css を読み込む
import "./App.css";
```

App.css

```css
body {
  background: wheat;
}

.list {
  height: 100vh;
  display: flex;
  flex-direction: column;
  flex-wrap: wrap;
  list-style: none;
}

.item {
  width: 10%;
}

.image {
  width: 100%;
}
```

### クラスネームを付与する

index.js

```javascript
renderImageList(list) {
    const imageList = list.map(url => {
      return (
        <li className="item">
          <img className="image" src={url} />
        </li>
      );
    });

    return <ul className="list">{imageList}</ul>;
  }
```

