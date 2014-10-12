## リアクティブ アクセサ

デフォルトの ModelController は、自分に見つからないメソッドをそのモデルにプロキシします。時には、追加のデータをリアクティブな状態で、かつコントローラーに保持させて、モデルの外側に持っておく必要があります。(普通であれば、別のコントロールかコントロールを検討するかもしれませんが)。この場合には、```reactive_accessor``` を追加することができます。それらは ```attr_accessor``` と同様の振る舞いをします。ただし、追跡して評価されるので、代入される値と戻り値はその評価された結果となります。

```ruby
  class Contacts < ModelController
    reactive_accessor :query
  end
```

Now from the view we can bind to query while also changing in and out the model.  You can also use ```reactive_reader``` and ```reactive_writer```  When query is accessed it tracks that it was accessed and will any Computations when it changes.
