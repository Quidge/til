# `pr-review` slash command

For years I will 'pre-review' pull requests before I push that code to colleagues. There's something about viewing code in the GitHub PR UI that casues me to catch things I don't see in my editor. Maybe it's modal and I shift into a 'reviewer' mode. I tend to catch lots of small things this way.

Usually I'll push up a PR in draft mode first, do this pre-review, fix anything I find, then switch the PR to a ready state and request colleagues to review.

Anyways, I've been using a newer slash command now with Claude Code that's become a useful tool in that process:

```
---
argument-hint: [PR-number]
description: Perform a code review on of a GitHub pull request
allowed-tools: Bash(gh pr:*)
model: claude-opus-4-1
---

Use the GitHub CLI (`gh`) to view the GitHub PR #$1. Your goal is to critique how changes in this pull request fit into the larger project.

Review all additions or changes both for code quality as well as adherence to existing project conventions and patterns. Think deeply through things like:
- Does new method belong at the level of the application?
- Is an addition at the correct level of abstraction?
- Is a new parameter name consistent with naming elsewhere in the project?

Prepare an assessment for discussion with another colleague. Use numbering for critiques so conversation about specific points can be referred to by number for faster and more exact referencing.
```

I use this in Claude Code via `/pr-review <pr number on github>`

So far 'another colleague' is just me, and I've rarely used this on someone else's PR. A very useful prompting trick in general is that `Use numbering for critiques` bit -- because of that CC will spit out critiques like:

```
1. Some problem about something
2. This isn't being considered
3. This could be improved
...
11. Another note about another thing
```

Due to this numbering I can have very terse replies that save a lot on typing, like '5, 9, 10 are good points. implement them and ignore the rest.' or 'elaborate on 3'.
