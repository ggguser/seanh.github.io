---
draft: true
sitemap: false
robots: noindex, nofollow
---

How to Use Vim's Built-in Help
==============================

Vim has a comprehensive built-in manual. Unfortunately you need some help to know how to use the help.
This post is a quick reference and tutorial for Vim's <kbd>:help</kbd> files.

<div class="seealso" markdown="1">
#### See also

* <kbd>:help</kbd> opens Vim's "main help file" ([`help.txt`](https://vimhelp.org/)).
  There's a short tutorial on how to use the help files at the top.
  
* <kbd>:help helphelp</kbd> opens [`helphelp.txt`](https://vimhelp.org/helphelp.txt.html),
  which is the full documentation for the `:help` commands and how to use the help files.

* The Getting Started pages of the docs also have a [Finding Help](https://vimhelp.org/usr_02.txt.html#02.8) section
  (<kbd>:help 02.8</kbd> from within Vim)
  
* You can browse and search all of the help pages online at <https://vimhelp.org/>
  (you _don't_ want to use the copy at <http://vimdoc.sourceforge.net/>, it's hopelessly out of date)
</div>

## Opening the help window

<kbd>:help</kbd> (or just <kbd>:h</kbd>) opens the "main help file" (the front page of the help manual, `help.txt`)
in a new window.
<kbd>F1</kbd> also does the same thing. The <kbd>Help</kbd> key on your keyboard might also work if it has one.
Use <kbd>:vert help</kbd> to open it in a vertical split instead of a horizontal one,
or <kbd>:tab help</kbd> to open it in a new tab.
I don't think it's possible to open a help file in or in-place-of the current non-help window.
If there's already a help window open <kbd>:help</kbd> will use that window instead of opening a new window
(even if the cursor is currently in a different window).

<kbd>:help {subject}</kbd> (or just <kbd>:h {subject}</kbd>) opens the help tag `{subject}`.
`{subject}` can be lots of different types of thing:

* Topics, e.g.
  [<kbd>:help deleting</kbd>](https://vimhelp.org/change.txt.html#deleting)
  or <kbd>[:help options](https://vimhelp.org/options.txt.html)</kbd>

* Normal-mode commands:
  <kbd>[:help x](https://vimhelp.org/change.txt.html#x)</kbd>
  or <kbd>[:help cc](https://vimhelp.org/change.txt.html#cc)</kbd>.
  
  Use `ctrl-` for commands that're prefixed with <kbd>Ctrl</kbd>, e.g.
  <kbd>[:help ctrl-a](https://vimhelp.org/change.txt.html#CTRL-A)</kbd>.
  
  Use `_` for multi-key commands, e.g.
  <kbd>[:help ctrl-w_w](https://vimhelp.org/windows.txt.html#CTRL-W_W)</kbd>.
  
  `^` also works insead of `ctrl`, e.g.
  <kbd>:help ^p</kbd> is the same as <kbd>:help ctrl-p</kbd>.

  Names of special keys need to be wrapped in angle brackets, e.g.
  <kbd>[:help ctrl-w_<Up>](https://vimhelp.org/windows.txt.html#CTRL-W_%3CUp%3E)</kbd>.
  
* Insert-mode commands have an `i_` prefix, e.g.
  <kbd>[:help i_ctrl-r](https://vimhelp.org/insert.txt.html#i_CTRL-R)</kbd>

* Visual-mode commands have a `v_` prefix,
  e.g. <kbd>[:help v_o](https://vimhelp.org/visual.txt.html#v_o)</kbd 

* Ex commands start with `:`, e.g.
  <kbd>[:help :substitute](https://vimhelp.org/change.txt.html#:substitute)</kbd>

* Keyboard commands that you can use when in Vim's command-line mode start with
  `c_`, for example
  <kbd>[:help c_ctrl-r](https://vimhelp.org/cmdline.txt.html#c_CTRL-R)</kbd>.
  
  Special characters for use in Ex commands also use `c_`, for example:
  <kbd>[:help c_%](https://vimhelp.org/cmdline.txt.html#c_%)</kbd>.

* Vim command-line arguments start with `-`, e.g.
  <kbd>[:help -t](https://vimhelp.org/starting.txt.html#-t)</kbd>

* The names of settings have to be wrapped in single quotes, e.g.
  <kbd>[:help 'number'](https://vimhelp.org/options.txt.html#'number')</kbd>

* Error messages have their own help tags, e.g. [<kbd>:help E37</kbd>](https://vimhelp.org/message.txt.html#E37)

* And more! See <kbd>[:help help-summary](https://vimhelp.org/usr_02.txt.html#help-summary)</kbd> for the complete list of help tag types.

## Closing the help window

<kbd>:q</kbd> or <kbd>ZZ</kbd> will close a help window like any other window if the cursor is in the help window.

<kbd>:helpclose</kbd> or <kbd>:helpc</kbd> will close the help window even if the cursor isn't in it.

## Navigating in the help window

<kbd><kbd>Ctrl</kbd>-<kbd>]</kbd></kbd> opens the help tag under the cursor.

<kbd><kbd>Ctrl</kbd>-<kbd>t</kbd></kbd> or <kbd><kbd>Ctrl</kbd>-<kbd>o</kbd></kbd> goes back to the previous location.


## Searching for help topics

<kbd>:help {subject}</kbd> (or just <kbd>:h {subject}</kbd>) opens the help tag `{subject}`.
`{subject}` can include wildcards like `*`, `?` or `[a-z]`.

If there are multiple help tags matching the given subject it open the "best" match.
See <kbd>:help {subject}</kbd> (literally) for details of the algorithm. 

You can use <kbd><kbd>Ctrl</kbd> + <kbd>d</kbd></kbd> or <kbd>Tab</kbd> to search for tag names.
For example type <kbd>:help buffer</kbd> and then instead of <kbd>Enter</kbd> press
<kbd><kbd>Ctrl</kbd> + <kbd>d</kbd></kbd> or <kbd>Tab</kbd> to see a list of all help tags
matching "buffer".

## Searching the full text of help files with `:helpgrep`

<kbd>:helpgrep {pattern}</kbd> or <kbd>:helpg {pattern}</kbd> does a full-text search of all help files
for `pattern` and opens the first match.
It populates the quickfix list with all the matches so you can use quickfix commands like
<kbd>:cn</kbd> to go to the next match, <kbd>:cp</kbd> to go to the previous match,
<kbd>:copen</kbd> to open the quickfix window with the list of all matches.

Patterns are case-sensitive, regardless of the `ignorecase` setting, unless you append `\c` to the end of the pattern.

<kbd>:lhelpgrep</kbd> (or just <kbd>:lh</kbd>) does the same but uses the per-window location list (of the help window) instead of the quickfix list.
