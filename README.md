# VisuArche
A node.js library that builds semantic markup from visual/presentation styling. 

## 説明
VisuArche（ビジュアルケイと読みます）は見た目重視型マークアップ（HTML要素の`style`属性、Bootstrap、Atomic/Functional CSS）からセマンティックなつながりを抽出して論理的に整理されたCSSとHTMLに変換するNode.jsモジュールです。

## 例
以下の様なHTMLがあったとします。

```html
<!-- source.html -->
<p style="margin: 0 0 2em; padding-inline-start: 1em;">○○○○</p>
<p style="margin: 0 0 2em; padding-inline-start: 1em;">××××</p>
```

これをコンパイルした際に、以下の様なHTMLとCSSに変換します。

```html
<!-- source-compiled.html -->
<p>○○○○</p>
<p>××××</p>
```

```css
/* compiled.css */
p {
    margin: 0 0 2em;
    padding-inline-start: 1em;
}
```

### 抽出方法
抽出方法としては、以下の通りから選べます。

1. 要素名：デフォルトです。同じ要素に同じスタイルが適用されている場合、一致するスタイルを全て要素のスタイルとして抽出します。差分はクラスでCSS定義されます。一部の要素にのみクラスが付いていた場合、他の要素と同じスタイルならすべての同じ要素にクラスを付けることを提案します。また、スタイルの差分をそのクラスに抽出します。
2. クラス：スタイルの一致するすべての要素に同じクラスを適用します。クラス名の初期値はランダムですが、反映前に変更も可能です。ただし、クラス付けされている要素に関してはそのクラスにスタイルを展開するかどうか選択できます。
3. 入力タイプ：`<input>`および`<button>`のみに適用されるルールです。各要素の`type`属性に合わせてCSSを抽出します。
