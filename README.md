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


### Cell/Line magic

In a code cell execute:
```python
from IPython.core.magic import register_line_cell_magic

@register_line_cell_magic
def mysh(line, cell=None):
    command = line
    if cell:
        command += '\n' + cell
    get_ipython().system(f"zsh -c 'source ~/.zshrc; {command}'")
```

#### Line magic
```zsh
%dotfiles country
```

    "The Netherlands"

#### Cell magic

```zsh
%%dotfiles
country
```

    "The Netherlands"
