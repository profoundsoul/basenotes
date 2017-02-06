# node debug

## Node原生debug

> V8提供了一个强大的调试器，可以通过TCP协议从外部访问。

### file debug

> 指定文件调试

```shell
node debug script.js

< Debugger listening on port 5858
connecting to 127.0.0.1:5858 ... ok
break in e:\Project\node\mycomponent.js:5
  3 }
  4
> 5 Hello.prototype.setName = function(name){
  6     this.name = name;
  7 }

```

常见情况下，会配合js脚本中debugger;语句使用

```javascript
var num = 10;
debugger;
function getName(){
    return this.name;
}
```

此时，断点会在debugger;处停顿下来


#### 常用的Commond:

+ cont,c  Continue execution
+ next,n  Step next
+ step,s  Step In
+ out, o  Step Out
+ setBreakpoint(),sb() support empty,number line, string function name,setting breakpoint
+ clearBreakpoint(),cb() support empty,number line, string function name clear breakpoint
+ watch(string) watch express value, functionname
+ unwatch(string)

### pid debug

```shell
node debug -p <pid> - Connects to the process via the pid

```


### url debug

```shell
node debug <URI> - Connects to the process via the URI such as localhost:5858
```

## node-inspector

```shell
#配合node --debug-brk script or app
node --debug-brk=7777 script.js
node-inspector --debug-port=7777 --web-port=4040
```

执行成功后，会出现chrome或浏览器调试的url

```shell
Node Inspector v0.12.8
Visit http://127.0.0.1:4040/?port=7777 to start debugging.
```


启动node程序的--debug-brk与--debug-port中的端口必须对应上。默认情况如果不设置端口为5858

## node-debug 

```
node-debug --web-port=2001 --debug-port=2000 file
```

基于node-inspector插件集成调试脚本，node-debug 是最简单调试方法

#### Node-inspector console not working in latest version of Google Chrome


The latest version of Google Chrome doesn’t execute commands when the Enter button is pressed and instead just wraps to a new line. Instead of downgrading Chrome, a quick fix appears on the node-inspector issue list [here.](https://maltronic.io/2016/12/01/node-inspector-console-not-working-in-latest-version-of-google-chrome/)






