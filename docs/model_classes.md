## Modelクラス

デフォルトでは、すべてのコレクションはModelクラスを使用します。

```ruby
    page._info.class
    # => Model
```

標準のModelクラスの代わりに使用するクラスを提供し、それを読み込むことも可能です。クラスは /app/{component}/models フォルダに格納します。例えば、```app/main/info.rb``` という具合です。モデルとするクラスは```Model```を継承する必要があります。

```ruby
    class Info < Model
    end
```

これで、```_info```というサブコレクションにアクセスすることができます。それは```Info```のインスタンスとして読み込まれます。

```ruby
    page._info.class
    # => Info
```

これによって、コレクションにカスタムメソッドやバリデーションを設定することが可能です。
