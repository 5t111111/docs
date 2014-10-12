# ビュー

Voltでは、ビューにHandlebarsに似たテンプレート言語を使用します。ビューはセクションに分割することができます。例えば、セクションヘッダーは以下のようになります。

```html
<:Body>
```

セクションヘッダーは先頭が大文字で始まる必要があります。[コントロール](#コントロール)と混同しないようにしてください。また、セクションヘッダーに閉じタグは使いません。If no section header is provided, the Body section is assumed.

セクションは同じファイル上のコンテンツの異なるパーツ(タイトルと本文など)を区別するのに役立ちます。

# Bindings

In Volt, views are written in a simple template language where ruby can be inserted anywhere between ```{{``` and ```}}```.  Volt lets you use the usual flow control statements in views (```if's```, ```elsif```, ```else```, ```each```)  You can also render other views using the ```template``` binding.

# Controller Backing

While we use the controller terminology, Volt is closer to a MVVM framework.  Any method call or instance variable lookup runs in the context of a controller.  The controller

If you have a view at ```app/home/views/index/index.html``` it will load the controller at ```app/home/controller/index_controller.rb```.
