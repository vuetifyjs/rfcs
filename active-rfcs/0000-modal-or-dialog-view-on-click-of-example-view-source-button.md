# Overview

- Start Date: 2020-11-05
- Target Major Version: 2.3.x
- Reference Issues: nil
- Implementation PR:

## Summary

This feature is a pop-up modal or v-dialog that enables users of vuetify view source code of designs/samples and the design/sample itself side by side in one view!

## Motivation

I began using vuetify about a month ago. As a Vuetify beginner, while studying the component samples or designs and viewing the source code, it was quite frustrating that on click of "view source code" the sample/design i was viewing moved down the page for the source code to show.

I wish i could view the source code of those vuetify component samples and the samples themselves at the same time.

Viewing the source code and the component side by side at the same time would really help users , especially beginners, learn how vuetify "tags" e.g v-row, v-col, e.t.c. are used to make such components, which enables them to tweak or make their own components really fast. 


## Detailed design

The design is simple, a v-dialog is set to true on click of the "view source code".

This v-dialog or pop-up modal is divided into two parts, one part shows the component sample, and the other shows the source code.

I made a tweet about this when i encoutered this problem and gave a possible solution, that was before i knew i could actually contribute!

A short video (17 seconds long) showing how it works is in this tweet. please check it out.

The link: https://twitter.com/oluwo_aji/status/1312706773820809216?s=09


## Drawbacks

I can't think of any for now

## Alternatives

I can't think of any for now

## Adoption strategy
This is a change to the user interface of the vuetify documentation. It does not affect existing users' project/projects.

It aims to provide a better user experience

---

All questions pertaining to this template should be directed to the Vuetify commmunity [#rfc-discussions](https://discord.gg/eXubxyJ) channel.
