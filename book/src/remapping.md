# Key remapping

Helix currently supports one-way key remapping through a simple TOML configuration
file. (More powerful solutions such as rebinding via commands will be
available in the future).

To remap keys, create a `config.toml` file in your `helix` configuration
directory (default `~/.config/helix` on Linux systems) with a structure like
this:

```toml
# At most one section each of 'keys.normal', 'keys.insert' and 'keys.select'
[keys.normal]
C-s = ":w" # Maps Ctrl-s to the typable command :w which is an alias for :write (save file)
C-o = ":open ~/.config/helix/config.toml" # Maps Ctrl-o to opening of the helix config file
a = "move_char_left" # Maps the 'a' key to the move_char_left command
w = "move_line_up" # Maps the 'w' key move_line_up
"C-S-esc" = "extend_line" # Maps Ctrl-Shift-Escape to extend_line
g = { a = "code_action" } # Maps `ga` to show possible code actions
"ret" = ["open_below", "normal_mode"] # Maps the enter key to open_below then re-enter normal mode

[keys.insert]
"A-x" = "normal_mode"     # Maps Alt-X to enter normal mode
j = { k = "normal_mode" } # Maps `jk` to exit insert mode
```

## Minor modes

Minor modes are accessed by pressing a key (usually from normal mode), giving access to dedicated bindings. Bindings
can be modified or added by nesting definitions.

```toml
[keys.insert.j]
k = "normal_mode" # Maps `jk` to exit insert mode

[keys.normal.g]
a = "code_action" # Maps `ga` to show possible code actions

# invert `j` and `k` in view mode
[keys.normal.z]
j = "scroll_up"
k = "scroll_down"

# create a new minor mode bound to `+`
[keys.normal."+"]
m = ":run-shell-command make"
c = ":run-shell-command cargo build"
t = ":run-shell-command cargo test"
```

## Custom descriptions

Remapping of singular typable commands or seqences of any commands, can be given a custom description for the keymap menus (infoboxes).
This is the text on each row that's paired together with each key event trigger.

```toml
[keys.normal]
A-k = { description = "Edit Config", exec = ":open ~/.config/helix/config.toml" }
# (Note that the example example above mostly for illustrative purposes, a :config-open is provided out of the box.)
"C-r" = { "description" = "Sort selection", "exec" = ["split_selection_on_newline", ":sort", "collapse_selection", "keep_primary_selection"]             }
```

A custom descriptions can also be defined for sub-menus.
Aside from being them being shown in the parent-menu infobox,
sub-menu descriptions also act as infobox titles for the submenu itself.

```toml
# A submenu accessed though space->f in normal mode.
[keys.normal.space.f]
description = "File"
f = "file_picker"
s = { description = "Save", exec = ":write" }
c = { description = "Format", exec = ":format" }
```

## Special keys and modifiers

Ctrl, Shift and Alt modifiers are encoded respectively with the prefixes
`C-`, `S-` and `A-`. Special keys are encoded as follows:

| Key name     | Representation |
| ---          | ---            |
| Backspace    | `"backspace"`  |
| Space        | `"space"`      |
| Return/Enter | `"ret"`        |
| \-           | `"minus"`      |
| Left         | `"left"`       |
| Right        | `"right"`      |
| Up           | `"up"`         |
| Down         | `"down"`       |
| Home         | `"home"`       |
| End          | `"end"`        |
| Page Up      | `"pageup"`     |
| Page Down    | `"pagedown"`   |
| Tab          | `"tab"`        |
| Delete       | `"del"`        |
| Insert       | `"ins"`        |
| Null         | `"null"`       |
| Escape       | `"esc"`        |

Keys can be disabled by binding them to the `no_op` command.

<<<<<<< HEAD
A list of commands is available in the [Keymap](https://docs.helix-editor.com/keymap.html) documentation
 and in the source code at [`helix-term/src/commands.rs`](https://github.com/helix-editor/helix/blob/master/helix-term/src/commands.rs) at the invocation of `static_commands!` macro and the `TypableCommandList`.
=======
Making a mode "sticky" can be achieved by adding `sticky = true` to the mapping. 
(Predefined sticky keytries can like wise be made unsticky with `sticky = false`.)

Commands can be found at [Keymap](https://docs.helix-editor.com/keymap.html) Commands.
> Commands can also be found in the source code at [`helix-term/src/commands.rs`](https://github.com/helix-editor/helix/blob/master/helix-term/src/commands.rs) at the invocation of `static_commands!` macro and the `TypableCommandList`.
>>>>>>> a0d918a47a7fa7ddeaf07963e148ce4993bb9020
