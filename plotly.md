# plotly

# 安装
conda install -c plotly plotly-orca psutil cufflinks

## 初始化
```python
from plotly import __version__
from plotly.offline import download_plotlyjs, init_notebook_mode, plot, iplot
init_notebook_mode(connected=True)
import cufflinks as cf
print(__version__)
```

## 保存图片文件
df[..].iplot(..., asFigure=True)

或者

import plotly.graph_objs as go
import plotly.io as pio

fig = go.Figure()
pio.write_image(fig, "文件名.后缀")


## box plot 按照某一类
df.pivot(columns='publication', values='fans').iplot(
        kind='box',
        yTitle='fans',
        title='Fans Distribution by Publication')
        



