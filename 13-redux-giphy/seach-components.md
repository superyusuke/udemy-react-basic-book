# Search コンポーネントの作成

https://codesandbox.io/s/zn9ymy41x3

### /components/search.js 
 
 ```js
 import React from "react";

class Search extends React.Component {
  constructor(props) {
    super(props);
    this.state = { title: "" };
  }

  render() {
    return (
      <div>
        <form onSubmit={this.handleSubmit}>
          <input value={this.state.title} onChange={this.handleChange} />
          <input type="submit" value="Find Your GIFs" />
        </form>
      </div>
    );
  }

  handleChange = event => {
    const title = event.target.value;
    this.setState({ title: title });
  };

  handleSubmit = event => {
    event.preventDefault();
    //this.props.addTodo(this.state.title);
    this.setState({ title: "" });
  };
}

export default Search;
```

### app.js

作ったコンポーネントを使用する

```js
import React from "react";

import ImageList from "./containers/ImageList";

// Search Component を追加する
import Search from "./components/Search";

const App = () => {
  return (
    <div>
      App
      <Search />
      <ImageList />
    </div>
  );
};

export default App;

```