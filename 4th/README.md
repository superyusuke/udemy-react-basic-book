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

state を変更するための「addTodo や deleteTodo」といったメソッドは、一番親になるコンポーネントである TodoApp にもたせて、子コンポーネントに渡していく。これが React 設計の基本です。
     
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

## 手順4: state を変更するメソッドを作成し、子コンポーネントに渡す

https://codesandbox.io/s/8l8jvmy36l

TodoApp.js 内の state を変更するメソッド

```js
addTodo = title => {
    this.setState({
      todos: [...this.state.todos, { id: this.state.nextId + 1, title: title }],
      nextId: this.state.nextId + 1
    });
  };
  
// 新しい配列を作成するシンタックス
// 配列に、オブジェクトを追加し、新規配列を作成する
[...配列, {新しく追加したいオブジェクト}]

```

同じく TodoApp.js 内で addTodo メソッドを、AddTodo コンポーネントに渡す

```js
render() {
    // state を変更するための addTodo メソッドを
    // AddTodo コンポーネントに渡す
    return (
      <div>
        <h2>TodoApp</h2>
        <AddTodo addTodo={this.addTodo} />
        <List todos={this.state.todos} />
      </div>
    );
  }
```

AddTodo.js 内で受け取ったメソッドを実行する

```js
handleSubmit = event => {
    event.preventDefault();
    // 親コンポーネントから受け取った state を変更するメソッドを実行する
    // 受け取ったものなので props の中にある
    this.props.addTodo(this.state.title);
    this.setState({ title: "" });
  };
```

## 手順5: todo を削除するメソッドを作成し、子コンポーネントに渡す

https://codesandbox.io/s/jlwk292mw

TodoApp.js

```js
// 削除するメソッドの追加
// filter を使って、id が一致するものを取り除く
  deleteTodo = id => {
    this.setState({
      todos: this.state.todos.filter(todo => {
        return todo.id !== id;
      })
    });
  };
```

```js
render() {
    // deleteTodo を子コンポーネントに渡す
    return (
      <div>
        <h2>TodoApp</h2>
        <AddTodo addTodo={this.addTodo} />
        <List deleteTodo={this.deleteTodo} todos={this.state.todos} />
      </div>
    );
  }
```

List.js

```js
// button を追加し、
// click 時に 受けとった deleteTodo を実行する
  render() {
    const list = this.props.todos.map(todo => {
      return (
        <li>
          #{todo.id} {todo.title}{" "}
          <button
            onClick={() => {
              this.props.deleteTodo(todo.id);
            }}
          >
            delete
          </button>
        </li>
      );
    });
```




