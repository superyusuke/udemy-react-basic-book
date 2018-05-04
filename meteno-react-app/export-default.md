# export default

[https://codesandbox.io/s/93qnn3wyzp](https://codesandbox.io/s/93qnn3wyzp)

### export default というシンタックスについて

export default と書くシンタックスがあり、先ほど説明したものとは少し異なります。大きな違いは以下の通りです。

* export default したものに関しては、import するときに {} を使わない。
* 1 ファイル内で、1 export default だけしかできない。\(通常の export は複数できる\)
* そのため、1ファイルに1コンポーネントだけを作る場合には、default を使う場合がスタンダード

```javascript
// index.js

import React from "react";
import { render } from "react-dom";
// export default のパターン
import ClassComponent1 from "./ClassComponent1";
import ClassComponent2 from "./ClassComponent2";
// export (default ではない)パターン
import { ClassComponent3 } from "./ClassComponent3";

render(
  <div>
    <ClassComponent1 />
    <ClassComponent2 />
    <ClassComponent3 />
  </div>,
  document.getElementById("root")
);
```

### export default するパターン

```javascript
// ClassComponent1.js

import React from "react";

// class の定義をすると同時に 
// export default する書き方
export default class ClassComponent extends React.Component {
  render() {
    return <div>ClassComponent</div>;
  }
}

```

```javascript
// ClassComponent2.js

import React from "react";

// 一旦 class の定義をしてから
class ClassComponent2 extends React.Component {
  render() {
    return <div>ClassComponent2</div>;
  }
}

// 定義した class を export default するやり方
export default ClassComponent2;
```

### export default 「しない」パターン

```javascript
// ClassComponent3.js

import React from "react";

// default はしない export
export class ClassComponent3 extends React.Component {
  render() {
    return <div>ClassComponent3</div>;
  }
}
```

