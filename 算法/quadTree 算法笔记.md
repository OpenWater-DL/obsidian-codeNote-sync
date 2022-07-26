代码结构
# 1. sketch
	sketch里的重点是，如何使用quadtree
**setup **
创建要表现的对象（例如particles，直接数组创建）

**draw**
	1. 创建最大的quadtree。后面的会自动根据情况判断是否要分裂。
	2. 遍历表现对象。
		- ``根据表现对象，创建被侦测替代品point，插入quadtree。``
		- 表现对象(particle)，该咋show就咋show。（做move show等）
	3. 判断是否要改变表现对象的状态。
		``核心：用query返回的数组作为遍历的基准，以节省for的次数。``
		遍历所有表现对象（仅1次）；
		- 创建1个属于此粒子的判断范围Circle。
		- 查询这个范围里，quadtree里有多少个粒子。
			``let points = qtree.query(range); // return a Point array``
		- 再根据返回的粒子数组，做for循环，这样就能在小范围内遍历。
			至于要做什么判断，是看具体的目的。

# 2. QuadTree
分别写class
### 单位（方块） Rectangle(x,y,w,h)
1. 点在这个方块里 contains(point)
2. 检测框和该方块是否产生交集 intersects(range)



### 检测区域（范例用的是circle） 
Circle(x,y,r)


 ### 组织（框架） QuadTree(boundary边界,容量)
		*boundary本质是上面的单位方块.*
1. 构造函数
2. 是否要分裂
3. 是否要在此处插入点
4. 查询包含的点
		
###   被测物 Point(x,y,userData)
只需构造函数，声明存入的内容。
userData在此例中是particle，在创造这个point实例时，录入的是粒子的x,y的值，且记录了对应的是哪个粒子实例。

# 3. 应用对象particle（按需改变）