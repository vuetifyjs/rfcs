# Overview

- Start Date: 2019-12-22
- Target Major Version: 3.0
- Reference Issues: N/A
- Implementation PR: (leave this empty)

## Summary

Rename color classes ~~and JavaScript colors object~~ to better match how they are referenced in Material Design. 

## Basic example

Using as a class:

```js
// v2.x

.primary--text
.secondary--text.text--darken-1

.primary
.primary.darken-1

// v3.0

.text-primary
.text-secondary.text-darken-1

.bg-primary.bg-darken-1
```

Text types:

```js
// v2.x

.text--primary
.text--secondary
.text--disabled

// v3.0
// https://material.io/design/color/text-legibility.html#text-backgrounds

.text-high-emphasis
.text-medium-emphasis
.text-disabled
```

~~Usage in JavaScript:~~

```js
import { colors } from 'vuetify/util'

// v2.x
colors.red.lighten5
colors.pink.accent1

// 3.0
colors.red['50']
colors.pink['a200']
```

## Motivation

The current system borrows from Materialize CSS’s color class structure; e.g. ‘text—primary.text—darken4’. As we move into v3, this is a perfect time to not only remove the erroneous BEM syntax from the classes, but also to improve the naming conventions based on the Material Spec system, (100-900 and accents) and is more in line with our other helper classes.

## Detailed design

N/A

## Drawbacks

- Breaking change but can be automated with eslint plugin. 
- Any custom implementations with the current syntax would break

## Alternatives

N/A

## Adoption strategy

Can be mostly automated with eslint plugin. For use cases that can’t be covered, user would need to change the targeted class from:

```text
accent-1 -> bg-accent-1
accent-2 -> bg-accent-2
accent-3 -> bg-accent-3
accent-4 -> bg-accent-4

lighten-5 -> bg-lighten-5
lighten-4 -> bg-lighten-4
lighten-3 -> bg-lighten-3
lighten-2 -> bg-lighten-2
lighten-1 -> bg-lighten-1

darken-4 -> bg-darken-4
darken-3 -> bg-darken-3
darken-2 -> bg-darken-2
darken-1 -> bg-darken-1

text--lighten-5 -> text-lighten-5
text--darken-3 -> text-darken-3
```

## Unresolved questions

- ~~what does the current text—primary and text—secondary turn into~~

---

All questions pertaining to this template should be directed to the Vuetify commmunity [#rfc-discussions](https://discord.gg/eXubxyJ) channel.
