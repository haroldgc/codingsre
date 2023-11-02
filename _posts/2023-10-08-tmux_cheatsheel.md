---
layout: post
title: tmux cheatsheel
date: 2023-11-02 16:15 +0200
categories: [Systems]
tags: [Systems]     # TAG names should always be lowercase
---

# Keybindings

## Panes

+ ```c-b %``` : Split pane with horizontal layout.
+ ```c-b "``` : Split pane with vertical layout.
+ ```c-b {``` : Move pane to the left.
+ ```c-b }``` : Move pane to the right.
+ ```c-b <arrow key>``` : Switch to panel in corresponding direction.
+ ```c-b o``` : Toggle to next panel.
+ ```c-b ;``` : Toggle to last active pane.
+ ```c-b z``` : Pane zoom.
+ ```c-b !``` : Convert pane into a window.
+ ```c-b space``` : Toggle panel layout.
+ ```: setw synchronize-panes```: Send command to all panes.
+ ```c-b q``` : Show pane number.
+ ```c-b q #``` : Select pane by number.
  
# Windows

+ ```c-b c``` : Create window.
+ ```c-b #``` : Switch to window by number.
+ ```c-b ,``` : Rename current window.
+ ```c-b p``` : Switch to previous window.
+ ```c-b n``` : Switch to next window.
+ ```c-b p``` : Switch to previous window.
+ ```c-b l``` : Switch to last window.
+ ```c-b &``` : Close current window.
+ ```: swap-window -t -1``` : Move curent window to the left.

# Config file

```
set-option -g status-bg colour108
set-option -g mouse on
```

# Source 

https://tmuxcheatsheet.com/