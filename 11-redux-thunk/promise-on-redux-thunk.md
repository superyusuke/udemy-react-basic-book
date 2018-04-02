
```js
// axios をインポート
import axios from "axios";

export const plus = num => {
  return { type: "PLUS", payload: { num: num } };
};

export const minus = num => {
  return { type: "MINUS", payload: { num: num } };
};

export const asyncMinus = num => {
  return dispatch => {
    setTimeout(() => {
      dispatch({ type: "MINUS", payload: { num: num } });
    }, 1000);
  };
};

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