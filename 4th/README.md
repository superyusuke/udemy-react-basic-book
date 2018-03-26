# Todo App の作成

![](/assets/todoApp.001.png)

## コンポーンントの構造
このアプリケーションは、以下のようにコンポーネントを組み合わせて作成されています。

- TodoApp.js (アプリケーション全体のためのコンポーネント)
    - AddTodo.js (state にtodo を追加するためのコンポーネント)
    - List.js (state を元に List を作成するコンポーネント)
    
## state の構造

- todos: todo リストの内容のための state
- nextId: 次に追加するリストの内容に付与する ID のための state

## state を変更するメソッドは親コンポーネントから子コンポーネントに渡す

state を変更するための「addTodo や deleteTodo」といったメソッドは、一番親になるコンポーネントである TodoApp にもたせて、子コンポーネントに渡していく。これが React 設計の基本。
     
## 手順1: TodoApp のコンポーネントを配置する

単純にコンポーネントを配置します。

https://codesandbox.io/s/m5jzz7nv0p

## 手順2: state を与え、List コンポーネントに渡す

https://codesandbox.io/s/q816304yn9

- TodoApp.js に state を持たせる
- this.state.todos を List に渡す
- List が、受け取った props を元に ul,li を返す

## 手順3: AddTodo コンポーネントを作り込む

https://codesandbox.io/s/xvpk08v9pw

```js
import React from "react";

export class AddTodo extends React.Component {
  constructor(props) {
    super(props);
    // input の内容のための state
    this.state = { title: "" };
  }

  render() {
    // form の内容を作り込む
    return (
      <div>
        <h2>AddTodo</h2>
        <form onSubmit={this.handleSubmit}>
          <input value={this.state.title} onChange={this.handleChange} />
          <input type="submit" value="Add to todo list" />
        </form>
      </div>
    );
  }

  // input の内容を変更した場合に発動するメソッド
  handleChange = event => {
    // value を取得する
    const title = event.target.value;
    this.setState({ title: title });
  };

  // submit した場合に発動するメソッド
  handleSubmit = event => {
    // ページ遷移を止める
    event.preventDefault();
    alert(this.state.title);
    this.setState({ title: "" });
  };
}

```




