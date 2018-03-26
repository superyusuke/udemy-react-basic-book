# 実践 H20 Component 1

https://codesandbox.io/s/8y2p8280wl

```js
import React from "react";
import { render } from "react-dom";

class H20 extends React.Component {
  constructor(props) {
    super(props);
    this.state = { temp: 15 };
  }

  render() {
    return (
      <div>
        <h2>{this.state.temp} 度</h2>
        <button onClick={this.onPlusClick}>+</button>
        <button onClick={this.onPlus10Click}>+10</button>
        <button onClick={this.onMinusClick}>-</button>
        <button onClick={this.onMinus10Click}>-10</button>
      </div>
    );
  }

  onPlusClick = () => {
    this.setState({ temp: this.state.temp + 1 });
  };

  onPlus10Click = () => {
    this.setState({ temp: this.state.temp + 10 });
  };

  onMinusClick = () => {
    this.setState({ temp: this.state.temp - 1 });
  };

  onMinus10Click = () => {
    this.setState({ temp: this.state.temp - 10 });
  };
}

render(<H20 />, document.getElementById("root"));
```