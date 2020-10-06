# Overview

- Start Date: 2019-01-09
- Target Major Version: 3.x
- Reference Issues: (Github, Stack Overflow, etc)
- Implementation PR: (leave this empty)

## Summary

Change how presets are used by end-user and with it how typings for it are defined

## Basic example


```js
// v2.x

import Vue from 'vue'
import Vuetify from 'vuetify'
import { preset } from 'some-preset'

Vue.use(Vuetify)

const vuetify = new Vuetify({
	preset,
	theme: {
		dark: true
	}
})

// v3.x

// typing for preset would be VuetifyPreset | VuetifyPreset[]
// and if an array is passed, all entries are merged together

import { createApp } from 'vue'
import Vuetify from 'vuetify'
import { preset } from 'some-preset'

Vue.use(Vuetify, {
	preset: [preset, {
		theme: {
			dark: true
		}
	}]
})
```

## Motivation

To me it feels quite odd to have a structure like this:

```tsx
{
	preset: VuetifyPreset,
	...VuetifyPreset
}
```

The way it is currently typed also makes it way too loose:

```tsx
interface UserVuetifyPreset {
	preset?: VuetifyPreset
	[key: string]: any
}

// it won't complain about misspelled or superfluous properties
const preset: UserVuetifyPreset = {
	theme: { ... },
	something: { ... },
}
```

## Detailed design

N/A

## Drawbacks

- There will be a migration cost for end-users since the syntax will change

## Alternatives

What other designs have been considered? What is the impact of not doing this?

## Adoption strategy

Users would have to update their code to reflect changes in syntax. However since there are other breaking changes with how vuetify will be instantiated in 3.x, this will just be one more thing to do at the same time.

## Unresolved questions

N/A

---

All questions pertaining to this template should be directed to the Vuetify commmunity [#rfc-discussions](https://discord.gg/eXubxyJ) channel.
