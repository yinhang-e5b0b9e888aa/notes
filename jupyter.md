# jupyter

- ESC之后进入命令模式，DD删除cell，A插入cell到above，B插入cell到Below
- Shift TAB TAB，查看当前鼠标处的docstring
- 任意symbole？，相当于help symbole
- 安装extensions: conda install -c conda-forge jupyter_contrib_nbextensions
- /Users/yinhang//anaconda3/share/jupyter/nbextensions/scratchpad/main.js     改成ctrl+;
- 移动cell快捷键设置
- command + /  注释block

```javascript
%%javascript

IPython.keyboard_manager.command_shortcuts.add_shortcut('Ctrl-k', {
    help : 'move up selected cells',
    help_index : 'jupyter-notebook:move-selection-up',
    handler : function (event) {
        IPython.notebook.move_selection_up();
        return false;
    }}
);

IPython.keyboard_manager.command_shortcuts.add_shortcut('Ctrl-j', {
    help : 'move down selected cells',
    help_index : 'jupyter-notebook:move-selection-down',
    handler :  function (event) {
        IPython.notebook.move_selection_down();
        return false;
    }}
);
```


- 重新引用修改之后的包：
```python
import importlib
importlib.reload(包名)
```

# 重新加载模块

```python
import imp
imp.reload(module_name)
```
注意, imp.reload(A) 如果是from A import a,  a()的定义还是老定义，A.a()会使用新的定义


# 安装R语言的notebook

命令行打开R终端：
```
install.packages('devtools')
devtools::install_github('IRkernel/IRkernel')
IRkernel::installspec()
```


# jupyter 输入 希腊字母
输入 \sigma  然后 TAB


# cell显示行号
L

# cell切换为markdown
M

# cell切换为代码
Y


# rpy2
```
import rpy2.rinterface
%load_ext rpy2.ipython
```

一般用%%R

## R cell 引入python变量
%%R -i p_vals

## R cell 导出到python
%%R -o to_r_vals

或者::::::::::

## python cell 导出到 R
%Rpush to_r_vals

## python cell 引入 R
val_name = %Rget r_val

