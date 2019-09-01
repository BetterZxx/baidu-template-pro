### 一个简便轻量的模板引擎

### 由于原库比较老，现在只能兼容浏览器环境，且原库不再维护，此版本解决对node环境兼容性问题

### 改后兼容：浏览器环境，node及nodejs支持的react、vue等

### 原库地址： [https://github.com/BaiduFE/BaiduTemplate](https://github.com/BaiduFE/BaiduTemplate)

### 用法
```
baidu.template(String modelHtml,Object data)
```
### 模板基本语法（默认分隔符为<% %>，也可以自定义）
+ 分隔符内语句为js语法，如：
```
<% var test = function(){
    //函数体
};
if(1){}else{};
function testFun(){
    return;
};
%>
```
+ 假定事先设置数据为
```
var data={
    title:'baiduTemplate',
    list:['test1<script>','test2','test3']
}
```
+ 注释
```
<!-- 模板中可以用HTML注释 -->  或  <%* 这是模板自带注释格式 *%>

<% //分隔符内支持JS注释  %>
```
+ 输出一个变量
```
//默认HTML转义，如果变量未定义输出为空
<%=title%>  

//不转义
<%:=title%> 或 <%-title%>

//URL转义，UI变量使用在模板链接地址URL的参数中时需要转义
<%:u=title%>

//UI变量使用在HTML页面标签onclick等事件函数参数中需要转义
//“<”转成“&lt;”、“>”转成“&gt;”、“&”转成“&amp;”、“'”转成“\&#39;”
//“"”转成“\&quot;”、“\”转成“\\”、“/”转成“\/”、\n转成“\n”、\r转成“\r”
<%:v=title%>

//HTML转义（默认自动）
<%=title%> 或 <%:h=title%>
```
+ 判断语句
```
%if(list.length){%>
    <h2><%=list.length%></h2>
<%}else{%>
    <h2>list长度为0<h2>
<%}%>
```
+ 循环语句
```
<%for(var i=0;i<list.length;i++){%>
        <li><%=list[i]%></li>
<%}%>
```
### 例子
```
var model = `
<div>
  <%for(var i=0;i<list.length;i++){%>
        <p><%=list[i]%></p>
  <%}%>
</div>
`
var data = {
    list:['test1','test2','test3']
}
var html = baidu.template(model,data)

console.log(html)
/*
<div>
  <p>test1</p>
  <p>test2</p>
  <p>test3</p>
</div>
*/
```

