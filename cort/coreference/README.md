## Компиляция проекта в PyCharm

Сначала компилируем файл filename.pyx в filename.c командой 

```cython -a filename.pyx```

После чего надо собрать библиотеку filename.pyd при помощи команды

```python setup.py build_ext --inplace```

Внутри файла <b>setup.py</b> должно содержаться примерно следующее 

```
try:
  from setuptools import setup
  from setuptools import Extension
except ImportError:    
  from distutils.core import setup    
  from distutils.extension import Extension

from Cython.Distutils import build_ext
import numpy as np

ext_modules = [Extension("filename",["filename.pyx"])]

setup(    
  name= 'Generic model class',    
  cmdclass = {'build_ext': build_ext},    
  include_dirs = [np.get_include()],    
  ext_modules = ext_modules)
```

Теперь, когда нужная библиотека собрана, можно запускать проект из PyCharm!
