---
tags:
  - "#video-notes"
src-date: 2023-01-03
src-author:
  - Kevin Powell
src-link: https://youtu.be/a69OMEJXaJo
---
# CSS Selectors - beyond the very basics

## Descendant combinator (`a b`)

Affects all paragraphs inside `.foo` elements.

```css
.container p {
	color: red;
}
```
```html
<div class="container">
	<p>this is red</p>
	<div>
		<p>this is red too</p>
	</div>
</div>
```

## Child combinator (`a > b`)

Affects only those paragraphs that are direct descendant of `.foo` elements, excluding nested paragraphs.

```css
.container > p {
	color: red;
}
```
```html
<div class="container">
	<p>this is red</p>
	<div>
		<p>this is not red</p>
	</div>
</div>
```

## Universal selector (`*`)

Selects every single element (except pseudo-elements).

```css
* {
	box-sizing: border-box;
}
```

- Don't use to set font properties across the whole page, prefer `body` or `html`.

You can use it with combinators. In the example below, the ruleset with selector `.even-columns > *` applies to all *direct* descendants of `.even-columns`

```css
.even-columns {
	display: flex;
}

.even-columns > * {
	flex: 1;
}
```
```html
<div class="even-columns">
	<p>1</p>
	<p>2</p>
	<div>3</div>
	<section>4</section>
</div>
```

## Pseudo-classes `a:foo`

Allows to select elements based on certain conditions. #wip

```css
.primary-button:hover,
.primary-button:focus {
	background-color: white;
	border-color: black;
}

li:nth-child(even) {
	background-color: black;
	color: white;
}

article > p:first-of-type {
	font-weight: 700;
}

link:not(.nav-link) {
	color: var(--text-color-primary);
}
```

## Pseudo-elements `a::foo`

Create new DOM elements. #wip

```css
::selection {
	background-color: white;
	color: black;
}

ul > li::marker {
	content: '>'
	color: plum;
}
```

## Attribute selectors (`[]`)

Select only those elements that match the attributes specified.

```css
button[data-active] {
	background-color: var(--surface-color-contrast);
}

a[href="/"] {
	color: black;
	weight: 500;
}
```
