# webpack笔记
## webpack的安装：
- npm install webpack -g
- 安装cnpm淘宝镜像，可以使用淘宝镜像来替代npm，安装cnpm: npm install cnpm -g
- webpack的使用
### cnpm命令
- cnpm install （安装包）; cnpm uninstall（卸载包）; cnpm init （用来生成package包）
-eg: cnpm install style-loader css-loader --save-dev 将这两项依赖包店家到这个package.json文件
## webapack的配置
- 入口文件 entry
- 出口文件
```
output:
    path:'dist', //告诉webpack将来所有的打包文件都要放到dist文件目录上来
    filename:'/build.js' // 打包的以后的输出文件名称，'/build.js'表示输出当前目录的路径及名称
}
```
### webpack打包css文件
- 需要在入口文件或者依赖的其他文件中使到css需要打包的文件，
- require("./site/site.css");
- autoprefixer-loader-css浏览器内核前缀自动补全工具包

### webpack打包less文件
### webpack打包sass文件
### webpack-dev-server的配置
- 1.安装webpack-dev-server依赖包: npm/cnpm install webpack webpack-dev-server --save-dev
- 2.缩短服务启动指令:在package.json文件中配置启动项，在scripts对象中的配置属性和属性值
```
"scripts": {
  "dev": "webpack-dev-server --inline --hot --open --port 3008"
},
```
- 3.安装第三方包，让webpack在内存中自动生成一个入口HTML文件，这时候要使用到第三方包:npm install html-webpack-plugin --save-dev，配置如下：
```
// 然后在wenpack.config.js中配置
var HtmlWebpackPlugin = require('html-webpack-plugin');
module.exports = {
    plugins:[
        new HtmlWebpackPlugin({
            title: 'My Index',
            filename: 'index.html',
            template: 'index.html'
        })
    ]    
}
```
### es6语法转换为es5语法
```
1.相关转换包
    bebal-core
    bebal-loader
    babel-preset-es2015 ->转码器
    babel-plugin-transform-runtime -> 实时转码
2.webpack.config.js的配置代码
    写法1
module: {
        loaders: [
            {
                test: /\.js$/,
                loader: "bebal-loader",
                exclude: /node_modules/,
                query: {
                    "presets": ["es2015"]
                }
            }
        ]
    }
bebal: {
    plugins: ['transform-runtime']
}
写法2
module: {
        loaders: [
            {
                test: /\.js$/,
                loader: "bebal-loader",
                exclude: /node_modules/
            }
        ]
    }
bebal: {
    presets: ['es2015'],
    plugins: ['transform-runtime']
}

个人遇到的问题：
babel属性会在webpack编译项目的时候，会报错，无法加载babel属性,建议使用query属性来查找presets和plugins
module: {
        loaders: [
            {
                test: /\.js$/,
                loader: "bebal-loader",
                exclude: /node_modules/,
                query: {
                    presets: ['es2015'],
                    plugins: ['transform-runtime']
                }
            }
        ]
    }
```