# map と filter

## map

[https://codesandbox.io/s/ykzkmjkmq9](https://codesandbox.io/s/ykzkmjkmq9)

map は配列に対して実行できる JavaScript の組み込みメソッド\(元から用意されているメソッド\)で、配列の内容を元に**「新しい配列」**を作るために使用します。

```javascript
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

## filter

[https://codesandbox.io/s/qq7j1k06p4](https://codesandbox.io/s/qq7j1k06p4)

map は配列に対して実行できる JavaScript の組み込みメソッド\(元から用意されているメソッド\)で、配列を元に **「**`true`** を返した場合の要素だけが採用された」**新しい配列を作るために使用します。

```javascript
const array1 = [1, 2, 3, 4, 5];

const newArray1 = array1.filter((output, index) => {
  return output > 3;
});

console.log(newArray1);

const array2 = ["nakanishi", "Hurukawa", "Tanaka"];

const newArray2 = array2.filter((output, index) => {
  return output === "nakanishi";
});

console.log(newArray2);

const newArray3 = array2.filter((output, index) => {
  return output.length > 7;
});

console.log(newArray3);
```

