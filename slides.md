---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: true
# some information about the slides, markdown enabled
info: |
  ## なぜSvelteを選ぶのか
  [GitHub](https://github.com/baseballyama/slides-svelte)
# persist drawings in exports and build
drawings:
  persist: false
favicon: "svelte.png"
fonts:
  sans: 'Robot'
  serif: 'Robot Slab'
  mono: 'Fira Code'
download: true
exportFilename: 'svelte.pdf'

---

# なぜSvelteを選ぶのか

baseballyama

<div class="abs-br m-6 flex gap-2">
  <a href="./svelte.pdf" download alt="pdf"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-download />
  </a>
  <a href="https://github.com/baseballyama/slides-svelte" target="_blank" rel="noopener noreferrer" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

---

<div class="flex items-center justify-center h-1/1">
  <h1>Svelteとは何か</h1>
</div>
---

<div style="height: 100%; width: 100%;">
<iframe src="https://svelte.dev/"
  height="170%"
  width="170%"
  style="transform:scale(0.6);-o-transform:scale(0.6);-webkit-transform:scale(0.6);-moz-transform:scale(0.6);-ms-transform:scale(0.6);transform-origin:0 0;-o-transform-origin:0 0;-webkit-transform-origin:0 0;-moz-transform-origin:0 0;-ms-transform-origin:0 0;"
></iframe>
</div>

---

# Svelteとは何か

- 1. 記述量が少ない
- 2. 仮想DOMがないので高速
- 3. 直感的なリアクティビティ

---

# 1. 記述量が少ない

このようなSvelteでは145文字で実現できる処理が...

<div style="height: 100%; width: 100%;">
<iframe src="https://svelte.dev/repl/embed?example=blog-write-less-code"
  height="150%"
  width="170%"
  style="transform:scale(0.6);-o-transform:scale(0.6);-webkit-transform:scale(0.6);-moz-transform:scale(0.6);-ms-transform:scale(0.6);transform-origin:0 0;-o-transform-origin:0 0;-webkit-transform-origin:0 0;-moz-transform-origin:0 0;-ms-transform-origin:0 0;"
></iframe>
</div>
---

# 1. 記述量が少ない

Reactでは442文字必要です...

```js
import React, { useState } from 'react';

export default () => {
	const [a, setA] = useState(1);
	const [b, setB] = useState(2);

	function handleChangeA(event) {
		setA(+event.target.value);
	}

	function handleChangeB(event) {
		setB(+event.target.value);
	}

	return (
		<div>
			<input type="number" value={a} onChange={handleChangeA}/>
			<input type="number" value={b} onChange={handleChangeB}/>

			<p>{a} + {b} = {a + b}</p>
		</div>
	);
};
```
---

# 1. 記述量が少ない

Vueでは263文字必要です...

```js
<template>
	<div>
		<input type="number" v-model.number="a">
		<input type="number" v-model.number="b">

		<p>{{a}} + {{b}} = {{a + b}}</p>
	</div>
</template>

<script>
	export default {
		data: function() {
			return {
				a: 1,
				b: 2
			};
		}
	};
</script>
```
---

# 1. 記述量が少ない

- コードのサイズに応じてバグの数は二次関数的に増えます
- 大抵の場合10行のPRは100行のPRと比較して高い密度のレビューが行われます
- 1個のモジュールが1画面に収まらない場合、認知負荷は大幅に増加します
- Svelteは記述量が少ないだけでなく自然と読みやすいコードを記述できるように設計されています


参考 : https://svelte.dev/repl/embed?example=blog-write-less-code
---

# 1. 記述量が少ない

もう一度Svelteのコードを見てみましょう

<div style="height: 100%; width: 100%;">
<iframe src="https://svelte.dev/repl/embed?example=blog-write-less-code"
  height="150%"
  width="170%"
  style="transform:scale(0.6);-o-transform:scale(0.6);-webkit-transform:scale(0.6);-moz-transform:scale(0.6);-ms-transform:scale(0.6);transform-origin:0 0;-o-transform-origin:0 0;-webkit-transform-origin:0 0;-moz-transform-origin:0 0;-ms-transform-origin:0 0;"
></iframe>
</div>
---

# 2. 仮想DOMがないので高速

- 2013年 [PeteHunt](https://www.youtube.com/watch?v=x7cQ3mrcKaY)は仮想DOMにより実DOM操作の回数を減らすことで高速化できることを説明しました
- しかし、実DOMの更新箇所を特定するために仮想DOMを比較する作業はコストがかかります
- React / Vue / Angular で実現したいことは、宣言的UIの実現でした (仮想DOMは手段です)
- 宣言的UIを仮想DOMなしで実現できることがわかったため、Svelteが生まれました

参考 : https://svelte.dev/blog/virtual-dom-is-pure-overhead

---

# 2. 仮想DOMがないので高速

2019年、Rich Harris はReactの性能を計測しました...

<div class="flex items-center justify-center mt-12">
<iframe width="560" height="315" src="https://www.youtube.com/embed/AdNJ3fydeao?start=1150" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

---

# 2. 仮想DOMがないので高速

Svelteで同じことを実行すると...明らかにReactよりもスムーズです

<div class="flex items-center justify-center mt-12">
<iframe width="560" height="315" src="https://www.youtube.com/embed/AdNJ3fydeao?start=1250" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>
</div>

---

# 3. 直感的なリアクティビティ

React / Vue などのフレームワークは、独自のHooksを実装しました

```jsx{all|6}
// Reactの場合
import React, { useState } from 'react';

function Example() {
  // Declare a new state variable, which we'll call "count"
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>
        Click me
      </button>
    </div>
  );
}
```

---

# 3. 直感的なリアクティビティ

React / Vue などのフレームワークは、独自のHooksを実装しました

```vue{all|5-6}
<!-- Vueの場合 -->
<script setup>
  import { ref } from "vue";

  const count = ref(0);
  const setCount = () => (count.value += 1);
</script>

<template>
  <p>You clicked {{ count }} times</p>
  <button onClick="{setCount}">Click me</button>
</template>

```

---

# 3. 直感的なリアクティビティ

<p>
Svelteチームは、最高のAPIはAPIが全くないことだと気がつきました。<br />
スプレッドシートが良い例です。<br />
スプレッドシートは利用者が数式の依存関係を意識することなく自動的に計算結果を表示します。<br />
UIフレームワークにおけるリアクティビティも同じようにあるべきです。
</p>

```svelte{all|3-4}
<!-- Svelteの場合 -->
<script>
	let count = 0;
  const setCount = () => (count += 1);
</script>

<p>You clicked { count } times</p>
<button on:click="{setCount}">Click me</button>
```

参考 : https://svelte.dev/blog/svelte-3-rethinking-reactivity

---

<div class="flex items-center justify-center h-1/1">
  <h1>私たちがSvelteを使うと決めた理由</h1>
</div>

---

# とにかく学習しやすい (Svelte)

非常に洗練された学習プラットフォーム

<div style="height: 100%; width: 100%;">
<iframe src="https://svelte.dev/tutorial/adding-data"
  height="150%"
  width="170%"
  style="transform:scale(0.6);-o-transform:scale(0.6);-webkit-transform:scale(0.6);-moz-transform:scale(0.6);-ms-transform:scale(0.6);transform-origin:0 0;-o-transform-origin:0 0;-webkit-transform-origin:0 0;-moz-transform-origin:0 0;-ms-transform-origin:0 0;"
></iframe>
</div>

---

# とにかく学習しやすい (Svelte)

すぐに試せるREPL

<div style="height: 100%; width: 100%;">
<iframe src="https://svelte.dev/repl/hello-world"
  height="150%"
  width="170%"
  style="transform:scale(0.6);-o-transform:scale(0.6);-webkit-transform:scale(0.6);-moz-transform:scale(0.6);-ms-transform:scale(0.6);transform-origin:0 0;-o-transform-origin:0 0;-webkit-transform-origin:0 0;-moz-transform-origin:0 0;-ms-transform-origin:0 0;"
></iframe>
</div>

---

# とにかく学習しやすい (Svelte)

豊富なサンプル集

<div style="height: 100%; width: 100%;">
<iframe src="https://svelte.dev/examples/area-chart"
  height="150%"
  width="170%"
  style="transform:scale(0.6);-o-transform:scale(0.6);-webkit-transform:scale(0.6);-moz-transform:scale(0.6);-ms-transform:scale(0.6);transform-origin:0 0;-o-transform-origin:0 0;-webkit-transform-origin:0 0;-moz-transform-origin:0 0;-ms-transform-origin:0 0;"
></iframe>
</div>

---

# とにかく学習しやすい (Svelte)

日本語訳の学習プラットフォームもあります

<div style="height: 100%; width: 100%;">
<iframe src="https://svelte.jp/tutorial/basics"
  height="150%"
  width="170%"
  style="transform:scale(0.6);-o-transform:scale(0.6);-webkit-transform:scale(0.6);-moz-transform:scale(0.6);-ms-transform:scale(0.6);transform-origin:0 0;-o-transform-origin:0 0;-webkit-transform-origin:0 0;-moz-transform-origin:0 0;-ms-transform-origin:0 0;"
></iframe>
</div>

---

# とにかく学習しやすい

<div class="my-2">
Svelte kit にも
<a 
  href="https://learn.svelte.dev/tutorial/welcome-to-svelte"
  target="_blank"
  rel="noopener noreferrer"
  alt="Svelte Kit"
  class="inline-block">
    <span class="mb-2">同様の学習サイト</span>
</a>
があります
</div>
---

# 状態管理が標準で用意されている

<div style="height: 100%; width: 100%;">
<iframe src="https://svelte.dev/examples/auto-subscriptions"
  height="160%"
  width="170%"
  style="transform:scale(0.6);-o-transform:scale(0.6);-webkit-transform:scale(0.6);-moz-transform:scale(0.6);-ms-transform:scale(0.6);transform-origin:0 0;-o-transform-origin:0 0;-webkit-transform-origin:0 0;-moz-transform-origin:0 0;-ms-transform-origin:0 0;"
></iframe>
</div>

---

# トランジション・アニメーションを簡単に実装できる

<div style="height: 100%; width: 100%;">
<iframe src="https://svelte.dev/examples/adding-parameters-to-transitions"
  height="160%"
  width="170%"
  style="transform:scale(0.6);-o-transform:scale(0.6);-webkit-transform:scale(0.6);-moz-transform:scale(0.6);-ms-transform:scale(0.6);transform-origin:0 0;-o-transform-origin:0 0;-webkit-transform-origin:0 0;-moz-transform-origin:0 0;-ms-transform-origin:0 0;"
></iframe>
</div>

---

# Webフレームワークである Svelte kit がある

Next.js / Nuxt の Svelte 版です。まだベータ版です。

- Viteを使用した素晴らしい開発体験を提供 (高速な起動 / 高速なHMR)
- SPAとSSRのいいところどり
- ファイルシステムルーター
- SEO

<div style="height: 100%; width: 100%;">
<iframe src="https://kit.svelte.dev/"
  height="100%"
  width="170%"
  style="transform:scale(0.6);-o-transform:scale(0.6);-webkit-transform:scale(0.6);-moz-transform:scale(0.6);-ms-transform:scale(0.6);transform-origin:0 0;-o-transform-origin:0 0;-webkit-transform-origin:0 0;-moz-transform-origin:0 0;-ms-transform-origin:0 0;"
></iframe>
</div>

---

# その他 (一部を抜粋)

- 構文が直感的
- 記述量が少ない
- head要素を細かく管理できる (`<svelte:head>`)
- テンプレート内で定数を宣言できる (`{@const}`)
- 動的に要素を出し分けられる (`<svelte:element>`)

<br />

```svelte{all|5-7|9-10|11}
<script>
	let boxes = [{width: 3, height: 4}, {width: 10, height: 20}];
</script>

<svelte:head>
	<link rel="stylesheet" href="/tutorial/dark-theme.css">
</svelte:head>
{#each boxes as box}
	{@const area = box.width * box.height}
	{@const tag = area > 100 ? "h1" : "h4"}
	<svelte:element this="{tag}">{box.width} * {box.height} = {area}</svelte:element>
{/each}
```
---

<div class="flex items-center justify-center h-1/1">
  <h1>Svelteの使いどころ</h1>
</div>

---

# Svelteの使いどころ

- 1. 新規Webアプリケーション
- 2. 性能 / バンドルサイズを気にするアプリケーション
- 3. 既存のWebアプリケーションの一部に組み込む
- 4. Webコンポーネントとして配布する

---

# Svelteの使いどころ (新規Webアプリケーション)

<div class="mb-8">
  <p>
  ここまでの紹介でSvelteが良いと感じた方は新規アプリはSvelteで作成してみてはいかがでしょうか。<br />
  Svelteの強みの1個は、作者のRich Harris が NYTimes で実際に使われながら改善を続けてきたことです。<br />
  </p>
</div>

<div class="flex gap w-1/1">
  <div class="w-1/2 flex flex-col items-center mr-2">
    <img class="w-1/1 h-9/10" src="/note.png" />
    <span class="mt-2">Noteでは一部にSvelteが使用されているようです</span>
  </div>
  <div class="w-1/2 flex flex-col items-center ml-2">
    <img class="w-1/1 h-9/10" src="/apple-music.png" />
    <span class="mt-2">Apple Music は Svelte で作られています</span>
  </div>
</div>

---

# Svelteの使いどころ (性能 / バンドルサイズを気にするアプリケーション)

<div>
  <p>
  Svelteの性能が良いことは、以前のスライドで、ReactとSvelteの比較動画で説明しました。<br />
  ここでは、バンドルサイズについて説明します。
  </p>
</div>

<arrow v-click="1" x1="700" y1="230" x2="775" y2="335" color="#ff3e00" width="5" arrowSize="1" />

<h4>表 : バンドルサイズごとにTODOアプリを何個含めることができるか</h4>
<table>
<thead>
<tr>
<th></th>
<th>React</th>
<th>Vue</th>
<th>Preact</th>
<th>Solid</th>
<th>Svelte</th>
</tr>
</thead>
<tbody>
<tr>
<td>10kb</td>
<td>-</td>
<td>-</td>
<td>4.6</td>
<td>4.7</td>
<td>4.3</td>
</tr>
<tr>
<td>20kb</td>
<td>-</td>
<td>2.8</td>
<td>12.9</td>
<td>12.4</td>
<td>9.7</td>
</tr>
<tr>
<td>40kb</td>
<td>3.1</td>
<td>21</td>
<td>29.4</td>
<td>28.7</td>
<td>20.3</td>
</tr>
<tr>
<td>70kb</td>
<td>27.5</td>
<td>48.3</td>
<td>54.2</td>
<td>52.5</td>
<td>36.3</td>
</tr>
<tr>
<td>100kb</td>
<td>51.9</td>
<td>75.6</td>
<td>79.0</td>
<td>76.3</td>
<td>52.2</td>
</tr>
</tbody>
</table>

参考 : https://zenn.dev/jay_es/articles/2021-10-22-javascript-framework-size-comparison

---

# Svelteの使いどころ (既存のWebアプリケーションの一部に組み込む)

<div class="flex gap w-1/1" style="height: 100%; width: 100%;">
  <div class="w-1/2 flex flex-col items-center mr-2">
    <a href="https://github.com/baseballyama/svelte-in-react-ts" target="_blank" rel="noopener noreferrer" class="mb-2">Svelte in React</a>
    <div class="bg-white" style="height: 80%; width: 100%;">
      <iframe src="https://baseballyama.github.io/svelte-in-react-ts/"
        height="170%"
        width="170%"
        style="transform:scale(0.6);-o-transform:scale(0.6);-webkit-transform:scale(0.6);-moz-transform:scale(0.6);-ms-transform:scale(0.6);transform-origin:0 0;-o-transform-origin:0 0;-webkit-transform-origin:0 0;-moz-transform-origin:0 0;-ms-transform-origin:0 0;"
      ></iframe>
    </div>
  </div>
  <div class="w-1/2 flex flex-col items-center mr-2">
    <a href="https://github.com/baseballyama/svelte-in-vue3-ts" target="_blank" rel="noopener noreferrer" class="mb-2">Svelte in Vue3</a>
    <div class="bg-white" style="height: 80%; width: 100%;">
      <iframe src="https://baseballyama.github.io/svelte-in-vue3-ts/"
        height="170%"
        width="170%"
        style="transform:scale(0.6);-o-transform:scale(0.6);-webkit-transform:scale(0.6);-moz-transform:scale(0.6);-ms-transform:scale(0.6);transform-origin:0 0;-o-transform-origin:0 0;-webkit-transform-origin:0 0;-moz-transform-origin:0 0;-ms-transform-origin:0 0;"
      ></iframe>
    </div>
  </div>
</div>

---

# Svelteの使いどころ (Webコンポーネントとして配布する)

SvelteはWebComponentとしてビルドするオプションがあるので、<br />
CDNに配備することで既存のアプリから使用することができる。 

```js{all|7-9}
// vite.config.js
import { svelte } from '@sveltejs/vite-plugin-svelte';
import { defineConfig } from 'vite';

export default defineConfig({
  plugins: [
    svelte({
      compilerOptions: {
        customElement: true,
      },
    }),
  ],
});
```

但し、WebComponentのサポートは数点課題があるので、使用する際は事前に確認することをお勧めします。<br />
参考 : https://zenn.dev/tnzk/articles/835d3252ce01ed

---

# まとめ

- Svelteは少ない記述量で記述できる
- 仮想DOMがないので高速に動作する
- 直感的なリアクティビティを実現
<br /><br />
- Svelteはとにかく学習環境が整っている
- 状態管理が標準で用意されている
- トランジション・アニメーションを簡単に実装できる
- Svelte kit というWebフレームワークがあります
<br /><br />
- 既に大企業でも実績があり、安心して業務アプリでSvelteを使用できます
- 性能 / バンドルサイズを気にするアプリケーションで活躍します
- React / Vue で実装されたアプリの一部に組み込むことができます
- WebComponent としても配布できます