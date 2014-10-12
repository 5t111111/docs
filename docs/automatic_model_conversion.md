## 自動モデル変換

### Hash -> Model

利便性のために、ある Model (モデル) の中にハッシュを入れた場合には、自動的に Model に変換されるようになっています。Model はハッシュに似ていますが、例えば永続化の機能を持っている点や、イベントをトリガできる点が異なります。

```ruby
    user = Model.new
    user._name = 'Ryan'
    user._profiles = {
      _twitter: 'http://www.twitter.com/ryanstout',
      _dribbble: 'http://dribbble.com/ryanstout'
    }

    user._name
    # => "Ryan"
    user._profiles._twitter
    # => "http://www.twitter.com/ryanstout"
    user._profiles.class
    # => Model
```

Model へのアクセス方法はハッシュとは異なります。`model[:symbol]` としてアクセスするのではなく、`model.method_name` としてメソッドを呼び出します。これは統一されたデータ保存のための機構として動的に提供されるものであり、セッター/ゲッターを追加するためにコードを書く必要はありません。

Model をハッシュに戻したい場合には、`#to_h` を実行してください。

### Array -> ArrayModel

Model の中のアレイは自動的に ArrayModel のインスタンスに変換されます。ArrayModel は通常のアレイと同様に振る舞いますが、バックエンドのデータにバインドしたり、リアクティブなイベントを発生させたりできる点が異なります。

```ruby
    model = Model.new
    model._items << {_name: 'item 1'}
    model._items.class
    # => ArrayModel

    model._items[0].class
    # => Model
    model._items[0]
```


Model や ArrayModel を通常のハッシュに戻したい場合には、それぞれ .to_h と .to_a を実行してください。(JavaScript のコードに渡すために) JavaScript のオブジェクトに変換したい場合には、`#to_n` (to native) を実行してください。

```ruby
    user = Model.new
    user._name = 'Ryan'
    user._profiles = {
      _twitter: 'http://www.twitter.com/ryanstout',
      _dribbble: 'http://dribbble.com/ryanstout'
    }

    user._profiles.to_h
    # => {_twitter: 'http://www.twitter.com/ryanstout', _dribbble: 'http://dribbble.com/ryanstout'}

    items = ArrayModel.new([1,2,3,4])
    # => #<ArrayModel:70226521081980 [1, 2, 3, 4]>

    items.to_a
    # => [1,2,3,4]
```

ArrayModel に対して .to_a を実行することで通常の配列を得ることができます。
