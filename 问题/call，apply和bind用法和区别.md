
### call，apply和bind都属于Function.prototype的一个方法
### 通过修改this指向来实现方法盗用
```
//建一个Animal类
function Animal(name) {
	this.name = name;
	this.say = function(food,word){
		console.log(this.name+' love '+food+'... '+word);
	}
}

//用Animal实例化一个cat
var cat = new Animal('cat');

//创建一个普通对象dog
var dog = {
	name : 'dog'
}

//1. call测试    语法:  fn.call(obj,arg1,arg2...)
//依次输入参数,正确
cat.say.call(dog,'bone','wanwan');		//'dog love bone... wanwan'
//如果用数组形式，会将该数组转换为一个字符串作为一个参数传入，不要这样使用！！
cat.say.call(dog,['bone','wanwan']);		//'dog love bone,wanwan... undefined'

//2. apply测试		语法:  fn.call(obj,[arg1,arg2...])
//将参数放入一个数组内，正确
cat.say.apply(dog,['bone','wanwan']);       	//'dog love bone... wanwan'
//cat.say.apply(dog,'bone','wanwan');	        //会报错！！

//3. bind测试	语法:  fn.bind(obj)(arg1,arg2...)  IE9+支持！！
//先指定this
var bind_fn = cat.say.bind(dog);		//返回一个绑定了dog的函数
//依次输入参数，正确
bind_fn('bone','wanwan');			//'dog love bone... wanwan'
//以数组形式传参，结果同call方法，不要这样使用！！
bind_fn(['bone','wanwan']);			//'dog love bone,wanwan... undefined'

//bind不会影响cat的say方法
cat.say('bone','wanwan');			//'cat love bone... wanwan'
```