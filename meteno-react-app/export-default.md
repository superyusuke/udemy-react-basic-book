# export default

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

