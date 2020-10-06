- Start Date: 2019-12-26
- Target Major Version: v3.0
- Reference Issues: N/A
- Implementation PR: (leave this empty)

## Summary

N/A

## Basic Example

#### Icons

Removed the **iconfont** and **values** props. All icons are now passed at the root level. Icons import moved from `vuetify/services/icons/presets/mdi` to `vuetify/icons/mdi` for a cleaner interface.

```tsx
// Icon service
class Icons {
  icons: {
    close: 'mdi-vuetify',
    ...
  }
}

// Icon preset
const icons = {
  close: 'mdi-vuetify',
  ...
}

// Usage
import { icons } from 'vuetify/icons/mdi' // e.g. fa4, md, fa, etc..

new Vuetify({ icons })

// Customizing
import { icons } from 'vuetify/icons/fa4'

new Vuetify({
  icons: {
		...icons,
		close: 'fa fa-close',
		myCustomIcon: 'fa fa-icon',
		...
	},
})
```

#### Theme

Removed **dark** property from root of **theme service**. Is now defined within each theme. Active themes are now set by the **theme** prop. This property designates what theme is active.

```tsx
// Types
interface VuetifyTheme {
	dark?: boolean = false
	colors?: VuetifyThemeVariant
	fill?: boolean = true
}

// Theme service public interface
class Theme {
	public disabled: boolean = false
	public theme: string = 'light'
	public fallback: string = 'light'
	public themes: Record<string, VuetifyTheme>
	public get current(): VuetifyTheme
	public get dark(): boolean // returns current theme's dark value
}

// Theme options
const ThemeOptions = {
	disabled: false, // skips theme generation
	theme: 'custom', // defaults to 'light'
	fallback: 'dark', // defaults to the provided current value
	themes: {
		custom: {
			dark: false,
			colors: {
				primary: '#000000',
				secondary: '#FFFFFF',
			},
			fill: false, // Removes lighter/darker generation
		},
		dark: {
			dark: true,
			colors: {
				primary: '#E0E0E0',
				secondary: '#EEEEEE',
			},
			fill: true, // defaults to true
		},
	},
}
```

## Motivation

N/A

## Drawbacks

N/A

## Adoption Strategy

N/A

## Unresolved Questions

- How to handle existing **dark** swapping in the theme service; e.g. `$vuetify.dark = true`