# 最小限の React Application の実装

[参考コード](https://codesandbox.io/s/ypz99xk111)

## 必要のないものを消す

CodeSandBox で React を選んで起動した後に、必要のないファイル、コードを削除する。

* index.js の中身を全て消す
* hello.js をファイルごと削除

## 最小限の React App を実装する

### import で必要な関数等を読み込む

ES2015\(ES6\) の記法である `import` を使って、JavaScript のモジュールを `index.js` の中で使えるようにするために、読み込む。\( `import` に関しては後述します。\)

```js
// index.js
import React from 'react'
import { render } from 'react-dom'
```

## 読み込んだ render 関数を使って、React App をレンダリングする

```js
// index.js
import React from 'react'
import { render } from 'react-dom'

render(<h2>こんにちは世界</h2>, document.getElementById('root'))
```

### render\(\) について

`import { render } from 'react-dom'` で読み込んだものを早速使う。

React-dom の render\(\) は、引数を2つ必要とする。一つ目は、JSX で書かれたコンテンツ。\(JSXについては後述するが、ほぼ HTML と同じ記法でコンテンツを規定する\)  二つ目は、React Application を紐づける対象。これは DOM Element で指定する。

```js
render(JSX, target)
```

結果次のようになる

```js
render(<h2>こんにちは世界<h2/>, document.getElementById('root'))
```



