# HTTP Cookie

参考：

<http://www.webryan.net/2011/08/wiki-of-http-cookie/>

<http://bubkoo.com/2014/04/21/http-cookies-explained/>

> Cookie通常也叫做网站cookie，浏览器cookie或者Http Cookie。就是浏览器存储在用户电脑的上的一段文本文件。并在发送Http请求时会默认携带的一段文本片段。它可以用来做用户认证，服务器校验等。

## Cookie的类别

###1. Session Cookie

生命周期：会话期间内有效，即:当关闭浏览器时候，它会被浏览器删除。

创建方法：在创建Cookie不设置Expire即可。

###2. Presistent Cookie

生命周期： 会长期在用户会话中生效。

创建方法：通过设置Max-Age或Expire的值

###3. Secure Cookie 
> 安全cookie是在https访问状态下的cookie形态，确保cookie从客户端传递到服务器端中始终加密的。

###4. HttpOnly Cookie
> 只允许http传递cookie，即：不支持javascript客户端读取cookie。

###5. 3rd-party cookie
> 第三方cookie是指种植在不同于浏览器地址的域名下的cookie。

	例如：用户访问a.com时，访问在ad.google.com设置了个cookie，在访问b.com的时候，也在ad.google.com设置了一个cookie

###6. Super Cookie
> 超级Cookie是设置公共域名前缀上的Cookie。

	例如：
	域名：a.b.com下设置cookie，可以是a.b.com/b.com下。但由于一些老版本却支持.com下设置cookie。

###7. Zombie Cookie
> 僵尸Cookie是指那些删不掉的，删掉后会自动重建的Cookie。一般是依赖于本地存储方法。

	例如：flash的share Object
		  html5的local storage等

**当Cookie删除后，自动从其他本地存储读取Cookie的备份，并重新种植**

## Cookie编码

> Cookie编码一直比较迷惑，原始规范明确指出：

+ 三个字符必须进行编码：逗号，分号，空格
+ 规范中还提到可以用URL编码，但并不是必须。

几乎所有的实现都对Cookie的值进行了一系列的URL编码。对于name=value格式，**对name和value进行编码，而不对等号进行编码**


## 创建Cookie
> 通常创建Cookie的方式有两种：
+ Web Server通过Http Respone 消息头设置Set-Cookie头创建，允许有多个Set-Cookie设置。
+ 在客户端允许执行脚本的情况下，Cookie是允许被JavaScript等脚本设置的。

##### Web Server创建Cookie

Set-Cookie格式如下：

	Set-Cookie: name=value[;expires=date][;domain=domain][;path=path][;secure]
	[]内表示是可选设置项

紧跟cookie值后面的每个选项都是以**逗号和空格**分开。*每个选项都指定了应该在什么时候发送至服务器*。


当存在一个Cookie，并允许设置可选项，该Cookie的值会在每次请求中发送到服务器。Cookie的值被存在Request的Http消息头：Cookie中，多个用逗号分隔。

	Cookie: value1; value2; name=value1; name2=value2

http方式:以访问http://www.webryan.net/index.php为例

Step1.客户端发起http请求到Server

	GET /index.php HTTP/1.1
	Host: www.webryan.net
	(这里是省去了User-Agent,Accept等字段)

Step2. 服务器返回http response,其中可以包含Cookie设置

	HTTP/1.1 200 OK
	Content-type: text/html
	Set-Cookie: name=value
	Set-Cookie: name2=value2; Expires=Wed, 09 Jun 2021 10:18:14 GMT
	(content of page)

Step3. 后续访问webryan.net的相关页面

	GET /spec.html HTTP/1.1
	Host: www.webryan.net
	Cookie: name=value; name2=value2
	Accept: */*

需要修改cookie的值的话，只需要Set-Cookie: name=newvalue即可，浏览器会用新的值将旧的替换掉。


##### 脚本方式种植Cookie：

> JavaScript或类似的寄宿在浏览器中的脚本语言也可以设置Cookie。在JavaScript里，可以通过document.cookie对象实现

	document.cookie = "key=newvalue";


### expires And Max-Age

> 指定Cookie何时不再发送至服务器，随后浏览器将删除Cookie，选项值是个Wdy, DD-Mon-YYYY HH:MM:SS GMT 日期格式的值；
在RFC 2965中规范提供了一个替代方案：Max-Age:seconds,来设置cookie在设置后多长秒后失效。

	Set-Cookie: name=Nicholas; expires=Sat, 02 May 2009 23:38:25 GMT

**没有设置expires时，表示仅限于当前会话，浏览器关闭删除cookie**

Demo:

	复选框是否记住登陆信息：勾选了，那么会加一个expires到登陆的Cookie上。

### domain And path

> domain是指定cookie要将被发送到哪个或那些域名中；path是指cookie在请求的资源URL中必须存在指定的路径是，才发送Cookie消息头。
+ 默认情况下domain会设置为创建该Cookie的页面所在的域名
+ domain选项与请求域名做一个尾部比较（即从字符串的尾部开始比较）
+ path选项只有在domain选项核实完毕后才进行。


	Set-Cookie: name=Nicholas; domain=nczonline.net
	Set-Cookie:name=Nicholas;path=/blog
	Set-Cookie:name=Nicholas;domain=nczonline.net;path=/blog

### secure and HttpOnly

> 当请求通过SSL或HTTPS创建时，包含secure选项的cookie才发送到服务器。

	Set-Cookie: name=Nicholas; secure

**默认情况下，在 HTTPS 链接上传输的 cookie 都会被自动添加上 secure 选项**

HttpOnly字段告诉浏览器，只有在HTTP协议下使用，对浏览器的脚本不可见。

	Google和Facebook都在使用HttpOnly的Cookie。

**跨站脚本攻击时也不会被窃取**。 













