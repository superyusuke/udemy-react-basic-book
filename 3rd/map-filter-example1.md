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

// 新しい React Component を map を使って作成する

const Todos = ({ todos }) => {
  const list = todos.map(todo => {
    return (
      <li>
        {todo.id} {todo.title}
      </li>
    );
  });

  return <ul>{list}</ul>;
};

render(<Todos todos={todos} />, document.getElementById("root"));

```

