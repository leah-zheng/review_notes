# webSocket、与HTTP请求的不同、聊天应用

WebSocket是一种通信协议，

区别于HTTP协议，HTTP协议只能实现客户端请求，服务端响应的这种单项通信。

WebSocket可以实现客户端与服务端的双向通讯，

浏览器和服务器只需要完成一次握手，两者之间就可以建立持久性的连接，并进行双向数据传输。

socket.io



```js
npm init

npm i express --save

npm i nodemon --save-dev

npm i socket.io@2.2.0 --save

//在package.json中设置脚本命令
"script":{
	"start":'node node_modules/nodemon/bin/nodemon.js index.js'
	//如果服务端代码改变，就会重启相对应的服务器
}

//后端设置
新建index.js
var express = require('express'),
    socket = require('socket.io');
//app的设置
var app = express(),
	//服务器的设置，监听端口号上的请求
	server = app.listen(7000,function(){
		console.log('正在监听7000端口')
	})  

index.js
//静态文件 将指定路径中的html文件展示在页面上
app.use(express.static('public'))
//socket的设置 传入参数为服务器
var io = socket(server);

io.on('connection',function(socket){
    //socket.id链接唯一的id 
    console.log('socket连接已建立',socket.id)
})

//前端设置
新建public文件夹 ->新建index.html
建立好html基本骨架
引入socket.io的CDN
<script type="text/javascript" src="https://lib.baomitu.com/socket.io/2.2.0/socket.io.js"></script>
<div id="chat">
    <div id="chatWindow">
        <div id="outputArea"></div>
    </div>

	<input id="username" placeholder="username"/>
    <input id="message" placeholder="message"/>
        
    <button id="sendBtn">发送</button>
</div>

<script type="text/javascript" src="./chat.js"></script> //前端配置cdn

//新建chat.js
//建立连接
var socket = io.connect('http://localhost:7000');
//获取dom元素
var message = document.getElementById('message'),
    username = document.getElementById('username'),
    sendBtn = document.getElementById('sendBtn'),
    outputArea = document.getElementById('outputArea');
sendBtn.addEventListener('click',function(){
    
})




运行npm run start







```

