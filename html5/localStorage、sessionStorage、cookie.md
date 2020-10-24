# localStorage、sessionStorage、cookie

|                   | Cookies            | local Storage | Session Storage |
| ----------------- | ------------------ | ------------- | --------------- |
| Capacity          | 4kb                | 10mb          | 5mb             |
| Browsers          | HTML4/HTML5        | HTML5         | HTML5           |
| Accessible frem   | Any window         | Any window    | same tab        |
| Storage Location  | Browser and server | Browser       | Browser         |
| Expires           | Manually set       | Never         | on tab close    |
| Sent with request | yes                | no            | no              |

cookie 小的偏好信息，如选择中文的信息保存到cookie

```js
localStorage.setItem('name','leah');
localStorage.getItem('name');
sessionStorage.setItem('name','leah');
sessionStorage.getItem('name');
```

若设置的key相同，不会新增，新的value会替换旧value

localStorage永远都不会过期，sessionStorage在标签页关闭后被清除

如何删除localStorage？

```js
localStorage.removeItem('name'); //删除一条
localStorage.clear(); //清除
```



http协议是无状态的 stateless （第一次请求与第二次请求是没有关系的）

cookie保存在客户端，会话信息保存在服务端

跟踪用户

1. HTTP headers
2. ip地址
3. 用户登陆
4. 胖URL
5. cookie  服务器发送给浏览器并保存在本地的一小块数据

服务器接收到http请求，在响应头添加setCookie，并返回给客户端，cookie就会保存到浏览器中，之后每次在对服务器请求时都会带上cookie这条信息，服务器就能通过cookie判断用户，在数据库里找到关于cookie值的相对应信息，并返回想要获得的数据 

cookie只能逐条设置

##### 添加cookie

```js
document.cookie = ‘name=zhengleah';
//如果没有设置cookie的过期时间，就会默认添加上一个1969-12-31的过期时间，即关闭浏览器后就会删除的cookie
document.cookie = ‘name=zhengleah;max-age=5000';
//当前的格林威治时间加上5000ms后才过期
var d = new Date,
    day = d.getDate();
d.setDate(day + 10);
document.cookie = 'name=leah;expires='+d
//十天后过期
```

##### 删除cookie

```js
var d = new Date,
    day = d.getDate();
d.setDate(day - 10);
document.cookie = 'name=leah;expires='+d
//设置过期时间为过去时间
```



##### 增删改查函数

```js
var manegeCookies = {
	set:function(key,value,expTime){
		document.cookie = key + '=' + value + ';max-age=' + expTime;
        return this;
	},
	delete:function(key){
		return this.set[key,'',-1]
	},
	get:function(key,callback){
		var CookieArray = document.cookie.split('; ');
        CookieArray.forEach(function(elem,idx){
            var CookieItemArray = elem.split('=');
            if(CookieItemArray[0] == key) {
                callback(CookieItemArray[1]);
                return this;
            }
        })
        callback(undefined);
        return this;
	},
}
manegeCookies.set('name','leah',1000);
manegeCookies.delete('name');
manegeCookies.get('name');
```

