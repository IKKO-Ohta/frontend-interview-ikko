---
title: HTML Questions
layout: layouts/page.njk
permalink: /questions/html-questions/index.html
---

-   What does a `doctype` do?
-   How do you serve a page with content in multiple languages?
-   What kind of things must you be wary of when design or developing for multilingual sites?
-   What are `data-` attributes good for?
-   Consider HTML5 as an open web platform. What are the building blocks of HTML5?
-   Describe the difference between a `cookie`, `sessionStorage` and `localStorage`.
-   Describe the difference between `<script>`, `<script async>` and `<script defer>`.
-   Why is it generally a good idea to position CSS `<link>`s between `<head></head>` and JS `<script>`s just before `</body>`? Do you know any exceptions?
-   What is progressive rendering?
-   Why you would use a `srcset` attribute in an image tag? Explain the process the browser uses when evaluating the content of this attribute.
-   Have you used different HTML templating languages before?

* * *

## `<!DOCTYPE html>` について説明せよ。

`<!DOCTYPE html>`宣言の目的は、ブラウザのレンダリングエンジンが「後方互換モード(Quirks)」に切り替わることを防ぐためである。というのも現在一般にレンダリングエンジンとして期待される「完全標準モード」以外にも、IE5やNavigator4のような非常に古いブラウザにおける非標準の動作をエミュレートするための「後方互換モード」、最小限の対応を施した「ほぼ標準モード」が存在するからである。「完全標準モード」以外に対応する必要は事実上ない。DOCTYPE宣言を通じて、明示的に「完全標準モード」を呼ぶことが望ましい。

[MDN - DOCTYPE](https://developer.mozilla.org/ja/docs/Glossary/Doctype)  
[MDN - 後方互換モードと標準準拠モード](https://developer.mozilla.org/ja/docs/Web/HTML/Quirks_Mode_and_Standards_Mode)

## 多言語対応についてすべきことを述べよ。

ユーザ エージェントが送信した言語選択情報(Language ヘッダー)に合わせた言語でHTML文書を返して目的を達成する。i18nと呼ばれるモジュールがサーバサイド側で多く実装されている。例えば

-   Ruby on Rails  
    <https://railsguides.jp/i18n.html>  
-   JavaScript Nuxt  
    <https://ja.nuxtjs.org/examples/i18n/>  

などが例としてあげられる。また返却されるhtml文書には、`<html lang='ja'>`などとlang属性を明記しておくことが翻訳やSEOの観点から重要である。

参考  
[lang属性を追加する - Hail2u](https://hail2u.net/documents/html-best-practices.html#add-lang-attribute)  
[i18n - Rails](https://railsguides.jp/i18n.html)

## 多言語サイトを構築する上でどのような点を考慮するべきかを述べよ。

-   言語設定について親切な導線設計がされているかを確かめる  
    ユーザが適切に自分の母国語のサイトにアクセスできるようになっていることが一番重要である。訪れるサイトのデフォルトがユーザの情報から推測される言語になっていなければならない。さらにそれらはわかりやすい仕方で切り替えられるようにしてあるべきだ。しかも、URLやドメインに言語情報が紐づいていることが、（同じURLをクリックすれば同じサイトに繋がるという一般的なユーザの期待を裏切らないために）重要である。例えば`hogehoge.com/ja`などのURL表示をしていることが望ましい。   

-   画像化したテキストはスケールしない  
    翻訳のたびに画像化したテキストを大量に抱えることになる。それらは収拾のつかないものになりがちである。その代わりに生のテキスト文字列を用い、コード側の処理によって適切な文字列を提供するように務めるべきである。そのための抽象化ライブラリが存在している。

-   文の長さに注意する  
    言語によって文の長さは変わりうる。ヘッドライン、ラベル、ボタンなどの表示が崩れないように留意する。特にbody textやコメントのようなテキスト情報が溢れないかは注意が必要である。

-   色の見え方は文化によって異なる  
    色の見え方は文化によって決まる。デザインにおいては適切に色を使用すること。

-   `<Template>`タグからテキストを完全に除去する  
    セクションタイトルやfooterなど、Template内部にテキストを残しておいてはいけない。多言語対応するためにそれらを翻訳する場合にも、そのままハードコーディングしてはいけない。これはaltやtitleにおいてもそうである。

-   日付のフォーマットに注意する。
    アメリカでは`May 31, 2012`と書き、ヨーロッパの一部では`May 31  2012`などと書く。日付を保存するときは考慮に入れること。

[What kind of things one should be wary of when designing or developing for multilingual sites? - quora](https://www.quora.com/What-kind-of-things-one-should-be-wary-of-when-designing-or-developing-for-multilingual-sites)
加えてRails i18nガイドが参考になる。

## `data- attribute`はどのような点で優れているか述べよ。

HTML5 カスタムデータ属性は、適切な属性や要素がない場合に、ページやアプリケーションに固有の独自データを格納することができる。そしてそれはJavaScriptなどから簡単に利用できる。

ただし、カスタムデータ属性の表記は一貫性のないものになりがちで、アルファベット順に属性を記述していくようなやり方は望ましくない。カスタムデータ属性を宣言するときは、読み手にとって読みやすいまとまりでタグを書いているかを確認する。

[Using data attribute - MDN](https://developer.mozilla.org/ja/docs/Learn/HTML/Howto/Use_data_attributes)

[data-\*とMicrodata、RDFa Lite用の属性と通常の属性を混ぜない - Hail2u](https://hail2u.net/documents/html-best-practices.html#dont-mix-data--microdata-and-rdfa-lite-attributes-with-common-attributes)

[data attribute - W3C](https://www.w3.org/TR/2014/REC-html5-20141028/dom.html#embedding-custom-non-visible-data-with-the-data-*-attributes)

## オープンwebプラットフォームとしてのHTML5について、HTML5はどのようなブロックに区分けされるか述べよ。

HTML5は次の7つのブロックに分かれて開発が進められている。

-   Semantics  
-   Connectivity
-   Offline and storage
-   Multimedia
-   2d/3d graphics effect
-   performance and integration
-   Device Access
-   Styling

Connectivity... サーバ側との接続が新しくなった。例えばwebソケットはその例の一つである。  
offline and storage... ウェブページがクライアント側にデータを保存するので効率的なオフライン操作が可能となる、くらいの意味。
<https://developer.mozilla.org/ja/docs/Web/Guide/HTML/HTML5>

## Describe the difference between a cookie, sessionStorage and localStorage.

 cookieは、サーバがユーザのwebブラウザに送信する小さなデータのこと。ブラウザに保存され、次のリクエストで一緒にサーバに送られる。一般的には、二つのリクエストが同じブラウザから送信されたものであるかを知るために利用される。HTTPプロトコル自体はステートレスな仕組みであるため、それを補う記憶領域の役割を持っている。  
 一方、汎用的な記憶領域としてのcookieの役割を引き受けるためのクライアントストレージAPIとしてWeb storage APIが開発された。現在はこちらを利用することが推奨される。なぜならcookieはリクエストのたびに送信されるので通信効率を悪くする原因となるからである。  
 Web storage APIは`localStorage`と`sessionStorage`に分かれており、両者は別々に制御されて機能する。`localStorage`はブラウザやタブを閉じても消えないデータだが、`sessionStorage`はそうではない。

 <https://developer.mozilla.org/ja/docs/Web/HTTP/Cookies>
 <https://developer.mozilla.org/ja/docs/Web/API/Web_Storage_API>

## Describe the difference between `<script>`, `<script async>` and `<script defer>`.

ブラウザのレンダリング・プロセス内部での処理順序に影響する属性である。属性表記なしのscriptタグにおいて、HTML parserはタグを見つけるとDOMツリーの構築を一旦停止してscriptのパースに入る。これは、JSによってDOMツリーが書き換えられる可能性を考慮してのことである（document.write()関数など）。しかしこれは遅いレスポンスでユーザの体験を損なう可能性がある。  
そこで、async/deferによって非同期にスクリプトタグを読ませることが速度のために重要である。asyncとdeferは非同期にスクリプトタグを読む点では同じだが、asyncはjsファイルのfetchのみ非同期に行うという違いがある。詳しいタイムラインの違いはwhatwg ページの図を参照のこと。

<https://html.spec.whatwg.org/multipage/scripting.html#attr-script-async>  
<https://developers.google.com/web/updates/2018/09/inside-browser-part3>

## Why is it generally a good idea to position CSS `<link>`s between `<head></head>` and JS `<script>`s just before `</body>`? Do you know any exceptions?

1.  外部リソース（主にcss）へアクセスするためのlinkタグは、titleなどと同じように、headerの内部に置くよう定められている。mdnのサイトを参考のこと。
2.  bodyからDOMツリーが構成されたあとにscriptによるjsの処理が始まるようにして、jsによるDOMツリー生成ブロッキングを回避するために、そのような方法が取られることがある。 しかし、前問でみたようにscriptタグ内部で非同期処理を指定していればこのような問題は起こらないので、その順序で置く必要はないことがわかる。なので、そのような場合が例外である。

<https://developer.mozilla.org/ja/docs/Web/HTML/Element/head>

## What is progressive rendering?

プログレッシブ レンダリングは、意味のある描画をユーザにできるだけ早く見せるための工夫である。言い換えると、HTML、CSS、JavaScriptの読み込みを遅らせ、もっとも必要な情報だけを可能な限り早く提供する取り組みのことをいう。  
スクリプトタグのasync/defer宣言をはじめとして、cssを分割する、画像のプレースホルダーを設けてローディングの時間の魅力低減を抑える、オンデマンドの画像読み込みを利用するなどの工夫がある。

<https://developer.mozilla.org/ja/docs/Web/Progressive_web_apps/Loading>

## Why you would use a srcset attribute in an image tag? Explain the process the browser uses when evaluating the content of this attribute.

`srcset`はレスポンシブ画像を表示させるための仕組みである。レスポンシブ画像とはネットワーク回線や計算資源、ウインドウサイズに応じて変更される画像を示す。例えば小さなウインドウでは重要な部分のみトリミングした写真を出したり、貧弱な帯域では低品質な画像を提供したりといったことである。srcsetを設定することで多くのユーザの体験を改善できる可能性がある。

```html
<img srcset="elva-fairy-320w.jpg 320w,
             elva-fairy-480w.jpg 480w,
             elva-fairy-800w.jpg 800w"
     sizes="(max-width: 320px) 280px,
            (max-width: 480px) 440px,
            800px"
     src="elva-fairy-800w.jpg" alt="妖精の衣装を着たエルバ">
```

例えば上記のタグは、次のような順序で読み込まれる。１）ブラウザのウインドウサイズを取得する。２）sizes属性をみて、条件（前の値）に適したの値(後の値)を画像幅として採用する。３）採用した画像幅からもっとも近い幅記述子`w`をもつ画像をロードする。

<https://developer.mozilla.org/ja/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images>

## Have you used different HTML templating languages before?

template engineを使用したことはない。template engineは、サーバサイドでデータを紐つけて動的にhtmlを作成するサーバプログラムである。具体的にはPythonの`jinja`やPhpの`Twig`などがある。  

（関連する重要な論点の一つとして、SPAとSSRの対立がある。SPAは一つのjavascriptファイルがルーティングからDOMの組み立てまで全てを担当する仕組みである。一方で、SSRはサーバサイド側でそのJavaScriptを実行し、htmlを生成してから配信する。SSRは配信するhtmlをキャッシュできる可能性がある点が魅力である。htmlをサーバサイドで生成するという観点からみると、SSRはtemplate engineの考えを引き継いだ仕組みともいえる。)

<https://www.publickey1.jp/blog/17/server_side_renderingserver_side_rendering_ng-japan_2017.html>
