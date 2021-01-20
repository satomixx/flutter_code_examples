# 【備忘録】Dart/Flutterプロジェクトでの静的解析によるLintルールについて

---

## 概要
Dart/Flutterのプロジェクトでコードの静的解析を行うには、 `analysis_options.yaml` を設定します。

コードの静的解析については[こちら](https://dart.dev/guides/language/analysis-options)が参考になります。

また、Dart/FlutterでのLintルールは、[こちらに一覧が記載されています。](https://dart-lang.github.io/linter/lints/index.html)

VS CodeやAndroid Studioで、静的解析によるエラーに遭遇しても、じゃあどうしたらいいのか、すぐにわからないことが度々あるので、こちらにそれを記載していきます。

ただ、本来は各IDEで適切なpackageを設定するか、[こちらのLintルール一覧](https://dart-lang.github.io/linter/lints/index.html)で検索するのが適切な解決策かなとは思います。

## ルール
### avoid_init_to_null
[ドキュメント](https://dart-lang.github.io/linter/lints/avoid_init_to_null.html)
*nullを使って初期化しない*
*Dartでは、明示的に初期化されていない変数やフィールドは、自動的にnullに初期化されます。
このため、nullを使って初期化することは冗長であり、不要です。
また、Dartには、初期化されていないメモリという概念はありません。*

```dart
// nullで初期化してはいけない
int somethingNumber = null;

// こうする
int somethingNumber;
```

https://qiita.com/colorrabbit/items/287b9a866ef782a15ebe


### avoid_single_cascade_in_expression_statements
- [ドキュメント](https://dart-lang.github.io/linter/lints/avoid_single_cascade_in_expression_statements.html)
- 式文では単一のカスケードを避ける

```dart
// こういった用法を避ける、だってカスケードの使い方として間違っている
cake..bake();

// こうする
cake..bake();

// 本来カスケードはこう使う
cake
  ..bake()
  ..putStrawberryOnTheTop()
  ..eat();
```

https://qiita.com/colorrabbit/items/c03a5eb9ecb2b23469a4

### implicit_dynamic_variable
*変数の型を明示的にする*

```dart
// 変数（_createdAt）の型が明示的になっていない
final _createdAt = data['createdAt'];

// こんな感じにする
final _createdAt = data['createdAt'] as DateTime;
```

↑のようにするか、解析オプションファイルから implicit-dynamic を削除する

https://qiita.com/colorrabbit/items/7efd86faacfcd35a6e74


### unnecessary_lambdas
- [ドキュメント](https://dart-lang.github.io/linter/lints/unnecessary_lambdas.html)
- `DON'T create a lambda when a tear-off will do.`
    - `tear-offが可能な場合は、ラムダを作成しないでください。`
    - つまり、`メソッドに渡された引数と同じ引数でメソッドを呼び出す関数がある場合、呼び出しをラムダでラップしないようにしましょう`、ということ
    - tear-offとは、メソッドと同じパラメータを取り、それを呼び出すクロージャのこと


```dart
// ダメ、よくあるやり方
listItems.forEach((eachList) {
  print(eachList);
});

// こうする、便利
listItems.forEach(print);
```

### curly_braces_in_flow_control_structures
- [ドキュメント](https://dart-lang.github.io/linter/lints/curly_braces_in_flow_control_structures.html)
- `DO use curly braces for all flow control structures.`
    - `すべてのフロー制御構造に中括弧を使用してください`

```dart
// if文の際、 {} を省略せずにちゃんと書く
if (todayIsApril) {
  print('Spring has come!');
} else {
  print('Please wait for Spring.');
}

// こうしちゃダメ、JSなどに慣れているとやりがちかもしれません
if (todayIsSummer)
  return print('Too hot!');

// 例外: これはOK、else文がないif文で、bodyが1行の短文の場合
if (isAutumn) return '🌰';
```

## その他
- 今後随時追記していきます

## 参考
- [Effective Dart: Usage](https://dart.dev/guides/language/effective-dart/usage)
- https://medium.com/flutter-jp/analysis-b8dbb19d3978
