# 【備忘録】Dart/Flutterの静的解析ルールのavoid_function_literals_in_foreach_callsへの対応

---

- https://qiita.com/colorrabbit/items/92f794279d608975c6a3

---

# avoid_function_literals_in_foreach_calls
*AVOID using forEach with a function literal.*
*関数リテラルでforEachを使うことは避ける*

## 概要

シーケンスの反復処理においては、for文をもちいる。

```dart
// この使い方は避けること
dogs.forEach((dog) {
  .....
});

// for文にする
for (var dog in dogs) {
  .....
}

// この様な書き方はOK
dogs.forEach(print);
```

https://dart-lang.github.io/linter/lints/avoid_function_literals_in_foreach_calls.html
