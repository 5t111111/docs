# Content binding

もっとも基本的なバインディングはコンテンツのバインディングです。

```html
<p>Hello {{ name }}</p>
```

コンテンツのバインディングとは、{ と } の間のRubyコードを実行し、その戻り値をレンダリングするものです。Any time the data a content binding relies on changes, the binding will run again and update the text.  Text in content bindings is html escaped by default.
