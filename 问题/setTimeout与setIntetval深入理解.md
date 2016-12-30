### setTimeout与setIntetval深入理解[link](https://segmentfault.com/a/1190000004034739)
```
//可以实现异步的效果
console.log(1);
setTimeout(function(){
	console.log(2);
},0);
console.log(3);
//依次输出 1，3，2

//并非正常的异步，Javascript本质为单线程
//设置的时间会与函数执行的时间会出现偏差
setTimeout(function(){
    alert('can you see me?');
},1000);        //永远不会弹出
while(true) {}
```


