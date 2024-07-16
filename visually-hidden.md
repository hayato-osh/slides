---
marp: true

theme: fastman

title: visually hidden を使おう
footer: #yumemi_grow

---
# visually-hidden を使おう

---
## 私は誰

- fastman
- 株式会社ゆめみ
  - フロントエンドエンジニア
  - 23卒入社
- https://x.com/fastman2nd

![w:100](https://avatars.githubusercontent.com/u/74091672?s=400&u=5a64d8292302ac121a793c6d863008e6c95c2fbd&v=4)

---

## visually-hidden とは
要素を視覚的に非表示にしつつ、スクリーンリーダーなどの支援技術には認識されるためのパターン

---
## 視覚的に非表示にする CSS
```css
display: none;

visibility: hidden;
```
これらはアクセシビリティツリーから削除されるため、
支援技術に読み上げられなくなってしまう

---
## `.visually-hidden`

```css
.visually-hidden {
	border: 0;
	clip: rect(0 0 0 0);
	width: 1px;
	height: 1px;
	margin: -1px;
	overflow: hidden;
	padding: 0;
	position: absolute;
	white-space: nowrap;
}
```

---
## Q. とはいえ、いつ使うん？

---
## A. たくさんあります！

---
## 例1：日付表示
- 2024/7/16
- 2024-7-16
- 2024.7.16

「スラッシュ」「ハイフン」「ドット」などと読み上げられてしまう

---
本来は `2024年7月16日`と表記すれば問題ない。
しかし、プロダクトの都合上、現実問題そうはいかない場合もある！

---
```html
<time datetime="2024-07-16" aria-hidden="true">2024/7/16</time>
<span class="visually-hidden">2024年7月16日</span>
```

---

## 例2：アイコンのみのボタン
```html
<button type="button">
  <span class="visually-hidden">メニュー</span>
  <span aria-hidden="true">☰</span>
</button>
```

---
`visually-hidden` ではなく `aria-label` でよくない？

```html
<button type="button" aria-label="メニュー">
  <span aria-hidden="true">☰</span>
</button>
```

---
個人的には `visually-hidden` のほうが良いと思います

---
- `aria-label` はブラウザの自動翻訳サービスの精度が不安定。
  - 翻訳されないことがある
- `visually-hidden` はあくまで視覚的に表示されないだけ

---
## ライブラリで見る Visually Hidden
- React を使っているプロダクトなら
  - [Radix UI](https://www.radix-ui.com/primitives/docs/utilities/visually-hidden)
  - [Chakra UI](https://v2.chakra-ui.com/docs/components/visually-hidden/usage)
- [Tailwind CSS](https://tailwindcss.com/docs/screen-readers)

---
## 注意
- 晴眼者にとっても伝わりづらいデザインは避けるべき
- `visually-hidden` を使う際は `aria-hidden` を使うケースも多い
- 晴眼者とスクリーンリーダーユーザー間で情報の差異がないように

---
## 最後に
適切に visually-hidden を使ってアクセシブルな Web を提供しよう

---
## 参考
- https://www.a11yproject.com/posts/how-to-hide-content/
- https://adrianroselli.com/2019/11/aria-label-does-not-translate.html
