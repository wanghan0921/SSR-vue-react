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


#### 2.页面导航

2.1.1 路由跳转

  1. Link组件
    ```js
    import Link from 'next/link';

    const index = () => {
        return (
            <div>
                <p>Next.js入门啊哈哈哈哈哈</p>
                {/* link组件
                    注意: 
                    1. Link组件内不能直接放字符串 , 可以用一个标签包裹起来
                    2. Link内只能有一个子节点
                    3. 不能直接给Link组件设置样式, 因为他是一个HOC(高阶组件), 给可以给它的子元素设置样式
                */}
                <Link href="/next-route/myindex">
                    <span>myindex</span>
                </Link>
            </div>
        )
    }

    export default index
    ```

  组件`<Link>`可接收URL对象, 而且它还会自动格式化生成URL字符串
    ```js
    <Link href={{pathname: '/next-route/myindex', query: {id: 1}}}>
        <span>myindex</span>
    </Link>
    ```
  
  
  2. 命名式路由
  
    ```js
    import Router from 'next/router'
    
    <div onClick={()=> {Router.push('/next-route/students')}}>student</div>
    ```
    
  URL语法对象
    ```js
    <div onClick={()=> {Router.push({pathname:'/next-route/students', query: {id: 1}})}}>student</div>
    ```

  > 注意: 1. 如果没有匹配到的话, 默认会去找`_error.js`中定义的组件 
  >       2. 路由跳转不会向服务器发送页面请求 



