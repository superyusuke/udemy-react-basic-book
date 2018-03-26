# map と filter の実践

## filter

https://codesandbox.io/s/jl8v3n7r6y

```js
import React from "react";
import { render } from "react-dom";

const todos = [
  { id: 1, title: "title1" },
  { id: 2, title: "title2" },
  { id: 3, title: "title3" },
  { id: 4, title: "title4" }
];

const deleteTargetId = 3;

// filter を使って
// deleteTargetId 以外のものだけを採用する

const deletedArray = todos.filter(todo => todo.id !== deleteTargetId);

console.log(deletedArray);

```

## map

https://codesandbox.io/s/2wr8mq3nqy

```js
import React from "react";
import { render } from "react-dom";

const todos = [
  { id: 1, title: "title1" },
  { id: 2, title: "title2" },
  { id: 3, title: "title3" },
  { id: 4, title: "title4" }
];

const deleteTargetId = 3;

const deletedArray = todos.filter(todo => todo.id !== deleteTargetId);

console.log(deletedArray);

// 新しい React Component である Todos を 
// map を使って作成する

const Todos = ({ todos }) => {
  // 一旦 List へ、受け取った配列(todos)を元に
  // li 要素を複数保持した、新しい配列を入れる
  const list = todos.map(todo => {
    return (
      <li>
        {todo.id} {todo.title}
      </li>
    );
  });

  // 先ほど作った list を使用する
  // この部分が実際にレンダリングされる内容
  return <ul>{list}</ul>;
};

render(<Todos todos={todos} />, document.getElementById("root"));

```

