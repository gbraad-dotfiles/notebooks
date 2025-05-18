Dotfiles usage in notebooks
===========================

## Installation

```bash
!apt-get install vim tmux powerline zsh
!git clone https://github.com/gbraad/dotfiles.git ~/.dotfiles
!~/.dotfiles/install.sh
```

or

```bash
!curl -fsSL https://dotfiles.gbraad.nl/install.sh | sh
```


## Usage

### Source inside scriptblock
```zsh
%%script zsh
. ~/.zshrc.d/dotfiles.zsh
dotfiles resource
country
```


### Line magic

In a code cell execute:
```python
from IPython.core.magic import register_line_magic

@register_line_magic
def dotfiles(line):
    return get_ipython().system(f"zsh -i -c '. ~/.dotfiles/source.sh; {line}'")
```

```zsh
!dotfiles country
"The Netherlands"
```
