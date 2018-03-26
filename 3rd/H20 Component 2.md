# 実践 H20 Component 2

https://codesandbox.io/s/50o76xpy6x

```js
import React from "react";
import { render } from "react-dom";

class H20 extends React.Component {
  constructor(props) {
    super(props);
    this.state = { temp: 15 };
  }

  H20State(temp) {
    if (temp <= 0) {
      return "ice";
    }

    if (100 <= temp) {
      return "steam";
    }

    return "water";
  }

  render() {
    return (
      <div>
        <h2>
          phase: {this.H20State(this.state.temp)},{this.state.temp} 度
        </h2>
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