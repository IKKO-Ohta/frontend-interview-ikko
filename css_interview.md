---
title: CSS Questions
layout: layouts/page.njk
permalink: /questions/css-questions/index.html
---

* What is CSS selector specificity and how does it work?
* What's the difference between "resetting" and "normalizing" CSS? Which would you choose, and why?
* Describe Floats and how they work.
* Describe z-index and how stacking context is formed.
* Describe BFC (Block Formatting Context) and how it works.
* What are the various clearing techniques and which is appropriate for what context?
* How would you approach fixing browser-specific styling issues?
* How do you serve your pages for feature-constrained browsers?
  * What techniques/processes do you use?
* What are the different ways to visually hide content (and make it available only for screen readers)?
* Have you ever used a grid system, and if so, what do you prefer?
* Have you used or implemented media queries or mobile specific layouts/CSS?
* Are you familiar with styling SVG?
* Can you give an example of an `@media` property other than `screen`?
* What are some of the "gotchas" for writing efficient CSS?
* What are the advantages/disadvantages of using CSS preprocessors?
  * Describe what you like and dislike about the CSS preprocessors you have used.
* How would you implement a web design comp that uses non-standard fonts?
* Explain how a browser determines what elements match a CSS selector.
* Describe pseudo-elements and discuss what they are used for.
* Explain your understanding of the box model and how you would tell the browser in CSS to render your layout in different box models.
* What does ```* { box-sizing: border-box; }``` do? What are its advantages?
* What is the CSS `display` property and can you give a few examples of its use?
* What's the difference between inline and inline-block?
* What's the difference between the "nth-of-type()" and "nth-child()" selectors?
* What's the difference between a relative, fixed, absolute and statically positioned element?
* What existing CSS frameworks have you used locally, or in production? How would you change/improve them?
* Have you played around with the new CSS Flexbox or Grid specs?
* Can you explain the difference between coding a web site to be responsive versus using a mobile-first strategy?
* Have you ever worked with retina graphics? If so, when and what techniques did you use?
* Is there any reason you'd want to use `translate()` instead of *absolute positioning*, or vice-versa? And why?

---

## What is CSS selector specificity and how does it work?
CSS selector specificity CSSセレクタ詳細度とは、CSS命令が競合したとき、優先度を判定するための仕組みである。要素型セレクタ（h1など）、クラスセレクタ、idセレクタの順で優先順位が高くなる。それらが組み合わされているときは、それぞれの単位ごとに計算し、最もスコアの高いCSS命令を選ぶ。
`!important`命令は詳細度を無視してそのCSSを直接適用する。しかしデバッグを困難にするため`!important`は外部ライブラリを上書きするときを除いて使うべきではないとされる。

https://developer.mozilla.org/ja/docs/Web/CSS/Specificity

## What's the difference between "resetting" and "normalizing" CSS? Which would you choose, and why?

1. resetting CSSとは、各ブラウザがもっているデフォルトCSSを消去するためのCSSファイルである。resetting CSSの利用すると、ブラウザ間のデフォルトCSSの差異を消去して、どのブラウザで見ても同じスタイリングを提供できる。一方、normalizing CSSは、できる限り元のデフォルトCSSを活かして最小限のリセットを行うことを目的としている。

2. その2つのうち、normalizing CSSを用いることが望ましい。第一に、十分共通のものとして利用できるスタイリングを自分で宣言するのは手間がかかる。第二に、normalize CSSではresetting CSSがよく引き起こすバグを修正している。特にフォームについてはresetting CSSが不適切な動作を引き起こすことが多いと言われている。第三にデバッグツールのCSSインスペクタにおける表示が読みにくくならない。resetting cssを用いてCSSを分析すると巨大な継承チェーンに邪魔をされて状況が確認できないことがよくある。第四に、normalizing cssはドキュメントが充実している。系統的な調査の結果やその実装の詳細について、GitHubの該当リポジトリからチェックすることが可能である。

http://nicolasgallagher.com/about-normalize-css/

## Describe Floats and how they work.
Floatは支配下の要素を横並びにする効果をもつ。より詳しく言うと、通常の要素は上から下に並べられるが、`float:right`なら右並びになる。floatした領域について、テキストやインライン要素が"回り込める"ようになる。しばしば”回り込み”は意図しない動作をもたらすので、`clear`を適宜用いてそれを解除する。

## Describe z-index and how stacking context is formed.
z-indexはz軸上の位置(レンダリング上のレイヤ)を定める値である。そのような仮想的なZ軸上に並べられたレイヤの概念図を重ね合わせコンテキスト stacking contextと呼ぶ。値が小さいほど、その要素はレイヤの奥に表示される。z-indexは親子関係によって基本的には決定される（親よりも子に高い値がつけられる）。兄弟要素に対しては独立している。望むなら、任意の要素におけるz-indexの値を任意に指定することも可能である。
https://developer.mozilla.org/ja/docs/Web/CSS/CSS_Positioning/Understanding_z_index/The_stacking_context

## Describe BFC (Block Formatting Context) and how it works.
BFC ブロック整形コンテキストはCSSの視覚的なwebページ生成の一部である。その中でブロックボックス（ex. float, 表のセル要素, display, フレックスアイテム）が整理され、それぞれの配置が決定される。ブロックボックスとして定められた要素は下のリンクの一覧がある。`float`ブロックを用いる場合はBFCの概念が重要である。回り込みの作用やマージン相殺の処理はこのBFCによって行われる。
