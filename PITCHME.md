# デザイナーに

# 覚えてほしい JS

---

## 経緯

昨今 JS フレームワークが流行る中で  
デザイナーがコーディングする際に  
JS を知っている事が求められるようになってきた

以前の HTML/CSS/JQuery の知識だけでは  
コーディングで躓くことが増えたように思われる

---

## ゴール

JS フレームワークでよく使われる  
基本的な JS を学ぶことによって  
コーディング時の無駄な躓きを減らすこと

---

## 注意事項

今回取り扱うのは ES2015 で  
基本的にエンジニアが環境構築をして  
ES2015 が使えるようになっていることを  
この講座では前提としている。

そのため webpack, babel などの  
環境構築面については対象外とする

---

## 目次

1. var / let / const

1. アロー関数

1. import / export

1. テンプレート文字列

1. map 関数

1. 分割代入

1. スプレッド演算子

---

## var, let, const

+++

### 目的

今までの JS では var しか無かったが  
ES2015 で let, const が増えた  
ここではその使い方をゆるく学ぶ

+++

### var

ES2015 以降 var を使うことはほぼ無い  
var はエラーの元で使わなくていいので  
もう忘れてください

+++

### let

後で再代入する可能性がある変数は let を使う

```javascript
let name = "島袋";
name = "山袋"; // OK
```

+++

### const

定数的な使い方をしたい場合は const を使う

```javascript
const name = "島袋";
name = "山袋"; // ERROR
```

+++

### まとめ

まずは const を使って  
無理そうなら let を使ってください

スコープの話とかあるんだけど  
とりあえず最低限これだけ覚えてください

---

## アロー関数

+++

### 目的

今まで **function** で  
関数を書いてきたと思われるが  
ES2015 では **アロー関数** という  
新しい記法を用いて書くことが多くなった  
この章ではその使い方を学んでいこう

+++

### 今までとの比較

```javascript
// 今まで
function hoge(x, y) {
  return x + y;
}

// アロー関数
const hoge = (x, y) => {
  return x + y;
};
```

+++

### return しかない場合 {} は省略可

```javascript
const hoge = (x, y) => x + y;
```

+++

### 引数が 1 つの場合 () は省略可

```javascript
const hoge = x => x;
```

+++

### 例えば React だと下記は全て同義

```javascript
function hoge(props) {
  return (
    <div>
      <h1>{props.title}</h1>
    </div>
  );
}

// prettier-ignore
const hoge = (props) => {
  return (
    <div>
      <h1>{props.title}</h1>
    </div>
  );
};

// prettier-ignore
const hoge = (props) => (
  <div>
    <h1>{props.title}</h1>
  </div>
);

// prettier-ignore
const hoge = props => (
  <div>
    <h1>{props.title}</h1>
  </div>
);

// prettier-ignore
const hoge = props =>
  <div>
    <h1>{props.title}</h1>
  </div>
```

+++

### まとめ

this のスコープが違うとか  
これも本当はいろいろあるんだけど  
とりあえず記述を簡素化できると  
覚えておいてください

---

## import / export

+++

### 目的

ある js ファイルから  
別の js ファイルに渡す変数や関数を  
**モジュール** と呼びます

この章ではそのモジュールの  
受け渡しの方法を学ぶ

+++

### import 側

例えば React を書くときに  
下記の記述を見たことはないだろうか？

```javascript
import React, { Component } from "react";
import { createStore, combineReducers } from "redux";
```

+++

### export 側

export 側をモジュールを見てみる  
（講座の便宜上勝手に書き換えている笑）

```javascript
// react
export default React;
export { Component };
```

```javascript
// redux
export { createStore, combineReducers };
```

+++

### {} が有るとき

export 側はこうする

```javascript
// パターン1
const Hoge = () => <div>hoge</div>;
const Fuga = () => <div>fuga</div>;
export { Hoge, Fuga };

// パターン2
export const Hoge = () => <div>hoge</div>;
export const Fuga = () => <div>fuga</div>;
```

+++

### {} が無いとき part1

export default を使う  
（ファイル内で 1 度しか使えない）

```javascript
// パターン1
const Hoge = () => <div>hoge</div>;
export default Hoge;

// パターン2
export default () => <div>hoge</div>;
```

+++

### {} が無いとき part2

{} が無い場合は import 側は勝手に命名可能

```javascript
// export (Hoge.js)
const Hoge = () => <div>hoge</div>;
export default Hoge;

// import
import MyFavoriteName from "./Hoge";
```

+++

### まとめ

こちらも細かい違いはありますが  
とりあえず上記を覚えておけば問題ない

---

## テンプレート文字列

+++

### 目的

この章は一瞬で終わる  
変数を使うときにもっと  
スマートにしようぜっていう章

+++

### 比較

```javascript
// 今まで
const protocol = "https://";
const yahoo = protocol + "www.yahoo.co.jp";

// スマート
const protocol = "https://";
const yahoo = `${protocol}www.yahoo.co.jp`;
```

+++

### まとめ

積極的に使おうぜ

---

## map 関数

+++

### 目的

繰り返しの list を作る場合に  
map 関数がよく使われる  
その使い方を学ぼう

+++

### パース

api から引っ張ってきたデータを

```javascript
{
  users: [
    { name: "島袋", age: 20 },
    { name: "山袋", age: 30 },
    { name: "海袋", age: 40 }
  ];
}
```

+++

### パース

こうしたい

```html
<ul>
  <li>島袋: 20歳</li>
  <li>山袋: 30歳</li>
  <li>海袋: 40歳</li>
</ul>
```

+++

### こうする

```javascript
response = fetch(url); // さっきのjsonが入る
return (
  <ul>
    {response.users.map(val => (
      <li>
        {val.name}: {val.age}歳
      </li>
    ))}
  </ul>
);
```

+++

### まとめ

このように配列の繰り返しに使われる  
api からデータを引っ張ってきて  
パースするときに頻出なので覚えよう

---

## 分割代入

+++

### 目的

配列やオブジェクトからデータを取り出し  
別の変数に代入することを簡単にするために  
分割代入というものがある

react でもよく使われるのでここで学ぼう

+++

### 普通のパターン

```javascript
const ages = [20, 30, 40];
const hatachi = ages[0];
const misoji = ages[1];
const yosoji = ages[2];
```

+++

### 分割代入パターン

```javascript
const ages = [20, 30, 40];
const [hatachi, misoji, yosoji] = ages;
```

+++

### react でよく使われるパターン

```javascript
// 下記データがあるとして
this.props = {
  name: "しまぶー",
  age: 25,
  body: {
    height: 175,
    weight: 60
  }
};

const { name, age, body: { height, weight } } = this.props;
```

+++

### まとめ

分割代入を使うことによって  
記述量を減らすことができる

---

## スプレッド演算子

+++

### 目的

「...」で表現される演算子で  
色々と便利なやつなんで覚えよう

+++

### 配列の操作が簡単

```javascript
// 今まで
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
Array.prototype.push.apply(arr1, arr2);

// スプレッド演算子
var arr1 = [0, 1, 2];
var arr2 = [3, 4, 5];
arr1.push(...arr2);
```

+++

### 関数の引数として使う

```javascript
function add(x, y, z) {
  console.log(x + y + z);
}
const args = [1, 2, 3];
add(...args); // 6
```

+++

### React でよく使われるやつ

```javascript
// こういう props があるとして
const props = {
  name: '島袋',
  age: 25',
}

// 従来
<MyComponent name={props.name} age={props.age} />

// スプレッド演算子
<MyComponent {...props} />
```

+++

### まとめ

簡素な記述ができる  
上記以外にも色んな場面で使われる

---

## おわりに

こんな感じで JS は  
昔とだいぶ記述が変わっているので  
基本的な部分だけでも覚えて  
快適コーディングできるようにしよう
