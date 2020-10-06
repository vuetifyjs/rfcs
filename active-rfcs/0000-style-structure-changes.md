# Overview

- Start Date: 1/24/2020
- Target Major Version: v3
- Reference Issues: N/A
- Implementation PR: (leave this empty)

## Summary

Clean-up style structure, normalize naming conventions. Update default styles for the code element and modify sass variable names.  

#### Related RFCs

[0003-color-class-naming-conventions](https://www.notion.so/0003-color-class-naming-conventions-49db36d317db4b04b79e4eadf9b928d3)

## Basic example

N/A

## Motivation

- Majority of our helper classes follow the naming convention `{target}-{modification}` while many areas of the framework are still using `{modification}--{target}` or `{modification}-{target}`.
- `elevations.scss` is overly verbose
- rename a few variables in `variables.scss`
    - $body-font-family → $font-family-root
    - $heading-font-family → $font-family-heading-root
    - [https://github.com/vuetifyjs/vuetify/blob/fb8432741ebe4bb4c84cf40c65826e72896c39d2/packages/vuetify/src/styles/settings/_variables.scss#L218](https://github.com/vuetifyjs/vuetify/blob/fb8432741ebe4bb4c84cf40c65826e72896c39d2/packages/vuetify/src/styles/settings/_variables.scss#L218) should be moved/removed
    - add `$code-background-color` variable with a default value of #FBE5E1
    - `$headings.h1` → `$headings.display-4` etc.
- Update code styles in `code.sass`
    - `$code-color`: #BD4147 → #C0341D
    - remove `+elevation(1)`
    - `code` `background-color` map-get($grey, 'lighten-4') → $code-background-color
    - add `dark` and `light` mode support

## Detailed design

N/A

## Drawbacks

None that I'm aware of.

## Alternatives

N/A

## Adoption strategy

As of now the user will have to:

- Update to new class names

## Unresolved questions

- I'm sure I missed a few areas

---

All questions pertaining to this template should be directed to the Vuetify commmunity [#rfc-discussions](https://discord.gg/eXubxyJ) channel.
