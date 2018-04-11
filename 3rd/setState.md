# クリック時に state をsetState で変更する

[参考コード](https://codesandbox.io/s/2w4jn7y3kp)

先ほど書いた App では、 state は用いていましたが、state を変更する仕組みはありませんでした。そのため動的に変化する App ではありませんでした。

今回はさらに this.setState() を用いて state を変更する仕組みを追加していきましょう。クリックされた時に、state を変更します。


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
      // クリック時にメソッド（コールバック）を発動させるために
      // onClick を用いる
      <h2 onClick={this.onButtonClick}>
        {this.state.name} {this.props.age}
      </h2>
    );
  }

  // click 時に発動するメソッドとして指定したもの

  // JSX のコールバックに指定された場合には
  // ()=> という形で書き、this を意図した挙動にさせること
  onButtonClick = () => {
    // setState で state を変更する
    // setState にはオブジェクトを渡す
    this.setState({ name: this.state.name + "san" });
  };
}

render(<Human age="30" />, document.getElementById("root"));

```

## onClick アトリビュートを用いて、クリック時にメソッドを実行させる

- h2 をクリックした時に、onClickButton というメソッドを実行させる。
- クリックした時に何かをさせるには、onClick アトリビュートを用いる。
- JSX 内で使用される onClick, onChange, onSubmit 等に指定するメソッド(コールバック)は、[= () => というアローファンクションに似た方式](https://babeljs.io/docs/plugins/transform-class-properties/)で書くこと。そうしないと this が意図しない対象をさすためにエラーとなる。

```js
class Human extends React.Component {
  constructor(props) {
    super(props);
    this.state = { name: "Nakanishi" };
  }

  render() {
    return (
      // クリック時にメソッド（コールバック）を発動させるために
      // onClick を用いる
      <h2 onClick={this.onButtonClick}>
        {this.state.name} {this.props.age}
      </h2>
    );
  }

  // click 時に発動するメソッドとして指定したもの

  // JSX のコールバックに指定された場合には
  // ()=> という形で書き、this を意図した挙動にさせること
  onButtonClick = () => {
    // setState で state を変更する
    // setState にはオブジェクトを渡す
    this.setState({ name: this.state.name + "san" });
  };
}
```

## setState を用いて、state を更新する

- this.setState() というメソッドを用いて、state を更新する。
- このメソッドは自分では書いていないが、React.Component を extends (継承)した際に受け継がれたもの。
- this.setState() の引数には、state のうち、変更したいオブジェクトを指定する。(上書きされる)

```js

// state を変更するためには this.setState() を用いる
this.setState({ name: this.state.name + "san" });

```





