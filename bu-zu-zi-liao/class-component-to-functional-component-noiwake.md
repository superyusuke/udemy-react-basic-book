# Class Component と Functional Component の使いわけ

Class Component と Functional Component、どちらを選択するのが良いのかという質問をいただきましたのでご回答させていただきます。

### Class Component を使う場合

まず以下のような場合は、確実に Class Component を用いる必要があります。これらの機能は Functional Component には持たせることができないからです。

* state を持たせる必要がある
* Lifecycle method を使う必要がある\(componentDidMount 等\)

```javascript
class Component extends React.Component {
    constructor(props){
        super(props)
        this.state = {name: ''}
    }
    
    componentDidMount() {...}
    
    calcurlate() {...}
    
    maltiply() {...}
    
    render() {...}
}
```

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
    
    maltiply() {...}
    
    render() {...}
}
```

### props を元に render するだけのものは Functional Component にする方が良い

props を受け取って、それを元にレンダーするだけの Component であれば、Functional に書いた方が基本的に良いと思います。

```javascript
const Component = ({title, day, imageUrl}) => {
    const alt = `${title} ${day}`
    return <img href={imageUrl} alt={alt}/>
}
```

### ただし最後は任意

以上のような原則はありますが、最終的にはどちらを選択しても問題ありません。参考になれば幸いです。

