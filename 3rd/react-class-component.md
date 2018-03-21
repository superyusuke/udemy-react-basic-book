# React Class Component の書き方

[参考コード](https://codesandbox.io/s/9jo8jz0q94)

```js
import React from "react";
import { render } from "react-dom";

class Human extends React.Component {
  constructor(props) {
    super(props);
    this.state = { name: "Nakanishi" };
  }

  render() {
    return (
      <h2>
        {this.state.name} {this.props.age}
      </h2>
    );
  }
}

render(<Human age="30" />, document.getElementById("root"));

```

## React.Component を拡張 = extends する

class 宣言から始まり constructor を持つ点は同じだが、加えて `extends React.Component` する必要がある。これによって単なるクラスではなく、React Component に必要な諸性質を受け継いだクラスを作成することができる。

さらに constructor は props を引数にとり、内部で `super(props)` も実行すること。`super(props)` により extends した元のクラスの性質を受け継ぐ。

```js
class Human extends React.Component {
  constructor(props) {
    super(props);
  }
}
```

## render メソッドは必須

必ず render メソッドを持つこと。このメソッドが、コンポーネントの render する内容となる。

```js
class Human extends React.Component {
  constructor(props) {
    super(props);
  }
  
  render() {
    return <h2>Human</h2>
  }
}
```


