---
published: true
layout: post
title: "Calamares Branches"
---

The Calamares repositories are switching the
default branch -- the one where most development
happens, and where features land, and from which
releases are made -- to the *calamares* branch.

This applies to all of the currently-used Calamares repositories:
- [source](https://github.com/calamares/calamares)
- [extensions](https://github.com/calamares/calamares-extensions)
- [website](https://github.com/calamares/calamares.github.io)

Repositories not-yet-changed because of GitHub limitations:
- [wiki](https://github.com/calamares/calamares/wiki)

Repositories not-yet-changed because of coordination with downstream:
- [debian](https://github.com/calamares/calamares-debian/) -- slated for removal anyway
- [manjaro](https://github.com/calamares/calamares-manjaro/) -- slated for removal anyway
- [tools](https://github.com/calamares/calamares-tools/) -- slated for removal anyway 

To update a Calamares repository clone:

- `git fetch -p`
- `git checkout calamares`
- `git branch -d master`
