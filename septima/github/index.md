---
marp: true
---

# GitHub@Septima
##### https://github.com/Septima (and some other places)

---

# What is Git

* A version control system that tracks versions of files
* Made by Linus Torvalds (git means "unpleasant person") in 2005
* Works well for text files for example source code
* Works less well for binary files (but can handle them to some extent)
* Distributed

---

# What is GitHub

* Centralized Git hosting, issue tracking and project management
* Launched 2008 with rapid growth from ~2010 due to free tier and open source popularity
* Bought by Microsoft in 2018 (yay!)

---

# Why do we use GitHub?

* We need centralized Git hosting, issue tracking and project management
* One of two places that we have blessed with proper backup of what we produce (the other one is Google Drive)
* Provides versioned traceability of the work we do and allows documenting why specific work has been done
* Issue tracking (aka. poor man's project management)
* Project management ("larger" projects)

---

# Will GitHub help me use Git properly?

## For example:

* Branch strategies
* Merge conflict resolution
* Rebasing

## Answer:

* No.
* Learn Git to the extent that is required for your work

---

## Suggestions:

* Use an editor/IDE with good Git and possibly GitHub integration
* Do not use GitHub plain in browser UI for git stuff
* Do not fear git command line tools

---

# What do we *not* use at GitHub?

* Wiki
* Git LFS (large file storage)
* GitHub Actions (we use CircleCI)

---

# Best practices

* Keep it simple
* Use branch protection (not rules)
* Use issues + pull requests

## If project isn't exceptionally large

* One project - one repository
* Simple issue tracking (no project management)
* Project name = system name = host name (if applicable)
