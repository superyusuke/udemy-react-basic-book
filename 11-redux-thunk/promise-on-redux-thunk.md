# Promise を Redux-thunk 上で活用する

https://codesandbox.io/s/jxwyxr9vv

## redux-thunk を使って任意のタイミングでアクションを発行する

actions/index.js

```js
// axios をインポート
import axios from "axios";

export const changeTitle = title => {
  return { type: "CHANGE_TITLE", payload: { title: title } };
};

// Axios でデータを取得する
export const getJson = () => {
  return dispatch => {
    // まずロード開始のためのアクションを発行する
    dispatch({ type: "WAIT" });
    const url = "https://api.myjson.com/bins/159wqn";

    axios.get(url).then(res => {
      // データが取得できたら、
      // そのデータを元にタイトルを変更するアクションを発行する
      dispatch(changeTitle(res.data.member[0].name));
    });
  };
};

```

### Reducer を変更する

reducers/title.js

```js
const title = (state = "test title", action) => {
  switch (action.type) {
    // title を変更するアクションを受ける
    case "CHANGE_TITLE":
      return action.payload.title;

    // title を wait にするアクションを受ける
    case "WAIT":
      return "Wait";

    default:
      return state;
  }
};

export default title;

```

### containers/App.js の修正

```js
import App from "../components/App";
import { connect } from "react-redux";

// getJson を読み込む
import { minus, plus, asyncMinus, getJson } from "../actions";

const mapStateToProps = state => {
  return {
    number: state.number,
    day: state.day,
    title: state.title
  };
};

const mapDispatchToProps = dispatch => {
  return {
    plus: num => {
      dispatch(plus(num));
    },
    minus: num => {
      dispatch(minus(num));
    },
    asyncMinus: num => {
      dispatch(asyncMinus(num));
    },
    getJson: () => {
      // 追加する
      dispatch(getJson());
    }
  };
};

export default connect(mapStateToProps, mapDispatchToProps)(App);

```

### components/App.js の修正

