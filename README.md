# TaylorDiagram
绘制泰勒图，比其它库相比，可以指定绘制的ax，可调参数更灵活，需要手动添加legend

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
[![IPNrC5.md.png](https://s3.jpg.cm/2021/06/16/IPNrC5.md.png)](https://imagelol.com/image/IPNrC5)
