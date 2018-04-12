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
- redux で管理した state を変更するためには、かならず ** aciton ** を ** dispatch ** することで行うこと。(`this.setState()`は使わない)
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

`state` を変更するために使用される関数です。
一つ前の state と、受け取った action の内容を元に、新しい state を作って return する関数です。action.type で分岐して、返す内容を決めています。


```js
// 一つ前の state と、受け取った action の内容を元に
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

### action と dispatch

`action` は単なるオブジェクトです。`dispatch` によって発行されます。
`dispatch` で `action` を発行すると、`store` に送られて、state の更新のために使われます。`reducer` が受け取って、`action.type` によって分岐していましたよね。

```js
// action の dispatch
store.dispatch({
  type: "DO_SOMETHING",
  payload: "something"
});

// action はこの部分
// type は必須だが、
// 他にも任意のプロパティ(ここでは payload)を追加してもよい
{
  type: "DO_SOMETHING",
  payload: "something"
}
``` 

## store を react で使うために Provider, connect が必要

Redux の store を作っただけでは、store は宙ぶらりんの状態で、React で使う準備はできていません。React で store を使うために、準備が必要です。この役割は ** react-redux ** が担います。

### Provider

`Provider` コンポーネントで、App の一番上のコンポーネントをラッピングし、store を渡すことで、それより下のコンポーネントに対して、store を渡します。

```js
// react と redux を結びつけるために react-redux を用いる
import { Provider } from "react-redux";

// 階層的に一番上のコンポーネントを Provider でラッピングし
// store を渡すことで、それより下位層で store を使用できるように準備する

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
);

```

