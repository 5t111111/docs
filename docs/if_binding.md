# If binding

ifバインディングは、基本的な制御文を提供します。

```html
{{ if _some_check?}}
  <p>render this</p>
{{ end }}
```

Blocks are closed with a ```{{ end }}```

When the if binding is rendered, it will run the ruby code after if.  そのコードが真の場合にのみ、下のコードがレンダリングされます。Again, any changes to the branch check code will update the showing branch.

If bindings can also have ```elsif``` and ```else``` blocks.

```html
{{ if _condition_1?}}
  <p>condition 1 true</p>
{{ elsif _condition_2?}}
  <p>condition 2 true</p>
{{ else }}
  <p>neither true</p>
{{ end }}
```
