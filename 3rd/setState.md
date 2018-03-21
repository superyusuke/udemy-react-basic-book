# クリック時に state をsetState で変更する

[参考コード](https://codesandbox.io/s/2w4jn7y3kp)

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