Higher Order Functions in JS

[youtube](https://www.youtube.com/watch?v=H4awPsyugS0&list=PLRqwX-V7Uu6aAEUqu96Newc-7qpuh-cxc)

# Higher Order Functions
之所以叫这个名字，关键在于理解啥是Higher，到底高在了哪里。
因为一般的function只返回一些特定的值。
而这个higher order function可以把function当成参数传入，而这些传入的function又通常由我们自己定义。所以他叫higher order function。

比如这篇笔记的下面列举的map(), reduce()等都是高阶函数。

# =>的基础认识
## 作用：让代码更简洁
## 功能含义

“代表后面的function”(个人理解)

## Example
比如说，这是一个基本的想法
我想定义一个【可以构造函数】的函数,它是一个乘法器，可以自定义乘以多少。

1. 定义
可以像下面这样写,定义返回一个function
```js

function multiplier(factor){
	return function(x){ //此处的x只是一个构造的“虚设位置”，它代表未来真正使用时被传入的数值。
	return x * factor;
	}
}

```

2. 执行
然后在控制台可以执行
```js

let doubler = multiplier(2); // 构造了一个乘法器，设定是乘以2,然后返回结果

doubler(3); //就会执行 3*2 ，返回 6


```

3. 进入正题，使用 => ，可以让定义更简洁
```js

//原本
function multiplier(factor){
	return function(x){ 
	return x * factor;
	}

//简化。如果有多个参数，多行内容，可以这样写。

(x)=>{
return x * factor;
}

//简化至一行。如果只有一行，可以简到最简,连括号和return都省去。
x =>  x * factor;


//所以，最终可以写成：

function multiplier(factor){
	return x =>  x * factor;
	}

```

4. 心理练习
看到`=>`，可以在心理练习暗想，“这是一个函数，x是传参代号”


# =>施展拳脚的地方
返回新数组的Array Function
## 群体魔法 map()
map()是一个“群体魔法”，它会使用数组里的每一个值进行传参得到结果，最后再返回出一个对应的“结果”数组。
```js

let vals = [4,8,1,2];
console.log(vals);

//如果想放到新的数组里这样写
let newVals = vals.map(x=> x*2); 
console.log(newVals);

//如果想覆盖原数组里这样写
vals = vals.map(x=> x*2); //数组中的每一项都被传入箭头函数里处理。x就是数组里每一项的“代号”

//log:[8,16,2,4]
```

## fill()
**fill()不是一个高阶函数。写在这里只是为了对比一下map**
fill也是一个群体魔法，但是它的主要作用是在原位填充某个值，就像倒入油漆一样，人人都相等（是同一个值）
```js

let vals = new Array(10);
vals = vals.fill(0);

//就会得到有10个0的数组。

vals = vals.map(()=>Math.random()); //这就对每一个位置都放入了一个随机数,=>前面是空的是因为我不需要传参进random去。


```

上面的内容，甚至可以这样写
```js
vals = Array(100).fill().map(()=>Math.random);
//fill在这里的作用仅仅是使这些项不为空，这样map才能起作用。

```

## 累加器 reduce()
[MDN Docs](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce)   [youtube](https://www.youtube.com/watch?v=-LFjnY1PEDA&list=PLRqwX-V7Uu6aAEUqu96Newc-7qpuh-cxc&index=3)

升序累加器（很奇怪，为什么叫reduce这个名字）。
它的核心作用就是，对数组从0开始累加执行某个命令。

格式是 `arrayName.reduce(累加器fnt,当前值val) `.

当前值可以不写。
当`当前值`不写的时候，默认最初的当前值为`数组的第一个元素`(相当于当前值为0)；如果设定了， 就是这个当前值+整个数组遍历后的结果。

累加器的性质是个function，当前值是个数值。

最简单的例子，真正的“累加”。一个计算总数的功能
```js
let vals = [3,4,5,1]
let sum = vals.reduce( (acc,val) => acc + val);//得到13
```

还可以用它来找最大值
```js
let vals = [3,4,5,1];

function findMax(acc,val){

if (val > acc){
acc =val;
}
return acc;
}

let biggest = vals.reduce(findMax);

```

利用=>简化写法
```js

let vals = [3,4,5,1];

(acc,val)=>{
if (val > acc)acc =val;
return acc;
}

let biggest = vals.reduce(findMax);

```

甚至，用三元运算符
`a>b? a:b`  如果真，返回a；如果假，返回b；


```js

let vals = [3,4,5,1];


let biggest = vals.reduce((a,b)=> a>b? a:b);

//(a,b)=> a>b? a:b 只相当于第一个参数，第二个参数现在没有写，所以默认是数组里的第一个值

```


## 过滤 filter()
filter是个过滤器，只留下返回值为true的对象。
注意，它返回的是一个新的过滤后的数组。要覆盖的话自己手动写一下。
[youtube](https://www.youtube.com/watch?v=qmnH5MT_luk&list=PLRqwX-V7Uu6aAEUqu96Newc-7qpuh-cxc&index=4)

例：判断该项是否为偶数。
```js
let vals = [3,4,5,1];

function isEven(num){
return (num%2 ==0)  
}

vlas.filter( isEven )//数组中的每一项，都被传入isEven里去执行

```

简化：
```js
let vals = [3,4,5,1];

return


vlas = vlas.filter( x=> x%2 == 0)// 结果是true的留下。

vlas = vlas.filter( x=> x%2)// 更简，因为这个结果不是0就是1，也对应着false和true


```

另一个例子，筛选文本
在js里使用正则表达式
`/写入内容/` 在两个斜杠里写入内容。
这里匹配的是非字母的内容`\W`,个数是{1,无限}`+`，即`/\W+/`
```js
let s = "It was a dark and stormy night."

let words = s.split(/\W+/).filter(word => word.length >= 3);
console.log(words);

```

 
  /n
## 排序 sort() 
[youtube](https://www.youtube.com/watch?v=MWD-iKzR2c8&list=PLRqwX-V7Uu6aAEUqu96Newc-7qpuh-cxc&index=5)

sort()可以让数组里按某个规则排序。不写的时候，只是按它的规则来排，只能识别数字和字母。

接着上面那个例子，我们可以试着把分割出来的单词，按长度来排序。
```js
let s = "It was a dark and stormy night."

let words = s.split(/\W+/).filter(word => word.length >= 3);
console.log(words);

words.sort((a,b) => b.length - a.length);//

```

# 综合应用
[粒子的例子](https://www.youtube.com/watch?v=m9bRVQ_-DXY&list=PLRqwX-V7Uu6aAEUqu96Newc-7qpuh-cxc&index=6)

创建一个数组装下粒子时，可以直接使用
`particles = Array(100).fill().map(p => new Particle())`

for loop 1
```js

for(let p of particles){
p.update();
p.show();
}



```

for loop2
```js
particles.forEach(p => p.update());
particles.forEach(p => p.show());

```


删除死亡粒子
```js

particles = particles.filter(p => !p.isFinished());//只留下还没结束的
```


按亮度排序粒子
```js

particles.sort((a,b) => a.col - b.col );
```
