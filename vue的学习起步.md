# vue的学习
## 基础的语法
### 数据双向绑定
- 在vue中所有的数据，包括属性和方法都是以对象的形式存在。
- v-model,可以将表单的value值和当前的标签内容尽心绑定同步
- v-for,循环渲染。例如对列表进行渲染
- data属性表述的数数据，它用来存放数据对象，methods属性表述的是方法，它可以用来存放方法对象。


## .vue组件模板文件结构
```
    <template>
        <--html codes-->
    </template>
    <script>
        <--js codes-->
        这里的js代码分为两部分
        导入其他依赖的模块(任何需要依赖的文件，任何格式的 .js .css .less .vue .png ...)
        import name form '模块路径'
        导出相关组件的对象和方法供其他组件使用
            导出对象的固定写法：
            export default{
                // 返回一个data方法，组件中(.vue文件中)导出数据时，这个data肯定是方法，并且肯定是return一个对象
                data(){
                    return {}
                }
            }
    </script>
    <style>
        <--style codes-->
    <style>
```
### 注意点：
- vue2.0要求末班中编写的html文件中必须放到一个根元素上
```
    <-- 错误写法 -->
    <template>
        <h1></h1>
        <h2></h2>
    </template>

    <-- 正确写法 -->
    <template>
        <div class="tmep">
            <h1></h1>
            <h2></h2>
        </div>
    </template>
```
### vue的数据要在html页面上显示出来的话必须挂在到html文件中的一个id为app的根元素上

### vue中的mvc模式
- M：负责实现业务功能
- V：展示数据
- C：调度模型视图
```
    <!-- 控制器 -->
    export default{
        <!-- data方法中的内容成为模型（model） -->
        data(){
            return {
                msg: '欢迎学习vuejs'
            }
        }
    }
```

### vue的基本指令
- v-text: 作用和插值表达式功能一样
- v-html: 能将标签标签字符串渲染成页面标签
- v-bind: 这个指令能够在html上扩展任何的属性，例如<span v-bind:title="tip" :pid="tip">欢迎学习vue.js</span>
- v-show: 使用display属性控制元素的显示和隐藏
- v-on: 给元素注册事件，简写方式使用@进行简写，例如@click="fun"与v-on:click="fun"是一样的效果

### vue相关参数
- data: 所有视图上通过v- 或者插值表达式使用到的数据变量的数据里来源
- method: method中要访问data方法中的的属性，使用this.
### vue组件命名规则：
- 建议使用驼峰命名法
### vue组件之间的通信-
- components: 在一个组件注册使用另外一个组件
- props: 作用，一般写在子组件中的export default{}中，用于接收父组件传过来的数据；作用：父组件向子组件传入数据的一种方式。
```
父组件中怎样使用子组件
    1. 导入子组件对象，import SubVue form './sub.vue'
    2. 在components属性中注册子组件实例
    3. 在html结构中使用子组件，可以使用同名标签挂在子组件'<SubVue></SubVue>'，也可以使用'<sub-vue></sub-vue>'
父组件向子组件传输数据
    1. 在父组件data中定义数据
    2. 在父组件中挂载子组件的标签使用v-bind:将数据创给子组件，注意要使用与数据同名的属性
    3. 在子组件中使用props属性接收父组件传过来的数据，这个props属性是子组件export default {}中的属性
```
- created
- computed

### vue中的路由vue-router
- 什么是路由
```
    根据不同的url加载不通的vue组件，这叫做路由
```
- 路由的路由规则
```
    其实就是我们在浏览器看到url后面的#之后的一串字符
```
- 路由规则的集中表现形式
```
    无参数路由规则
        /Home
        /Home/News
    有参数路由规则
        /Home/News/:id ->传一个id值
    eg:
        /Home/News/13
        /Home/News/abc
```
- 使用vue-router
```
    1.安装vue-router
    2.在main.js中导入vue-router
    3.使用Vue对象使用vue-router。
        import Vue form 'vue'
        import vueRouter form 'vue-router'
        Vue.use(vueRouter);

    4. 配置路由规则
        var routers = new vueRouter([

            ])
```
