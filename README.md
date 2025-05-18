Dotfiles usage in notebooks
===========================

## Installation

```bash
!apt-get install vim tmux powerline zsh stow
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
. ~/.dotfiles/source.sh
country
```


### Line amd Cell magic

In a code cell execute:
```python
from IPython.core.magic import register_line_cell_magic

@register_line_cell_magic
def mysh(line, cell=None):
    command = line
    if cell:
        command += '\n' + cell
    get_ipython().system(f"zsh -i -c '. ~/.dotfiles/source.sh; {command}'")
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

### Extension

This is only available if the `.dotfiles` has also stwoed `ipython`. This can be done as follows
```bash
%%script zsh
cd ~/.dotfiles
stow ipython
```

After this you can use the following in your notebook to load the extension:
```python
$load_ext dotfiles
```

If for some reason you get a `ModuleNotFoundError: No module named 'dotfiles'`, it might be that the extensions is not part of the `sys.path`. This can be fixed with:

```python
import sys, os
sys.path.append(os.path.expanduser("~/.ipython/extensions"))
```
