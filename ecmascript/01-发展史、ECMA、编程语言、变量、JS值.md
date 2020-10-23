# 01-发展史、ECMA、编程语言、变量、JS值

## 5大主流浏览器的内核

- IE	trident
- chrome    webkit blink
- safari        webkit
- firefox       gecko                                                                                                                                                                                                
- opera        presto

## 浏览器的历史和js诞生

1. 1990    蒂姆·伯纳斯·李  超文本分享资讯的人

   world wide web 移植到C  =>libwww=>nexus

   允许别人浏览他人编写的网站

2. 1993  美国伊利诺大学NCSA组织（马克·安德森）开发了MOSIAC浏览器（图形化浏览器）能够显示图片

3. 1994  马克·安德森和吉姆·克拉克（硅图SGI）成立MOSIAC communication corporation

   MOSIAC =>伊利诺大学=>spy glass公司=>Netscape communication corporation

   网景公司=>Netscape navigator  =>2003

4. 1996  

   1. 微软的公司收购spy glass

   =>IE  1.0

   ​	IE3  JScript

   ​	2. 网景公司Brendan eich在Netscape navigator开发出了livescript(javascript前生) 

   3. SUN的JAVA有知名度，网景livescript不温不火，网景与sun合作推广和宣传产品，livescript=>javascript

5. 2001  IE6 xp诞生

   ​			JS引擎

6. 2003   Mozilla公司  firefox => 根据Netscape navigator复制

7. 2008   google基于webkit blink gears

   chrome =>V8=>JS引擎

   1. 直接翻译机器码
   2. 独立于浏览器运行

8. 2009  甲骨文oracle收购了sun公司

   ​			JS 所有权给甲骨文

## ECMA

European Computer Manufactures Association 欧洲计算机制造联合会

评估、开发、认可电信、计算机标准

ECMA-262 脚本语言规范  ECMAScript

ES5 ES6 规范化脚本语言

## 编程语言

高级语言：人能理解机器不能理解

编译器  解释器

翻译过程不同：

编译性语言：源码=>编译器=>机器语言=>可执行的文件；适合写逻辑性强的大型项目

解释性语言：源码=>解释器=>解释一行执行一行； 不需要根据不同的系统平台进行移植，速度更快一些，

.java =>javac=>.class=>JVM解释执行

C++ .cpp源码=>编译器=>.s汇编=>汇编器=>.obj目标代码=>链接器=>可执行文件

脚本语言：

​	=>脚本引擎=>解释器

javascript客户端脚本：解释器在浏览器

 php服务端脚本：解释器在服务器

## JavaScript

ECMAscript

DOM  document object model  W3C

BOM  browser object model   没有规范

JS引擎是单线程引擎

单线程：一次只能执行一个任务

​				=>如何模拟多线程  

​	轮转时间片：短时间之内轮流执行多个任务片段

1. 任务1 任务2...
2. 切分任务
3. 随机排列任务片段，组成队列
4. 按照这个队列顺序将任务片段送进JS进程
5. JS线程执行一个又一个的任务片段

多线程：一次能同时执行多个任务

```
<script type='text/javascript'></script>
```

编程语言必备：变量、数据结构、函数、运算能力

## 变量

```js
var a;  //变量声明
a=3;	//变量赋值
var a=3 //变量声明并赋值
```

变量命名规范：

- 不能以数字开头，能字母_$开头
- 变量里可以包含字母_$数字
- 不能以关键字、保留字命名
- 驼峰命名法 小驼峰 大驼峰

**先运算>再赋值**

## JS值

### 原始值->基本类型（5种）

- Number 数字
- String 字符串
- Boolean 布尔值
- undefined 未被定义
- null 空值

### 引用值

- object
- array
- function
- date
- RegExp

### 变量空间存储原始值和引用值

```js
var a = 3,
	b = a;
var a = 1;
```

原始值存储在栈内存，先进后出。重新给a赋值会开辟新的内存空间并赋值，原来的值保持不变，只是对应的名称不在了。

![](https://s1.ax1x.com/2020/08/12/ajOhKf.png)

```
var arr1 = [1,2,3,4,5],
	arr2 = arr1;
var arr1 = [1,2];
```

引用值的实际数据存储在堆内存，而栈内存中存储的只是指向堆内存的地址。将arr1的值赋值给arr2，其实就指向同一个堆内存的地址。

![](https://s1.ax1x.com/2020/08/12/ajjWB8.png)

给arr1重新赋值就是在栈内存中开启新的空间，存储指向存在堆内存中的新数据的地址。

![](https://s1.ax1x.com/2020/08/12/ajv93R.png)

