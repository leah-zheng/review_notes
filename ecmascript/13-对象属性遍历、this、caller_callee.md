# 链式调用、对象属性遍历、this、caller_callee

##   链式操作                         

return this

```js
var sched = {
	morning:function(){
		console.log('studying');
		return this;
	},
	afternoon:function(){
		console.log('reading')
		return this;
	},
	evening:function(){
		console.log('sleeping')
		return this;
	}
}
sched.morning().afternoon().evening()
```

## 属性名拼接

```js
obj['name']===obj.name
obj['No'+num] //可以凭借属性名
```

## 对象、数组属性遍历

```js
for(var key in obj){
	//car.key ->car['key'] ->undefined
	console.log(key, obj[key])
			  // 键名   键值
}
```

```js
for(var i in arr){
	//arr.i ->car['i'] ->undefined
	console.log(i, arr[i])
			  // 键名   键值
}
```

## hasOwnProperty

判断参数是否为对象自身的属性,排除原型链上的自定义属性

```js
function Car(){
	this.brand = 'Benz'
}
Car.prototype = {
	width: 5
}
Object.prototype.name = 'Object'
var car = new Car()

for(var k in car){
	if(car.hasOwnProperty(k)){
		console.log(car[k])
		//只输出实例对象自身的属性
	}
}
```

## in

判断对象中是否有某属性,不排除原型上的属性

```js
console.log('brand' in car) 
// 属性要为字符串 car['brand']
```

## instanceof

判断该实例化对象是否为该构造函数构造出的，包括原型链上原型的构造函数

```js
console.log(a instanceof A)
console.log([] instanceof Object) // true
console.log({} instanceof Object)  //true
console.log([] instanceof Array)  //true
```

## 判断类型

```js
var a = [];
a.constructor //Array()
a instanceod Array // true
Object.prototype.toString().call(a) //[object Array]
```

```js
var str = Object.prototype.toString(),
    trueTip = '[object Array]'
if (str.call(a) === trueTip){
	console.log('是数组')
}else{
	console.log('不是数组')
}
```

## this 指向 

- **全局this指向window**

- **普通函数里的this指向window**

- **构造函数this指向实例化对象**

  ```js
   function Test(){
   	//var this = {
   	// __proto__:Test.prototype
   	//}
   	this.name = '123'
   }
   var test = new Test()
   //AO = {
   //  this:{
   //		name:'123'
   //		__proto__:Test.prototype
   //  }
   //}
   //GO = {
   //	 Test:funciton test(){...}
   //  test:{
   //		name:'123'
   //		__proto__:Test.prototype
   //  }
   //}
  ```

- **call和apply**

## callee和caller

### callee

实参列表的属性，arguments.callee返回所在函数

```js
function test (a,b,c){
	console.log(arguments.callee.length);//3
	console.log(test.length) //3 形参的个数
	console.log(argument.length)//2 实参的个数
}
test(1,2)
```

##### 使用场景：

在立即执行函数或匿名函数中需要调用函数时

```js
var sum = (function (n){
	if(n<=1){
		return 1;
	}
	return n + argumnents.callee(n-1);
})(10)
```

### caller

返回调用当前函数的函数引用

```js
function test1(){
	test2();
}
test1()
function test2(){
	console.log(test2.caller)
}
```

 