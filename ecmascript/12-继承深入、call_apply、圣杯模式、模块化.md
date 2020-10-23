# 继承深入、call_apply、圣杯模式、模块化

## call_apply

借用其他构造函数的属性与方法             

```js
Teacher.prototype.wife = 'Ms.Liu';
function Teacher(name, mSkill){
    this.name = name;
    this.mSkill = mSkill;
}
function.Sturdent(name,mSkill,age,majer){
    Teacher.call(this,name,mSkill);
    this.age = age;
    this.majer = majer;
}
var student = new Student('leah','js',20,'computer')
console.log(student)
//借用了Teacher的属性和方法，但没有继承Teacher的原型
```

#### 练习题：

```js
function foo(){
	bar.apply(null,arguments)
}
function bar(){
	console.log(arguments) //空
}
foo(1,2,3,4,5)

//1,2,3,4,5
//bar()->bar.call(arguments)->bar(arguments)
```



## 对象继承——圣杯模式     

### **原型的继承和隔离**      

创建一个缓冲器(构造函数)，将被继承的构造函数的prototype赋值给缓冲器的prototype，将缓冲器new出的实例化对象赋值给继承的构造函数的prototype，这样修改继承的原型prototype就不会影响到被继承函数的prototype                                                                                

```js
function Teacher(){
    this.name = 'Mr.li';
    this.mSkill = 'JAVA';
}
Teacher.prototype = {
    pSkill:'js'
};
var t = new Teacher()
function.Sturdent(r){
    this.name = 'Wr.Wang';
}
-------------------------------
function Buffer(){}
Buffer.prototype = Teacher.prototype;
var buffer = new Buffer()
Student.prototype = buffer;
-------------------------------
Student.prototype.age = 18'
var student = new Student()
```

### 继承函数封装

```js
function inherit(Target,Origin){
	function Buffer(){};
    Buffer.prototype = Origin.prototype;
    Target.prototype = new Buffer();
    Target.prototype.constructor = Target;
    Target.prototype.super_class = Origin;
}
```

### 模块化开发

防止变量的全局污染，有利于后期维护

```js
;var inherit =(function (){
	function Buffer(){}	
	rerutn function (Target,Origin){
        Buffer.prototype = Origin.prototype;
        Target.prototype = new Buffer();
        Target.prototype.constructor = Target;
        Target.prototype.super_class = Origin;
    }
})()
```

防止变量的全局污染，有利于后期维护

```js
var inherit = (function() {
    function Buffer() {};
    return function(Target, Origin) {
           Buffer.prototype = Origin.prototype;
           Target.prototype = new Buffer();
           Target.prototype.constructor = Target;
           Target.prototype.super_class = Origin;
    }
})()

var initProgrammer = (function() {
    function Programmer() {};
    Programmer.prototype = {
         work: '程序员',
         tool: '电脑',
         intro: function() {
           console.log('我是一名' + this.name + this.work + ',我用' + this.tool + '编写' + this.lang.toString());
         }
     }

    function FrondEnd() {}

    function BackEnd() {}

    inherit(FrondEnd, Programmer);
    inherit(BackEnd, Programmer)

    FrondEnd.prototype.name = '前端';
    BackEnd.prototype.name = '后端';
    FrondEnd.prototype.lang = ['js', 'css', 'html'];
    BackEnd.prototype.lang = ['node', 'sql', 'java'];

    return {
         FrondEnd: FrondEnd,
         BackEnd: BackEnd
    }
})()

var frondEnd = new initProgrammer.FrondEnd();
var backEnd = new initProgrammer.BackEnd();
console.log(frondEnd);
frondEnd.intro()
backEnd.intro()
```

不立即执行，按需执行

##  闭包的三种形式

1. 返回普通函数

   ```js
   function test (){
   	var num = 0;
	function compute(){
   		num++;
   	}
   	return compute
   }
   var add = test()
   ```
   
2. 返回对象

   ```js
   function test(){
   	var num = 0;
   	var compute = {
   		add:function(){
   			num++
   		},
   		minus|:function(){
   			num--
   		}
   	}
   	return compute
   }
   var compute = test()
   compute.add;
   compute.minus;
   ```

3. 构造函数

   实例化对象时隐式创建this对象，再return this

   ```js
   function Compute(){
   	var num = 0;
   	this.add = function() {
   		num++
   	};
   	this.minus = funciton(){
   		num--
   	}
   }
   var compute = new Compute();
   compute.add();
   compute.minus;
   ```

   