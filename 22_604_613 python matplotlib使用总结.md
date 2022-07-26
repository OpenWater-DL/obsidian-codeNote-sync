# 资料
[知乎的一个matplotlib详细讲解](https://zhuanlan.zhihu.com/p/93423829)

# 架构层面
.plt 和 ax.plot 
为什么matplotlib 能用不同方式来实现同一功能的原因。  
  
首先 matplotlib 架构上分为三层  
底层：backend layer  
中层：artist layer  -> 【ax.plot】
最高层：scripting layer   -> 【.plt 】
  
在任意一层操作都能够实现画图的目的，而且画出来还都一样。
但越底层的操作越细节话，越高层越易于人机交互。  
  
.plt 对应的就是最高层 scripting layer。
这就是为什么它简单上手，但要调细节就不灵了。  
  
ax.plot 是在 artist layer 上操作。基本上可以实现任何细节的调试。  
  
backend layer, 至今，我还没有见有人在这个layer上操作过。  
  
另外，对于axes (翻译就是 坐标系)，我看到有个评论写了很多，说的没有错，但也没说到点子上。  
如果大家学过大学物理的话，会知道每一个物体都有一个独立的坐标系。而matplotlib 就是引用这一理念。所以在artist layer上画多条曲线时，你会用 ax1.plot, ax2.plot ... 而最后显示在一张图上是因为所有独立坐标系对齐的结果。

# 基本概念
- 画板 figure
- 图表（轴域）Axes
>一个figure里可以包含多个Axes，就像一个画板里可以包含多个图层一样。
matplotlib里还有另一个概念叫subplot，实际它源码上引用的也是Axes，只是它被限制得更规范了。
知乎上有个比喻是, axes就像电脑上的图标一样，可以发生重叠。而subplot则是“贴紧网格模式”

- x轴 y轴： x asis , y asis
- x轴上的刻度（目盛り）　x ticks
- legend 图例（凡例）


# 声明方法
```py
import matplotlib.pyplot as plt
import japanize_matplotlib

%matplotlib inline
A = np.arange(1,5)
B = A**2
C = A**3

```
```

这个function创建了一个大小为（14，7）的画布，把这个画布赋值给变量fig，同时在这个画布上创建了一个axes，把这个axes赋值给ax。这样，所有未来的fig.xxx都是对这个画布的操作，所有ax.xxx都是对这个axes的操作。

```python
fig, ax = plt.subplots(figsize=(14,7))
# fig, ax = plt.subplots(2,1,figsize(14,7))
# ax[0].***
# ax[1].***

```
## draw
注意，我们这里依然不使用plt！因为我们要在这个axes上画数据，因此就用ax.plot()来画。画完第一个再call一次，再画第二个。

```python
ax.plot(A,B)
ax.plot(B,A)
```


## 各种信息设定

数据画好了就可以各种细调坐标轴啊，tick啊之类的。

首先把标题和xy坐标轴的标题搞定。Again, 不用plt。直接在axes上进行设定。

```python
ax.set_title('Title',fontsize=18)
ax.set_xlabel('xlabel', fontsize=18,fontfamily = 'sans-serif',fontstyle='italic')
ax.set_ylabel('ylabel', fontsize='x-large',fontstyle='oblique')
ax.legend()
```

然后是xy坐标轴的一些属性设定, 也是在axes level上完成的

```python
ax.set_aspect('equal') 
ax.minorticks_on() 
ax.set_xlim(0,16) 
ax.grid(which='minor', axis='both')
```

最后是坐标轴tick和细节，这个在axes.xaxis or axes.yaxis上完成。

```python
ax.xaxis.set_tick_params(rotation=45,labelsize=18,colors='w') 
start, end = ax.get_xlim() 
ax.xaxis.set_ticks(np.arange(start, end,1)) 
ax.yaxis.tick_right()
```

