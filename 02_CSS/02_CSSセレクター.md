# CSS セレクター

## 基本のセレクター

| 種類             | 書き方           | 意味                       | 意味                                |
| ---------------- | ---------------- | -------------------------- | ----------------------------------- |
| 要素セレクター   | `p`, `id`, `div` | 特定のタグ名を指定         | `p { color: red; }`                 |
| クラスセレクター | `.クラス名`      | class 属性を持つ要素に適用 | `.title { font-size: 20px; }`       |
| ID セレクター    | `#id名`          | id 属性を持つ要素に適用    | `#main { background-color: gray; }` |
| 全称セレクター   | `*`              | すべての要素に適用         | `* { margin: 0; }`                  |

## 組み合わせセレクター

| 種類           | 書き方    | 意味                    | 意味                            |
| -------------- | --------- | ----------------------- | ------------------------------- |
| 子孫セレクター | `div p`   | `div` 内の全ての `p`    | `div p { color: red; }`         |
| 子セレクター   | `div > p` | `div`直下の`p`のみ      | `div > p { color: blue }`       |
| 隣接セレクター | `h1 + p`  | `h1`の直後にある`p`     | `h1 + p { font-weight: Bold; }` |
| 兄弟セレクター | `h1 ~ p`  | `h1`の後にある全ての`p` | `h1 ~ p { color: green; }`      |

## 属性クラスセレクター

| 書き方           | 意味                 | 意味                                        |
| ---------------- | -------------------- | ------------------------------------------- |
| `[type]`         | 指定の属性を持つ要素 | `[type] { color: red; }`                    |
| `[type="text"]`  | 属性値が一致する要素 | `input[type="text"] { border: 1px solid; }` |
| `[type^="text"]` | 属性値が`t`で始まる  | `[type^="t"] { color: blue; }`              |
| `[type$="t"]`    | 属性値が`t`で終わる  | `[type$="t"] { color: green; }`             |
| `[type*="t"]`    | 属性値が`t`を含む    | `[type*="t"] { color: gray; }`              |

## 擬似クラスセレクター

| 書き方          | 意味                   | 意味                                         |
| --------------- | ---------------------- | -------------------------------------------- |
| `:hover`        | カーソルを乗せたとき   | `button:hover { background-color: yellow; }` |
| `:active`       | クリック中             | `a:active { color: pink; }`                  |
| `:focus`        | 入力欄が選択されたとき | `input:focus { border-color: blue; }`        |
| `:first-child`  | 最初の子要素           | `li:first-child { font-weight: Bold; }`      |
| `:last-child`   | 最後の子要素           | `li:last-child { color: gray; }`             |
| `:nth-child(n)` | n 番目の要素           | `li:nth-child(n) { color: black; }`          |

# 擬似要素セレクター

| 書き方           | 意味              | 意味                                   |
| ---------------- | ----------------- | -------------------------------------- |
| `::before`       | 要素の前に追加    | `p::before { content: "・" }`          |
| `::after`        | 要素の後に追加    | `p::after { content: "?" }`            |
| `::first-line`   | 最初の 1 行のみ   | `p::first-line { font-weight: bold; }` |
| `::first-letter` | 最初の 1 文字のみ | `li:first-letter { font-size: 150%; }` |
