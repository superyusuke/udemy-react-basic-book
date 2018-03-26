# Todo App の作成

![](/assets/todoApp.001.png)

## コンポーンントの構造
このアプリケーションは、以下のようにコンポーネントを組み合わせて作成されています。

- TodoApp.js (アプリケーション全体のためのコンポーネント)
    - AddTodo.js (state にtodo を追加するためのコンポーネント)
    - List.js (state を元に List を作成するコンポーネント)
    
## state の構造と変更

- todos: todo リストの内容のための state
- nextId: 次に追加するリストの内容に付与する ID のための state
     
