# Note

## Map in lua

```lua
local keymap_options = {
  noremap = true,
  silent = true
}
vim.api.nvim_set_keymap('t', 'jk', '<c-\\><c-n>', keymap_option)
```
mode list:

- n : Normal
- i : insert
- t : terminal
- v : visual

#TODO : mkdnflow + telekasten
#TODO : marksman
