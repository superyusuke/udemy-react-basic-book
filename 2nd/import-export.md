# import, export, js module


### index.js (読み込む側)
```js
import React from "react";
import { render } from "react-dom";

import { var1, function1, ReactComponent } from "./module";

console.log(var1);
function1();

render(<ReactComponent />, document.getElementById("root"));
```

### module.js (出力する側)
```js
import React from "react";

export const var1 = "string";

export const function1 = () => console.log("this is function1");

export const ReactComponent = () => <h2>name</h2>;

```

## import は別ファイルに切り出した JavaScript (module) から変数、関数、クラス等を読み込むための宣言

変数、関数、クラス等を、別ファイルに切り出し、それを読みこむために import を使う。また出力する側では export をしておく。

- 出力する側で変数、関数、クラスの前に `export` をつける。
- 読み込む側では、`import` {名前} `from` 'ファイル名' とする。
- この場合のファイル名は、`hello` のように、拡張子をつけなくていい。
- あとは普通に使う。

## module
JavaScript におけるモジュールとは、別ファイルに切り分けられた変数、関数、クラス等のこと。これを用いるために import / export を使う。

