+++
title = 'neovim setup for solidity'
date = 2023-10-15T00:00:00
draft = false
type = 'posts'
summary = 'It has been over 2.5 months now since the [solidity-analyzer introduction post](/posts/introducing-solidity-analyzer) and the development has been slow after the burst of development after start. Next things to do for me on `solidity-analyzer` is to add [code navigation](https://github.com/parmanuxyz/solidity-analyzer/issues/18) and...'
tags = ["solidity-analyzer", "solidity", "LSP", "ethereum", "nvim"]
+++

It has been over 2.5 months now since the [solidity-analyzer introduction post](../introducing-solidity-analyzer)
and the development has been slow after the burst of development after start. Next things to
do for me on `solidity-analyzer` is to add [code navigation](https://github.com/parmanuxyz/solidity-analyzer/issues/18)
and I have been thinking of using [tree-sitter](https://tree-sitter.github.io/tree-sitter/) for it.

I recently started using nvim again since I wanted to test the LSP with something other than VSCode too.
I figured out how to hook solidity-analyzer into nvim past week and have added the same to the 
[project readme](https://github.com/parmanuxyz/solidity-analyzer#neovim) as well and is likely to be more
up-to-date than this post.

Here's how:

```lua
local configs = require 'lspconfig.configs'
local lspconfig = require 'lspconfig'

-- Check if the config is already defined (useful when reloading this file)
if not configs.solidity_analyer_lsp then
  configs.solidity_analyzer_lsp = {
    default_config = {
      cmd = {vim.fn.expand('$HOME/.cargo/bin/solidity-analyzer-ls')},
      filetypes = {'solidity'},
      root_dir = lspconfig.util.root_pattern('foundry.toml') or function(fname)
        return lspconfig.util.find_git_ancestor(fname)
      end,
      settings = {},
    },
  }
end

lspconfig.solidity_analyzer_lsp.setup{}
```

This is what I have along with the [kickstart.nvim](https://github.com/nvim-lua/kickstart.nvim)
starter config which adds a bunch of lsp utilities and most importantly the [`on_attach`
handler for LSP](https://github.com/nvim-lua/kickstart.nvim/blob/5d8921990bf2fab9a1c9dc0d74bf1bbe1b6dc980/init.lua#L405-L448).

Another thing I have is [nvim-treesitter-context](https://github.com/nvim-treesitter/nvim-treesitter-context/) configured
for solidity. The config for which is quite simple and is more documented in their readme.

Here's my excerpt:

```lua
require "treesitter-context".setup {
  mode = "topline",
}
```
