- Start Date: 2020-12-12
- Target Major Version: v3.0
- Reference Issues: N/A
- Implementation PR: https://github.com/vuetifyjs/vuetify/pull/12741

## Summary

Change how the icon service and v-icon works in v3. This includes breaking changes to both.

### Service -> Composable

Internally, the global icon configuration service will be replaced by a composable in v3. 

The configuration options available to end-users will also change. See the code below.

```ts
// V2.4

type VuetifyIcon = string | { component: Component; props?: object }

interface VuetifyIcons {
  complete: VuetifyIcon
  ...
}

interface IconOptions {
  component?: Component
  iconfont?: string
  values?: Partial<VuetifyIcons>
}

// V3

type VuetifyIcon = string | Component

interface VuetifyIcons {
  complete: VuetifyIcon
  ...
}

interface IconProps {
  tag: string
  set: string
  icon: VuetifyIcon
  disabled?: Boolean
  class?: unknown[]
  style?: Record<string, unknown> | null
}

interface IconSet {
  component: (props: IconProps) => Component
  values?: Partial<VuetifyIcons>
}

interface IconOptions {
  [key: string]: IconSet
}
```

Each icon set requires a component function used to render the icon. There will be several default types included in V3, but a custom component can of course be used as well.

The included `mdi` icon set would look something like this.

```js
import { VClassIcon } from 'vuetify'

export default {
  component: (props: IconProps) => h(VClassIcon, props),
  values: {
    ...,
  },
}
```

Usage would look like this

```js
// V2.4

new Vuetify({
  icons: {
    values: {
      mycustomicon: 'mdi-foo',
    },
  },
})

// <v-icon>$mycustomicon</v-icon>

// V3
import { VSvgIcon } from 'vuetify'
import { mdi } from 'vuetify/icons'

// Specified icon options would be merged with a set of default options
createVuetify({
  icons: {
    mdi: {
      values: {
        mycustomicon: 'mdi-foo',
      },
    },
    svg: {
      component: (props: IconProps) => h(VSvgIcon, props),
    },
  },
})

// <v-icon type="mdi" icon="$mycustomicon" />
```

### VIcon

There are two big breaking changes for VIcon

1. It no longer tries to infer what icon set an icon belongs to based on its name. There is now a `set` prop that matches a `IconSet` from the vuetify configuration.
2. It no longer uses the default slot for the icon name. Instead there is an `icon` prop. (This might not be very popular? Could possibly support default slot but make it deprecated and removed in V4?)

```html
// V2.4
<v-icon>home</v-icon>
<v-icon>mdi-home</v-icon>
<v-icon>fa-home</v-icon>

// V3
<v-icon set="material-icons" icon="home"/>
<v-icon set="mdi" icon="home"/>
<v-icon set="fa4" icon="home"/>
```

### SVG

Using simple SVG paths is easily supported

```js
// index.ts
import { VSvgIcon } from 'vuetify'

createVuetify({
  icons: {
    svg: {
      component: props => h(VSvgIcon, props),
    },
  },
})
```

```html
<v-icon type="svg" icon="M7,10L12,15L17,10H7Z" />
```

### Custom icon components

Libraries using individual components for each icon can also be used

```js
// index.ts
import { CloseIcon, HomeIcon } from 'foo-icon-library';

createVuetify({
  icons: {
    foo: {
      component: props => h(props.icon, props),
      values: {
        close: CloseIcon,
      }
    },
  },
})
```

```html
<v-icon set="foo" icon="$close" />
<v-icon set="foo" :icon="HomeIcon" />
```

## Motivation

The main motivation behind these changes are increased maintainability and extensibility. The logic necessary to infer the correct icon type is brittle and not easy to maintain or add new icon sets to.

Using a custom icon component has become slightly easier in v2.4 with the `component` option, but it is a global replacement, so that handling multiple icon types becomes the developer's responsibilty.

## Drawbacks

- Can be argued that the markup is more verbose than before
- Can be argued that ease of use is reduced since there is no longer any automatic inference

## Adoption Strategy

- If default slot is not preserved, then migration work could possibly be minimized with a codemod that tries to translate `<v-icon>mdi-home</v-icon>` to `<v-icon type="mdi" icon="home"/>` etc.

## Unresolved Questions

- Is there a better name than `values` for the mapped icons?
