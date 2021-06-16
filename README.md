# TaylorDiagram
绘制泰勒图，比其它库相比，可以指定绘制的ax，可调参数更灵活，需要手动添加legend
返回dia包含属性，他记录了所有绘制的点，可以直接调用`dia.ax.legend()`或`fig.legend()`，然后调整位置即可
## 所需库
![matplotlib](https://matplotlib.org/stable/_static/logo2_compressed.svg)
1. `matplotlib` 3.4.2及以上
2. `pandas`
3. `numpy`

## 接受参数
`ax`, `ref`, `samples`, `Normalize=False`, `markers`=[], `colors`=[], `scale`=1.2, `ms`=10, `mkwargs`={}

`ax`为绘制的参考ax

`ref`为`参考值`/`真值`的pandas.Series，即pandas.DataFrame的一列

`samples`为样本的pandas.DatsFrame，多列

`markers`和`colors`为绘制点的样式和颜色

`scale`乘积因子，获取最大的STD值`Smax`，然后将泰勒图限制在`Smax*scale`内

`ms`即markersize，标记点大小

`mkwargs`标记点的其他参数，类型为字典

`Normalize`是否归一化

## 示例
```python
import sys
sys.path.append("F:/python/NASA/matplotlib_advanced/")  # taylor_diagram.py所在目录
from taylor_diagram import TaylorDiagram
```
```python
fig, axes = plt.subplots(1, 4, figsize=(24, 6), dpi=300)
fig.subplots_adjust(bottom=0.15, top=0.8)
for months, ax in zip([[12, 1, 2], [3, 4, 5], [6, 7, 8], [9, 10, 11]], axes):
    sub_df = df[df.month.isin(months)]
    dia = TaylorDiagram(ax, sub_df.iloc[:, 5], sub_df.iloc[:, 6:], ms=12, mkwargs=dict(markeredgecolor='none'))
    dia._ax.set_title('Month in ' + str(months))
fig.legend(dia.points, [p.get_label() for p in dia.points], loc='lower center', ncol=7, frameon=False, bbox_to_anchor=(0.1, 0, 0.8, 0.1))
dia.points
```
![IPNF1t.png](https://s3.jpg.cm/2021/06/16/IPNF1t.png)


```python
fig, axes = plt.subplots(1, 4, figsize=(23, 6), dpi=300)
fig.subplots_adjust(bottom=0.15, top=0.8)
for months, ax in zip([[12, 1, 2], [3, 4, 5], [6, 7, 8], [9, 10, 11]], axes):
    sub_df = df[df.month.isin(months)]
    dia = TaylorDiagram(ax, sub_df.iloc[:, 5], sub_df.iloc[:, 6:], ms=12, mkwargs=dict(markeredgecolor='none'))
    dia._ax.set_title('Month in ' + str(months))
fig.legend(dia.points, [p.get_label() for p in dia.points], loc='lower center', ncol=7, frameon=False, bbox_to_anchor=(0.1, 0, 0.8, 0.1))
dia.points
```
![IPStGE.png](https://s3.jpg.cm/2021/06/16/IPStGE.png)
