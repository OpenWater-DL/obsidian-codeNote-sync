[python中“if __name__=='__main__':”理解与总结笔记](https://www.cnblogs.com/chenhuabin/p/10118199.html)

```Py
if __name__=='__main__':

```



这句话的意思是，如果“执行该程序的文件（`__name__`），是运行程序的文件(`__main__`)”，则执行以下内容。

它的作用在于可以隔离模块引用时，不想被直接执行的内容。
例如A模块有一个print，B模块里import了A，如果A里没有这行判断，就会直接执行print；但如果有这行判断（print写在判断执行内），在运行B时，就不会运行里面的内容

若是被引用时print（`__name__`），则会输出该文件的名字。如amoudule.py就会输出amodule