# weinre 调试部署服务器搭建



## 安装环境

```shell
npm install pm2 -g
npm install weinre -g
```



## 配置pull Refresh

> 加入下拉刷新，方便清除浏览器缓存，跳出真机调试浏览器（webView）缓存的茅坑

找到weinre的安装目录下，路径为：web/target

+ 篡改target-script.js文件，加入pulltorefresh.js中的内容



## 启动weinre环境

```shell
# 启动weinre中间代理服务器
pm2 start ecosystem.json 
```

