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

```js
import { connect } from "react-redux";

const Component = ({ someState, doSomeThing }) => {
  return <div onClick={() => doSomeThing("some")}>{someState}</div>;
};

const mapStateToProps = state => {
  return {
    someState: state
  };
};

const mapDispatchToProps = dispatch => {
  return {
    doSomeThing: some => {
      dispatch({ type: "DO_SOMETHING", payload: some });
    }
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(Component);

```

```js
store.dispatch({
  type: "DO_SOMETHING",
  payload: "something"
});
````