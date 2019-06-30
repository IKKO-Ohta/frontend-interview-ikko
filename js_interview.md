---
title: JavaScript Questions
layout: layouts/page.njk
permalink: /questions/javascript-questions/index.html
---

* Explain event delegation.
* Explain how `this` works in JavaScript.
  * Can you give an example of one of the ways that working with `this` has changed in ES6?
* Explain how prototypal inheritance works.
* What's the difference between a variable that is: `null`, `undefined` or undeclared?
  * How would you go about checking for any of these states?
* What is a closure, and how/why would you use one?
* What language constructions do you use for iterating over object properties and array items?
* Can you describe the main difference between the `Array.forEach()` loop and `Array.map()` methods and why you would pick one versus the other?
* What's a typical use case for anonymous functions?
* What's the difference between host objects and native objects?
* Explain the difference between: `function Person(){}`, `var person = Person()`, and `var person = new Person()`?
* Explain the differences on the usage of `foo` between `function foo() {}` and `var foo = function() {}`
* Can you explain what `Function.call` and `Function.apply` do? What's the notable difference between the two?
* Explain `Function.prototype.bind`.
* What's the difference between feature detection, feature inference, and using the UA string?
* Explain "hoisting".
* Describe event bubbling.
* Describe event capturing.
* What's the difference between an "attribute" and a "property"?
* What are the pros and cons of extending built-in JavaScript objects?
* What is the difference between `==` and `===`?
* Explain the same-origin policy with regards to JavaScript.
* Why is it called a Ternary operator, what does the word "Ternary" indicate?
* What is strict mode? What are some of the advantages/disadvantages of using it?
* What are some of the advantages/disadvantages of writing JavaScript code in a language that compiles to JavaScript?
* What tools and techniques do you use debugging JavaScript code?
* Explain the difference between mutable and immutable objects.
  * What is an example of an immutable object in JavaScript?
  * What are the pros and cons of immutability?
  * How can you achieve immutability in your own code?
* Explain the difference between synchronous and asynchronous functions.
* What is event loop?
  * What is the difference between call stack and task queue?
* What are the differences between variables created using `let`, `var` or `const`?
* What are the differences between ES6 class and ES5 function constructors?
* Can you offer a use case for the new arrow `=>` function syntax? How does this new syntax differ from other functions?
* What advantage is there for using the arrow syntax for a method in a constructor?
* What is the definition of a higher-order function?
* Can you give an example for destructuring an object or an array?
* Can you give an example of generating a string with ES6 Template Literals?
* Can you give an example of a curry function and why this syntax offers an advantage?
* What are the benefits of using `spread syntax` and how is it different from `rest syntax`?
* How can you share code between files?
* Why you might want to create static class members?

## Coding questions
* Make this work:
```javascript
duplicate([1,2,3,4,5]); // [1,2,3,4,5,1,2,3,4,5]
```
* Create a for loop that iterates up to `100` while outputting **"fizz"** at multiples of `3`, **"buzz"** at multiples of `5` and **"fizzbuzz"** at multiples of `3` and `5`


## Explain event delegation.
イベント デリゲーションは、親要素が子要素に対し同一のイベントリスナの参照を与えることをいい、JavaScriptによる直接的なDOM操作の一つである。イベント デリゲーションを用いると、たとえば`ul`配下の複数の`li`に同一の`onclick`を渡すことができる。`event delegation`命令で最もよく用いられるのは`EventTarget.addEventListener()`メソッドで、このメソッドはイベントに対応する任意オブジェクトの子どもたちに対して再帰的に機能する。
- [JS Interview: Explain Event Delegation by Matthew Holman](https://link.medium.com/WyXdP1CUdX)
- [MDN](https://developer.mozilla.org/ja/docs/Web/API/EventTarget/addEventListener)

## Explain how this works in JavaScript.
`this`はjsにおいて他の言語と違った特性を見せる。特に`this`は関数の **呼ばれ方** によって決定され、その関数の **内部で決定されない** という特性がある。  
より詳しく言うと、グローバルコンテクストにおいて`this`はグローバルオブジェクトに等しい。例えば、
```JavaScript
this === window
```
はグローバルコンテクスト(全てのスコープの外)において真である。いわゆるグローバル宣言のように`this`はスコープを超越して値を共有する特別な領域である。しかし、オブジェクトのメソッドやメンバとして`this`が呼ばれるとき、`this`は自身の所属するオブジェクトを示す参照である。たとえば、
```JavaScript
var o = {
  prop: 37,
  f: function() {
    return this.prop;
  }
};
```
このとき`this`は所属するオブジェクト`o`への参照である。それなので何らかの理由でこのオブジェクトに後から何かメソッドが追加されたとしても（JavaScriptではオブジェクトに後付けでメソッドを加えられる）、この`this`の参照が変わることはない。
そのほかにも、`new`コンストラクタでの振る舞いや、`apply`での振る舞い、アロー関数の上での振る舞い、全ての場合で`this`が参照するものは異なる。ルールが競合した場合優先順位の高いものが有効となる。

- [educative - The Complete Rules to `this`
](https://www.educative.io/collection/page/5679346740101120/5707702298738688/5676830073815040)  
- [MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/this)

## Explain how prototypal inheritance works.
プロトタイプの継承の振る舞いについて、まずJavaScriptにおけるプロトタイプについて説明し、それから本題のプロトタイプ継承について議論する。プロトタイプとは、JavaScriptのすべてのオブジェクトがもつ原型であり、他のオブジェクトへの内部的な繋がりである。プロトタイプ オブジェクトそのものもプロトタイプをもっており、その連鎖は最後には`null`に行き着く(`null`はプロトタイプをもたない)。そのようなプロトタイプの繋がりをプロトタイプチェーンと呼ぶ。  
そして本題に入ると、プロトタイプの継承とは、このプロトタイプチェーンを結ぶことに相当する。より具体的にいうと、`extended.a`が命令されると、JavaScriptはオブジェクト`extended`のプロパティをまず探し、そこに適切なプロパティが見当たらないと、継承元である`origin`に`.a`がないかを探しに行く。このようにして遡っていき、お目当てのものを見つけると探索を打ち切ってその答えを返す。これがプロトタイプチェーンによって実現されるプロパティ継承である。

補足的な事項を三点述べる。
 1. このようなプロトタイプチェーンの仕組みは、実のところES6になっても変わっていない。`class`構文のように見えるものは結局のところプロトタイプチェーンと継承のラッパーに過ぎない。
 2. このような理由から、プロトタイプチェーンのどこにもないプロパティの探索を命じるのはコストがかかる。`.hasOwnProperty`メソッドは唯一のプロトタイプチェーンを辿らないメソッドで、これは`Object.prototype`から継承されたメソッドである。 これは *そのオブジェクト自身* が該当するプロパティを持つかどうかだけを判定する。
 3. `new` 演算子は、全てのオブジェクトがもっている特別なプロパティ`prototype`に深く関係する。
```javascript
var a1 = new A()
```
 を例に取る。`new`演算子が宣言されると、`A()`の実行よりも前に、`a1.[[prototype]] = A.prototype` を計算する
。こうしてJavaScirptにおける変数は型のようなものをランタイムに得ることになる。

## What's the difference between a variable that is: null, undefined or undeclared?
`null`はリテラルで`undefined`はグローバルオブジェクトである。`undeclared`はプロトタイプチェーン上を探索した結果そのプロパティが見当たらなかったという探索結果の表明であり、リテラルやオブジェクトではない。
開発の立場では、`null`と`undefined`は 1)厳密等価演算子`===`では等しくないこと、2) `null`はプロパティが存在しないことを明示するために用いられるが`undefined`はそうではないこと、を特に覚えておく必要がある。

## What is a closure, and how/why would you use one?
クロージャは独立した変数を参照する関数である。もう少し詳しく言うと、クロージャという概念は関数そのものと関数が生成された環境に分割される。
```javascript
function makeAdder(x) {
  return function(y) {
    return x + y;
  };
}

var add5 = makeAdder(5);
var add10 = makeAdder(10);

console.log(add5(2)); // 7 と表示される
console.log(add10(2)); // 12 と表示される
```
この`makeAdder()`関数はクロージャの性質をよく表している。すなわち、`makeAdder()`によって作成された関数たちは、その関数が生成されたときの環境を引き継いでおり、両者は`x`の値の点で「環境が異なる」。これがクロージャの概要と動作の様子である。

このようなことはごく一般的におこなれていることである。たとえばReactコンポーネント`Modal`から、ほとんどの動作が共通でありしかし微妙にプロパティが異なる`UserModal`と`PaymentModal`は同じ関数から生成できる。クロージャは関数の再利用性を高め、オブジェクト指向に似たデータ構造を提供する。興味深いことに、クロージャを利用してJavaのようなプライベートメソッドを模倣することもできる。

[MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Closures)

## What language constructions do you use for iterating over object properties and array items?
 - `for/in`
 - `forEach`
 - `for(let i; i<n;i++){}`
JavaScriptにはたくさんのループがあり、気に入ったものやその場で見通しが立ちやすいものを使えばよい。

[MDN](https://developer.mozilla.org/ja/docs/Web/CSS/flex-direction)

## Can you describe the main difference between the Array.forEach() loop and Array.map() methods and why you would pick one versus the other?
語義のままであるが、`Array.foreach()`は配列の一つずつに対して行う処理を示し、`Array.map()`は配列(ベクトル)に適用する写像である。ゆえに後者は新たな配列値を返すことを期待する。利用シーンでいうと、例えばデータベースに一つずつの要素を登録していく処理であれば前者のほうが向いているし、あるベクトルに線型写像を適用するなら`Array.map()`を使うべきだ。

[MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/map)

## What's a typical use case for anonymous functions?
ES2015以降、無名関数はアロー関数として用いられることが多くなった。例えば`Promise()`は良い例で、多くのコードがpromiseに無名関数（アロー関数記法）を用いている。
```javascript
const promise = new Promise( (resolve,_)=>{
  setTimeout(() => {
    resolve("hello world!")
  },100);
});

promise.then((v) =>{
 	console.log(v)
})
```

## What's the difference between host objects and native objects?
どちらもグローバルスコープにある概念だが、host objectは`window`や`document`のように実行環境によって提供されるオブジェクトである。一方native objectはJavaScriptが組み込みとして持っているオブジェクトである。たとえば`Array`はそうである。
[MDN](https://developer.mozilla.org/ja/docs/Web/API/document
注）テクニカルタームとして`host object` `native object`という語があるわけではないようだ。少し調べてみると「開眼! JavaScirpt」に書いてある分類概念のようだが。

## Explain the difference between: function Person(){}, var person = Person(), and var person = new Person()?
この問題を言い換えると、`new`演算子が何者でどのような振る舞いをするか、結果としてどのような返り値になるかということである。ゆえに、`new`演算子について説明する。
`new`演算子は組み込みの計算でオブジェクトのインスタンスを定義するものである。`new Person()`をすると、まず`Person.prototype`を継承する新しいオブジェクトが生成される。次にコンストラクタが呼ばれる。指定した引数があればそれを利用してオブジェクト内部の計算が行われる。最後に完成したオブジェクトが返り値として表現される。
この問題の結論としては、前者は関数のエイリアスであり、後者はインスタンスであるということである。

[MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Operators/new)

## Can you explain what Function.call and Function.apply do? What's the notable difference between the two?
`Function.call`はあるオブジェクトに所属するプロパティを、別なオブジェクトに割り当てて呼ぶ関数である。
```js
function Product(name, price) {
  this.name = name;
  this.price = price;
}

function Food(name, price) {
  Product.call(this, name, price);
  this.category = 'food';
}

console.log(new Food('cheese', 5).name);
// expected output: "cheese"
```
ゆえに、ここで`Food()`のプロパティには3つのプロパティが設定されたことになる。
`.apply`はほとんど同じものであるが、2つめ以降のargsにおいて、リスト（ES5以降は.length()をもつようなオブジェクト全て）を引数の型として取るようになっている点で異なる。

## Explain Function.prototype.bind
`.bind()`は関数を生成する。生成された関数オブジェクトには`this`の参照先が追加されている。具体例をみると、
```js
var module = {
  x: 42,
  getX: function() {
    return this.x;
  }
}

var unboundGetX = module.getX;
console.log(unboundGetX()); // The function gets invoked at the global scope
// expected output: undefined

var boundGetX = unboundGetX.bind(module);
console.log(boundGetX());
// expected output: 42
```
当然ながら、`getX`関数のみを`module`から抜き出しても、`module.x`が抜き出されるわけではない。ゆえに最初の出力はundedinedになるが、`bind()`を用いて作成された関数では、`this`の内容も関数にバインドされて`42`が得られる。

[MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Function/bind)

(蛇足:bindといえば過去のバージョンのReactのmethod.bind(this)を思い出す)

## What's the difference between feature detection, feature inference, and using the UA string?
 - Feature Detectionはある機能がその環境でサポートされているかを調べるコードである。その方法はいくつかあるが、基本的な戦略はグローバルオブジェクトの中に期待するメンバが含まれているかどうかを調べるということである。例えばユーザの物理位置情報について知りたければ`window.navigator`の`geolocation`が定義されているかどうかを調べる。
 - Feature interfaceはそのメンバがあるという前提で書かれる処理である。
 - UserAgent stirngとは`navigator.UserAgent`の内部に定義されるブラウザ固有のstringである。一般的に、ブラウザ特定のためにUA stringを用いるのは信頼性の低い方法であるとされ、するのであればバージョン番号を用いるのが良いとされている。

[medium](https://medium.com/@nupoor_neha/javascript-front-end-interview-questions-1cbc5e32792b)  
[MDN](https://developer.mozilla.org/ja/docs/Web/HTTP/Browser_detection_using_the_user_agent)  
[MDN](https://developer.mozilla.org/ja/docs/Web/API/Navigator)  

 Feature Interfaceについては正確な資料が見つからない状況である。

## Explain "hoisting".
`hoisting/巻き上げ`はJavaScriptのコードの処理順の独特な機構である。`var`や`Function`などの定義宣言はファイルの先頭にあるものとして扱う。一方でその実行や初期化についてはその処理を実行しない。
なお、現代的な変数宣言であるところの`let`および`const`では(一般的な局面では)巻き上げが起こらない。

[MDN](https://developer.mozilla.org/ja/docs/Glossary/Hoisting)

## Describe event bubbling.
## Describe event capturing.
 eventのbubblingとcapturingは対の関係にある語なのでまとめて説明する。
 HTML要素は通常入れ子状になっている。ある要素においてイベントが発火したとき、そのイベントはどのように伝搬するだろうか。bubblingとcapturingはその伝搬方法である。　

- 子から親にイベントが流れていくことをbubblingという。
- 親から子にイベントが流れていくことをcapturingという。

( TODO: capturingのコードを書く状況が思いつかないのだけど理屈としては書きうるよな、というくらいです。モダンなコードで書く例があったら追記したいので教えて下さいmm)
[medium](https://medium.com/@nupoor_neha/javascript-front-end-interview-questions-1cbc5e32792b)  

## What's the difference between an "attribute" and a "property"?
簡単に言うとattributeはDOM要素に渡す引数で、propertyはオブジェクトのメンバ変数である。
attributeは、Documentオブジェクト上では`Element.attributes()`によって返却されるリストである。それらのリスト要素を参照してレンダラは適切な修飾を与えて描画する。一方でpropertyは(特にJavaScriptにおいて)あるデータ構造と関連づけられた情報群を指す。オブジェクトに与えられるメンバ変数と言い換えてもよい。

[MDN](https://developer.mozilla.org/ja/docs/Web/API/Element/attributes)

## What are the pros and cons of extending built-in JavaScript objects?
組み込みオブジェクトを **拡張してはいけない** 。組み込みオブジェクトはグローバルに位置するために、これを改変することは他人のコードを破壊することにつながる。

[MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects)

## What is the difference between == and ===?
両者はそれぞれ等価演算子と厳密等価演算子と呼ばれ、通常同値の判定には`==`ではなく`===`を使うべきである。両者のもっとも大きな違いは`==`においては暗黙的に型変換が行われることだろう。逆に`===`では型変換が起こらず、型が異なった時点で右辺と左辺は異なるオブジェクトとして判定する。
[MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Equality_comparisons_and_sameness)

## Explain the same-origin policy with regards to JavaScript.
同一オリジンポリシー/same-origin policyとは、あるオリジンから読み込まれた文書やスクリプトは、他のオリジンからのスクリプトに改変されないという原則である。同一オリジンポリシーはウェブ セキュリティの重要な一項目であり、悪意ある行動を起こしかねないリソースを分離するのに役立つ。
一方で、モダンなJavaScript web開発にとっては、クロスサイトリクエストすなわち異なるオリジンからの情報を入手することは必要不可欠なことである。例えばTwitterのSNSボタンは典型的なクロスサイトリクエストである。このようなアクセスを安全に許可する仕組みとしてオリジン間リソース共有/cross-origin resource sharing/CORSがある。

[MDN](https://developer.mozilla.org/ja/docs/Web/Security/Same-origin_policy)   
[MDN](https://developer.mozilla.org/ja/docs/Web/HTTP/CORS)

## Why is it called a Ternary operator, what does the word "Ternary" indicate?
`condition ? A : B`すなわち
```js
if (condition) {
  return a
} else {
  return b
}
```
である。三項/Ternaryは、例えば`+`や`-`が二つの項を取り扱う演算子であるのに対して、`?:`はcondition,A,Bの3つの項を取り扱う演算子であることを意味している。

## What is strict mode? What are some of the advantages/disadvantages of using it?
`use strict` strictモードはES5に存在した、その名の通り厳格な文法規則を定めるオプションである。[ECMA Script](http://www.ecma-international.org/ecma-262/6.0/#sec-strict-mode-code)によればES6は常にstrictモードで動作することが定められている。ナチュラルなJSと異なる点として代表的な要素を三つあげると、例えば予期しないグローバルオブジェクトの生成を防止することや、オブジェクト プロパティに対しての無効な代入を検知することや、`eval`の仕様がより単純になっていることが挙げられる。

[MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Strict_mode)

## What are some of the advantages/disadvantages of writing JavaScript code in a language that compiles to JavaScript?
 問題のような言語で、最も勢いがある言語がTypeScriptであることは論を待たない。TypeScriptを採用するメリットはそれがスケールするからだとされている。言い換えると、保守性が高くランタイムエラーが生じにくくなる。また特にTypeScriptにはVSCodeを始めとする周辺ソフトウェアが整理されており、生産性が高いということである。
 TypeScriptはJSのsupersetであるから、JSに比べて不利な点はその設定にまつわる部分を除けば存在しない。チームメンバーが新しくTypeScriptを学ぶためのコストや、既存プロジェクトを順次TypeScriptに置き換える工数を鑑みて、その取引が特になるなら採用をするべきである。

[TypeScript](https://www.typescriptlang.org/)

## What tools and techniques do you use debugging JavaScript code?
  - console デバッグ  
  consoleオブジェクトには`.log()`だけでなく`.table()`などの機能もある。どんな場合にも使えるもっとも基本的なデバッグ手法である。
  - Chrome DevTool など   
  Chrome Devtoolは、コンソールやDOMの状態を調べるのに使う以外にも豊富な使い道がある。例えばネットワークタブや、JavaScriptのable/enable、cookieやローカルストレージの検査、Vueコンポーネントの調査ができるアドオンなど、外部拡張も含めてたくさんの機能が詰め込まれている。
  - テストを書く  
  テストを書くことはデバッグのために重要である。テストを書いていれば、プログラムのうちどの部分までは正常なのか担保できる。それは発生したバグの範囲を絞り込むことに繋がり、結果的にデバッグに貢献する。

## Explain the difference between mutable and immutable objects.
### What is an example of an immutable object in JavaScript?
  string
### What are the pros and cons of immutability?
  pros:
   関数の参照透過性を維持できる。参照透過な関数とは、引数の値によって一意に出力が決定されるような関数である。例えばsin()やcos()は参照透過な関数である。一方で、クラスメソッドでそのクラスメンバ変数の値を計算中に用いるような関数は参照透過ではない。このような性質を持つ関数は単体テストが容易で、保守しやすい特長がある。   
  cons:
   実装の自由度を犠牲にする。
### How can you achieve immutability in your own code?
  immutable.jsを使うとよい。  
  [immutable js](https://immutable-js.github.io/immutable-js/docs/#/)

## Explain the difference between synchronous and asynchronous functions.
  同期関数は計算結果の返却タイミングが一定な関数で、非同期関数は不定な関数である。非同期関数の具体例として外部のサーバとのHTTP通信がある。例えばサーバと通信するアプリケーションを例にとると、同期関数のみでプログラミングしたとすると通信の完了を待たねば後続の処理を行うことができないが、非同期の関数として通信を実装すれば先方のレスポンスを待つことなく後続の処理に取りかかることができる。
  [MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Promise)

## What is event loop?
イベントループとは、javascript処理エンジンのランタイムにおける実行モデルである。
前提として、実行中の関数はスタックとして積み重ねられている。その一単位をフレームと呼ぶ。フレームの内部で関数が呼ばれると、新しいフレームがスタックにプッシュされる。一方で、処理されるメッセージのリストはキューの形を取っている。スタックが空になると、メッセージがキューから取り出され、新しい処理が始まる。これはJavaScriptのランタイムの基本である。（補足：ここから分かるように、「メッセージ」とは一つのスタック内で相互に収まらないような処理単位を意味している。メッセージはOSなどjsの外部が管理するものである）。
さて、イベントループは次のようなコードで抽象化できる。
```js
while(queue.waitForMessage()){
  queue.processNextMessage();
}
```
これは先頭のメッセージの返答を待っている間にも先に次のメッセージを処理してしまうということを意味している。この実装はGUI操作において非常に役立つ。あるメッセージAの処理が遅れても、メッセージBの処理が滞ることはないからである。寄り具体的に言えば、DBやファイルの書き込みによってユーザのタイピングをブロックされることがない。
[MDN](https://developer.mozilla.org/ja/docs/Web/JavaScript/EventLoop)

## What is the difference between call stack and task queue?
## What are the differences between variables created using let, var or const?
## What are the differences between ES6 class and ES5 function constructors?
## Can you offer a use case for the new arrow => function syntax? How does this new syntax differ from other functions?
##  What advantage is there for using the arrow syntax for a method in a constructor?
##  What is the definition of a higher-order function?
##  Can you give an example for destructuring an object or an array?
##  Can you give an example of generating a string with ES6 Template Literals?
##  Can you give an example of a curry function and why this syntax offers an advantage?
##  What are the benefits of using spread syntax and how is it different from rest syntax?
##  How can you share code between files?
##  Why you might want to create static class members?
