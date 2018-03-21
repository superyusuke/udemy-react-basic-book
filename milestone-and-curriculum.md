## スケジュール

3スプリントで計画。

* Sprint 1  
    3/5 から 3/25 までの20日間
    ここまでの資料はすでに一回作ったことがある。
    マイク、動画編集、Udemy の操作なれることが目標。
    風邪と制作業務が重なって、一週間遅れをとる。
    3/21 時点で6割。

* Sprint 2  
    3/25 から 4/3 までの一週間

  * Ajax, Material UI, ローカル開発環境, Giphy で実践
    アプリケーション的にも複雑になり、量も多いので、ここをクリアーできないと、納期に間に合わない。ここで間に合わなければ、4月頭納品は難しい。ただ、基本的な動画作成フローに慣れるフェイズが終わり、速度アップを期待。

* Sprint 3  
    3/20 から 3/27 までの一週間

  * react-router
  * 開発者ツール
  * redux, redux todoApp
  * redux-thunk の実践 Giphy アプリ

    内容的には高度だが、すでにほとんど説明しているので、説明を簡略化でき、スムーズに進めれることを期待。Redux-thunk の説明が厳しいのと、アプリケーションが大きいので、時間かかる。

* ## Codesandbox で作る最速 React 開発環境

  sprint1.1 3/13 までに

  ブラウザ上で動く開発環境である CodeSandbox を使うことで、即 React 開発をスタートする。React の開発環境の構築でつまづく人が多いので、それを防ぐ。まずは React を書いてもらうところから始める。なお、本講義中盤で Create-react-app を用いたローカル開発環境の作り方も解説する。Webpack を用いた環境構築には他の講座に譲る。

  1. ### CodesandBox を使用する利点 3/6 済

     1. 開発環境構築は難しいのでそれを一旦避ける
     2. クラウド上で動いているのですぐに人に見せることができる
  2. ### 使い方

     1. github との連携 3/6 済

        必須ではないが、することでプロジェクトの管理が容易になる。またコード整形機能も使えるようになる。大きなプロジェクトを作るまでには連携をするよう促す。

     2. 構造、エディター、ショートカットの説明  
         1. index.js, index.html, フォルダ階層など構造の説明  
         1. JS をさしあたって動かす/  alert を出す done3/11
         1. 保存、フォーク、プロジェクト管理リスト done 3/11

* ## 初めての React App , React Component

  sprint1.2 3/13 までに

  1. import React, react-dom, render 3/11 done
  2. JSX とは何か 3/11 done
  3. Component とは何か 3/22 done
  4. ES2015 の基礎の確認
     1. import/export 3/11 done
     2. arrow function 3/11 done
  5. props で動的に値を受け取る
     1. props を与える、受ける 3/11 done
     2. \({}\)タイプの受け取り方 3/11 done

* ## State を持ち動的に変化するコンポーネントの作成

  sprint1.3 3/25 までに

  1. ### ES2015 の class の解説　3/20done
  2. ### React の class コンポーネント 3/20done

     1. state, constructor, super 3/20 done
     2. setState で表示を変えるだけのアプリをつくる 3/20
  3. ### state に関するより進んだ説明

     1. 状態を水・氷・蒸気で説明
     2. state で見た目が分岐するH2Oコンポーネントの作成していく
     3. CSS を導入, className, className を条件分岐

* ## 基礎的な Todo App の作成

  sprint1.4 3/25 までに

  1. ### 必要になる ES2015 の記法の学習

     1. map, filter
     2. \[..., {}\] spread operator, Array.concat\(\), Object.assign\(\)
  2. ### Component を組み合わせる
  3. ### state を下に渡していく
  4. ### state を変更するメソッドを下に渡していく

* ## Ajax, XMLHttpRequest で外部 API を叩いてデータを取得するアプリの作成

  sprint2.1 4/3 までに

  エンジニアに馴染みのある勉強会紹介サイト Connpass の API で記事取得するだけのアプリの作成。Ajax, XMLHttpRequest, 非同期通信, Promise 等々の説明。

  1. ### XMLHttpRequest とは
  2. ### promise, axios, ajax
  3. ### API とは
  4. ### Connpass API の使い方
  5. ### 取得したデータを展開する

* ## Material UI の使用

  sprint2.2 4/3 までに

  \(ブートストラップのようにあらかじめスタイリングされたコンポーネントです\)  
   超豪華な todoApp の作成をします。単なる見た目の問題なので App の機能はシンプルな方がいい。

  1. ### Material UI の設定
  2. ### 使い方
  3. ### todoApp に適応していく

* ## create-react-app を使ったローカル開発環境の作成

  sprint2.3 4/3 までに

  ここでついにローカル開発環境に移行。しかも簡単にできる create-react-app を使うことで、つまづきをなくす。Webpack 等々の設定はこの段階では不要と考える。

  1. ### Node のインストール

     1. Node のバージョン管理ツール nvm のインストール
     2. nvm 経由の Node.js のインストール
     3. nvm によるバージョンの切り替え
  2. ### npm, package.json の説明

     1. npm とはそもそも何か / JS エコシステム
     2. npm init, npm install, npm run 等の基本的な操作
  3. ### sass の導入

     1. npm script で scss =&gt; css に変換
     2. BEM で CSS を書いていく

* ## [giphy](https://giphy.com/) を使った画像検索アプリ

  sprint2.4 3/20 までに

  1. giphy は　API 経由で画像を返してくれるサービス
  2. 猫→猫の画像が帰って来る→それを表示するサービス

* ## React-router の導入

  sprint3.1 3/27 までに

  1. ただルーティングするだけの App を作る
  2. history API
     1. push, query の利用等々
     2. query から値を取得して表示
     3. 入力した文字列を URL にプッシュ

* ## 開発者ツールの使い方

  sprint3.2 3/27 までに

  1. Chrome の React 開発者ツールのインストールと説明
  2. JS のデバッグ
  3. CSS, Element を確認する方法

* ## Redux, React + Redux の導入

  sprint3.3 3/27 までに

  1. Provider, createStore, reducer, connect を先に React に組み込んでしまう
  2. Reducer の仕組み、 dispatch の仕組み
  3. 数字が増えるだけのカウンターを Redux で組む
  4. redux 公式ドキュメントにある todoApp の簡易版を作成する
     1. combineReducer, actionCreator, connect 等々
     2. Presentational と Container コンポーネント
     3. 最後に redux-devtool をインストールする（今後の開発のために）

* ## Giphy アプリを Redux, Redux-router, Redux-thunk, Aiox で作る

  sprint3.3 3/27 までに

  総決算。非同期処理\(XMLHttpRequest 等\)を redux-thunk で処理するのが一番のテーマ。Material UI も使用する予定。

  1. Redux-thunk の導入。ミドルウェアの説明。



