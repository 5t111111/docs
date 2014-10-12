# Controls

Everyone wishes that we could predict the scope and required features for each part of our application, but in the real world, things we don't expect to grow large often do and things we think will be large don't end up that way.  Controls let you quickly setup reusable code/views.  The location of the controls code can be moved as it grows without changing the way controls are invoked.

To render a control, simply use a tag like so:

```html
    <:control-name />
```

or

```html
    <:control-name></:control-name>
```

To find the control's views and optional controller, Volt will search the following (in order):

| セクション | ビューのファイル | ビューのフォルダー | コンポーネント |
|------------|------------------|--------------------|----------------|
| :{名称}    |                  |                    |                |
| :body      | {名称}.html      |                    |                |
| :body      | index.html       | {名称}             |                |
| :body      | index.html       | index              | {名称}         |
| :body      | index.html       | index              | gems/{名称}    |

**もし名称とフォルダーが一致した場合、ビューのフォルダーにあるすべてがコントローラーを読み込むことに注意してください*。*


上記のそれぞれについての説明は以下の通りです:

1. セクション
ビューはセクションから構成されます。セクションは ```<:セクション名>``` で始まり、閉じタグはありません。Volt はまず同じビュー内のセクションを探します。

2. views
Next Volt will look for a view file with the control name.  もしそこで見つかれば、ビューの body セクションにレンダリングします。

3. ビューのフォルダー
上記で見つからなければ、Volt はビューのフォルダーの中で、コントローラーの名前のファイル、もしくは index.html を探します。そして、:body セクションにレンダリングされます。もしコントローラーがビューのフォルダーに存在した場合には、そのコントローラーのインスタンスが新しく生成され、そのインスタンスでレンダリングが行われます。

4. コンポーネント
次に、app/ 以下のすべてのフォルダーをチェックします。対象となるビューのパスは {component}/index/index.html で、:body セクションを持っているものになります。

5. gem
最後に、「volt」で始まるすべての gem の app フォルダをチェックします。コンポーネントに対しても上記と同様にチェックされます。

When you create a control, you can also specify multiple parts of the search path in the name.  The parts should be separated by a :  Example:

```html
    <:blog:comments />
```

The above would search the following:

| Section   | View File    | View Folder    | Component   |
|-----------|--------------|----------------|-------------|
| :comments | blog.html    |                |             |
| :body     | comments.html| blog           |             |
| :body     | index.html   | comments       | blog        |
| :body     | index.html   | comments       | gems/blog   |

Once the view file for the control or template is found, it will look for a matching controller.  If the control is specified as a local template, an empty ModelController will be used.  If a controller is found and loaded, a corresponding "action" method will be called on it if its exists.  Action methods default to "index" unless the component or template path has two parts, in which case the last part is the action.
