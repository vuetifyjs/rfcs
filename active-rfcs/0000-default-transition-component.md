# Overview

- Start Date: 2020/02/08
- Target Major Version: 3.0
- Reference Issues: (Github, Stack Overflow, etc)
- Implementation PR: (leave this empty)

## Summary

## Basic example

Demonstrate the new or changed API if applicable.

```html
<!-- Example -->

<v-transition 
  in="slide-x" 
  out="fade-out"
>
  <div v-if="foobar">...</div>
</v-transition>

<v-transition 
  transition="slide-x" 
  @transitionend="onEnd"
  @transitionstart="onStart"
>
  <div v-if="foobar">...</div>
</v-transition>

<!-- Usage with Skeleton Loader -->

<v-skeleton-loader :loading="isLoading">
  <v-transition transition="fade" appear>
    <div>...</div>
  </v-transition>
</v-skeleton-loader>
```

## Motivation

Why is this change necessary? What does it improve within the framework?

Please focus on explaining the motivation so that if this RFC is **not** accepted,
the motivation could be used to develop alternative solutions. In other words,
enumerate the constraints you are trying to solve without coupling them too
closely to the solution you have in mind.

## Detailed design

This is the bulk of the RFC. Explain the design in enough detail for somebody
familiar with Vue to understand, and for somebody familiar with the
implementation to implement. This should get into specifics and corner-cases,
and include examples of how the feature is used. Any new terminology should be
defined here.

## Drawbacks

Why is this change necessary? What does it improve within the framework?

- implementation cost, both in term of code size and complexity
- whether the proposed feature can be implemented in userland
- integration of this feature with other existing and planned features
- cost of migrating existing Vuetify applications (is it a breaking change?)

There are tradeoffs to choosing any path. Attempt to identify them here.

## Alternatives

What other designs have been considered? What is the impact of not doing this?

## Adoption strategy

If this proposal is implemented, please consider the following:

- What steps would existing Vuetify users need to take in order to upgrade their project?
- How does this RFC affect projects in the Vuetify ecosystem?
- Can we implement a change into [eslint-plugin-vuetify](https://github.com/vuetifyjs/eslint-plugin-vuetify)

## Unresolved questions

If applicable, what aspects of this proposal are still TBD?

---

All questions pertaining to this template should be directed to the Vuetify commmunity [#rfc-discussions](https://discord.gg/eXubxyJ) channel.
