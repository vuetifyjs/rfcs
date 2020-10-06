# Overview

- Start Date: 2019-12-26
- Target Major Version: v3.0
- Reference Issues: N/A
- Implementation PR: (leave this empty)

## Summary

Move all components to the root of `src/components`.

## Basic Example

The component structure would move to a group of subcomponents to a flat structure:

```js
// v2.2
import VList from 'vuetify/lib'

// v3.0
import { VList } from 'vuetify/lib'
import VList from 'vuetify/lib' // would fail
```

```bash
# v3.0

. components
│
└───VList
│   └───__tests__
│   │   └───__snapshots__
│   │   │   └───VList.spec.ts.snap
│   │   └───VList.spec.ts
│   │   _mixins.scss # or sass
│   │   _variables.scss # or sass
│   │   index.ts
│   │   VList.sass
│   └───VList.ts
└───VListItem
    └───__tests__
    │   └───__snapshots__
    │   │   └───VListItem.spec.ts.snap
    │   └───VListItem.spec.ts
    │   _mixins.scss # or sass
    │   _variables.scss # or sass
    │   index.ts
    │   VListItem.sass
    └───VListItem.ts
```

This would change how sibling components (under the same folder) are imported:

```js
// v2.2.x

// components/VList/VList.ts
import VListItem from './VListItem'

export default { /* use VListItem somewhere */ }
```

```js
// v3.0.0

// components/VList/VList.ts
import { VListItem } from '../VListItem'

export default { /* use VListItem somewhere */ }
```

All components would change their export signature:

```js
// v2.2.x

// components/VList/index.ts
import VList from './VList'
import VListItem from './VListItem'

export default {
  $_vuetify_subcomponents: {
	  VList,
    VListItem,
  },
}

export {
	VList,
  VListItem,
}
```

```tsx
// v3.0

// components/VList/index.ts
export { default as VList } from './VList'

// components/VListItem/index.ts
export { default as VListItem } from './VListItem'
```

## Motivation

- Normalize how components structured

## Drawbacks

- Large in scope
- Splitting child component stylesheets up may cause more css ordering issues

## Adoption Strategy

<ins>If this proposal is implemented, what steps would existing Vuetify users need to take in order to upgrade their project?</ins>

- none - all components are exported from the `vuetify/lib` root

## Unresolved Questions

- how do we handle shared functionality:
    - shared mixins
    - shared variables
- <ins>how do we handle functional components that use the `createSimpleFunctional` fn</ins>

[0007-change-default-exports ](https://www.notion.so/0007-change-default-exports-e9ff14a3fe154cbbb9b44231f932092b)