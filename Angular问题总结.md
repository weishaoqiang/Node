webpack遇到的几个坑
第一 React.render 报错不是一个function 是因为1.5以上的react已经把react分成了react和reactdom两个文件需要
	```
	npm install react --save-dev
	npm install react-dom --save-dev
	```
最后在页面上 要引入两个js文件
	
	```
	<script src="src/react.js"></script>
	<script src="src/react-dom.js"></script>
	```
第二 报错 Cannot find module 'less'
	是因为没有安装less包
	npm install less --save-dev

第三 运行了webpack成功但是不出效果 可能是 页面引用输出后的文件的路径不对查看output输出文件路径再查看js引入的路径

	```
	  output: {
        filename: "./build/build.js",
        path: __dirname
    }
	```
第四 Cannot find module 'babel-core'

	npm install babel-core --save-dev

第五  Cannot find module 'gulp-webpack'
	npm install gulp-webpack --save-dev
第六 didn't return a function

第七 Cannot resolve module 'url-loader'
	npm install url-loader --save-dev
第八 Cannot find module 'file-loader'
	npm install file-loader --save-dev
第九 'webpack-dev-server' 不是内部或外部命令，也不是可运行的程序
	npm install -g webpack-dev-server  没有全局安装webpack-dev-server这个包 这是一个独立的包需要单独安装
第十 实现保存后自动刷新页面 执行 webpack-dev-server --inline

第十一 GulpUglifyError: unable to minify JavaScript
	可能js文件里面代码有错 通过
	uglify().on('error', function(e) {
            console.log(e);
        }
   打印错误信息 排查
第十二 'SyntaxError: Unexpected token: punc ({)
	多了个大括号 删掉即可
第十三 允许gulp server 之前把所有任务要把所有都先执行一遍
	gulp style script image html
第十四 实现浏览器自动刷新 
	在每个任务后面加上  .pipe(browserSync.reload({ stream: true }))
	同时 监视所有文件变化 触发对应的任务
	```
	 gulp.watch('css/*.less', ['style']);
    gulp.watch('js/*.js', ['script']);
    gulp.watch('images/*.*', ['image']);
    gulp.watch('*.html', ['html']);
	```
第十五 mongodb 开启服务报错 
	Tue Nov 15 17:43:34.540 [initandlisten] exception in initAndListen: 12596 old lock file, terminating
	Tue Nov 15 17:43:34.542 dbexit:
	Tue Nov 15 17:43:34.543 [initandlisten] shutdown: going to close listening sockets...
	Tue Nov 15 17:43:34.544 [initandlisten] shutdown: going to flush diaglog...
	Tue Nov 15 17:43:34.545 [initandlisten] shutdown: going to close sockets...
	Tue Nov 15 17:43:34.546 [initandlisten] shutdown: waiting for fs preallocator...
	Tue Nov 15 17:43:34.553 [initandlisten] shutdown: closing all files...
	Tue Nov 15 17:43:34.555 [initandlisten] closeAllFiles() finished
	Tue Nov 15 17:43:34.561 dbexit: really exiting now
	

	解决方案 
	找到当前数据库对应的数据库文件
	删除掉后缀为.lock的文件
第十六 angular模板绑定标签数据无法显示
	解决方案
	使用 $sce模块  ['$scope', '$http', '$sce']
	实用 $sce.trustAsHtml(要转换的属性) 
	通过遍历所有数据将需要显示的标签数据转换成angular能够识别的html编码
	通过ng-bind-html=	要显示的属性 切记这里绑定的时候不要带{{}} 同时要写在标签身上
第十七 angular.js:13236 ReferenceError: $scope is not defined
	$scope 不存在 
	原因是没用引入$scope模块 或者没有写在回调函数的形参里面
	解决方案  ["$scope", "$http", "$sce", function($scope, $http, $sce) 
	在function 里面加上$scope形参
第十八
	angular.js:13236 Error: [ngRepeat:iexp] Expected expression in form of '_item_ in _collection_[ track by _id_]' but got ''.
	问题 ng-repeat 属性里面没用写值 或者不是一个集合
	解决办法 给ng-repeat里面加上 item in collection
第十九
	angular 里面的ng-repeat 里面想拿到循环遍历 的索引可以通过
	{{$index}} 拿到循环遍历的索引
第二十
	angular 里面使用ajax传入参数的写 params 不是data
	params:{'titleid':0}
第二十一
	angular路由传入多个参数的方式
	在app.js中写法
      when(
        '/online_show_list/:video_type/:factory/', 
        {
          templateUrl: 'statics/partials/online_show_list.html', 
          controller: OnlineShowListController
        }).
第二十二
	angular路由的模板通过 ng-view属性去渲染 需要在主页放一个标签加上ng-view属性
第二十三 
	angular报错 TypeError: Cannot read property '1' of null
    at 
   原因是ng-controller=""  双引号里面没写控制器名字就会提示报错
   删除掉或者加上控制器名称就好了
第二十四
	如果引用了route.js 并且angular 和 route的包都引入了发现路由没生效
	可能是主页body 没写ng-App="路由的APP名称" 或者是写错了
第二十五
	angular.js:13236 Error: [$controller:ctrlfmt] Badly formed controller string ''. Must match `__name__ as __id__` or `__name__`.
	如果引用的模板ng-controller里面没有写内容就会报这个错
	解决方案 删掉ng-controller 或者加上控制器名字
第二十六 
	angular.js:13236 Error: [ng:areq] Argument 'fn' is not a function, got Object
	路由里面的控制器名称没有带引号
	解决方案就是把路由器使用到的控制器都带上引号
第二十七
	angular.js:13236 Error: [ng:areq] Argument 'IndexController' is not a function, got undefined
	IndexController 这个控制器没有找到
	解决方案 就是路由里面的控制器名称和js里面定义的控制器名称是否一致
	如果路由里面的控制器名称和js里面定义的控制器名称 已经一致了有可能是模板里面使用的控制器和他们两个不一致
第二十八
	如果请求了页面但是数据为空 可能是参数没有获取到
	这个 $routeParams 参数没加 或者写错了
	解决方案就在控制器里面加上 $routeParams 参数