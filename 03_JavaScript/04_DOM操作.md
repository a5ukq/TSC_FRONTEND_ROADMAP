# JavaScript による DOM 操作

## DOM(document object model)とは

ブラウザは HTML を解析し、DOM 作成して画面を描画している。
DOM とは、HTML の情報をプログラムから扱いやすい形にして、メモリに保存したもの。

### 具体的な DOM の構成要素と、取得方法(html, Head, body)

```javascript
// html要素を取得できます
const html = document.documentElement;
// head要素を取得できます
const head = document.head;
// body要素を取得できます
const body = document.body;
```

上記のように、document オブジェクトを通して DOM にアクセスできる。

### node の取得方法

node とは、DOM を構成する 1 つの要素を表す。

```JavaScript
// 子供のnodeを配列のような形式で取得
html.childNodes;
// 最初の子nodeを取得
body.firstChild;
// 最後の子nodeを取得
body.lastChild;
// 同じ階層の次のnodeを取得
head.nextSibling;
// 同じ階層の前のnodeを取得
html.previousSibling;
// 親のnodeを取得
body.parentNode;
```

### element の取得方法

```JavaScript
// 子供のelementを配列のような形式で取得
html.children;
// 最初の子elementを取得
body.firstElementChild;
// 最後の子elementを取得
body.lastElementChild;
// 同じ階層の次のelementを取得
head.nextElementSibling;
// 同じ階層の前のelementを取得
body.previousElementSibling;
// 親のelementを取得
body.parentElement;
```

element は node の種類である。h1, div, ul など。

### 特定の element の取得方法

```JavaScript
// cssセレクタを指定して一致する最初の要素を取得
html.querySelector("div");
// cssセレクタを指定して一致する全ての要素を取得
html.querySelectorAll("div");
// cssセレクタを指定して祖先を遡って一番近くにあるものを取得
body.closest("html");
// elementを指定して一致するかを返す
body.matches("body");
// nodeを指定して一致するかを返す
html.lastChild.contains(html.lastChild);
```

`querySelector`は、比較的新しいメソット。古いメソッドを以下に示す。

```JavaScript
// id名をを指定して一致する最初の要素を取得
document.getElementById("app");
// name属性を指定して一致する全ての要素を取得
document.getElementsByName("title");
// tag名を指定して一致する全ての要素を取得
document.getElementsByTagName("div");
// class名を指定して一致する全ての要素を取得
document.getElementsByClassName("container");
```

基本的に`querySelector`で代替可能である。

## DOM の変更

### UPDATE（DOM の更新方法）

```JavaScript
// DOMの中身を　全て書き換える
body.innerHTML = "<h1>Hello !</h1>";
// DOMの中身に追記する
body.insertAdjacentHTML("afterbegin", "<h1>Hello2 !</h1>");
// textの中身を　全て書き換える
body.innerText = "Hello!";
// textの中身に追記する
body.insertAdjacentText("afterbegin", "Hello2 !");
```

`insertAdjacentHTML`と`insertAdjacentText`は、第一引数に挿入する場所を選べる。

ユーザーから受け取ったデータを表示する際に innerHTML などを使ってしまうと、XSS などの脆弱性に繋がる。そういった場合は、innerText を使うように。

### CREATE（DOM の作成方法）

createElement で DOM を作成することができる。

```JavaScript
const div = document.createElement("div");
```

そして、次の 4 つのメソッドで ODM に追加することができる。

| メソッド名 | 説明                   |
| ---------- | ---------------------- |
| `prepend`  | 1 つ下の階層の一番前   |
| `append`   | 1 つ下の階層の一番後ろ |
| `before`   | 同階層の一番前         |
| `after`    | 同階層の一番後ろ       |

```JavaScript
const div = document.createElement("div");
div.innerText = "hello"
const body = document.body;
body.append(div)
```

### DELETE (DOM の削除方法)

```JavaScript
const div = document.createElement("div");
div.innerText = "hello";
const h１ = document.createElement("h1");
h１.innerText = "hello";
body.before(div);
// 指定したnodeを子要素も含めて削除
div.remove();
// 指定したnodeを削除して他のnodeと入れ替える
div.replaceWith(h1);
```

上記のメソッドを使って DOM を削除することができる。
