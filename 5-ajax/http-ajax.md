# HTTP プロトコルと Ajax

## HTTP プロトコルとは

クライアント(例えば Chrome 等のウェブブラウザ)とサーバーが、World Wide Web（ウェブ）の世界で通信するためのプロトコル = 規約です。

![](/assets/http-ajax.001.png)

## いつどのように使われているか

- ブラウザのアドレスバーに入力 -> HTTP Request -> Server 
- a タグのリンクをクリックする -> HTTP Request -> Server

## 通常のブラウザから HTTP Request をした場合には、ブラウザを更新してしまう

通常のブラウザから HTTP Request をした場合にはブラウザを更新してしまいます。こうすると、せっかく React の App が様々な状態を持っていても、ページを遷移する際に情報を失ってしまってリセットされてしまいます。また、ブラウザからの通常の HTTP 通信は、同期通信なので、レスポンスがあるまで待たなくてはいけません。

## そこで Ajax / XMLHttpRequest object を使用した HTTP 通信

AJAX 二つの技術の組み合わせのことです。簡潔に言えば、「JavaScript でサーバーと非同期な通信をおこない、それによって得た情報を JavaScript で DOM に反映させることユーザーに表示する手法」です。

- ブラウザに組み込まれた XMLHttpRequest object を用いたサーバーとの非同期な HTTP 通信
- 受け取ったデータを用いて JavaScript で HTML DOM を変更する 



