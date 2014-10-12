# レンダリング

ユーザーがウェブページで操作をしたときの処理は、以下が典型的なものでしょう。

1. アプリケーションの状態を変える
2. DOMを更新する

例えば、ユーザーが「新しいtodoアイテムをtodoリストに追加」するためにクリックしたときの処理は、「todoアイテムを表すオブジェクトを作成し、そのアイテムをリストのDOMに追加する」といったものになると思います。  その際、オブジェクトとDOMの状態が確実に同期しておくようにするためには、多くの手間のかかる処理が必要です。

The idea of "reactive programming" can be used to simplify maintaining the DOM.  Instead of having event handlers that manage a model and manage the DOM, we have event handlers that update reactive data models.  We describe our DOM layer in a declarative way so that it automatically knows how to render what's in our our data models.

## 状態と評価について

Webアプリケーションの中心的な仕事は状態を管理することです。多くのイベントが状態を変更します。例えば、フォーム要素へテキストを入力する、ボタンをクリックする、リンク、スクロール...などなど。これらの操作はすべてアプリケーションの状態を変更するものです。かつては、ページに対するイベントは、ページが持っている状態をそれぞれ手動で変更していました。

Voltでは、アプリケーションの状態管理をシンプルにするため、すべてのアプリケーションの状態を永続化されるモデルの中に保存します。保存のしかたはオプションで様々なものを指定可能です。
このようにアプリケーションの状態を一元管理することで、ページを更新するために本来必要となるはずの複雑なコードを、かなりの分量削減することができます。また、このことでページのHTMLを宣言的に組み立てることができます。ページのモデルへの結びつきは、関数とメソッド呼び出しによってバインドされます。

モデルのデータが変更されたときには、それに応じて自動的にDOMを更新したいと考えることでしょう。To make this happen, Volt lets you "watch" any method/proc for updates.

## Computations

実例を見てみましょう。ここでは、```page```コレクションを例とします。(後でより多くのコレクションを紹介します)

はじめに、評価のための監視設定を行います。計算はProcオブジェクトに対して .watch! を実行ことで設定されます。Ruby 1.9のProcの短縮シンタックス ```-> { .. }``` を使ったProcオブジェクトで .watch! を実行しています。これを一度実行すると、以後 page._name が変更されたときに毎回Procが実行されます。
```ruby
page._name = 'Ryan'
-> { puts page._name }.watch!# => Ryan
page._name = 'Jimmy'
# => Jimmy
```

Each time ```page._name``` is assigned to a new value, the computation is run again.  また、前回の実行でアクセスされたデータのいずれかに変更があったときには、再評価が実行されます。これによって、メソッドを介してデータにアクセスしながらデータの監視を続けることができます。

```ruby
page._first = 'Ryan'
page._last = 'Stout'

def lookup_name
  return "#{page._first} #{page._last}"
end

-> do
  puts lookup_name
end.watch!# => Ryan Stout

page._first = 'Jimmy'
# => Jimmy Stout

page._last = 'Jones'
# => Jimmy Jones
```

When you call ```.watch!``` the return value is a Computation object.  In the event you no longer want to receive updates, you can call ```.stop``` on the computation.

```ruby
page._name = 'Ryan'

comp = -> { puts page._name }.watch!# => Ryan

page._name = 'Jimmy'
# => Jimmy

comp.stop

page._name = 'Jo'
# (nothing)
```

## Dependencies

TODO: Explain Dependencies

As a Volt user, you rarely need to use Comptuations and Dependencies directly.  Instead you usually just interact with models and bindings.  Computations are used under the hood, and having a full understanding of what's going on is useful, but not required.
