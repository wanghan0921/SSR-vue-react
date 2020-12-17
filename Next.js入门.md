### Next.js

[Next.js官网](https://www.nextjs.cn/)

Next.js是一个基于React的一个服务端渲染简约的框架. 它使用React语法, 可以很好的实现代码的模块化, 有利于代码的开发和维护.

Next.js带来了很多好的特性: 
+ 默认服务端渲染模式, 以文件系统为基础的客户端路由
+ 代码自动分割是页面加载更快
+ 以webpack的热替换(HMR)为基础的开发环境
+ 使用React的JSX和ES6的module, 模块化和维护更方便
+ 可以运行在Express和其他Node.js的HTTP服务器上
+ 可以定制化专属的babel和webpack配置

使用服务端渲染的好处: 
+ 对SEO友好
+ 提升在手机以及低能耗设备上的性能
+ 快速显示首页


#### Next.js体验

1. 创建一个Next.js的项目
```js
mkdir hello-next
cd hello-next
npm init -y
npm i --save react react-dom next
mkdir pages
```

2. 配置package.json中的scripts属性
```js
{
  "scripts": {
    "dev": "next",
    "build": "next build",
    "start": "next start"
  }
}
```
but, 此时`npm run dev`会得到一个404页面

3.创建一个pages/index.js文件
```js
const index = () => {
    return (
        <div>
            Next.js入门啊哈哈哈哈哈
        </div>
    )
}

export default index
```











































