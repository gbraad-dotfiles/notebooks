---
jupyter:
  jupytext:
    formats: ipynb,md
    text_representation:
      extension: .md
      format_name: markdown
      format_version: '1.3'
      jupytext_version: 1.17.3
  kernelspec:
    display_name: Python 3 (ipykernel)
    language: python
    name: python3
---

# Template

```python
import sys, os
sys.path.append(os.path.expanduser("~/.dotfiles/ipython/.ipython/extensions"))
ip = get_ipython()
ip.extension_manager.load_extension("dotfiles")
```

### Test function

```python
%%dotscript
country
```
