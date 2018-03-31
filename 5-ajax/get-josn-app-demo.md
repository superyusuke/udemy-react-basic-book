# JSON を取得し、その内容をレンダリングする React App の作成

- React App のボタンを押したら、HTTP リクエストをして、JSON を取得する
- 取得先は myjson.com (http://myjson.com/)
- myjson.com に、返す JSON を自分であらかじめ設定しておく
- 帰ってきたデータを state に保持させ、state を元にリストをレンダリングする

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