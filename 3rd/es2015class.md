#ES2015 のクラス構文

[参考コード](https://codesandbox.io/s/rjon921l5q)

React.Component を ES2015 の class 構文で書く前に、単なる JavaScript の ES2015 class 構文を復習します。

```js
// class クラスネームで class を作成する
class Human {
  // constructor はクラスからインスタンスを作成した時に実行される
  constructor(name, age) {
    // this は作成されたインスタンスを指す
    this.name = name;
    this.age = age;
  }

  // クラスメソッド
  // クラスが持つファンクションのこと
  callMyProfile() {
    // 自分自身の値を参照するためにここでも this を使う
    console.log(this.name, this.age);
  }
}

// class からインスタンスを作成するために new 演算子を使う
// その際に引数も与える
const Nakanishi = new Human("Nakanishi", 33);

// console.log(Nakanishi.name);
// console.log(Nakanishi.age);

const Tanaka = new Human("Tanaka", 43);

// console.log(Tanaka.name);
// console.log(Tanaka.age);

// クラスメソッドにアクセスする
Nakanishi.callMyProfile();
Tanaka.callMyProfile();

```

## 最小限のクラスの作成

何もプロパティを持たない Human というクラスの作成と、Human クラスからインスタンスを作成し、Nakanishi という変数に代入する方法。

```js
// クラスを定義する
class Human() {
  constructor() {}
}

// new 演算子を使って class からインスタンスを作成する
const Nakanishi = new Human()
```

## new でインスタンスを作成する際に、引数を渡し、インスタンスのプロパティにアサインする

```js
class Human() {
  constructor(name, age) {
    // this は new で作成されたインスタンスを指す
    // つまり自分自身
    this.name = name
    this.age = age
  }
}

const Nakanishi = new Human('Nakanishi', 33)
console.log(Nakanishi.name + Nakanishi.age)
```

## class が持つファンクション = class method を定義する

```js
class Human() {
  constructor(name, age) {
    this.name = name
    this.age = age
  }
  
  // constructor の外でメソッドは定義すること
  callMyProfile() {
    console.log(this.name + this.age)
  }
}

const Nakanishi = new Human('Nakanishi', 33)
// クラスメソッドの呼び出し
Nakanishi.callMyProfile()
```