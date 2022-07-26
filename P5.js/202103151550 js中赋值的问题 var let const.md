[var let const之间的区别](https://juejin.cn/post/6844903760133619720)

# 三种声明变量的区别
**var**
的作用域更大，是函数级别。是function包起来的级别。

**let**
作用域较小，是块级别。for循环或if语句里，被花括号包起来的那些部分。

**const**
不能改变（不完全是这个意思，但先定性理解就可。）不想改变的量就用const来声明。

---

# 赋值注意前后会不会产生关系
JavaScript 通常是通过值来赋值变量。

## 1.基本数据型不会建立关系
JavaScript 基本数据类型（布尔值、null、undefined、字符串和数字）的赋值是**拷贝赋值**
基本数据类型，var1不会被var2的改变而影响。
简单点说：var str int float这类数据，如果声明一个新的量v2，把v1赋值给v2，传进去就进去了，原本的那个v1值不会因此跟v2产生什么联系而改变。
```js
let var1 = ‘My string’;
let var2 = var1;
var2 = ‘My new string’;
console.log(var1);// 'My string’
console.log(var2);// ‘My new string’
```


## 2.“复杂”数据型会建立关系
而数组，函数或对象的赋值是**引用赋值**。
说人话，就是多了个名字，数据的本质是还是那些。v2 v1都指向同一个数据，改v2，v1也会改。

```js
let var1 = { name: ‘Jim’ }
let var2 = var1;
var2.name = ‘John’;
console.log(var1);// { name: ‘John’ }
console.log(var2);// { name: ‘John’ }
```
