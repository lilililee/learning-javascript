[JS创建对象几种不同方法详解       link](http://blog.csdn.net/u013510614/article/details/51818620)

#### 1. 工厂模式
```
//缺点:只能生成Object，没有解决对象识别的问题
function createPerson(name, age){
	var obj = new Object();
	obj.name = name;
	obj.age = age;
	obj.sayName = function(){
		console.log('my name is '+obj.name);
	}
	return obj;
}
var p = createPerson('lee',22);
p.sayName();	//'my name is lee'
```

#### 2. 构造函数模式
```
//缺点:会重复为多个对象添加sayName方法，占内存空间
function Person(name, age){
	this.name = name;
	this.age = age;
	this.sayName = function(){
		console.log('my name is '+this.name);
	};
}
var p = new Person('lee',22);
p.sayName();		//'my name is lee'
```

#### 3. 原型模式
```
//确定：灵活性极差，生成的对象属性和方法值都一致，不需要
function Person1(){

}
Person1.prototype.name = 'lee';
Person1.prototype.age = 22;
Person1.prototype.sayName = function(){
		console.log('my name is '+this.name);
};
var p = new Person1();
p.sayName();
```

#### 4. 构造函数加原型模式(墙裂推荐！！！)
```
//单独属性和函数在构造函数中，公有属性和方法在原型中
function Person3(name, age){
	this.name = name;
	this.age = age;
}
Person3.prototype.sayName = function(){
		console.log('my name is '+this.name);
};
var p = new Person3('lee',22);
p.sayName();
```

