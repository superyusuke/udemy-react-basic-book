# store を作る

## 動画 1

https://codesandbox.io/s/0q54o9lxw0

index.js

```js
import React from "react";
import { render } from "react-dom";

import App from "./App";

import { createStore } from "redux";

import { Provider } from "react-redux";

// まだ rootReducer がないのでエラーになる
const store = createStore(rootReducer);

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
);
```

App.js
```js
import React from "react";

const App = () => {
  return <div>App</div>;
};

export default App;
```

## 動画2

