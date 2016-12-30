### 1. arguments    [link](https://gold.xitu.io/entry/57f081d5128fe100542a02fc)
```
//arguments不可显示创建，在函数执行时会自动创建
//arguments主要有length属性和callee方法
function fn(a,b){
	console.log(arguments.length);	//0，实际传入的参数个数
	console.log(arguments.callee);	//返回fn函数本身
}
fn();

//1. length属性表示实际传入的参数个数，可通过arguments下标来访问
function fn(a,b){
	console.log(arguments.length);	//1，实际传入的参数个数
	console.log(arguments[0]);	//'one'，对应形参a
	console.log(arguments[1]);	//undefined，对应形参b
}
fn('one');

//arguments是一个类数组对象，可以转换为一个真正的数组
var args = Array.prototype.slice.call(arguments);   //推荐
//或者
var args = [];
for(var i=0,len=arguments.length;i<len;i++){
    args.push(arguments[i]);
}
```
### 2. callee 
```
//callee表示函数本身，主要用于参数长度判断和递归
function fn(n) {
	if(n===1){
		return 1;
	}
	//return n*fn(n-1);		
	return n*arguments.callee(n-1);	//作用同上，会在严格模式中报错
}
console.log(fn(5));		//120

//callee虽然方便又强大，但已不推荐使用，原因有两点：
//a. 在ECMAScript5严格模式会报错
//   Uncaught TypeError: 'caller', 'callee', and 'arguments' properties may not be accessed on strict mode functions or the arguments objects for calls to them
//b. 会影响Javascript引擎性能
//附：callee性能测试（Chrome下）
var count = 0;
function fn(n) {	
	if(n===1){
		return;
	}
	count++;	
	arguments.callee(1);	//1533ms
	//fn(1);		//131ms
}
var t_start = new Date();
for(var i=0;i<10000000;i++){
	fn();
}
var t_end = new Date();
 console.log(count);		
 console.log(t_end-t_start);
```
### 3. caller [link](http://www.css88.com/archives/1706)
```
//3. caller参数表示调用该函数的上层函数引用
//访问方式：a.functionName.caller;  b.arguments.callee.caller;
function callerDemo() {
	if(callerDemo.caller){
		console.log(callerDemo.caller);
		console.log(typeof callerDemo.caller);
	}
	else{
		console.log('this function is top function');
	}	
}
callerDemo();		//直接调用，callerDemo.caller为null
function handerCaller() {
	callerDemo();
}
handerCaller();		//通过函数嵌套来调用，返回handerCaller函数，即调用callDemo的函数
```