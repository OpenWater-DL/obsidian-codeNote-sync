```js

/* 从HTML里获取变量，并赋值给JS里的值 */
var numOne= document.getElementById("num-one");
var numTwo= document.getElementById("num-two");
var addSum= document.getElementById("add-sum");

/* 监听事件，并执行什么function，在这里就是执行add */
numOne.addEventListener("input",add);
numTwo.addEventListener("input",add);


/* 定义add是干什么的 */
function add(){
    var one= parseFloat(numOne.value) || 0;
    var two= parseFloat(numTwo.value) ||0;
    var sum = one+two ;
    addSum.innerHTML = "your sum is"+ sum;
    console.log(sum);
}

```

