+++
title = "Git Reset isn’t scary, Reflog has your back"
date = "2025-06-14T20:00:00+08:00"
draft = true

#
# description is optional
#
# description = "An optional description for SEO. If not provided, an automatically created summary will be used."

tags = ["git"]
+++

> Ever hesitated to run git reset because you’re afraid of losing your work? You’re not alone. Many developers tiptoe around Git’s reset command, especially when using the --hard flag.

**But here’s the good news: Git Reflog is your safety net.**

<br>

# What is Git Reset?

At its core, git reset moves the HEAD and optionally changes the index (staging area) and your working directory. There are three main types:

<br>

`--soft`: Keeps everything staged.

`--mixed` (default): Unstages everything, but keeps changes in your working directory.

`--hard`: Danger zone — unstages and discards working directory changes.

<br>

Scary? Maybe. But not with **Reflog.**

<br>

# Enter Reflog: Your Git Undo Button

`git reflog` records every movement of HEAD, even if it’s not in the commit history anymore. That means even if you do something drastic like:

```bash
git reset --hard HEAD~3
```

...and realize you just blew away your last few commits, you can get them back!

<br>
Just run:

```bash
git reflog
```

Find the commit you lost, then:

```bash
git checkout <commit_hash>
# or even better:
git reset --hard <commit_hash>
```

# Real-World Example

You accidentally reset too far back:

```bash
git reset --hard HEAD~2
```

Panic sets in. But wait:

```bash
git reflog
```

You see:

```bash
asdf1234 HEAD@{1}: commit: foo bar
2134asdf HEAD@{2}: commit: lorem ipsum
```

You can go back safely:

```bash
git reset --hard asdf1234
```

**Back in business.**

<br>

# TL;DR

- _git reset can be powerful and safe — if you know Reflog exists._
- `git reflog` is your time machine in Git.
- Don’t fear experimenting — Git gives you tools to recover.
- So next time you think you’ve made an irreversible mistake, just remember: Reflog has your back.
