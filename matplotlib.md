# matplotlib

# matplotlib mac 中文

1. 下载SimHei.ttf,放在 matplotlib/mpldata/fonts~/anaconda3/lib/python3.6/site-packages/matplotlib/mpl-data/fonts
import matplotlib
matplotlib.matplotlib_fname()
2. 修改matplotlibrc文件，
```
font.family         : sans-serif
font.sans-serif     : SimHei, DejaVu Sans, Bitstream Vera Sans, Lucida Grande, Verdana, Geneva, Lucid, Arial, Helvetica, Avant Garde, sans-serif
axes.unicode_minus  : False# use unicode for the minus symbol
```
3. 删除~/.matplotlib/*.
4. 重启python
*需要解决的问题：使用color codes之后中文仍然乱码*
*注意每次更新matplotlib之后都要重新操作*

添加图注释
```python
ax = sns.distplot(anesthesia_type_durations["非全麻"], kde=False, label="非全麻")
plt.title("非全麻")
plt.xlabel("时长(秒)")
plt.ylabel("记录数", rotation=0)
plt.text(0.5, 0.5, '测试', horizontalalignment="center", verticalalignment="center", transform=ax.transAxes)
```

隐藏tick
```python
plt.plot(sample_signs_ts)
plt.tick_params(
    axis="x",
    which="both",
    bottom=False,
    top=False,
    labelbottom=False
)
```

# seaborn 柱状图
```python
>>> sns.set_style('whitegrid')
>>> fig, ax = plt.subplots()
>>> biz_df['review_count'].hist(ax=ax, bins=100)
>>> ax.set_yscale('log')
>>> ax.tick_params(labelsize=14)
>>> ax.set_xlabel('Review Count', fontsize=14) 
>>> ax.set_ylabel('Occurrence', fontsize=14)
```

# 解读 pyLDAvis
A good topic model will have fairly big, non-overlapping bubbles scattered throughout the chart instead of being clustered in one quadrant.

A model with too many topics, will typically have many overlaps, small sized bubbles clustered in one region of the chart.
