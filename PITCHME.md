# デザイナーに覚えてほしい JS

---

## 経緯

昨今 JS フレームワークが流行る中で  
デザイナーがコーディングする際に  
JS を知っていることが求められるようになってきた

以前の HTML/CSS/JQuery の知識だけでは  
コーディングで躓くことが増えたように思われる

この講座は JS フレームワークでよく使われる  
基本的な JS を学ぶことによって  
コーディングでの無駄な躓きを減らすことを目的とする

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

1. アロー関数

1. import / export

1. テンプレート文字列

1. map 関数

1. スプレッド演算子

1. 分割代入

---

## 1. アロー関数

+++

### 1 章の目的

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
  return x + y;
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

### 1 章の考察

「結局どれを使えばいいの？」  
というのは当たり前の質問だが  
答えはプロジェクトによるとしか言えない

プロジェクトによって  
コーディングのルールがあると思うが  
基本的にはそれに従うのが良い

もしコーディングルールが策定されていなかったら  
自らルールを提案してみるのも良いかもしれない

---

## 2. import / export

+++

### 2 章の目的

まず定義として、ある js ファイルから  
別の js ファイルに渡す変数や関数などを  
**モジュール** と呼びます

この章ではそのモジュールの受け渡しの方法を学ぶ

+++

### import 側

例えば React を書くときに  
下記の記述を見たことはないだろうか？

```javascript
import React, { Component } from "react";
import { createStore, combineReducers } from "redux";
import App from "./App";
```

+++

### export 側

なんで {} があったりなかったりするの？  
と思うかもしれない  
ちょっと実際のモジュールを見てみる  
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

```javascript
// App
const App = () => <h1>Headline</h1>;
export default App;
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

export 側はこうする

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
// export
const Hoge = () => <div>hoge</div>;
export default Hoge;

// import
import MyFavoriteName from "./Hoge";
```

### 2 章の考察

実は細かいところで違いがあったりするが  
とりあえずこのレベルを最低限覚えておけば  
コーディング時に困ることは少なくなる

こちらもプロジェクトによって  
export の規約などを決めているところもあれば  
決めていないところもあるので  
基本的にはプロジェクトに従って書けば良い

---
