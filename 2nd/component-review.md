# 2章の復習

[参考コード](https://codesandbox.io/s/3xlop5o8p1)

### index.js

```js
import React from "react";
import { render } from "react-dom";

import { ReactComponent } from "./ReactComponent";

render(
  <ReactComponent name="nakanishi" music="jazz" />,
  document.getElementById("root")
);

```

### ReactComponent.js

```js
import React from "react";

export const ReactComponent = ({ name, music }) => (
  <div>
    {name} {music}
  </div>
);

```