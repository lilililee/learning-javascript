### 正则 exec()和match()区别 [link](http://blog.csdn.net/z69183787/article/details/17886369)
```
//a. exec是正则对象的方法
//b. match是String对象的方法
//c. 均返回的是数组

//非全局时
//两者结果一样
var str = 'hello world! hello world!';
var reg = /lo/;

console.log(reg.exec(str));	//["lo", index: 3, input: "hello world! hello world!"]
console.log(str.match(reg));	//["lo", index: 3, input: "hello world! hello world!"]

//全局时
//exec只会匹配第一次
//match会多次匹配
var str = 'hello world! hello world!';
var reg = /lo/g;

console.log(reg.exec(str));	//["lo", index: 3, input: "hello world! hello world!"]
console.log(str.match(reg));	//["lo", "lo"]		//没有index，input属性

//非全局有分组时
//两者结果一致，会有多个分组的内容
var str = 'hello world! hello world!';
var reg = /he(l(lo))/;

console.log(reg.exec(str));	//["hello", "llo", "lo", index: 0, input: "hello world! hello world!"]
console.log(str.match(reg));	//["hello", "llo", "lo", index: 0, input: "hello world! hello world!"]

//全局有分组时
//exec只匹配一次，有多个分组内容
//match返回多个匹配结果，不考虑分组
var str = 'hello world! hello world!';
var reg = /he(l(lo))/g;

console.log(reg.exec(str));	//["hello", "llo", "lo", index: 0, input: "hello world! hello world!"]
console.log(str.match(reg));	//["hello", "hello"]		//只返回整体的匹配结果，不考虑分组
```
### 总结
```
1. 全局时，两者结果一致（不论是否分组）
2. 全局对exec不生效,永远只匹配一次
```