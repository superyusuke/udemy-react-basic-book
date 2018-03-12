```js
// 伝統的な関数の書き方
function name1() {
  console.log("nanan");
}

// アロー関数
// => が矢印に似ていることから
const name2 = () => {
  console.log("name2");
};

//name2()

// 引数を与える場合
const name3 = (val) => {
  console.log(val);
};

//name3('passed value')

// 引数が一つの場合は () を省略可能
const name4 = val => {
  console.log(val);
};

//name4('passed value2')

// 引数が二つの場合は () を省略できない
const name5 = (val1, val2) => {
  console.log(val1, val2);
};

//name5('arg1', 'arg2' )

// return する場合
const name6 = () => {
  return "retunred value";
};

//console.log(name6())

// return する場合の省略記法
// return, {} を取り除き、
// return 内容を変数宣言と同じ行に配置する
const name7 = () => "retunred value2";

//console.log(name7())

// 1行だけの実行であればこのように書くことも可能
const name8 = () => console.log("console");

name8();
```