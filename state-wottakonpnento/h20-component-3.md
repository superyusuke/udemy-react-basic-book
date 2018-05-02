# H20 Component 3

[https://codesandbox.io/s/pw3k3nvm0](https://codesandbox.io/s/pw3k3nvm0)

```javascript
import React from "react";
import { render } from "react-dom";

import "./App.css";

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
      <div className={this.H20State(this.state.temp)}>
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

App.css

```css
.ice {
  background-color: blue;
}

.water {
  background-color: blueviolet;
}

.steam {
  background-color: red;
}
```

