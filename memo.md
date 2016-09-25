## html & Javascript メモ

### DOM (Document Object Model)
DOMとは、htmlファイルを見たときに現れるhtmlのbodyを表す **\<body\>タグ**、パラグラフを表す **\<p\>タグ** などの要素にアクセスする仕組み(API)のことです。JavaScriptなどからDOMを使い、上に挙げたようなタグを操作することにより、それぞれの要素の値を **動的に** 編集することが出来ます。  
ここで、botterのソースコードを見てみましょう。

https://github.com/ababup1192/botter/blob/master/index.html
```index.html
<!DOCTYPE html>
<html lang="ja">

  <head>
      <meta charset="UTF-8">
      <title>Twitter</title>
  </head>

  <body>
      <input id="tweet" type="text" placeholder="ツイート" />
      <ul id="tweets"></ul>

      <script type="text/javascript" src="./immutable.min.js"></script>
      <script type="text/javascript" src="./main.js"></script>
  </body>

</html>
```

1行目はこの文章がhtmlソースである事の宣言文なので、2行目から順に下って行きます。最初に\<html\>と言うタグに囲まれて、大きく分けて\<head\>、\<body\>とタグが見つかると思います。ここでは更に\<body\>タグの中の要素に着目してみましょう。  
一番最初に、以下のようなコードが書かれています。
```
<input id="tweet" type="text" placeholder="ツイート" />
```

一番最初の **\<** の後にある文字 **input** がこのタグの名前です。その後に空白区切りで続いているのが、属性と、その属性に指定する値です。
例えばここでは **id属性** に"tweet"、 **type属性** に"text"、 **placeholder属性** に"ツイート"と言う文字を代入している事がわかります。  
この一文だけでは、これらの属性は最初にhtmlソースを記述した時に指定した値から変動しませんが、JavaScriptからDOMを利用する事により、任意の操作を行った際に、それぞれの属性の値を変更する事が出来ます。

頭でっかちな説明だな

### Json (JavaScript Object Notation)
Jsonとは、JavaSCriptのオブジェクトの表記をそのまま応用したデータ構文のことです。Jsonの形式になっていれば、ソースコードに貼り付けるだけでJavaScript内で利用することが出来るようになります。  
Jsonには大きく分けて

* オブジェクト  
* 配列  

の二つのデータ形式が存在します。以下にルールとその例を挙げます。
#### Jsonオブジェクト
* ルール：全体を中括弧 **{ }** で囲み、 **キー** と **値** をコロン **:** で区切って表記したペアをカンマ区切りで列挙。
* 例  

```test.json
{"firstName":"John, "lastName":"Doe"}
{"1st_period":"LS2", "2nd_period":"csI", "3rd_period":"csI_ex", "4th_period":"literacy"}
```

#### Json配列
* ルール：全体を角括弧 **[ ]** で囲み、 **値** をカンマ **,** 区切りで列挙。
* 例
```
[
  1,
  "string",
  true
]
```

上で挙げたJsonオブジェクトを **値** としてカンマ区切りで列挙することも出来ます。
```test.json
[
  {"firstName":"John, "lastName":"Doe"},
  {"1st_period":"LS2", "2nd_period":"csI", "3rd_period":"csI_ex", "4th_period":"literacy"}
]
```

Json配列の要素で **値** として使うことが出来るのは、基本的に以下のデータ型になります。

* 数値（整数・浮動小数点）
* 文字列（「" "」で括る）
* 配列（「[ ]」で括る）
* オブジェクト（「{ }」で括る）
* bool（true・false）
* null

### localStorage (JavaScript)
localStorageは、ブラウザ上にユーザーが持つデータを保持しておく事が出来る仕組みの事です。Cookieと異なってくる点は、http通信が発生せず、あくまでもユーザーのローカルにあるブラウザで、JavaScriptから参照され動作するという点です。 webサービスを設計するにあたり、どうしてもユーザーが入力した情報をweb上で保持しておきたい事があります。そんな時にlocalStorageを用いる事で、サーバーを用いずにユーザーそれぞれのローカル環境にデータを保持しておく事が出来ます。  
Cookieと違う点を以下にまとめてみましょう。

* Cookieの特長
  * 保存容量が最大4KB
  * HTTPリクエストの度にサーバと通信
  * 有効期限あり

* localStorageの特長
  * 保存容量はブラウザにより異なる(5MB～10MB)
  * サーバへ値を送信しない
  * 無期限

今回サンプルとして挙げられているbotterも、ブラウザを起動する度に前回送信したデータが消えずに残っている事が確認できると思います。実際に幾つか "ツイート" を送信して確認してみましょう。  
実際にソースコード上でも確認出来ます。botterのJavaScriptソースを開いてみましょう。

https://github.com/ababup1192/botter/blob/master/main.js#L13
```main.js
function setStorageTweet(list) {
    localStorage.setItem("tweets", JSON.stringify(list))
}
```

ここでは詳しい説明は省きますが、main.jsの13行目でlocalStorageを使ってユーザーから送信されたデータを保存しています。ブラウザ上でユーザーから送信されたデータを保持！と言うと難しそうに感じるかも知れませんが、ここで見られる通りとても単純な記述で使える事が分かると思います。

### 参考
https://ja.wikipedia.org/wiki/Document_Object_Model
http://piyo-js.com/05/dom.html
http://www.atmarkit.co.jp/ait/articles/0803/12/news149.html
http://uhyohyo.net/javascript/2_2.html
http://www.trident-game.com/blog/2015/10/14/%E3%80%90%E8%BC%AA%E8%AC%9B%E3%80%91json%E3%81%AE%E6%9B%B8%E3%81%8D%E6%96%B9/
http://uhyohyo.net/javascript/14_1.html
http://wp.tech-style.info/archives/742
