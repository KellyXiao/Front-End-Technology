## 什么是JSON

* 英文全称JavaScript Object Notation(标记)
* 是一种轻量级的数据交换格式



## JSON 实例

```json
{"employees":[  
    {"firstName":"John", "lastName":"Doe"},  
    {"firstName":"Anna", "lastName":"Smith"},  
    {"firstName":"Peter", "lastName":"Jones"}  
]}
```

> 语法规则：数据为键/值 对，键值用：隔开，数据用逗号隔开，[]保存数组，{}保存对象
>
> JSON 值可以为：数字，字符串，逻辑值，数组，对象，null 示例：30, true, {"xx" : "xx"}, null



## JSON 字符串和Javascript 对象相互转换

> JSON通常是与服务器端交换得到的数据，在接收服务器数据时一般获得的是字符串，可是使用JSON.parse()方法将接收到的字符串转化为js对象

```javascript
var text = '{ "name":"zhang", "alexa":10000 }';
var obj = JSON.parse(text)

document.getElementById("demo").innerHTML = obj.employees[0].firstName + " " +obj.employees[0].lastName;
//通过数组下标可以访问数组元素
```



> js在向服务器发送数据时通常为字符串，可以使用JSON.stringify() 将js对象转换为字符串

```js
var myJSON  = JSON.stringify(obj)
```





## 如何操作JSON对象

```js
var myObj = { "name":"zhangsan", "age":11};
```



* 通过(.)来访问 或者 通过([])来访问对象的值;

  ```js
  var x, y;
  x = myObj.name;
  y = myObj[age];
  ```

  

* 通过循环对象，可以得到对象的属性 和 属性的值

  ```js
  for(x in myObj) {
  	console.log(x + " " + myObj[x]);
  	//输出 name  张三...
  }
  ```

* 删除对象属性

  ```js
  delete myObj.name
  delete myObj[age]
  ```

  

## 服务器端如何操作JSON

> 后台接收到JSON字符串如何操作？后台返回对数据前台时需要json字符串，又如何转化呢？
>
> 可以使用 fastJson ，Gson，Jackson
>
> 其中fastJson 速度最快，Jackson是spring默认的json包



## JSONP 

* 安全策略中的同源策略指的是：所有的请求必须同源，不能再A网站内发送B网站的请求

* <script> <img> <iframe> 包含src属性的html标签不受此限制



如果情况确实需要跨域访问，可以使用JSONP，它的原理就是 *借助的就是script 标签不受同源策略限制

```html

<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
    <title></title>
    <script type="text/javascript">
    // 得到天气信息
    var weatherHandler = function(data){
        alert('温度 ' + data.temperature + '度，描述 ' + data.desc);
    };
    // 提供天气信息的接口
    var url = "http://xxxxxxx?callback=weatherHandler";
    // 创建script标签，设置其属性
    var script = document.createElement('script');
    script.setAttribute('src', url);
    document.getElementsByTagName('head')[0].appendChild(script); 
    </script>
</head>
<body>
 
</body>

```



或者使用Ajax 封装后的jsonp

```js
$.ajax({
    type: "get", //规定请求的类型（GET 或 POST）。
    data: "",  //  规定要发送到服务器的数据。
    url: "XXX",  //规定发送请求的 URL。默认是当前页面。
    dataType: "jsonp",  //预期的服务器响应的数据类型。
    jsonp: "callback",  //在一个 jsonp 中重写回调函数的字符串。
    success: function(data) {  //请求成功后返回
        console.log(data);
    },
    error: function() {  //请求失败后返回
        console.log('Request Error.');
    }
});
```



可以简写为

```js
jQuery.getJSON("xxx?callback=?",{
    random: Math.random()
}, function(data){
    console.log(data);
});
```



