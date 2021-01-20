# 【備忘録】Dart/Flutterの静的解析ルールのimplicit_dynamic_variable , implicit-dynamicへの対応

---

- https://qiita.com/colorrabbit/items/7efd86faacfcd35a6e74

---

# implicit_dynamic_variable
*変数の型を明示的にする*

## 概要

```dart
// 変数（_createdAt）の型が明示的になっていない
final _createdAt = data['createdAt'];

// こんな感じにする
final _createdAt = data['createdAt'] as DateTime;
```

↑のようにするか、解析オプションファイルから implicit-dynamic を削除する
