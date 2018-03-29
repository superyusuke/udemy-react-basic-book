# 非同期処理

JavaScript 一度に一つのことを処理するシングルスレッドという方式なので、基本的に書かれた順に上から実行していきます。しかし一見すると、書かれた順番には実行されていないようにみえる処理があります。それが非同期処理です。

例えば次のコードは、setTimeout を使っているので、console.log は 1000ms 後に実行されます。つまり、ある時間経過したら、何かを実行してね、とあらかじめお願いしておくような処理があるものを、非同期処理といいます。

```js
setTimeout(() => {
  console.log("done", getSeconds());
}, 1000);
```

こちらもよく見るコードですが、ユーザーのクリックを待ち受けています。
このコードが実行された時には、当然ですがアラートは出ません。ユーザーがクリックするまで待って、された際にはアラートを出してね、という予約を実行しているわけです


```js
import $ from "jquery";

$(".button").on("click", () => {
  alert("click");
});
```

```js
const url = "https://developer.mozilla.org/en-US/docs/Web/HTML";

axios.get(url).then(res => {
  console.log(res.data);
  document.body.innerHTML = res.data;
});
```

