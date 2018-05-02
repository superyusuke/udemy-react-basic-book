# Class Component と Functional Component の使いわけ

Class Component と Functional Component、どちらを選択するのが良いのかという質問をいただきましたのでご回答させていただきます。

### Class Component を使う場合

まず以下のような場合は、確実に Class Component を用いる必要があります。これらの機能は Functional Component には持たせることができないからです。

* state を持たせる必要がある
* Lifecycle method を使う必要がある\(componentDidMount 等\)

### Functional Component を使う場合

反対に、こういったケース「以外」は全て Functional Component にすることができます。

* Class Component にしなくてはいけない場合「以外」

### しかしメソッドが多い場合には Class Component の方が見通しは良い

ただし、必ずしも全て Functional Component にしなくてはいけないということはありません。例えば「state を持たず、Lifecycle method も使用しない」が、メソッドは複数持つような場合です。こういった場合には Class を使って書いた方が見通しは良くなります。

```javascript
class Component extends React.Component {
    constructor(props){
        super(props)
    }
    
    calcurlate() {...}
    
    
    render() {...}
}
```



