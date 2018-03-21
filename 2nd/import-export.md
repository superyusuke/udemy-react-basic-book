# import, export, js module



```js
import React from "react";
import { render } from "react-dom";

import { var1, function1, ReactComponent } from "./module";

console.log(var1);
function1();

render(<ReactComponent />, document.getElementById("root"));
```