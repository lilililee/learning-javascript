````
//1. 对于字符串
var str1 = 'hello world';
console.log(str1.toString());	        //'hello world'
console.log(str1.toLocaleString());	//'hello world'
console.log(str1.valueOf());	        //'hello world'
console.log('---------------------');

//2. 对于数组
var arr1 = [1,2,3];
var arr2 = [4,5,6];
var arr3 = [arr1,arr2];
console.log(arr1.toString());	        //'1,2,3'
console.log(arr1.toLocaleString());	//'1,2,3'
console.log(arr1.valueOf());	        //[1, 2, 3]  返回的是一个数组
console.log(arr3.toString());	        //'1,2,3,4,5,6'
console.log(arr3.toLocaleString());	//'1,2,3,4,5,6'
console.log(arr3.valueOf());	        //[Array[3], Array[3]] 返回数组
console.log('---------------------');

//3. 对于时间
var date = new Date();
console.log(date.toString());	        //Tue Dec 20 2016 22:54:18 GMT+0800 (中国标准时间)
console.log(date.toLocaleString());	//2016/12/20 下午10:54:18
console.log(date.valueOf());	        //1482245658477
````