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
+ expand 处理动态src-dest文件映射。
+ 除了基础属性外，其它都会传入任务中，允许自定义处理


## src-dest 

采用这种模式，只支持一个dest，N个src。采用1-N的dest-src的文件映射。

```javascript
grunt.initConfig({
	uglify: {
		main:{
			dest:'dist/index.js',
			src:['index.js', 'main.js']
		}
	}
});

grunt.loadNpmTasks('grunt-contrib-uglify');

```

## File Object Format 文件对象格式

采用这种方式，很是简洁优雅；然后不支持除src和dest之外的参数设置，比如：expand、filter等。

```javascript
grunt.initConfig({
	cssmin:{
		main:{
			'dist/main.css':['main.css', 'index.css']
		}
	}
});

```

## Files Array Format 文件数组格式

采用这种文件数组格式与src-dest没什么区别，唯一区别的地方就是支持多个dest数组。

```javascript
grunt.initConfig({
	concat:{
		options:{
			separator:'\n',
			banner:'/*this is my merge files*/'
		},
		merge:{
			files:[
				{dest:'pro.css',src:['user.css', 'account.css']},
				{dest:'framework.css',src:['common.css', 'fw.css']}
			]
		}
	}
});

```

## dynamic Files Mapping 动态文件路径映射

上面介绍的大部分都是指定dest具体文件方式，但在项目中常常会涉及到无法固定具体文件，需要按照src动态生成dest文件（也允许dest文件加文件名后缀）。

```javascript
grunt.initConfig({
	options:{
		optimizationLevel:3
	},
	imagemin:{
		dynamic:{
			expand: true,                  // Enable dynamic expansion 
			cwd: 'src/',                   // Src matches are relative to this path
			filter:'isFile', 
			src: ['**/*.{png,jpg,gif}'],   // Actual patterns to match 
			dest: 'dist/'
		}
	}
});

```

