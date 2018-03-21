# 初めての React Component


## 一般的に Component とは

![](/assets/react-component.001.png)


Component とは、input \(入力\) を受け取って、それを元に Operation \(なんらかの操作\) をした結果を、Output \(出力\) する部品のこと。

これを組み合わせて、より大きなアプリケーションを構築する。

## React における Component

React におけるコンポーネントは、基本的には React Element を返す単なる  Function です。ただし、ファンクションとは異なるのは、名前の冒頭が大文字でなければいけないことと、使用する際には `<Component />` とカスタムタグのように記述することです。

```js
// 単なる関数
const returnReactElement = () => {
  return <h2>name</h2>;
};

// 関数なので以下のように実行して使う
// returnReactElement()

// React Component にするには、
// 全く同じ内容のまま、冒頭を大文字にする
const ReturnReactElement = props => {
  return (
    <h2>
      {props.name} {props.music}
    </h2>
  );
};

// Component なので以下のようにタグを記述して使う
// 閉じタグを忘れないように
// <ReturnReactElement />
```

## Input を受けつける

ただし、単に React Element を返すだけでは、広義の Component とはいえませんし、あまり便利ではありません。では Input を受け取って、それを元に Output する Component を作成してみましょう。

Component に入力される値は、`<ReturnReactElement　name="nakanishi" music="jazz" />` のように、attribute と同じ形で渡します。

```js
render(
  <ReturnReactElement name="nakanishi" music="jazz" />,
  document.getElementById('root')
);
```

受け取った値は、コンポーネントの引数にオブジェクトとして入ってきます。

```js
props = {
  name: 'nakanishi',
  music: 'jazz'
};
```

受け取った値は `props.name` のようにオブジェクトにアクセスして使用します。

```js
import React from 'react'
import { render } from 'react-dom'

const ReturnReactElement = props => {
  return (
    <h2>
      {props.name} {props.music}
    </h2>
  );
};

render(
  <ReturnReactElement name="nakanishi" music="jazz" />,
  document.getElementById('root')
)
```

### `({})` タイプの引数の受け取り方

また、`({name, music})` として引数を受け取ると、直接、`name` と `music` にオブジェクトが展開して代入されます。

```js
name = 'nakanishi'
music = 'jazz'
```

```js
const ReturnReactElement = ({ name, music }) => {
  return (
    <h2>
      {name} {music}
    </h2>
  );
};
```

## コード全体像

```js
import React from "react";
import { render } from "react-dom";

// 関数
const returnReactElement = () => {
  return <h2>name</h2>;
};

// React Component にするには、
// 全く同じ内容のまま、冒頭を大文字にする
const ReturnReactElement = props => {
  return (
    <h2>
      {props.name} {props.music}
    </h2>
  );
};

const ReturnReactElement2 = ({ name, music }) => {
  return (
    <h2>
      {name} {music}
    </h2>
  );
};

render(
  <ReturnReactElement2 name="nakanishi" music="jazz" />,
  document.getElementById("root")
);

```