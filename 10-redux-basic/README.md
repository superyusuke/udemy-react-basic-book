```js
import { Provider } from "react-redux";
import { createStore } from "redux";
import reducer from "./reducer";

const store = createStore(reducer);

render(
  <Provider store={store}>
    <App />
  </Provider>,
  document.getElementById("root")
);

```