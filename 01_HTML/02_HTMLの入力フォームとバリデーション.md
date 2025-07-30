# HTML の入力フォームとバリデーション

## 入力フォームとは

- ユーザーが情報を入力してもらうための仕組み。
- 例：名前・メール・パスワード・コメントなど
- フォーム全体は`<form>`要素で囲む。

```html
<form action="/submit" method="post">
  <!-- 入力欄 -->
</form>
```

- `action` : 送信先の URL
- `method` : 送信方法（通常は`"post"`）

## 主なフォーム部品（input 要素など）

| タグ                      | 用途                     | 例                 |
| ------------------------- | ------------------------ | ------------------ |
| `<input type="text">`     | 1 行のテキスト入力       | 名前など           |
| `<input type="email">`    | メールアドレス入力       | メール確認付き     |
| `<input type="password">` | パスワード入力(非表示)   | セキュリティ用     |
| `<input type="number">`   | 数字専用入力             | 年齢など           |
| `<input type="checkbox">` | チェックボックス         | 複数選択           |
| `<input type="radio">`    | ラジオボタン（単一選択） | 性別など           |
| `<textarea>`              | 複数行のテキスト入力     | コメント欄など     |
| `<select>`                | プルダウンメニュー       | 選択肢の中から選ぶ |

## バリデーション

### 主な属性：

| 属性          | 説明                   | 使用例                                     |
| ------------- | ---------------------- | ------------------------------------------ |
| `required`    | 入力必須にする         | `<input required>`                         |
| `min/max`     | 数値や日付の範囲制限   | `<input type="number" min="1" max="100">`  |
| `maxlength`   | 文字数の上限           | `<input maxlength="20">`                   |
| `pattern`     | 正規表現で形式チェック | `<input pattern="[A-Za-z0-9]">`            |
| `type`        | 入力形式を推定         | `<input type="email">`でメール形式のみ許可 |
| `placeholder` | 入力欄にヒント表示     | `<input placeholder="例:田中太郎">`        |

## バリデーション付きフォームの例

```html
<form>
  <label>名前：<input type="text" required /></label><br />
  <label>年齢：<input type="number" min="0" max="120" /></label><br />
  <label>メールアドレス：<input type="email" required /></label><br />
  <label>パスワード：<input type="password" required minlength="8" /></label
  ><br />
  <button type="submit">送信</button>
</form>
```
