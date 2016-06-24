# Source-Destination 文件

由于大部分任务执行过程中都会有文件操作，Grunt官方对文件配置接口进行了良好的抽象，主要有以下几种src-dest的文件映射方式：
+ src-dest Format：其中src支持字符串路径数组和字符串路径，dest仅支持字符串路径
+ Files Object Format：文件对象属性格式。key-value表示dest-src，支持多个dest-src
+ Files Array Format：dest-src数组形式。
+ Custom Filter Format： 自定义帅选格式。支持filter和expand两种形式。


```
module.exports= function(grunt){
	grunt.initConfig({
		uglify:{
			srcdest:{
				src:'index.js',
				dest:'dist/index.js'
			},
			filesobj:{
				files:{
					'dist/index.js':'index.js'
				}
			},
			filesArr:{
				[dest:'dist/index.js',src:'index.js']
			},
			filter:{
				expand:true,
				cwd:'project',
				src:'src/*.js',
				dest:"dist"
			}
		}
	});
}
```

对于具有src-dest的三种方式（src-dest、Files Array Format、Custom Filter Format）还支持一些附件的属性：
+ filter--fs.Stats.method name与自定义返回值为Boolean
+   


## src-dest 

