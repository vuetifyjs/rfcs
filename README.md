# Vuetify RFCs

> ## *All RFCs are currently on hold until further notice.*

## What is an RFC

The **RFC** (request for comments) process is intended to provide a consistent and controlled path for new features to enter the framework.

Many changes, including bug fixes and documentation improvements can be implemented and reviewed via the normal GitHub pull request workflow.

Some changes though are _substantial_, and we ask that these be put through a bit of a design process and produce a consensus among the Vuetify [Core Team] and the [community].

## When to follow this process

You need to follow this process if you intend to make _substantial_ changes [Vuetify].

What constitutes a _substantial_ change is evolving based on community norms, but may include the following:

- A new feature that creates new API surface area
- Changing the semantics or behavior of an existing API
- The removal of features that are already shipped as part of the release channel.
- The introduction of new idiomatic usage or conventions, even if they do not include code changes to Vuetify itself.

Some changes do not require an RFC:

- Additions that strictly improve objective, numerical quality criteria (performance, quality of life)
- Fixing objectively incorrect behavior
- Rephrasing, reorganizing or refactoring
- Addition or removal of warnings

If you have any questions regarding when to follow this process, please join us in the [#rfc-discussion] channel of the [community].

## What the process is

In order to get a major feature added to Vuetify you must get your RFC merged into the this repository as a `.md` file. The following is a guide on how to get started:

- Fork the Vuetify RFC repo <http://github.com/vuetifyjs/rfcs>

- Copy `0000-template.md` to `active-rfcs/0000-my-feature.md` (where __my-feature__ is descriptive. **do not** assign an RFC number yet).

- Fill in the RFC. Put care into the details: **RFCs that do not present convincing motivation, demonstrate understanding of the impact of the design, or are disingenuous about the drawbacks or alternatives tend to be poorly-received**.

- Submit a pull request. As a pull request the RFC will receive design feedback from the larger community, and the author should be prepared to revise it in response. New RFC pull requests start in the **Pending** stage.

- Build consensus and integrate feedback. RFCs that have broad support are much more likely to make progress than those that don't receive any comments.

- Eventually, the [Core Team] will decide whether the RFC is a candidate for inclusion in [Vuetify].

- An RFC can be modified based upon feedback from the [Core Team] and [community]. Significant modifications may trigger a new _final comment_ period.

- An RFC may be rejected after public discussion has settled and comments have been made summarizing the rationale for rejection. A [Core Team] member will close the RFC's associated pull request, at which point the RFC will enter the **Rejected** stage.

- An RFC may be accepted at the close of its _final comment_ period. A [Core Team] member will merge the RFC's associated pull request, at which point the RFC will enter the **Active** stage.

Once an RFC is merged and the corresponding functionality implemented within the [Vuetify] repository, it will be part of the next _major_ or _minor_ release. Once released, the RFC will enter the **Released** stage and be locked.

## The RFC life-cycle

An RFC goes through the following stages:

- **Pending:** when the RFC is submitted as a PR.
- **Active:** when an RFC PR is merged and undergoing implementation.
- **Released:** when an RFC's proposed changes are part of a production release.
- **Rejected:** when an RFC PR is closed without being merged.

[Pending RFC List](https://github.com/vuetifyjs/rfcs/pulls)

## Why do you need to do this

It is great that you are considering suggesting new features or changes to Vuetify - we appreciate your willingness to contribute! However, as Vuetify continues to grow in size, we need to take stability more seriously, and thus have to carefully consider the impact of every change we make that may affect end users. On the other hand, we also feel that Vuetify has reached a stage where we want to start _consciously_ preventing further complexity from new API surfaces such as new components and directives.

These constraints and tradeoffs may not be immediately obvious to users who are proposing a change just to solve a specific problem they just ran into. The RFC process serves as a way to _guide_ you through our thought process when making changes to Vuetify, so that we can be on the same page when discussing why or why not these changes should be made.

## Gathering feedback before submitting

It's often helpful to get feedback on your concept before diving into the level of API design detail required for an RFC. **You may open an issue on this repo to start a high-level discussion**, with the goal of eventually formulating an RFC pull request with the specific implementation design.

## Details on Active RFCs

When an RFC enters the **Active** stage, authors may implement it and submit the feature as a pull request to the [Vuetify] repository. An RFC in the **Active** stage is not a rubber stamp, and in particular still does not mean the feature will ultimately be merged; it does mean that the [Core Team] has agreed to it in principle and are amenable to merging it.

In addition, an RFC in the **Active** stage implies nothing about what priority is assigned to its implementation, nor whether anybody is currently working on it.

Modifications to active RFC's can be done in followup PR's. We strive to write each RFC in a manner that it will reflect the final design of the feature; but the nature of the process means that we **cannot expect** every merged RFC to actually reflect what the end result will be at the time of the next _major_ release; therefore we try to keep each RFC document somewhat in sync with the language feature as planned, tracking such changes via followup pull requests to the document.

## Implementing an RFC

The author of an RFC is not obligated to implement it. Of course, the RFC author (like any other developer) is welcome to post an implementation for review after the RFC has been accepted.

An active RFC should have the link to the implementation PR listed if there is one. Feedback to the actual implementation should be conducted in the implementation PR instead of the original RFC PR.

If you are interested in working on the implementation for an **Active** RFC, but cannot determine if someone else is already working on it, feel free to ask (e.g. by leaving a comment on the associated issue).

## Reviewing RFC's

Members of the [Core Team] will attempt to review some set of open RFC pull requests on a regular basis. Please direct any questions pertaining to RFC review and / or implementation to the [#rfc-discussion] channel.

**Vuetify's RFC process owes its inspiration to the [Vue RFC process](https://github.com/vuejs/rfcs)**

[Core Team]: https://vuetifyjs.com/about/meet-the-team
[Vuetify]: https://github.com/vuetifyjs/vuetify
[#rfc-discussion]: https://discord.gg/eXubxyJ
[community]: https://discord.gg/eXubxyJ
