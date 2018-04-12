# Redux の概要

[https://codesandbox.io/s/kk2vx81z13](https://codesandbox.io/s/kk2vx81z13)

## React の場合

`state`(`this.state`, `this.setState()`) が state 管理の主役だった。

![](/assets/redux.001.jpeg)  

## Redux の場合
![](/assets/redux.002.jpeg)

- Redux は state の管理(保持と変更)を担当する。
- Redux の ** store ** がそれを主に担当する。
- ** store ** は 「一つ前の state, ** dispatch ** された ** action **, ** reducer **」を用いて、新しい state を生成し、これで自分自身の state を上書きすることで state を更新する。
- redux で管理した state を変更するためには、かならず ** aciton ** ** dispatch ** することで行うこと。(`this.setState()`は使わない)
- ** reducer ** は 「一つ前の state, ** dispatch ** された ** action **」を元に新しい state を生成するための ** 「関数」 **。
- Redux が生成した store を React で使用するためには、store を React Component に `Connect` する。（Redux 単体は、単に state 管理のためのアプリケーションなので、React と結び付ける作業は react-redux でおこなう）

      
![](/assets/redux.003.jpeg)

### store 
Redux の中心的な存在です。`action` を受け取ってその内容を元に、「一つ前の state」 に対して ** reducer ** で変更を加えた「新しい state」を生成し、それによって state を更新します。

```js
// redux から　createStore を読み込む
import { createStore } from "redux";

// これを使って store を作る
// その際に reducer が必要
const store = createStore(reducer);
```

### reducer 

`state` を変更するために使用する関数。

```js
// 一個前の state と、受け取った action の内容を元に
// 新しい state を作って return する関数
const reducer = (state = 0, action) => {
  switch (action.type) {
    case "DO_SOMETHING":
      return state + 1;
    default:
      return state;
  }
};
```

