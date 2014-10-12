# Attribute Bindings

バインディングは属性内にも配置することができます。

```html
<p class="{{ if _is_cool?}}cool{{ end }}">Text</p>
```

また、要素を"双方向バインディング"とするため、特別な機能が提供されます。

```html
<input type="text" value="{{ _name }}" />
```

## CheckBoxes

In the example above, if ```_name``` changes, the field will update, and if the field is updated, ```_name``` will be changed:

```html
<input type="checkbox" checked="{{ _checked }}" />
```

If the value of a checked attribute is ```true```, the checkbox will be shown checked. If it's checked or unchecked, the value will be updated to ```true``` or ```false``` respectively.

## Radio Buttons

ラジオボタンもcheckedにバインドすることができますが、true/falseの代わりに与えられたフィールドの値がセットされます。

```html
<input type="radio" checked="{{ _radio }}" value="one" />
<input type="radio" checked="{{ _radio }}" value="two" />
```

ラジオボタンがチェックされたとき、checkedには常にフィールドの値が設定されるようにバインドされます。checkedにバインドされた値が変更されたとき、ラジオボタンのバインドされた値にマッチするすべてのフィールドがチェックされた状態になります。 checked.  メモ: ラジオボタンに対しては、この振る舞いがもっとも利便性が高いと考えています。

## Select Boxes

Select boxes can be bound to a value (while not technically a DOM property, this is another convient behavior Volt adds).

```html
<select value="{{ _rating }}">
  <option value="1">*</option>
  <option value="2">**</option>
  <option value="3">***</option>
  <option value="4">****</option>
  <option value="5">*****</option>
</select>
```

選択されたオプションが変更されると、それに合うように```_rating```が変更されます。```_rating```が変更された場合には、それにマッチする最初のオプションが選択された状態になります。マッチするオプションが存在しなかった場合には、セレクトボックスは未選択の状態になります。

