# 非同期処理と Promise

JavaScript 一度に一つのことを処理するシングルスレッドという方式なので、基本的に書かれた順に上から実行していきます。しかし一見すると、書かれた順番には実行されていないようにみえる処理があります。それが非同期処理です。

例えば次のコードは、setTimeout を使っているので、console.log は 1000ms 後に実行されます。つまり、ある時間経過したら、何かを実行してね、とあらかじめお願いしておくような処理があるものを、非同期処理といいます。

```javascript
setTimeout(() => {
  console.log("done", getSeconds());
}, 1000);
```

こちらもよく見るコードですが、ユーザーのクリックを待ち受けています。  
このコードが実行された時には、当然ですがアラートは出ません。ユーザーがクリックするまで待って、された際にはアラートを出してね、という「予約を実行」しているわけです。

```javascript
import $ from "jquery";

$(".button").on("click", () => {
  alert("click");
});
```

先ほど書いたコードも非同期処理です。なぜなら「データを取得するのを待って」、  
取得できたら HTML を書き換えてね、という予約をしているからです。

```javascript
const url = "https://developer.mozilla.org/en-US/docs/Web/HTML";

axios.get(url).then(res => {
  console.log(res.data);
  document.body.innerHTML = res.data;
});
```

ある処理が終わった際に実行される関数のことを「コールバック」といいますが\(例えば setTimeout の例では、1000ms 後に実行される console.log\(\) の部分です\)、「コールバック」とは「折り返し電話」のことです。我々が非同期処理の際におこなっているのは、このコールバックと同じイメージで、「席が空いたら、連絡をしてね」という予約のお願いをしているわけです。

## コールバック地獄

さて、予約のお願いが、一個だけなら話はシンプルですが、予約が連鎖してくると、話は複雑に、そしてコードも複雑になっていきます。

八時になったらピザを頼んで、ピザが来たら田中さんに電話をしてね。そして田中さんがこれるようなら、コーラも改めて注文しておいて。

こんなふうに予約が連鎖してくると、コードはこうなります。

```javascript
setTimeout(() => {
  console.log("done1");
  setTimeout(() => {
    console.log("done2");
    setTimeout(() => {
      console.log("done3");
      setTimeout(() => {
        console.log("done4");
      }, 1000);
    }, 1000);
  }, 1000);
}, 1000);
```

コールバックの中で、さらにコールバックを必要をするコードを追加していくと、このように入れ子が深くなってしまいます。これは書くのも、読むのも、メンテナンスするのも大変です。

さて困りました…

## Promise を使ってコールバックを読みやすく書く

その解決方法の一つが「Promise」という仕組みを使うことです。

[https://codesandbox.io/s/yw43kj4rv1](https://codesandbox.io/s/yw43kj4rv1)

```javascript
// 現在の時間を取得するための補助的な関数
const getSeconds = () => new Date().getSeconds();

// 非同期処理を Promise を使って読みやすく書く
const async1 = num => {
  // Promise オブジェクトを作ってこれを返す
  // Promise オブジェクトに、コールバックを登録する
  return new Promise((resolve, reject) => {
    // start
    console.log("start" + num, getSeconds());
    // delayed
    setTimeout(() => {
      console.log("done" + num, getSeconds());
      // 処理が終わる場所で、resolve を実行する
      // ここで渡した引数が、then が受け取る引数になる
      // (このコードでは result に入る)
      resolve(num);
    }, 1000);
  });
};

// promise オブジェクトを作って実行する
async1(1)
  .then(result => {
    // resolve がきたら、then に移動する
    // さらに promise オブジェクトを返すことで、
    // 次の then につなげていく
    return async1(result + 1);
  })
  .then(result => {
    return async1(result + 1);
  });
```

詳しくは、Promise の資料を読んで欲しいのですが、手順をまとめると以下のようになります。

* 関数を作る。この関数は return new Promise で Promise インスタンスを作ってリターンする。
* Promise を作る際に、実行したい非同期処理をコールバックとして登録する。
* 非同期処理が終わる場所で resolve\(\) を実行する。
* 実行するには、この関数を呼び出して、Promise をインスタンス化する。
* resolve が実行されると、次の .then\(\) に実行が移動していく。
* 繋げるためには、次の then の中で、また新たな Promise インスタンスを作成して、リターンしてあげればいい

