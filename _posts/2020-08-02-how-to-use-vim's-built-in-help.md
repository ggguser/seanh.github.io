---
draft: true
sitemap: false
robots: noindex, nofollow
---

How to Use Vim's Built-in Help
==============================

See <kbd>:help help</kbd> for Vim's manual about using its built-in help files.
Here's a quick cheat sheet:

## Opening help

<kbd>:help</kbd> (or just <kbd>:h</kbd>) opens the "main help file" (the front page of the help manual, `help.txt`).
Use <kbd>:vert help</kbd> to open it in a vertical split instead of a horizontal one,
or <kbd>:tab help</kbd> to open it in a new tab.
I don't think it's possible to open a help file in the current window.

## Navigating between pages within help

<kbd><kbd>Ctrl</kbd>-<kbd>]</kbd></kbd> opens the help tag under the cursor.
<kbd><kbd>Ctrl</kbd>-<kbd>t</kbd></kbd> or <kbd><kbd>Ctrl</kbd>-<kbd>o</kbd></kbd> goes back to the previous location.

## Closing the help window

<kbd>:q</kbd> or <kbd>ZZ</kbd> will close a help window like any other window if the cursor is in the help window.
<kbd>:helpclose</kbd> or <kbd>:helpc</kbd> will close the help window even if the cursor isn't in it.

## Searching for help

<kbd>:help options</kbd> searches for subject "options" and opens the best-matching help page
:help subject<Ctrl-d> to see matches

:tag pattern and :tnext when in the help window, or :tselect

:helpgrep searches the contents of help files, puts list of matching files into quickfix list
Always case-sensitive regardless of ignorecase setting, add \c to ignore case
