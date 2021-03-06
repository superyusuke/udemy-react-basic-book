# Component に store を connect する

[https://codesandbox.io/s/5ykr13wjp4](https://codesandbox.io/s/5ykr13wjp4)

## components/ImageList.js

受け取った URL を元に img 要素を作成するコンポーネント

```javascript
import React from "react";

const ImageList = ({ urlList }) => {
  const list = urlList.map(url => {
    return (
      <li key={url}>
        {url}
        <img src={url} alt="" />
      </li>
    );
  });
  return <ul>{list}</ul>;
};

export default ImageList;
```

## containers/ImageList.js

store を先ほど作成したコンポーネントに connect する

```javascript
import ImageList from "../components/ImageList";
import { connect } from "react-redux";

const mapStateToProps = state => {
  return {
    urlList: state.imageUrls
  };
};

export default connect(mapStateToProps, null)(ImageList);
```

## app.js

connect されたコンポーネントを使用する

```javascript
import React from "react";

import ImageList from "./containers/ImageList";

const App = () => {
  return (
    <div>
      App
      <ImageList />
    </div>
  );
};

export default App;
```

