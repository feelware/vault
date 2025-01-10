---
tags:
  - "#video-notes"
src-date: 2021-12-23
src-author:
  - Kevin Powell
src-link: https://youtu.be/u044iM9xsWU
---
# Learn flexbox the easy way

- As soon as you add `display: flex` to an element, its direct children become flex items, overriding whatever `display` they might have (such as `block`, which is default for `li` elements).
- By default, flex items' length have a `fit-content`-like behavior: they try to be `max-content` if there's enough space in the parent, but they're allowed to shrink (wrapping their own content) if the parent runs out of space (see [`flex-shrink`](#`flex-shrink`)), and as soon as they reach `min-content`, they overflow the parent.

## `flex-shrink`

- Item property, defaults to `1`.
- Allows items to shrink their content if the parent runs out of space.
- As seen in the example below, if `flex-shrink` is set to `0`, the items overflow as soon as the parent can't keep their size as `max-content` within one "row".

![Pasted image 20241026155922](../../utilities/attachments/Pasted%20image%2020241026155922.png)

## `flex-grow`

- Item property, defaults to `0`.
- Allows items to take up the entire space available on the parent.
- The size of each item is proportional to their intrinsic size. Setting different `flex-grow` values on different items affects this proportion.

![Pasted image 20241026155835](../../utilities/attachments/Pasted%20image%2020241026155835.png)

## `flex-wrap`

- Parent property, defaults to `no-wrap`.
- When set to `wrap`, allows items to `wrap` if they exceed one "row" (assuming `flex-direction: row`).

![with `flex-grow: 0`](../../utilities/attachments/Pasted%20image%2020241026161011.png)

![with `flex-grow: 1`](../../utilities/attachments/Pasted%20image%2020241026155812.png)

- Items long enough for the parent to keep as `max-content` are allowed to shrink, as seen in the example below.

![Pasted image 20241026161221](../../utilities/attachments/Pasted%20image%2020241026161221.png)

## `flex-basis`

- Item property, defaults to `auto`.
- Similar to `width` (again, assuming `flex-direction: row`), sets the initial width of a flex item. From there, items grow or shrink if the parent has extra space or not enough space, depending on their `flex-grow` and `flex-shrink` values, respectively.

## `flex`

- Item property.
- Shorthand property for `flex-shrink`, `flex-grow`, and `flex-basis`.
- Setting all items' `flex` to `1` makes them take up equal length of the parent. More specifically, it sets `flex-shrink` to 1, `flex-grow` to 1, and `flex-basis` to 0.

## `justify-content` vs `align-items`

- Both are parent properties.

### `justify-content`

- Main axis distribution.
- Think of word processors' text justification options: left, right, center, and justify.
- Values: `flex-start` (default), `flex-end`, `center`, `space-between`, `space-around`, `space-evenly`.

## `align-items`

- Cross axis distribution.
- Think of an unaligned queue of people: some are skewed to the left; others, to the right.
- Values: `stretch` (default), `flex-start`, `flex-end`, `center`.
- For it to be noticeable, elements must have different lengths on the cross axis: different heights for `row`, and different widths for `column`. In other words, there must be empty space along the cross axis.
- Because there aren't multiple elements along the cross axis, it wouldn't make sense to have `space-*` values.

## `align-self`

- Item property.
- Allows a particular item to break out of its parent's `align-items`.
- There's no such thing as `justify-self` in flexbox. It is a `grid` property.
