# App = ({name}) => name 型のシンタックス / Destructuring assignment

https://codesandbox.io/s/r50k3n0z4m

index.js

```js
// この {} での import も Destructuring assignment に似たシンタックス
import { const1, const2 } from "./const";
console.log(const1, const2, "imported constant");

// object を定義
const obj1 = {
  name: "Nakanaishi",
  music: "Jazz-funk"
};

// name, music という変数を作って、
// 直接 object の内容を展開して代入するシンタックス
const { name, music } = obj1;
console.log(name, music, "obj1");

// 引数を受け取る際に、オブジェクトを展開して受け取るシンタックス
const func1 = ({ name, music }) => console.log(name, music, "func1");
// オブジェクトを関数に渡す
func1(obj1);
```

App.js

```js
import React from "react";

// 引数に入ってきた object を展開して受け取る
// 関数 であり、同時に React Component
const App = ({ name, music }) => (
  <div>
    App {name} {music}
  </div>
);

export default App;

```