# React Class Component の書き方

[参考コード](https://codesandbox.io/s/9jo8jz0q94)

```javascript
import React from "react";
import { render } from "react-dom";

// extend で性質を受け継ぐ
class Human extends React.Component {
  constructor(props) {
    super(props);
    // 必ずオブジェクトを与えること
    this.state = { name: "Nakanishi" };
  }

  // render は必須
  // コンポーネントが呼び出された時に返す内容
  render() {
    return (
      <h2>
        // state は内部の値 // props は外部から受け取った値
        {this.state.name} {this.props.age}
      </h2>
    );
  }
}

render(<Human age="30" />, document.getElementById("root"));
```

## React.Component を拡張 = extends する

class 宣言から始まり constructor を持つ点は同じだが、加えて `extends React.Component` する必要がある。これによって単なるクラスではなく、React Component に必要な諸性質を受け継いだクラスを作成することができる。

さらに constructor は props を引数にとり、内部で `super(props)` も実行すること。`super(props)` により extends した元のクラスの性質を受け継ぎつつ、props も受け取る。

```javascript
class Human extends React.Component {
  constructor(props) {
    super(props);
  }
}
```

## render メソッドは必須

必ず render メソッドを持つこと。このメソッドが、コンポーネントが呼び出された際に render する内容となる。

```javascript
class Human extends React.Component {
  constructor(props) {
    super(props);
  }

  render() {
    return <h2>Human</h2>
  }
}
```

## state を与える

```javascript
class Human extends React.Component {
  constructor(props) {
    super(props);
    // 必ずオブジェクトを与えること
    this.state = { name: "Nakanishi" };
  }

  render() {
    return (
      <h2>
        // state を参照する
        {this.state.name} {this.props.age}
      </h2>
    );
  }
}

render(<Human age="30" />, document.getElementById("root"));
```

