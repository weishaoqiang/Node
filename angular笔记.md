# angularjs笔记
## angualr思想：
- 基于mvc的开发框架，mvc是一种软件开发的架构模式，是一种开发思想。
- m->model模型：作用是用来操作数据的CRUD
- v->view试图: 展示数据
- c->controller控制器: 在试图和数据之间起到控制的作用，业务逻辑就属于控制器的范围。
## 单页应用程序
- 传统的页面请求返回整夜请求的页面：
- 弊端
```
重复性工作做得太多，浪费带宽
加载速度慢
用户体验不好
```
- 单页应用程序SPA (single page application)
- 过程

```
第一次请求一整个页面的数据
之后的请求都是通过ajax发送请求，通知返回数据，不再请求整个个页面。
```
- 实现单页应用程序的原理
- ajax
- 锚点链接location.hash#
- hashchange事件

## angular的使用
- 引包，引入整个angularjs文件。
- ng-app指令指定angular管理的区域。
- {{coding}} 双层花括号在angular中表示的是表达式。
- angular中的模块创建是没有顺序的。
## angular中的代码执行
## angular的指令
- ng-app指定angular的管理区域，也就是管理边界，在ng-app这个标签中才会收到angular的管理。
- ng-model是用来绑定数据的，这个指令只能够在表单标签中使用，它本质是操作的表单的value值
- {{}}成为angular中的表达式,也称为插值表达式，可以说他是用来展示数据的。
- ng-click指令

## angular中的模块
- angular中的代码都是依附在模块中的。


## 控制器的作用
- 初始化视图中使用的数据
- 通过$scope把数据暴露给试图
- 监视模型变化，对试图做出调整。
## $scope的说明
- 1 $scope是控制器和视图之间的桥梁，用于在控制器和视图之间传递数据
- 2 推荐：给 $scope 添加数据应该使用对象，而不是作为其属性
- 3 在控制器中暴露 数据模型（数据和行为），在视图中通过指令或表达式来使用
对比：局部变量
- 4 注意： $scope这个名称必须这么写！
- 5 $scope 是在控制器创建的时候，被注入进去的

## 数据监视
- $watch()方法
- 第一个参数表示监视的对象或者属性，这个方法是angular的内置方法。
- 第二个参数是一个回调函数，数据变化会执行这个回调函数
- 第三个参数:一个boolean值。如果监视的是对象，那么久要将第三个参数的值设为 true。
- $scope.$watch(obj,function(curValue,oldValue){},true)
- 但这个函数会一上来就调用一次。
- 监视的属性只能是$scope中的属性。

## 创建控制器方式
- 方式一：
```
controller("testController",function($scope){})
//这种方式存在一定的问题，压缩代码会存在一定的问题。
```
- 方式二（推荐做法）
```
//依赖注入方式
controller("testController",["$scope",function($scope){}]);
// 第一个参数是控制器名，第二个参数是一个数组。
```
- 构造函数法
```
// 通过this传值。
// HTML
<div ng-controller="testController as test">
    <p>{{test.name}}</p>
</div>

// js
angular.module("myApp",[]).controller('testController',["$scope",function($scope){
        this.name = "王茂";
    }]);
```

## angular闪烁问题和解决方法
- 因为在angular代码没执行，html的代码就已经渲染出来了。
- 解决方法:
- 方法一
```
直接把angular代码放在head标签中。先执行angular代码，在渲染html
```
- 方法二
```
只用ng-bind指令解决，这个指令实际上操作的是DOM中的innerText或者textContent属性。
会把之前标签中已经存在的内容覆盖掉了
```
- 方法三,移除样式
```
指令ng-cloak。解决闪烁问题，在angular执行完毕之后就将ng-cloak属性移除掉。
给当前标签添加class="ng-cloak"或者ng-cloak;
```

### ng-class指令
- ng-class="表达式或者字符串"，并以表达式的返回值 或者 字符串的值作为类名。
- ng-class="{}"还可放一个对象。

## angular中的服务
- 目的：对一些重复性的操作，进行封装，达到服用目的
- 服务只有第一次使用的时候，执行一次代码，有序在使用就不会在执行了（可以理解为angular中的缓存技术）
-

## 创建（配置）路由
- 语法：
```
myApp.config(['$routeProvider',function($routeProvider){
    // 第一个参数：表示锚点值(url)
    // 第二个参数：表示一个对象
    $routeProvider.when('/stu/lisi',{
        template:'<div>这是李四的信息</div>'
        })
        // 如果还有其他的不同信息，继续when就行了。
        .when('/stu/wangwu',{
            template:'<div>这是王五的信息</div>'
        })
        .when('/stu/teacher',{
        templateUrl:'文件路径/angular的模板id',
        // 指定管理当前的路由的控制器
        controller:'controllerName',
        })
        // 与when属性对应的的属性是otherwise属性,when中的路由都没有匹配的话就走otherwise
        .otherwise({
            redirectTo:'/默认链接参数',
            });

    }])
```
```
ng-view指令用于展示路由请求回来的信息
```
## $apply()方法
- 通过这个方法可以是angular代码重新执行一遍脏检查机制。

## angular注入失败
- 路径可能写错了

## angular 中url中的参数
- 在angular1.6+版本中，angular会给请求的参数前面加一个'!',是的这个参数不能够正确的获取，需要通过$locationProvider参数修改。

## angular中的跨域
- $http.jsonp()在angular中实现跨域的方法
- 只要是跨域请求，有需要在url中需要带有一个?callback = myCallback
- callback是参数
- myCallback是参数的值
- callback的用处：
 + 浏览器发送http请求，服务器会拿到真个url,并把url中的callback拿到，然后服务器去数据库查询并且拿到我们需要的数据数据。
 + 把数据和callback的值拼接处了一个固定结构并返回到浏览器端
## 跨域原理
- 跨域返回的是一个函数调用。

## angular中更新路由参数的服务$route
- 方法：$route.updatePramas({
    '参数名称': [参数值],
    ...
    })

## 创建指令
```
// 第一个参数是自定义指令名称
// 第二个参数是注入一些服务，最后是一个回调函数
- directive('myBtn',['',function(){
    // 自定义指令返回一个对象
    return {
        // 用于指定自定义的模板
        tenplate:,
    }
}])
```



## 控制器和路由之间的关系
- 只要路由规则能够匹配到，那么就会执行对应控制器中的代码。
