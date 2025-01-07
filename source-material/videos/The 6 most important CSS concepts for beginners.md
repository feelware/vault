---
tags:
  - "#video-notes"
src-date: 2022-01-04
src-author:
  - Kevin Powell
src-link: https://youtu.be/JnTPd9G6hoY
---
# The 6 most important CSS concepts for beginners

## Inheritance

- Rely on inheritance as much as possible rather than trying to style everything individually. You can later on pick and choose where do you want to break out of inheritance.
- **Only font properties are inherited**.
- Certain elements such as `button`, `input`, `textarea`, and `select` don't inherit font properties. You can solve it like this:

```css
button,
input,
textarea,
select {
	font: inherit;
}
```

## The Cascade

When many rulesets applied to the same element affect the same property, the one below gets preference (assuming all rulesets have the same level of [specificity](#Specificity)). In the example below, `background-color: purple` overrides `background-color.

![](utilities/attachments/Pasted%20image%2020241024184804.png)

You can use devtools to inspect where each declaration is being made, both the applied and the overwritten, as shown in the example above. Keep in mind that, in devtools, the cascade is "inverted". Specific declarations and those that are "winning" are on the top, while inherited declarations are below.

![](utilities/attachments/Pasted%20image%2020241024191841.png)

## The box model

Make sure of setting this:

```css
*,
*::before,
*::after {
	box-sizing: border-box;
}
```

This way, padding will grow *inwards*, not altering the width of the element in any way, as opposed to the default `box-sizing: content-box`.

## Specificity

(See [[Specificity (CSS)]])

- **Low specificity**: Element selectors (`body`, `h1`, `p`)
- **Medium specificity**: Class selectors (`.foo`)
- **High specificity**: ID selectors (`#bar`)

Specificity matters more than the cascade when deciding which declarations will "win".

## Creating layouts

- Choose either `flexbox` or `grid` to start with, preferably `grid`.
- Once you get used to it, add the other one to your arsenal.

## Content vs Layout

Don't set layout and style content in the same class, separate them in different classes. If the same `div` needs both layout and content styling, add both classnames to it.

```css
.dark-background {
	background-color: #333;
	color: white;
}

.columns {
	display: grid;
	gap: 1em;
	grid-template-columns: 1fr 1fr 1fr;
}
```

```html
<div class="dark-background columns">
	<div class="card">1</div>
	<div class="card">2</div>
	<div class="card">3</div>
</div>
```
