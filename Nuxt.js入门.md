### Nuxt.js入门

#### 1.1.1 什么是Nuxt.js

[Vue.js 服务器端渲染指南]([https://ssr.vuejs.org/zh/#%E4%BB%80%E4%B9%88%E6%98%AF%E6%9C%8D%E5%8A%A1%E5%99%A8%E7%AB%AF%E6%B8%B2%E6%9F%93-ssr-%EF%BC%9F](https://ssr.vuejs.org/zh/#什么是服务器端渲染-ssr-？))

[Nuxt.js](https://www.nuxtjs.cn/guide)

Nuxt.js是一个基于vue的通用应用框架

#### 1.1.2创建一个nuxt项目

```js
// 全局安装create-nuxt-app
npm i create-nuxt-app -g
// 创建项目
create-nuxt-app my-nuxt-demo
// 启动
cd my-nuxt-demo
npm run dev
```

#### 1.1.3 文件结构分析

```js
├ my-nuxt-demo 
 ├─.nuxt                      // nuxt自动生成,临时的用于编辑的文件, build
 ├─assets                     // 用于组织未编译的静态资源文件,如Less,Sass或JavaScript, 对于不需要通过webpack处理的静态资源文件, 可以放到 static 目录中
 ├─components                // 组件
 ├─layouts                   // 布局目录,用于组织应用的布局组件,不可更改
 ├─middleware                // 存放中间件
 ├─node_modules
 ├─pages					  // 用于组织应用的路由以及视图, Nuxt.js根据该目录结构自动生成对应的路由配置,文件名不可更改
 ├─plugins                   // 用于组织那些需要在vue.js应用实例化之前需要运行的JavaScript插件
 ├─static                  // 用于存放应用的静态文件,此类文件不会被Nuxt.js调用webpack进行构建编译处理,服务器启动的时候,该目录下的文件会映射到应用的根路径/下, 文件夹名不可更改
 ├─store				  
 ├─.editorconfig         // 开发工具格式化配置
 ├─.gitignore            // 配置git忽略文件
 ├─nuxt.config.js        // 用于组织Nuxt.js应用的个性化配置, 以便覆盖默认配置
 ├─package-lock.json
 ├─package.json
 ├─README.md
 
```

#### 1.2 页面和路由

##### 1.2.1 基本路由

Nuxt.js依据`pages`目录结构自动生成vue-router模板的路由配置

假设`pages`的目录结构如下

```js
├ pages
   ├─index,vue                     
   ├─user
      ├─index.vue
	  ├─one.vue
```

那么, Nuxt.js自动生成的路由配置如下:

```js
router:{
    routes: [
        {
            name:'index',
            path: '/',
            component: 'path/index.vue'
        },
        {
            name:'user',
            path: '/user',
            component: 'path/user/index.vue'
        },
        {
            name:'user-one',
            path: '/user/one',
            component: 'path/user/one.vue'
        }
    ]
}
```

##### 1.2.2 页面跳转

1. 不要写成a标签，因为是重新获取一个新页面，并不是SPA
2. `<nuxt-link to="/pageA"></nuxt-link>`
3. this.$router.push('/pageA')
4. this.$router.push({name: AAA})


##### 1.2.3 动态路由

+ 再Nuxt.js中定义带参数的动态路由, 需要创建对应的以**下划线作为前缀**的Vue文件或目录
+ 获取动态参数{{$route.qaram.id}}











































