# neovim attached multiple clients in cpp

change the clangd configure

```lua
local capabilities = vim.lsp.protocol.make_client_capabilities()
capabilities.offsetEncoding = 'utf-8'
require('lspconfig').clangd.setup{
    on_attach = on_attach,
    capabilities = capabilities
}
```
