[[Web/202107170948 js比较区别，Class in ES6 Vs constructor function]]
↑更新的整理。

写类
```
Class Bob{
constructor(x,y,i){
	this.x=x;
	this.y=y;
}

move(){

}

display(){

}


}
```


继承的写法：
`class 子类名 extends 父类名`

```js
//创建一个父类
class geeks {
constructor(g) {
	this.Character = g
}
}

//子类继承父类
class GeeksforGeeks extends geeks {
disp() {
	console.log("No of Character: "+this.Character)
}
}
var obj = new GeeksforGeeks(13);
obj.disp()
```

使用类：
1.创建一个类实例
```
let item = new Bob(x,y,i);
```
2.使用类
```
item.move();
item.show();
```

节省运算资源的相关做法：
[[202103141830 p5.js prototype的原型链]]