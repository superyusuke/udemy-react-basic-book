# 改善

## 小さな修正

### reducers/imageUrls.js

```js
// 初期値を空に
const initialState = [];
```

### components/ImageList.js

無駄に表示されていた URL を消す

```js
import React from "react";

const ImageList = ({ urlList }) => {
  const list = urlList.map(url => {
    return (
      <li key={url}>
        <img src={url} alt="" />
      </li>
    );
  });
  return <ul>{list}</ul>;
};

export default ImageList;

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

### reducers/index.js

buttonText reducer を rootReducer に束ねる

```js
import { combineReducers } from "redux";

import imageUrls from "./imageUrls";
// 新たな reducer をコンバインする
import buttonText from "./buttonText";

export default combineReducers({ imageUrls, buttonText });

```

### containers/Search.js

```js
// state を結びつける
const mapStateToProps = state => {
  return {
    buttonText: state.buttonText
  };
};

const mapDispatchToProps = dispatch => {
  return {
    getUrls: word => {
      dispatch(getUrls(word));
    }
  };
};

// state も追加
export default connect(mapStateToProps, mapDispatchToProps)(Search);

```

### components/Search.js

```js
render() {
    // props として受け取る
    const { buttonText } = this.props;
    return (
      <div>
        <form onSubmit={this.handleSubmit}>
          <input value={this.state.title} onChange={this.handleChange} />
          {/* button の値に使用する */}
          <input type="submit" value={buttonText} />
        </form>
      </div>
    );
  }
```

### actions/getUrls.js

リクエストが始まる直前に新たなアクションをディスパッチする

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



## CSS でスタイリングをする

https://codesandbox.io/s/4z7oy358vw

### index.js

```js
// CSS を読み込む
import "./App.css";
```

### App.css

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

### components/ImageList.js

クラスを追加する

```js
import React from "react";

const ImageList = ({ urlList }) => {
  const list = urlList.map(url => {
    return (
      <li className="item" key={url}>
        <img className="image" src={url} alt="" />
      </li>
    );
  });
  return <ul className="list">{list}</ul>;
};

export default ImageList;

```
