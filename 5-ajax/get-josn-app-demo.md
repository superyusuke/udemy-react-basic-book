# JSON を取得し、その内容をレンダリングする React App の作成

* React App のボタンを押したら、HTTP リクエストをして、JSON を取得する
* 取得先は myjson.com \([http://myjson.com/](http://myjson.com/)\)
* myjson.com に、返す JSON を自分であらかじめ設定しておく
* 帰ってきたデータを state に保持させ、state を元にリストをレンダリングする

## JSON とは

JSON = JavaScript Object Notation

JavaScript のオブジェクトとは少し形式が違うが、基本的に JavaScript のオブジェクトを定義するための形式です。

```json
{
  "member": [
    {
      "name": "yusuke",
      "age": 30
    },
    {
      "name": "tanaka",
      "age": 40
    },
    {
      "name": "sasaki",
      "age": 50
    }
  ]
}
```

```js
// 通常の JavaScript オブジェクトの書き方

export const data = {
  member: [
    {
      name: "yusuke",
      age: 30
    },
    {
      name: "tanaka",
      age: 40
    },
    {
      name: "sasaki",
      age: 50
    }
  ]
};
```

### 特徴

* 必ず「""」ダブルクオーテーションを使うこと。「''」ではだめ。
* key も value も「""」でくくって、文字列にすること。
* コメントは使えない。
* トレイリングコンマはあってはダメ。 

#### ダメな例

```json
{
  // コメントは使えない
  member: [ // key を文字列ではないものにはできない
    {
      "name": "yusuke",
      "age": 30, // トレイリングコンマはダメ
    },
    {
      'name': 'tanaka', // シングルクオーテーションはダメ
      'age': 40
    },
    {
      "name": "sasaki",
      "age": 50
    }
  ]
}
```

JSON フォーマッター等で確認しましょう。

[https://jsonformatter.curiousconcept.com/](https://jsonformatter.curiousconcept.com/)

## MyJson というサービスで JSON を返すだけの API を作る

myjson.com \([http://myjson.com/](http://myjson.com/)\) を使用する。返す JSON の内容を自分で決めることができる

```json
{
  "member": [
    {
      "name": "nakanishi",
      "age": 30
    },
    {
      "name": "tanaka",
      "age": 40
    },
    {
      "name": "suzuki",
      "age": 50
    }
  ]
}
```

## Axios で MyJson にデータを取りに行く

https://codesandbox.io/s/jvyrz73y9y

* Dependencies => Add Dependencies => Axios を追加する

```js
import axios from "axios";

const url = "https://api.myjson.com/bins/159wqn";

axios.get(url).then(res => {
  console.log(res.data);
});
```


## データを元にレンダリングする React App を作る



