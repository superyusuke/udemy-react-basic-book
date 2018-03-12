# JSX と React Element について

```js
import React from 'react'
import { render } from 'react-dom'

const reactElement = <h2>こんにちは世界</h2>

console.log(reactElement)

render(reactElement, document.getElementById('root'))
```

## JSX は HTML でも JavaScript でもない

`<h2>こんにちは世界</h2>` という部分は、HTML でも JavaScript でもない。.js ファイルに HTML は書けないはずだし、JavaScript としては定義されていない謎の値、つまり変数でも関数でもオブジェクトでもない謎の文字であるので、JavaScript でもない。

ではなぜ機能するかというと、JSX を開発環境\(今回ならば CodeSandbox ですし、ゆくゆくは Babel がその役割を担うことになります\)が認識して、ReactElement にコンパイルしてくれて、結果 JavaScript のオブジェクトに変換してくれているからなのです。

## JSX は開発環境がコンパイルして、JavaScript のオブジェクトに変換してくれる

JSX は開発環境がコンパイルして、JavaScript のオブジェクトに変換してくれるので、結果的には単なる JavaScript になっている。

そのため、変数に代入できる。

```js
const reactElement = <h2>こんにちは世界</h2>
```

なのでその値を、render\(\)に与えて、使用可能。

```js
render(reactElement, document.getElementById('root'))
```

## reactElement は単なる JavaScript Object

コンソールで表示するとわかるが、単なるオブジェクト。これを render\(\) が解釈して、本当の HTML に変換して、出力している。

```js
console.log(reactElement)
```



