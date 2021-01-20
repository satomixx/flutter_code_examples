# 【備忘録】Dart/Flutterの静的解析ルールのavoid_init_to_nullへの対応

---

- https://qiita.com/colorrabbit/items/287b9a866ef782a15ebe

---

# avoid_init_to_null
*DON'T explicitly initialize variables to null.*
*nullを使って初期化しない*

- [ドキュメント](https://dart-lang.github.io/linter/lints/avoid_init_to_null.html)

## 概要

Dartでは、明示的に初期化されていない変数やフィールドは、自動的にnullに初期化されます。
このため、nullを使って初期化することは冗長であり、不要です。
また、Dartには、初期化されていないメモリという概念はありません。

```dart
// nullで初期化してはいけない
int somethingNumber = null;

// こうする
int somethingNumber;
```
