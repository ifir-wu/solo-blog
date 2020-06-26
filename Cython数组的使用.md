title: Cython数组的使用
date: '2019-09-09 15:56:50'
updated: '2019-09-09 15:59:12'
tags: [Cython]
permalink: /articles/2019/09/09/1568015810489.html
---
![](https://img.hacpai.com/bing/20181207.jpg?imageView2/1/w/960/h/540/interlace/1/q/100) 

## Cython数组

首先写个fun.c，用于给Cython调用。注意需要传递给function一个整型指针参数

fun.c

```c
#include <stdio.h>
#include "fun.h"

void function(int *A, int length)
{
    for (int i = 0; i < length; i++)
    {
        A[i] += 10;
    }
}
```

### 第一种方法

_fun.pyx

```cython
# distutils: sources = fun.c

cimport cython

cdef extern from "fun.h":
    void function(int *A, int length);

@cython.boundscheck(False)  #省去了所有的数组越界检查， 当你知道下标访问不会越界的时候可以使用它
@cython.wraparound(False)   #消除了相对数组尾部的负数下标的处理（类似 Python 列表）
def fun(int[:] numbers):
    function(<int *> &numbers[0], numbers.shape[0])

```

参数`type[:]`表示一维的数组，`type[:,:]`表示二维数组，以此类推，使用`<int *> &numbers[0]`将数组转化为C指针。

main.py

```python
import fun
import numpy

b = numpy.array([1,2,3,4,5],dtype=int)
fun.fun(b)
print(b)
```

### 第二种方法

_fun.pyx

```cython
cimport cython

import numpy as np
cimport numpy as np

cdef extern from "fun.h":
    void function(int *A, int length);

@cython.boundscheck(False)  #省去了所有的数组越界检查， 当你知道下标访问不会越界的时候可以使用它
@cython.wraparound(False)   #消除了相对数组尾部的负数下标的处理（类似 Python 列表）
def fun(np.ndarray[int, ndim=1, mode="c"] numbers not None):
    function(<int *> np.PyArray_DATA(numbers), numbers.shape[0])
```

由于在`.pyx`文件中使用了`cimport numpy as np`，那么`setup.py`中应该把关于numpy的文件一并编译

setup.py

```python
from distutils.core import setup
from distutils.extension import Extension
from Cython.Build import cythonize
import numpy

setup(
    name="My fun app",
    ext_modules = cythonize(
        [
            Extension(
                "fun",
                ["pyhello.pyx","fun.c"],
            )
        ],
        compiler_directives = {'language_level': 3}, 
        annotate=True,
    ),
    include_dirs=[numpy.get_include()] # 如果在.pyx文件中cimport了numpy，那么需要在这里加入这一句
                                       # 以便将关于numpy的文件一并编译
)
```

~~网上很多教程都将`include_dirs=[numpy.get_include()]`放入`Extension`中，但我测试发现，放在`Extension`是无效的。~~

尽管如此，在编译时依然会收到编译器中的以下警告，因为 Cython 使用的是已弃用的 Numpy API：

```powershell
Compiling pyhello.pyx because it changed.
[1/1] Cythonizing _fun.pyx
running build_ext
building 'fun' extension
creating build
creating build\temp.win-amd64-3.7
creating build\temp.win-amd64-3.7\Release
D:\ProgramData\Anaconda3\Library\mingw-w64\bin\gcc.exe -mdll -O -Wall -DMS_WIN64 -ID:\ProgramData\Anaconda3\lib\site-packages\numpy\core\include -ID:\ProgramData\Anaconda3\include -ID:\ProgramData\Anaconda3\include -c pyhello.c -o build\temp.win-amd64-3.7\Release\_fun.o
In file included from D:\ProgramData\Anaconda3\lib\site-packages\numpy\core\include/numpy/ndarraytypes.h:1824:0,
                 from D:\ProgramData\Anaconda3\lib\site-packages\numpy\core\include/numpy/ndarrayobject.h:12,
                 from D:\ProgramData\Anaconda3\lib\site-packages\numpy\core\include/numpy/arrayobject.h:4,
                 from pyhello.c:609:
D:\ProgramData\Anaconda3\lib\site-packages\numpy\core\include/numpy/npy_1_7_deprecated_api.h:14:9: note: #pragma message: D:\ProgramData\Anaconda3\lib\site-packages\numpy\core\include/numpy/npy_1_7_deprecated_api.h(14) : Warning Msg: Using deprecated NumPy API, disable it with #define NPY_NO_DEPRECATED_API NPY_1_7_API_VERSION
 #pragma message(_WARN___LOC__"Using deprecated NumPy API, disable it with " \
         ^
pyhello.c: In function '__Pyx_ImportType':
pyhello.c:6028:13: warning: unknown conversion type character 'z' in format [-Wformat=]
             "%s.%s size changed, may indicate binary incompatibility. "
             ^
pyhello.c:6028:13: warning: unknown conversion type character 'z' in format [-Wformat=]
pyhello.c:6028:13: warning: too many arguments for format [-Wformat-extra-args]
D:\ProgramData\Anaconda3\Library\mingw-w64\bin\gcc.exe -mdll -O -Wall -DMS_WIN64 -ID:\ProgramData\Anaconda3\lib\site-packages\numpy\core\include -ID:\ProgramData\Anaconda3\include -ID:\ProgramData\Anaconda3\include -c hello.c -o build\temp.win-amd64-3.7\Release\fun.o
writing build\temp.win-amd64-3.7\Release\fun.cp37-win_amd64.def
D:\ProgramData\Anaconda3\Library\mingw-w64\bin\gcc.exe -shared -s build\temp.win-amd64-3.7\Release\pyhello.o build\temp.win-amd64-3.7\Release\hello.o build\temp.win-amd64-3.7\Release\hello.cp37-win_amd64.def -LD:\ProgramData\Anaconda3\libs -LD:\ProgramData\Anaconda3\PCbuild\amd64 -lpython37 -lmsvcr140 -o E:\VSCode\Cython\fun.cp37-win_amd64.pyd
```

其中警告在13-21行，目前，这只是一个警告，可以忽略。

main.py

```python
import fun
import numpy

b = numpy.array([1,2,3,4,5],dtype=int)
fun.fun(b)
print(b)
```
