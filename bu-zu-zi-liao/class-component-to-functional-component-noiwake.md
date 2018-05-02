# Class Component と Functional Component の使いわけ

Class Component と Functional Component、どちらを選択するのが良いのかという質問をいただきましたのでご回答させていただきます。

まず以下のような場合は、確実に Class Component を用いる必要があります。これらの機能は Functional Component には持たせることができないからです。

#### Class Component を使う場合

* state を持たせる必要がある
* Lifecycle method を使う必要がある\(componentDidMount 等\)

反対に、こういったケース「以外」は全て Functional Component にすることができます。

#### Functional Component を使う場合

* Class Component にしなくてはいけない場合「以外」

ただし、必ずしも全て Functional Component にしなくてはいけないということはありません。例えば

