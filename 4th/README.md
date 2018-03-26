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
     
