
# 安装node切换淘宝镜像
1、安装node环境
2、安装npm install nrm -g --registry=https://registry.npm.taobao.org/
3、使用nrm use taobao

# linux npm总是报错：unable to verify the first certificate

取消ssl验证：npm config set strict-ssl false

如果还没成功，则将npm源更换为国内镜像：
npm config set registry http://registry.cnpmjs.org/
npm config set registry http://registry.npm.taobao.org/

# 查找文件 

find -name 'nrm'


# node及npm安装

简单说就是解压后，在bin文件夹中已经存在node以及npm，如果你进入到对应文件的中执行命令行一点问题都没有，不过不是全局的，所以将这个设置为全局就好了。

```
cd node-v0.10.28-linux-x64/bin
ls
./node -v
```

这就妥妥的了，node文件夹具体放在哪，叫什么名字随你怎么定。然后设置全局：

```
ln -s /home/kun/mysofltware/node-v0.10.28-linux-x64/bin/node /usr/local/bin/node
ln -s /home/kun/mysofltware/node-v0.10.28-linux-x64/bin/npm /usr/local/bin/npm

```

# 软链ln

一般连接至：/usr/local/bin/

```
# name 表示软链后的名称
ln -s xxxxxxxx/xx  /usr/local/bin/name

```

删除软链接：

```
rm -rf /usr/local/bin/name
```

# npm global setting 

这里我们进行全局安装，命令的不同点就是需要加上参数 <-g>，即

1   npm -g install <模块名>
但是在执行这个命令前，首先要置顶全局安装的路径，可以使用以下命令查看当前的配置

1   npm config list
执行如下命令配置全局模块安装路径

1   npm config set prefix=< nodejs安装根目录 >
2   npm config set cache=< nodejs安装根目录 >/cache

# npm install node-sass (失败)

安装cnpm进行安装

```
npm install cpnm -g
ln -s 安装路径 /usr/local/bin/cnpm
```




