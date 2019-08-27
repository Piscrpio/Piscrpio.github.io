---
title: 有关js各种数组遍历
date: 2018-05-21 11:32:05
categories: web
tags: js数组
---

### 1、for循环
最先接触到的js遍历方法
<!--more-->
```
//假设存在一个数组arr
let arr = [1,2,3,4,5];

//for循环
for(let i = 0; i < arr.length; i++){
    //do someing……

    console.log(arr[i]);
}

//console.log
1
2
3
4
5

```
### 2、forEach循环
这个方法使用次数是仅次于上面的for循环的（个人观点），但是，实际效率其实并没有for循环高。forEach循环的参数有两个，第一个为参数为实际操作的函数function，第二个参数that是改变this指向的，一般也很少用。forEach参数的函数中也有两个参数，第一个是循环的每一项item，第二个参数是每一项对应的下标index。注意，使用中，that和index均可不写不用,而且forEach循环不支持return
```
//假设存在一个数组arr
let arr = [1,2,3,4,5];

//forEach循环
arr.forEach(function(item,index){
    //do someing……

    console.log(arr[i]);
},that);

//console.log
1
2
3
4
5

```
### 3、for in循环

这确实也是一个循环，但是平时基本不会用这个去遍历一个数组，因为他的“弊端”很明显，数组的私有属性也会遍历。再者，循环出来的值的类型将变成string

```
//假设存在一个数组arr
let arr = [1,2,3,4,5];
//给数组添加一个私有属性
arr.a = "key"

//for in循环
for(let key in arr){
    //do someing……

    console.log(typeof(key));
}

//console.log
//注意这里打印出来6个，for in循环会将数组的私有属性也遍历
string
string
string
string
string
string

```

### 4、for of循环(ES6)

for of循环是es6的方法，他弥补了forEach和for in循环的弊端。既有return，而且不会遍历数组的私有属性。注意：for of循环不能遍历对象
```
//假设存在一个数组arr
let arr = [1,2,3,4,5];
//给数组添加一个私有属性
arr.a = "key"

//for in循环
for(let val of arr){
    //do someing……

    console.log(val);
}

//console.log
//注意这里打印出来5个，for of循环不会将数组的私有属性遍历
1
2
3
4
5
```

### 5、filter过滤器

filter过滤器就个人而言，也是一个比较常用的方法。他会去遍历一个数组并返回一个新的数组，所以并不会影响原数组。遍历数组每一项，回调函数返回了true，就把这一项添加到新数组。其中回调函数有两个参数(item,index)，item是每一项，index是下标。index可以不写不用

```
//假设存在一个数组arr
let arr = [1,2,3,4,5];
//声明一个新的空数组
let newArr = [];
//给数组添加一个私有属性
arr.a = "key"

//filter过滤器
//这里使用的是es6箭头函数
newArr = arr.filter(item=>item>3);
//这里使用的是es5语法,和上面的操作相等
newArr = arr.filter(function(item){
    return item > 3;
})
console.log(newArr)

//console.log
[4,5]

```
### 6、map映射
map映射会去遍历数组的每一项，但是不会操作改变原数组，同filter一样会返回一个新的数组。回调函数返回的是什么，对应的新数组的那一项就会是什么
```
//假设存在一个数组arr
let arr = [1,2,3,4,5];
//声明一个新的空数组
let newArr = [];
//给数组添加一个私有属性
arr.a = "key"

//map映射
//这里使用的是es6语法
newArr = arr.map(item=>`<div>${item}</div>`);
//这里是一般语法
newArr = arr.map(function(item){
    return "<div>" + item + "</div>";
})
console.log(newArr)

//console.log
[
    "<div>1</div>",
    "<div>2</div>",
    "<div>3</div>",
    "<div>4</div>",
    "<div>5</div>"
]

```

### 7、include和find
include和find都是es6的的方法。include有一个参数，它会遍历数组的每一项与参数对比，如果存在该参数，则返回true。而find的参数是一个回调函数，函数的参数是每一项以及对应下标，find会返回匹配的那一项，一旦匹配就不会继续往下匹配,find返回一个新的数组

```
//假设存在一个数组arr
let arr = [1,2,3,4,5,55];

//include
console.log(arr.include(5));

//include console
true

//find
let res = arr.find(function(item,index){
    //如果这一项包含了5则返回true
    return item.toString().indexOf(5) > -1;
})
console.log(res);

//find console
5

```

### 8、some和every
some和every是两个作用截然相反的方法。some遍历数组，找到true，即返回true，否则返回false；every则是找到false返回false，否则返回true

```
//假设存在一个数组arr
let arr = [1,2,3,4,5,55];

//some
let someResult = arr.some(item=>item > 4);
console.log(someResult);

//some console
true

//every
let evevyResult = arr.every(item=>item < 0);
console.log(everyResult);

//every console
false

```


### 9、reduce
reduce 主要是迭代，回调函数里有两个参数，上一回 return 的值作为这一回迭代的第一个参数，而第二个参数则是遍历数组的下一个值。
```
//reduce对数组里面数字叠加求和
var arr = [1,2,3,5];
let total= arr.reduce(function(tem,item,index){
 //tem是上一次两两相加的和
 //item是当前项
//index是下标
			return tem + item;
		});
		console.log(total);//11
```
