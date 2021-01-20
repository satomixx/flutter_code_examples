# 【備忘録】Dart/Flutterの静的解析のエラー avoid_single_cascade_in_expression_statementsについて

---

# avoid_single_cascade_in_expression_statements
- [ドキュメント](https://dart-lang.github.io/linter/lints/avoid_single_cascade_in_expression_statements.html)

## 意味
- 式文では単一のカスケード用法の使用を避ける
- expression: 式
- statement: 文
- expression_statements: 式文

## 概要

```dart
// こういった用法を避ける、だってカスケードの使い方として間違っている
cake..bake();

// こうする
cake..bake();
```

### 式文について
- [こちらが参考になりました](https://www.notion.so/satomi/Write-Blog-1a93d0c003b847f3ad48748e6b23fdff#fcd0923a52174d4187f42e4a95251884)

### 本来カスケード用法はこう使う

```dart
// 本来カスケードはこう使う
cake
  ..bake()
  ..putStrawberryOnTheTop()
  ..eat();
```
