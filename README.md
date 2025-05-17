Dotfiles usage in notebooks
===========================

### Installation
```bash
!apt-get install vim tmux powerline zsh
!git clone https://github.com/gbraad/dotfiles.git ~/.dotfiles
!~/.dotfiles/install.sh
```

or

```bash
!curl -fsSL https://dotfiles.gbraad.nl/install.sh | sh
```

### Usage

```zsh
%%script zsh
. ~/.zshrc.d/dotfiles.zsh
dotfiles resource
country
```
