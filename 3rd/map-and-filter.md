# map と filter

https://codesandbox.io/s/ykzkmjkmq9

## map

map は配列に対して実行できる JavaScript の組み込みメソッド(元から用意されているメソッド)で、配列の内容を元に新しい配列を作るために使用します。


```js
const array1 = [0, 1, 2, 3, 4];

const newArray1 = array1.map((output, index) => {
  return `${index}番目は${output}です。`;
});

console.log(newArray1);

const array2 = ["tanaka", "nakanishi", "sasaki", "koyama", "oda"];

const newArray2 = array2.map((output, index) => {
  return `${index}番目は${output}さんです。`;
});

console.log(newArray2);


```