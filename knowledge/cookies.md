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









