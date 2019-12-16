#### Pandas

* sum(): 按列计算总和 
* mean()： 算术平均值
* var()： 样本方差
* std()：样本标准差
* corr()：Spearman/Pearson 相关系数矩阵
* cov()
* skew()
* kurt()
* describe()

### Numpy

>np.meshgrid() #生成网格点坐标矩阵  等高线 SVC中超平面的绘制
>
>xx.ravel()  :表示把一个矩阵行优先展成一个向量.跟flatten一样.

> import numpy as np
> a = np.array([0, 1, 2])
> b = np.array([3, 4, 5])
> c = np.array([6, 7, 8])
> np.column_stack((a, b, c))
> array([[0, 3, 6],
>        [1, 4, 7],
>        [2, 5, 8]])
> np.row_stack((a, b, c))
> array([[0, 1, 2],
>        [3, 4, 5],
>        [6, 7, 8]])

![np](https://img-blog.csdn.net/20180109095535985?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvdHltYXRsYWI=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

### plt

```
matplotlib:plt.contourf（画等高线）
contour：轮廓，等高线
cs = plt.contour(x, y, z)
plt.clabel(cs, inline=True, fontsize=10)#inline=True，表示高度写在等高线上
```

