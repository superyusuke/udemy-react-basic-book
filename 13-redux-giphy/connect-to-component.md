# コンポーネントに store を connect する

https://codesandbox.io/s/5ykr13wjp4

### components/ImageList.js

```js
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