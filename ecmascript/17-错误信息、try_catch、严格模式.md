# 错误信息、try_catch、严格模式

## JS错误信息类型

1. SyntaxError 语法错误

   - 变量名不规范
     - var 1ab=1
   - 关键字不可赋值
     - function = 1
   - 基本语法错误
     - var a = 5:

2. ReferenceError 引用错误

   - 变量或函数未被声明
   - 给无法赋值的对象赋值的时候

3. RangeError 范围错误

   - 数组长度赋值为负数
   - 对象方法参数超出可行范围

4. TypeError 类型错误

   - 调用不存在的方法
   - 实例化原始值

5. URIError URI错误

   URL：uniform resource identifier 统一资源标识符

   URL：uniform resource location  统一资源定位符

   ​			http://www.baidu.com/news#today

   URN:  uniform resource name  统一资源名称

   ​			www.baidu.com/news#today ->ID

   ```js
   var myUrl = 'http://www.baidu.com/name=窦靖童';
   var newUrl = encodeURI(myUrl);
   var newNewUrl = decodeURI(newUrl);
   
   var str = decodeURI('%radcrc%')//报错
   ```

6. EvalError eval函数执行错误

### 自定义实例化错误

```js
var error = new Error('代码错了');
console.log(error)

var error = new TypeError('代码错了');
console.log(error)
```



## try/catch/finally/throw

```js
try{
	console.log('正常执行');
	console.log(a) //执行报错
	console.log(b) //不执行
	console.log('正常执行2')
}catch(e){
	console.log(e.name+':'+e.message)
}finally{
	console.log('正常执行3')
}
console.log('正常执行3')
```

json字符串

```JS
var jsonStr = "";
try{
	if(jsonStr == ""){
		throw 'JSON字符串为空'
	}
	console.log('我要执行啦');
	var json = JSON.parse(jsonStr);
	console.log(json)
}catch(e){
	console.log(e);
	var errorTip = {
		name:'数据传输失败',
		errorCode:'10010'
	}
	console.log(errorTip)
}
```

## ECMAscript发展史

- 97    1.0
- 98    2.0
- 99    3.0  JS通行标准
- 07    4.0草案   只有Mozilla支持  Branden eich
- 08    4.0中止   容易改善 3.1  Harmony
- 09    5.0发布，Harmony -> 1/2 JS.NEXT  1/2JS.NEXT.NEXT
- 11     5.1   ISO国际标准
- 12     ES6 = js.next
- 13     ES6草案发布
- 15     ES6正式发布，ECMAscript2015

### 严格模式

ES5 正常模式 严格模式

IE9及以上版本

```
'use strict'

function test (){
	'use strict'
}

var test = (function(){
	'use strict'
})()
```

严格模式下不能使用with

```js
var a = 1;
var obj = {
	a:2
}
function test(){
	var a = 3;
	var b = 4;
	with(window){
		console.log(a);
		console.log(b)
	}
}
test()
```

严格模式下不能使用callee和caller

```js
function test(){
	console.log(arguments.callee)
}
test(1,2,3)
```

```
function test1(){
	test2()
}
function test2(){
	console.log(test2.caller)
}
```

严格模式下未声明变量赋值会报错包括函数内

```js
var a = b = 1

function test(){
    var a = b =1
}
test()
```

严格模式下函数未定义this指向默认为undefined

```js
function test(){
	console.log(this)
}
test()
//test.call({})
//var test1 = new test()
```

严格模式下函数的参数不能重复

```js
function test(a,a){
	console.log(a)
}
test(1,2)

var obj = {
    a:1,
    a:2
}
```

严格模式下不能在eval外使用其变量

```js
eval('var a = 1;console.log(a)')
console.log(a)
```

