# React でアロー関数を使用する

アロー関数の React アプリケーション開発における実際的なユースケースをみていきましょう。

```js
import React from "react";
import { render } from "react-dom";

// React Element を返すアローファンクション
const returnReactElement = () => {
  return <h2>text</h2>;
};

// return は省略可能
const returnReactElement2 = () => <h2>text2</h2>;

// 引数を受け取り JSX 内で使用するアロー関数
const returnReactElement3 = hello => <h2>{hello}</h2>;

const returnReactElement4 = (no, name) => {
  const newStrings = `${no}番目は${name}さんです。`;
  return <h2>{newStrings}</h2>;
};

render(returnReactElement4("#1", "Nakanishi"), document.getElementById("root"));

```