```js
const reducer = (state = 0, action) => {
  switch (action.type) {
    case "PLUS_ONE":
      return state + 1;
    case "MINUS_ONE":
      return state - 1;
    default:
      return state;
  }
};

```