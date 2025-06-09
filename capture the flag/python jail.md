---
title: pyjail
---

builtins
```python showLineNumbers
print.__self__
__build_class__.__self__
__import__.__self_

help.__call__.__builtins__
help.__repr__.__globals__["sys"]
license.__repr__.__builtins__
license.__repr__.__globals__["sys"]

func.__globals__['__builtins__']
(lambda:...).__globals__

(_ for _ in ()).gi_frame.f_builtins
(_ for _ in ()).gi_frame.f_globals["__builtins__"]
(await _ for _ in ()).ag_frame.f_builtins
(await _ for _ in ()).ag_frame.f_globals["__builtins__"]
```