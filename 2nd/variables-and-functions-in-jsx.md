# 変数と関数を JSX  の中で使用する
[参考コード](https://codesandbox.io/s/6wkz67jky3)

```js
import React from 'react'
import { render } from 'react-dom'

const title = 'こんにちは世界'
const body = 'こちらが本文の内容です'

const returnStrings = val => {
  return val
}

const reactElement = (
  <div>
    <h2>{title}</h2>
    <p>{body}</p>
    <p>{returnStrings('これが渡した引数です')}</p>
  </div>
)

console.log(reactElement)

render(reactElement, document.getElementById('root'))

```

## 変数を使うためには　{} で囲む

{} で囲んで、変数を入れれば JS の変数として認識される。

```js
const title = 'こんにちは世界'
const reactElement = <h2>{title}</h2>
```

## {} の中は、JavaScript として認識される

{} の中は、JavaScript として認識されるので、関数も実行できる。

```js
const reactElement = <h2>{Math.random()}</h2>
```

```js
const returnStrings = () => {
  return '返された文字列です'
}

const reactElement = <h2>{returnStrings()}</h2>
```

## JSX は一つのタグしかだめ(子要素に複数タグがあるのはOK)

```js
//ダメ
const reactElement = <h2>title</h2><p>body</p>

// OK
const reactElement = (
  <div>
    <h2>title</h2>
    <p>body</p>
  </div>
)
```