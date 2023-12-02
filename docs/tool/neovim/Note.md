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

## Autocmd in lua

create a augroup:

```lua
local group = vim.api.nvim_create_augroup("smart_markdown_enter", { clear = true })
```

create a autocmd

```lua
vim.api.nvim_create_autocmd("BufEnter", {
    group = group,
    -- use callback or command
    callback = function()
        if package.loaded["telekasten"] then vim.keymap.set("i", "[[", "<cmd>Telekasten insert_link<CR>") end
    end,
    pattern = { "*.md" },
})
```

#TODO : mkdnflow + telekasten
#TODO : marksman
#TODO : taskwirror
