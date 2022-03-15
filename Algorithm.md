## 编程相关

#### 1.实现一个 once 函数，传入函数参数只执行一次

```javascript
function ones(func){
var tag=true;
return function(){ 
  if(tag==true){
  func.apply(null,arguments); tag=false;
	}
return undefined
}
}
```

#### 2.将原生的 ajax 封装成 promise

```javascript
var myNewAjax=function(url){
return new Promise(function(resolve,reject){ 
  var xhr = new XMLHttpRequest();
  xhr.open('get',url);
	xhr.send(data);
  xhr.onreadystatechange=function(){
		if(xhr.status==200&&readyState==4){
			var json=JSON.parse(xhr.responseText);
      resolve(json)
		}else if(xhr.readyState==4&&xhr.status!=200){ 
        reject('error');
		}
  	} 
		})
}
```

#### 3.JS 监听对象属性的改变

```javascript
//我们假设这里有一个 user 对象,
//(1)在 ES5 中可以通过 Object.defineProperty 来实现已有属性的监听
Object.defineProperty(user,'name',{
set:function(key,value){
}})
缺点:如果 id 不在 user 对象中，则不能监听 id 的变化
//(2)在 ES6 中可以通过 Proxy 来实现
var user = new Proxy({}，{
set:function(target,key,value,receiver){
}})
这样即使有属性在 user 中不存在，通过 user.id 来定义也同样可以这样监听这个属性的 变化哦。
```

#### 4.如何实现一个私有变量，用 getName 方法可以访问，不能直接访问

```javascript
//(1)通过 defineProperty 来实现 
obj={
name:yuxiaoliang, getName:function(){
return this.name
}
} object.defineProperty(obj,"name",{ //不可枚举不可配置
});
//(2)通过函数的创建形式
function product(){
var name='yuxiaoliang';
 this.getName=function(){ return name;
}
}
var obj=new product();
```

#### 5.写个函数，可以转化下划线命名到驼峰命名

```java
public static String UnderlineToHump(String para){ StringBuilder result=new StringBuilder();
String a[]=para.split("_");
for(String s:a){
if(result.length()==0){ result.append(s.toLowerCase());
}else{
result.append(s.substring(0, 1).toUpperCase()); result.append(s.substring(1).toLowerCase());
}
}
return result.toString();
}
}
```

