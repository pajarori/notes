---
title: pyjail
---

## builtins
```python showLineNumbers
# obtain builtins from a globally defined built-in functions
# https://docs.python.org/3/library/functions.html
print.__self__
__build_class__.__self__
__import__.__self__

# obtain builtins from site-module constants
# https://docs.python.org/3/library/constants.html#constants-added-by-the-site-module
help.__call__.__builtins__ # or __globals__
help.__repr__.__globals__["sys"] # can chain with sys.modules
license.__repr__.__builtins__ # or __globals__
license.__repr__.__globals__["sys"] # can chain with sys.modules

# obtain the builtins from a defined function
func.__globals__['__builtins__']
(lambda:...).__globals__

# obtain builtins from generators
(_ for _ in ()).gi_frame.f_builtins
(_ for _ in ()).gi_frame.f_globals["__builtins__"]
(await _ for _ in ()).ag_frame.f_builtins
(await _ for _ in ()).ag_frame.f_globals["__builtins__"]
```