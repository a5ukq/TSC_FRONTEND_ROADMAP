# JavaScript の XHR と fetch

## XMLHttpRequest(XMR)とは

XMLHttpRequest は、従来のブラウザのネイティブ API として、主に次のような特徴がある。

- ブラウザとサーバ間でデータを非同期的に交換できる。
- ページの全体や部分的な更新が可能。
- ページ遷移せずにデータ通信ができる。

XMLHttpRequest オブジェクトを生成し、`open()`メソッドでリクエストを初期化する。
`send()`メソッドでリクエストをサーバーに送信する。
レスポンスが返ってくるとイベントが発火し、レスポンスデータが取得できる。

この XMLHttpRequest は Ajax 技術の基礎としてよく利用されている。

ページ全体をリロードせず、データの取得や送信が行えるため、より良い UX を提供できる。

### XHR の使い方：サーバーとの HTTP 通信の実現方法

XMLHttpRequest を使って、HTTP 通信を行うための使い方は難しくない、

1. XMLHttpRequest オブジェクトのインスタンスを作成する。

```JavaScript
var xhr = new XMLHttpRequest();
```

2. `open`メソッドで通信の方法や URL を指定する。

```JavaScript
xhr.open('GET', 'data.json');
```

3. 必要に応じてヘッダー等の追加設定を行う。

```JavaScript
xhr.responseType = 'json';
xhr.withCredentials = true;
```

4. `send`メソッドでリクエストを送信する。

```JavaScript
xhr.send();
```

5. イベントリスナーを登録して通信完了時の処理を定義する。

```JavaScript
xhr.onload = function() {
    if(xhr.status === 200) {
        // 成功時の処理
    } else {
        // エラー時の処理
    }
}
```

6. 必要に応じて通信進捗のイベントも処理する。

```JavaScript
chr.onprogress = function(event) {
    // 通信中の処理
}
```

目的に応じてイベント処理やオプションを設定していくことで、柔軟な通信を実現できる。

XMLHttpRequest の `send()`メソッドに JSON データの文字列をパラメータとして渡すことで、リクエストボディに JSON データを設定できます。

例を以下に示す。

```JavaScript
// JSONデータのオブジェクトを定義
var data = {
  name: "John",
  age: 30
}

// JSON.stringifyでJSON文字列に変換
var jsonData = JSON.stringify(data);

// XMLHttpRequestのインスタンスを生成
var xhr = new XMLHttpRequest();

// POSTメソッドでexample.phpにリクエスト送信
xhr.open("POST", "example.php");

// リクエストヘッダーのContent-Typeを設定
xhr.setRequestHeader("Content-Type", "application/json");

// リクエストボディにjsonDataをセット
xhr.send(jsonData);
```

このように、JavaScript のオブジェクトを `JSON.stringify` で JSON 文字列に変換し、それを `send()`に渡すことで JSON データを送信できます。サーバー側の処理でこの JSON を受け取り、解析することができます。

### XHR が非推奨の技術になった原因

近年、Fetch API の登場に伴って、長年ブラウザ標準の API である XMLHttpRequest が非推奨になりがち。原因を以下に示す。

- コールバック地獄に陥りやすい
  XMLHttpRequest は基本的にはイベントくどうでコールバック関数を使って処理を定義する。
  このため複雑な処理を書くとネストが深くなり、コールバック地獄になりがち。

- Promise などのモダンな非同期処理に対応できていない
  Fetch API や Async/Await など Promise ベースの新しい非同期処理が登場していますが、XMLHttpRequest はそれらと直接は相性が良くない。

- ストリーミング送受信に対応していない
  大きなデータを送受信する際、XMLHttpRequest では一度にすべてのデータをメモリに読み込む必要がある。

- 符号化や圧縮されたレスポンスに対応できない
  Fetch API などではさまざまなレスポンスフォーマットに対応できるが、XMLHttpRequest はそうした機能が貧弱である。

これらの制限を解決するために Fetch API が登場した。
Promise ベースで直感的なコーディングが可能で、ストリーミングや様々なデータフォーマットにも柔軟に対応できる。
しかし、ブラウザへの実装状況に依存する部分があるため、XMLHttpRequest も併用しつつ移行していくことが必要である。

## XHR とその後継である Fetch API との比較

Fetch は XMLHttpRequest の後継として登場した新しい API。
よりモダーンで優れたサーバー通信の仕組みを提供する。

Fetch API のメリットを以下に示す。

- Fetch は Promise ベースで設計されているため、非同期処理を直感的に表現でき、コールバック地獄が解消される。

- Fetch はリクエストとレスポンスを流暢に操作するストリーミング機能をサポートしている。

- Fetch にはキャッシュコントロールやリクエストのスコープ定義などの機能が備わっている。

- ブラウザや Node.js の最新バージョンでは、Fetch が本格採用されてきている。

上記の理由から、XMLHttpRequest の後継として、より高機能な Fetch がメインの API となりつつあり、将来的には XMLHttpRequest の代替が進む流れにあると言える。しかし、￥既存システムへの影響などもあり、当面は併用される可能性もある。

**XMLHttpRequest(XHR)と Fetch API の比較表**

| 項目                  | XMLHttpRequest                             | Fetch API                |
| --------------------- | ------------------------------------------ | ------------------------ |
| 概要                  | ブラウザでの HTTP 通信を実現するための API | XHR の新しい代替 API     |
| プロトコル            | HTTP/1.1                                   | HTTP/2                   |
| 非同期処理            | コールバック                               | Promise                  |
| コーディング          | 複雑                                       | シンプル                 |
| キャンセル            | 非対応                                     | 対応                     |
| ストリーミング        | 非対応                                     | 対応                     |
| リクエスト/レスポンス | 区別必要                                   | 単一オブジェクト         |
| キャッシュコントール  | 非対応                                     | 対応                     |
| 圧縮/エンコード       | 非対応                                     | 対応                     |
| ヘッダー制御          | 複雑                                       | シンプル                 |
| ブラウザ互換性        | 高い                                       | 新しいブラウザがほぼ対応 |

Fetch API は Promise ベースでシンプルな非同期処理の記述が可能である。ストリーミングや HTTP/2 などモダンな機能に対応しているが、ブラウザの互換性が課題になっている。XHR も併用しつつ徐々に移行が進んでいる。
