<div align="center">
      <h1> <img src="https://github.com/Ardnys/gingerbread.nvim/blob/main/images/steep_logo_glass_gpt.png" width="200px"><br/>steep.nvim</h1>
     </div>

Steep is built upon (and somewhat inspired by) popular [gruvbox](https://github.com/ellisonleao/gruvbox.nvim) theme.

<p align="center">
    <img src="https://github.com/Ardnys/gingerbread.nvim/blob/main/images/steep_palette.png" />
</p>

# Prerequisites

Neovim 0.8.0+

# Installing

## Using `packer`

```lua
use { "Ardnys/steep.nvim" }
```

## Using `lazy.nvim`

```lua
{ "Ardnys/steep.nvim", priority = 1000 , config = true, opts = ...}
```

## Using `vim-plug`

```vim
Plug 'Ardnys/steep.nvim'
```

# Basic Usage

Inside `init.vim`

```vim
set background=dark " or light if you want light mode which doesn't work by the way
colorscheme steep
```

Inside `init.lua`

```lua
vim.o.background = "dark" -- or "light" for light mode but you really should not
vim.cmd([[colorscheme steep]])
```

# Configuration

Additional settings for steep are:

```lua
-- Default options:
require("steep").setup({
  terminal_colors = true, -- add neovim terminal colors
  undercurl = true,
  underline = true,
  bold = true,
  italic = {
    strings = true,
    emphasis = true,
    comments = true,
    operators = false,
    folds = true,
  },
  strikethrough = true,
  invert_selection = false,
  invert_signs = false,
  invert_tabline = false,
  inverse = true, -- invert background for search, diffs, statuslines and errors
  contrast = "", -- can be "hard", "soft" or empty string
  palette_overrides = {},
  overrides = {},
  dim_inactive = false,
  transparent_mode = false,
})
vim.cmd("colorscheme steep")
```

**VERY IMPORTANT**: Make sure to call setup() **BEFORE** calling the colorscheme command, to use your custom configs

## Overriding

### Palette

You can specify your own palette colors. For example:

```lua
require("steep").setup({
    palette_overrides = {
        bright_green = "#990000",
    }
})
vim.cmd("colorscheme steep")
```

### Highlight groups

If you don't enjoy the current color for a specific highlight group, now you can just override it in the setup. For
example:

```lua
require("steep").setup({
    overrides = {
        SignColumn = {bg = "#ff9900"}
    }
})
vim.cmd("colorscheme steep")
```

It also works with treesitter groups and lsp semantic highlight tokens

```lua
require("steep").setup({
    overrides = {
        ["@lsp.type.method"] = { bg = "#ff9900" },
        ["@comment.lua"] = { bg = "#000000" },
    }
})
vim.cmd("colorscheme steep")
```

Please note that the override values must follow the attributes from the highlight group map, such as:

- **fg** - foreground color
- **bg** - background color
- **bold** - true or false for bold font
- **italic** - true or false for italic font

Other values can be seen in [`synIDattr`](<https://neovim.io/doc/user/builtin.html#synIDattr()>)
