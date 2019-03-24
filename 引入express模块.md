#Express 课程

### what：

​	1 基于Node.js的一个web开发框架

​	2 用力啊搭建服务器的模块

### How:

​	1 npm i express --save  //本地安装

​	2 语法：

```
		//引入express模块
		const express = require('express')
		//创建应用对象
		const app = express()
		//设置路由
		//app.get('/',(req,res) =>{ 
			res.send('返回的响应');
			})
		//开启服务器
		app.listen（3000）

```

###设置路由(Route)

​	what:

​		1 定义引用的端点（URls）响应客户端的请求

​		2 UR了，HTTP 请求（GET，POST等）和若干个句柄组成的。

​	1 作用：

​		--定义请求地址

​		--处理请求，返回响应

​	2 组成

​		第一部分：HTTP请求的方法（get或post）

​		第二部分：URI路径

​			--路由路径： 定义请求地址

​			基本 /   	/login/shop/a 一个 url网址对应一个路由

​			特殊 /xxx/：xxx 多个url网址对应一个路由

​		第三部分: 回调函数

​			--若干个回调函数（句柄函数）

​			request   请求信息， 浏览器 ==》服务器

​			response  响应信息    服 ==》浏

​		--请求方式：GET (查) /  POST （增） / PUT（改）  / DELETE（删）

​		

​	3 是什么 

​		--key -value的映射关系，key路由路径  value回调函数

​	4 执行顺序

​		从上到下，检测是否匹配上了，有就执行回调函数，无就看下一个 ，都无 返回 404.

//根路径

​	request

​		请求参数

​			get请求参数  -----查询字符串  req.urey

​			post请求参数 ----req.body(配合中间件使用)

​			params参数 req.params

​		请求头信息 

​			req.headers  获取所有请求头信息

​	response

​		返回响应

​			res.send()

​				如果是标签字符串

​				js对象，就转json数据作为响应体返回

​			res.end()快速响应

​			res.json()将对象转为josn数据并作为响应体返回

​			res.dowload(相对路径)返回响应并让浏览器下载

​			res.sendFile(__dirname+\相对路径）返回让浏打开

​			res.redirect（）重定向，默认响应码302

​			res.status()设置响应状态码

​			res.set()设置响应头

### 中间件

​	1 what：

​		本质上是一个函数，三个参数req,res，next

​		参数含义

​			req 请求对象

​			res 响应对象

​			next 函数，调用下一个中间件

​	2 作用：

​		执行任何代码

​		更改请求和响应对象

​		接受请求，返回响应 (注意中间件一般不直接返回响应，一般是由路由返回响应)

​	 	调用对栈中的下一个中间件函数

​	3 应用

​		应用程序级中间件（放在路由上面更改请求和响应）

​			更改请求和响应对象 过滤非法请求（防盗链）

​		路由器中间件

​			后面讲

​		内置中间件

​			express框架内置的中间件

​				express.static(资源文件目录）向外暴露静资源

​				express.urlencoded()  解析post请求体，参数，就能通过req,body获取

​		第三方中间件

​			社区开发中间件 cookie-parser 解析cookie数据

​		错误中间件

​		（err,req,res,next）=>{}

​			一旦中间件或者路由出现问题，就触发中间处理

​			404页面

//最基本的中间件 -能够接受处理的所有请求