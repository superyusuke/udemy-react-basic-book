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