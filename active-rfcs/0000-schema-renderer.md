# Overview

- Start Date: 2022-03-20
- Target Major Version: (2.x)
- Reference Issues: (Github, Stack Overflow, etc)
- Implementation PR: (leave this empty)

## Summary

Render vuetify elements tree with a JSON description.

## Basic example

```js
<temaplte>
    <v-schema-renderer :children="children" />
</template>

<script>
export default {
    data: vm => ({
        children: [
            {
                tag: 'VCard',
                props: {
                    color: 'red'
                },
                children: [
                    {
                        tag: 'VCardTitle'
                        children: 'Hello World'
                    },
                ]
            }
        ]
    })
}
</script>
```

## Motivation

I wanted to render dynamically generated JSON pages with Vuetify.
This component makes JSON parsing & rendering of components native to Vuetify framework.

## Detailed design

The component accepts a children property (an array of JSON descriptive properties of components) and renders those components with their respective properties. It includes some smart properties as well, for example support for v-for,v-show,v-model directives & automatice 2 way value bindings & event handling.

## Drawbacks

Why is this change necessary? What does it improve within the framework?

- implementation cost, both in term of code size and complexity
    a new component called VSchemaRenderer
- whether the proposed feature can be implemented in userland
    yes, but this will natively support component rendering with built in component loading capabilities
- integration of this feature with other existing and planned features
    togather this component with SchemaBuilder makes a UI Builder for Vuetify
- cost of migrating existing Vuetify applications (is it a breaking change?)
    does not break anything

## Alternatives

What other designs have been considered? What is the impact of not doing this?
You need to develop a new component to render json schemas.

## Adoption strategy

If this proposal is implemented, please consider the following:

- What steps would existing Vuetify users need to take in order to upgrade their project?
    upgrade vuetify.
- How does this RFC affect projects in the Vuetify ecosystem?
    no affect on internal structure of other components
- Can we implement a change into [eslint-plugin-vuetify](https://github.com/vuetifyjs/eslint-plugin-vuetify)

## Unresolved questions

If applicable, what aspects of this proposal are still TBD?

---

All questions pertaining to this template should be directed to the Vuetify commmunity [#rfc-discussions](https://discord.gg/eXubxyJ) channel.
