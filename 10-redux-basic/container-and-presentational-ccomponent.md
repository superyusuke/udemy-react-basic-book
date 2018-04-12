# Container Component と Presentational Component

参考翻訳記事

http://better-than-i-was-yesterday.com/presentational-and-container-components/

コード

https://codesandbox.io/s/o5rok9m2y9

## ロジックと見た目を切り分ける

** Presentational Component **、つまり見た目を担当するコンポーネントは、ロジックに関与しないようにします。

** Container Component ** が、Presentational Component にロジックを与える役割を担います。

プログラミングの原則として、疎結合 = つまり、各機能が切り分けられている状態を目指すことが推奨されます。Container Component と Presentational Component に分けることで、見た目とロジックを切り分けることができます

こうすることで、例えばデザイナー、マークアップ担当者は見た目の挙動だけを担当し
フロントエンドエンジニアはロジックだけを担当する、といった作業が容易になります。(プログラミングはそんなに簡単にはいきませんが…)

ここでは、Container Component は、Presentatinal Component に対して redux の store を connect する役割だけを担っています。

### components/App.js

```js
import React from "react";

const App = ({ number, plus, minus }) => (
  <div>
    <h2>App {number}</h2>
    <button
      onClick={() => {
        plus(10);
      }}
    >
      + 10
    </button>
    <button
      onClick={() => {
        minus(10);
      }}
    >
      - 10
    </button>
  </div>
);

export default App;

```

### containers/App.js


```js
import App from "../components/App";
import { connect } from "react-redux";

const mapStateToProps = state => {
  return {
    number: state
  };
};

const mapDispatchToProps = dispatch => {
  return {
    plus: num => {
      dispatch({ type: "PLUS", payload: { num: num } });
    },
    minus: num => {
      dispatch({ type: "MINUS", payload: { num: num } });
    }
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(App);

```

### index.js

```js
import React from "react";
import { render } from "react-dom";

import { createStore } from "redux";
import reducer from "./reducer";

import { Provider } from "react-redux";

// containers のほうを使う
import App from "./containers/App";

const store = createStore(reducer);

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
);

```
