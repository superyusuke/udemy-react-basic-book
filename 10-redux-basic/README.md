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

```js
const reducer = (state = 0, action) => {
  switch (action.type) {
    case "DO_SOMETHING":
      return state + 1;
    default:
      return state;
  }
};

export default reducer;

```