# 非同期処理

JavaScript 一度に一つのことを処理するシングルスレッドという方式なので、基本的に書かれた順に上から実行していきます。しかし一見すると、書かれた順番には実行されていないようにみえる処理があります。それが非同期処理です。

```js
setTimeout(() => {
  console.log("done", getSeconds());
}, 1000);
```

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



