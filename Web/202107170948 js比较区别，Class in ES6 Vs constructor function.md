[详解比较class和构造function的区别](https://www.javascriptjanuary.com/blog/es6-classes)

总的来说，ES6作为一个更新的版本，它允许了类似于java的class的写法，让代码的创建和可读性变得更高。

# 定义类的语法
## ES6
要写 constructor
```js
class Dog {
      constructor (name) {
        this.name = name;
      }
    }
```


## ES5或更早
```js
function Dog (name) {
      this.name = name;
    }

    var fido = new Dog('Fido');

    console.log(fido.name); // 'Fido'
```


# prototype
## ES6
直接写在class里,就像在Processing里那样。
```js
  class Dog {
      constructor (name) {
        this.name = name;
      }
    
      sayHi () {
        return 'woof';
      }
    }

```


## ES5或更早
要另外写，而且不是写在构造函数里，很长！很分散！
```js
  function Dog (name) {
      this.name = name;
    }
    
    Dog.prototype.sayHi = function () {
      return 'woof';
    }
```


# new保护
## ES6
必须要用new才能创建实例。否则会报错。这使得程序的运行更加保险。

```js
    class Dog {
      constructor (name) {
        this.name = name;
      }
    }
    
    var fido = Dog('Fido');  
	// 报错 Class constructor Dog cannot be invoked without 'new'
	
```


## ES5或更早
不用new也会执行，如果有指定`this`，就会直接传给window。

```js
function Dog (name) {
      this.name = name;
    }
    
    // missing new keyword
    var fido = Dog('Fido');//这里相当于普通地执行了一次function
    
    console.log(fido); // undefined :(
    console.log(window.name); // 'Fido' :(
```

# 继承
## ES6
在创建类的时候直接声明继承。
子类可以不写constructor，也可以写。

```js

//创建一个父类
    class Pet {
      constructor (name) {
        this.name = name;
      }
    }
    
	
	//下面是创建子类，继承父类。
    class Dog extends Pet {
      constructor (name_C, tricks) {
	        
	  super(name_C); 
	  //super用来传参给父类的constructor.这里相当于执行Pet(name_C)。
    
        this.tricks = tricks;
      }
    }
	
```


## ES5或更早
要在内部用call。主要是这样写在开头声明时可读性比较低。
```js
 function Pet (name) {
      this.name = name;
    }
    
    function Dog (name, tricks) {
      // invoke the Pet constructor function passing in our newly created this object 
      // and any required parameters
      Pet.call(this, name);
    
      // add additional parameters
      this.tricks = tricks;
    }
    
    // inherit the parent's prototype functions
    Dog.prototype = Object.create(Pet.prototype);
    
    // reset our child class constructor function
    Dog.prototype.constructor = Dog;
	
```



# static
还没怎么用过。顶部链接也有一定的解释。

# Array与class的配合使用
[[P5.js/202103041253 P5 数组+对象操作的写法]]
