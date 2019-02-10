---
layout: post
tags: vim syntax highlighting zsh vimrc
---

Syntax highlighting can be enabled or disabled in Vim by setting<!--more--> `:syntax on` or `:syntax off`. This works well as a once off.

Adding an entry to `~/.vimrc` will set a defult for all future Vim sessions. 
Create a `.vimrc` file in user home `~/`, if it's not already there, and add the line below. 

```
syntax on
```

Run `:help vimrc` for more info on the vimrc file and initialization commands.
