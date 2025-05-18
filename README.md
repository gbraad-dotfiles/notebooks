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
%dotfiles country
```

    "The Netherlands"


### Cell magic

You can also use the following for a cell:
```python
from IPython.core.magic import register_cell_magic

@register_cell_magic
def dotfiles(line, cell=None):
    import subprocess
    command = line
    if cell:
        command += '\n' + cell
    result = subprocess.run(
        ["zsh", "-i", "-c", f". ~/.dotfiles/source.sh; {command}"], 
        capture_output=True, text=True
    )
    print(result.stdout)
    if result.stderr:
        print(result.stderr)
```

```zsh
%%dotfiles
country
```

    "The Netherlands"

> [!NOTE}
> You can use `register_line_cell_magic` instead. This will however not print the output in color.
