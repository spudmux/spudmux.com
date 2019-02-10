---
layout: post
tags: git gitignore global
---

When working with multiple git repositories, all needing to ignore the same files. Instead of repeating<!--more--> the entries in multiple ignore files, a global git ignore can be setup.

There are two steps to the setup, crating the file, and telling git where it is. 

## Creating the Ignore File
Create an ignore file, usually in your user folder	 `~/.gitignore`

Add some common entries, needed in multiple repositories. 

```
.*.swp
.*.swo
```

## Add it to Git
Run `git config --global core.excludesfile` to check what git currently uses, if anything. Run the command again with the new git ignore file path at the end `git config --global core.excludesfile ~/.gitignore` to add it to git.
