# Neovim

## Install Neovim

install neovim

```sh
sudo pacman -S neovim
```

install pynvim

```sh
sudo pacman -S python-pynvim
```

install xclip for the use of clipboard

```sh
sudo pacman -S xclip
```

## Install neovim GUI

we choose [Neovide](https://neovide.dev/index.html)

```sh
pacman -S neovide
```

## Nvim switcher

install fzf and ripgrep

```sh
sudo pacman -S fzf
sudo pacman -S ripgrep
sudo pacman -S zip
```

there are many neovim-configuration

- NvChad
- LunarVim
- AstroNvim
- LazyVim
- kickstart.nvim

origin git clone

```sh
git clone https://github.com/NvChad/NvChad ~/.config/nvim --depth 1
```

now we change the folder

```sh
git clone https://github.com/NvChad/NvChad ~/.config/[name] --depth 1
```

I use [NvChad](https://nvchad.com/)

add these command to .zshrc

```sh
alias nvim-nvchat="NVIM_APPNAME=nvchad nvim"

function nvims() {
  # items=("default" "kickstart" "LazyVim" "NvChad" "AstroNvim")
  items=("default" "nvchad")
  config=$(printf "%s\n" "${items[@]}" | fzf --prompt=" Neovim Config  " --height=~50% --layout=reverse --border --exit-0)
  if [[ -z $config ]]; then
    echo "Nothing selected"
    return 0
  elif [[ $config == "default" ]]; then
    config="kickstart"
  fi
  NVIM_APPNAME=$config nvim $@
}
```
