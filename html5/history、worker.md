# history

历史记录存储在history栈中

```js
window.history.length //查看history条目数

history.back() //后退

history.forward() /前进

history.go() //前进或后退的步数

history.replaceState('this is test',null,'test.html')
					 //状态名称            路径
history.state  //'this is test'
//不会改变history栈中的条目，而是替换某一条历史条目

history.pushState('this is test',null,'test.html')
					 //状态名称            相对路径
1.state object是JS对象，与通过pushState()创建出的新的历史记录条目相关联
2.title null
3.url 不填默认为当前路径 可以填相对路径或绝对路径，但必须为同源地址
//history栈中的条目会增加
```



监听popState事件可以获取到状态名称，返回上一步会触发popState事件

```js
let boxes = Array.from(document.getElementByClassname.box);

function selectBox(){
    item.addEventListener('click',item =>{
        item.classList.toggle('selected',item.id === id)
    })
}
boxes.forEach(item =>{
    item.addEventListener('click',e =>{
        let id = item.id;
        history.pushState({id},null,`selected=${id}`);
        selectBox(id);
    })
})
window.addEventListener('popstate',e=>{
    let id = e.state.id;
    selectBox(id)
})
```

![image-20201024203353444](C:\Users\Magic Book\AppData\Roaming\Typora\typora-user-images\image-20201024203353444.png)

