---
title: 削除処理の実装
layout: play2.3-slick2.1
---

指定したIDのユーザを`USERS`テーブルから削除し、一覧画面へリダイレクトします。

## コントローラ

すでに一覧画面に「削除」ボタンは表示されているので、そこから呼び出されるコントローラのメソッドのみ実装します。

```scala
def remove(id: Long) = DBAction.transaction { implicit rs =>
  // ユーザIDを指定して削除
  Users.filter(t => t.id === id.bind).delete

  // 一覧画面へリダイレクト
  Redirect(routes.UserController.list)
}
```

上記のコードでは以下の記述でユーザ情報の削除を行っています。

```scala
Users.filter( t => t.id === id.bind).delete
```

これは以下のSQLと同じ意味になります。

```sql
DELETE FROM USERS WHERE ID = ?
```

## 実行

一覧画面から「削除」をクリックしてユーザ情報が削除されることを確認してください。
