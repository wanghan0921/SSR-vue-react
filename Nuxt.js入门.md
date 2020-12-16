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



##### 1.2.4 路由参数校验

Nuxt.js使用validate方法进行路由参数校验,这个方法必须返回一个布尔值
```js
<template>
    <div>
        详情{{$route.params.id}}
    </div>
</template>

<script>
    export default {
        // 使用validate方法进行路由参数校验,这个方法必须返回一个布尔值,
        validate(obj) {
            return /^\d+$/.test(obj.params.id)
        }
    }
</script>
```

##### 1.2.5 嵌套路由

1. 添加一个vue文件, 作为父组件
2. 添加一个与父组件同名的文件夹来存放子视图组件
3. 在父组件中. 添加组件`<nuxt-child></nuxt-child>`, 用于展示匹配到的子视图


#### 1.3 layouts & pages & components

##### 1.3.1 创建layout

1. 去layout文件夹下面新建一个新的layout组件, 例如`myLayout.vue`
2. 给需要的用到新layout的组件添加layout属性, 并指定需要使用的layout, 例如layout: 'myLayout'
```js
export default {
  layout: 'myLayout',
  data() {
    return {
      list: [
        {
          name: "aaa",
          id: 1
        },
        {
          name: "bbb",
          id: 2
        }
      ]
    };
  }
};
```

##### 1.3.2 特殊布局组件
在layout文件夹下, 创建一个error.vue , 名字只能叫这个, 所有匹配不到的页面都会同步到这个页面


##### 1.3.3 全局样式组件配置
1. 在asset下创建style文件夹, 里面创建index.css文件
2. nuxt.config.js文件中, 配置
```js
// Global CSS (https://go.nuxtjs.dev/config-css)
  css: [
    '~/assets/style/index.css'
  ],
```

#### 1.4 ElementUI使用
1. 下载 `npm i element-ui -S`
2. 在plugins文件夹下面, 创建ElementUI.js文件
```js
import Vue from 'vue'
import ElementUI from 'element-ui'
Vue.use(ElementUI)
```
3. 在nuxt.config.js中添加配置
```js
// Global CSS (https://go.nuxtjs.dev/config-css)
css: [
'~/assets/style/index.css',
'element-ui/lib/theme-chalk/index.css'
],

// Plugins to run before rendering page (https://go.nuxtjs.dev/config-plugins)
plugins: [
{src: '~/plugins/ElementUI', ssr: true}  // ssr:true表示这个插件只在服务端起作用
],

// Auto import components (https://go.nuxtjs.dev/config-components)
components: true,

// Modules for dev and build (recommended) (https://go.nuxtjs.dev/config-modules)
buildModules: [
],

// Modules (https://go.nuxtjs.dev/config-modules)
modules: [
],

// Build Configuration (https://go.nuxtjs.dev/config-build)
build: {
vendor: ['element-ui']  // 防止elementui被多次打包
}
```



#### 1.5 异步数据获取

**注意**
1. 在nuxt中, 生命周期函数只有created以及beforeCreate这两个生命周期函数能后在服务端正常使用
2. 在nuxt中发异步请求不能在created生命周期函数中去发, 因为他会在前端执行

Nuxt.js扩展了Vue.js, 增加了一叫`asynData`的方法, 使得我们可以在设置组件的数据之前能异步获取或处理数据.
`asynData`方法会在组件(**限于页面组件**)每次加载之前被调用.它可以在服务端或路由更新之前被调用. 所以需要注意这个函数不能使用`this`

使用方法:
`asynData(context, callback) {callback(null, data)}`
`context.route.params.XXXX`获取参数
`callback(new Error(), data)`渲染出错的页面
注意: 这个方法在服务端执行和客户端执行的区别

```js
asyncData(context, callback) {
    console.log(context)
    setTimeout(()=>{
      // callback有两个数据对象, 第一个数错误对象, 第二个是数据对象
      callback(null, {
        list: [
          {
            name: "aaa123",
            id: 1
          },
          {
            name: "bbb3123",
            id: 2
          }
        ]
      })
    },1000)
  },
```

```js
asyncData(context, callback) {
    return new Promise((resolve, reject)=> {
      setTimeout(()=>{
        resolve({
          list: [
            {
              name: "aaa",
              id: 1
            },
            {
              name: "bbb3",
              id: 2
            }
          ]
        })
      },1000)
    })
      .then(res => {
        console.log(res)
        callback(null, {list: res.data.list})
      })
      .catch(err => {
        // callback(err)
        context.error(err)
      })
  },
```



































