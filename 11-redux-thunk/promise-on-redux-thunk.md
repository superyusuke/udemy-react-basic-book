
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