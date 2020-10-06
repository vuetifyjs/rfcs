# Overview

- Start Date: 2020-01-08
- Target Major Version: v3.0
- Reference Issues: N/A
- Implementation PR: (leave this empty)

## Summary

## Basic example

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

## Detailed design

## Drawbacks

N/A

## Alternatives

What other designs have been considered? What is the impact of not doing this?

## Adoption strategy

N/A

## Unresolved questions

- How to handle existing **dark** swapping in the theme service; e.g. `$vuetify.dark = true`

---

All questions pertaining to this template should be directed to the Vuetify commmunity [#rfc-discussions](https://discord.gg/eXubxyJ) channel.
