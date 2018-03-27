# HTTP プロトコルと Ajax

## HTTP プロトコルとは

クライアント(例えば Chrome 等のウェブブラウザ)とサーバーが、World Wide Web（ウェブ）の世界で通信するためのプロトコル = 規約です。

![](/assets/http-ajax.001.png)

## いつどのように使われているか

- ブラウザのアドレスバーに入力 -> HTTP Request -> Server 
- a タグのリンクをクリックする -> HTTP Request -> Server

## 通常のブラウザから HTTP Request をした場合には、ブラウザを更新してしまう

通常のブラウザから HTTP Request をした場合にはブラウザを更新してしまいます。こうすると、せっかく React の App が様々な状態を持っていても、ページを遷移する際に情報をしなってしまってリセットされてしまいます



