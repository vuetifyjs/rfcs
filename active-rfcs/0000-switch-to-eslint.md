# Overview

- Start Date: 2019-12-11
- Target Major Version: 3.0
- Reference Issues: N/A
- Implementation PR: (leave this empty)

## Summary

Switch from tslint to eslint
Add recommended settings

```js
'plugin:@typescript-eslint/eslint-recommended',
'plugin:@typescript-eslint/recommended',
'plugin:vue/recommended',
```

Add more rules

- `newline-after-var` - this rule is related to the coding standard section, but afair it's included in the recommended settings

## Basic example

```js
module.exports = {
  'root': true,
  'env': {
    'browser': true,
    'es6': true,
    'node': true,
  },
  'extends': [
    'standard',
    "plugin:@typescript-eslint/eslint-recommended",
    'plugin:@typescript-eslint/recommended',
    'plugin:vue/recommended',
  ],
  ...
}
```

## Motivation

Tslint is deprecated and is not receiving as much updates (for example for newer versions of TS) as eslint.

Some rules will also allow to automatically format the code to match the coding guidelines.

## Detailed design

N/A

## Drawbacks

There might be a moderately high cost of initial conversion from tslint to eslint and applying all required rules - depending on how much the current code is in line with them

## Alternatives

What other designs have been considered? What is the impact of not doing this?

## Adoption strategy

In case the cost of applying all recommended rules is high we can at the beginning switch some rules off and add them later.

## Unresolved questions

Which rules (that are not in the recommended settings) should we add?

---

All questions pertaining to this template should be directed to the Vuetify commmunity [#rfc-discussions](https://discord.gg/eXubxyJ) channel.
