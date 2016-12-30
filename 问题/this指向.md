[this指向](http://mp.weixin.qq.com/s?__biz=MzAwNjI5MTYyMw==&mid=2651493447&idx=1&sn=dc00c4bc8bb03e0e4351864e16400790&chksm=80f19d8fb7861499c5867be746f34cd9918d79fc68ed5d9f2bba1dd526ca468853341e8ee4e1&mpshare=1&scene=23&srcid=1230VEx6oXutPOefupNPDAdH#rd)
#### !   在函数中this到底取何值，是在函数真正被调用执行的时候确定的，函数定义的时候确定不了

#### 1. 正常情况，this指向最近的对象
```
//a. 全局执行环境
// this 指向当前的全局对象（浏览器端是 Window，node.js 中是 global）
console.log(this);			//Window {top: Window, window: Window, location: Location, external: Object, chrome: Object…}

//b. 普通函数调用
function normalFn() {
	console.log(this);		//Window {top: Window, window: Window, location: Location, external: Object, chrome: Object…}
}
normalFn();
  //在严格模式下
function strictFn() {
	'use strict';
	console.log(this);		//undefined
}
strictFn();

//c. 对象方法中调用
// this 指向当前对象
var obj = {
	foo : function(){
		console.log(this);
	}
}
obj.foo();				//Object {foo: function}
```
#### 2. 构造函数调用
```
// this 指向实例化的对象
function Person(name){
	this.name = name;
	this.sayName = function(){
		console.log(this);
	}
}
var p = new Person('lee');
p.sayName();			//Person {name: "lee", sayName: function} ,即对象 p
```
#### 3. call,apply,bind中调用
```
// this 指向传入的对象
var obj = {
	value : 'zzz'
};
function callFn(){
	console.log(this);
}
callFn.call(obj);		//Object {value: "zzz"}
```
#### 4. 闭包中调用
```
//在闭包中 this 肯定是指向window
function outerFn(){
	var private = 'you cant see me';
	var innerFn = function(word){
		console.log(this);		//Window {top: Window, window: Window, location: Location, external: Object, chrome: Object…}
		console.log(private + word);	//you cant see me zzzz
	}
	return innerFn;
}
//outerFn()();				
var fn = outerFn();		//函数第一次运行后作用域就转换到了Window
fn(' zzzz');


//在setTimeout中的闭包问题
var obj = {
  name: 'qiutc',
  foo: function() {
    console.log(this);
  },
  foo2: function() {
    console.log(this);      
    setTimeout(this.foo, 1000); //setTimeout是一个函数，此时其内部环境是闭包环境，this指向Window
  }
}
obj.foo2();

//解决方案：用that保存this
var obj = {
  name: 'qiutc',
  foo: function() {
    console.log(this);
  },
  foo2: function() {
    console.log(this);
    var that = this;
    setTimeout(function(){
    	console.log(that);
    }, 1000);     //setTimeout是一个函数，此时其内部环境是闭包环境，指向Window
  }
}
//
 obj.foo2();
```