

- 性能调优
`conda install line_profiler`
```
%load_ext line_profiler
%lprun -f sub_function_name parent_function_call(arg1, arg2, ...)
```

- cpu性能
```python
import cProfile

def do_cprofile(func):
    def profiled_func(*args, **kwargs):
        profile = cProfile.Profile()
        try:
            profile.enable()
            result = func(*args, **kwargs)
            profile.disable()
            return result
        finally:
            profile.print_stats()
    return profiled_func
    
@do_cprofile
def function_to_test():
...
```


# 通过retrying 库重试任意函数
@retry(stop_max_attempt_number=5)

# python创建virtual environment
1. python -m venv 路径
2. source bin/activate


# 静态检查
pylint --reports=n metrictest.py

flake8 --statistics --count metrictest.py

# clyclomatic 圈复杂度
$python -m mccabe --min 1 tools/model/naive.py

Reducing class complexity: To reduce the number of classes a class derives from.
A metric called Response For Class (RFC) is a set of methods of a class C, plus the methods on other classes called by the methods of class C. It is suggested to keep the RFC of a class in manageable limits, usually not more than 50 for small- to medium- sized systems.

# mock和stub的区别

both Mocks and Stubs answer the question, What is the result?, but Mocks also answer the question, How has the result been achieved?


没有init.py的是namespace package
a namespace package is a special kind of package designed for merging different directories of code together under a common namespace

# 打包技巧

可以在目录下建立__main__.py文件，打包目录为zip，然后 python3 zip名 即可执行

# 读data文件最好的方式
import pkgutil
data = pkgutil.get_data(__package__, 'somedata.dat')


# 生成requirements.txt
pip install pipreqs
pipreqs /path/to/project


# 检查flask函数的内存使用
```python
import memory_profiler as mp

@route
@mp.profile
def ...
```
每执行一次会打印profile stats

# 随机打乱list, inplace
```python
random.shuffle(input_list)
```

# 读有BOM的文件
```python
open(file, "r", encoding="utf-8-sig")
```

# scale numerical data

quantizing counts with fixed-with bins
```python
np.floor_divide(small_counts, 10)
np.floor(np.log10(large_counts))
```

# python 定义 deprecate警告
```python
# 定义注解
import warnings

def deprecated(func, message="默认消息"):
  def inner(*arg, **keywords):
    warnings.warn(message, DeprecationWarning)
    return func(*arg, **keywords)
  return inner

from functools import partial
DEPRECATED_SOMETHING = partial(
  deprecated,
  message="某个deprecate消息"
)

# 使用注解
@DEPRECATED_SOMETHING
def some_function():
  ...

```


# frozenset可以作为key使用


# r dataframe 转换为 pandas dataframe
```
import rpy2.robjects as ro
from rpy2.robjects import pandas2ri
from rpy2.robjects.conversion import localconverter

with localconverter(ro.default_converter + pandas2ri.converter):
    df_from_r_df = ro.conversion.ri2py(r_df)
```
