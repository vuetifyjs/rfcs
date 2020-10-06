# Overview

- Start Date: 2019-12-23
- Target Major Version: v3.0
- Reference Issues:
    - [https://github.com/vuetifyjs/vuetify/issues/864](https://github.com/vuetifyjs/vuetify/issues/864)
    - [~~https://github.com/vuetifyjs/vuetify/issues/5196](https://github.com/vuetifyjs/vuetify/issues/5196) (maybe)~~
    - [https://github.com/vuetifyjs/vuetify/issues/9127](https://github.com/vuetifyjs/vuetify/issues/9127)
- Implementation PR: (leave this empty)

## Summary

Rename the **goTo** service to **scroll**. Use as a centralized location for handling scroll directive functionality. Move `html` overflow designation from our CSS reset to a configurable service option. Move easing pattern and existing goTo options into default preset. Only creates a scroll listener after the first registration.

## Basic Example

Within a template:

```html
<!-- v2.2 -->
<div @click="$vuetify.goTo(0)">...</div>

<!-- v3.0 -->
<div @click="$vuetify.scroll.to(0)">...</div>
```

Easing options would move from being imported in the goTo service (now scroll service) to the default preset.

```tsx
import * as patterns from '../../services/scroll/patterns'

export const preset: VuetifyPreset = {
	scroll: {
		app: true,
		easing: 'easeInOutCubic',
		overflow: 'scroll',
		patterns,
		target: null
  }
}
```

```tsx
interface ScrollOptions {
  app = true // take the Vuetify layout into account, defaults to false when using a target other than html
  easing = 'easeInOutCubic' // can still be overwritten with inline options
  overflow = 'scroll' as 'scroll' | 'hidden' | 'auto' | 'visible' // scroll is current behavior
  patterns = {} as Dictionary<EasingFunction> // current easing patterns
  target = null | string
}

class Scroll {
	current = 0

	// all GoToOptions options

	constructor (preset: VuetifyPreset) {
		// assign all settings
		// set main scroll target's overflow
		// add event listener for main scroll target
	}

	// move over mostly what scrollable does
	onScroll (event) {
    this.current = this.target
      ? this.target.scrollTop
      : window.pageYOffset
	}

	to (
		target: VuetifyGoToTarget,
		settings?: Partial<GoToOptions> = {},
	): Promise<number> {
		// get container

		if (this.app) {
			// use vuetify
			const vuetify = useVuetify()
			
			// continue the current process
		}
	}
}
```

Scroll directive changes:

```tsx
function inserted (el: HTMLElement, binding: ScrollVNodeDirective) {
  const callback = binding.value
  const options = binding.options || { passive: true }
  const target = binding.arg ? document.querySelector(binding.arg) : window

  if (!target) {
		warn(`Unable to find scroll target ${target}`)

		return
	}

  target.addEventListener('scroll', callback, options)

  el.__scroll= {
    callback,
    options,
    target,
  }
}

function unbind (el: HTMLElement) {
  if (!el.__scroll) return

  const { callback, options, target } = el.__scroll

  target.removeEventListener('scroll', callback, options)

  delete el.__scroll
}
```

## Motivation

- The goTo service behaves differently than all other services. It does this in order to maintain backwards compatibility with v1.5’s goTo. Normalizing the structure with other services will improve readability and maintainability.
- Moving the interaction of v-scroll provides a central place for all scrolling callbacks and sets up the default scroll target default for the `v-scroll` directive.
- Provides configuration options for removing our default css reset modification to the root html element and allows them to specify a custom target, such as `v-content` (see referenced issues for additional examples).
- ~~Also paves the way for a scrollbar replacement component ([I think](https://github.com/vuetifyjs/vuetify/issues/5196)).~~

## Drawbacks

- Requires the user to change all references of `$vuetify.goTo` to `$vuetify.scroll.to`.

## Adoption Strategy

- Change all references to `$vuetify.goTo` to `$vuetify.scroll.to`

    ```html
    <!-- In a component's template -->

    <!-- v2.2 -->
    <div @click="$vuetify.goTo(0)">...</div>

    <!-- v3.0 -->
    <div @click="$vuetify.scroll.to(0)">...</div>
    ```

    ```tsx
    // In a component's script

    export default {
      methods: {
    		onClick () {
    			// v2.2.x
    			this.$vuetify.goTo(0)
    			
    			// v3.0
    			this.$vuetify.scroll.to(0)
    		},
    	},
    }
    ```

- Can be automated with our eslint plugin

## Unresolved Questions

N/A