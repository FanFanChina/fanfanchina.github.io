## FS模块

### 文件读入

```js
// 导入fs模块
const fs = require('fs')
// 文件路劲 | 读取格式 | 回调函数
fs.readFile("1.txt", "utf8", function(err, dataStr) {
    // 读取失败结果
    console.log(err)
    console.log("-----")
    // 读取成功结果
    console.log(dataStr)
})
```

### 文件写入

```js
// 导入fs模块
const fs = require('fs')
// 文件路径 | 写入内容 | 回调函数
fs.writeFile('1.txt', 'Hello Node.js', function(err) {
        console.log(err)
})
```

### Add

```js
const fs = require('fs')
fs.writeFile('test.txt', 'hello node.js', function(err) {
    if(err) return console.log("文件写入失败")
    console.log('文件写入成功')
})
```

### 练习

```js
const fs = require('fs')
fs.readFile('test.txt', 'utf8', function(err, dataStr) {
    if(err) return console.log('读入文件失败' + err.message)
    console.log('读取文件成功' + dataStr)
    // 按空格分割为一个数组arrOld
    const arrOld = dataStr.split(' ');
    const arrNew = []
    // 将等号替换为空格
    // for(let i = 0; i < arrOld.length; i ++ ) arrNew.push(arrOld[i].replace('=', ':'))
    arrOld.forEach(x => {arrNew.push(x.replace('=', ':'))})
    // 加回车，转化为字符串
    let s1 = arrNew.join('\r\n')
    fs.writeFile('test.txt', s1, function(err) {
        if(err) return console.log('文件写入失败' + err.message)
        console.log('文件写入成功')
    })
})
```

- 文件路径动态拼接问题

    问题:  在执行js文件时会拼接当前所在目录和执行的文件的目录，如果当前目录和所在文件目录不是同一级别，会出错

    解决方案1 - 使用绝对路径

    解决方案2 - 使用__dirname   

    ```js
    __dirname + '/test.txt'
    ```


## Path路径模块

```js
const path = require('path')
// 路径拼接
let myPath = path.join('/a', '/b/c', '../', '/d', 'e')
console.log(myPath)
// 获取文件名
let baseName = path.basename('/hah/nihao/fs.js')
console.log(baseName)
// 获取文件拓展名
let extendName = path.extname('/hah/nihao/fs.html')
console.log(extendName)
```

## http模块

### 基本Web服务

```js
// 导入http模块
const http = require('http')
// 创建http实例
const server = http.createServer()
// 绑定函数
server.on('request', function(req, res) {
    console.log("有人访问了我们的网站")
})
// 启动服务
server.listen(8080, function() {
    console.log('web服务启动成功')
})
```

```js
// 导入http模块
const http = require('http')
// 创建http实例
const server = http.createServer()
// 绑定函数
server.on('request', function(req, res) {
    console.log("有人访问了我们的网站")
    // req - 客户端信息
    console.log(req.url)     // 请求地址
    console.log(req.method)  // 请求方式
    // res - 响应信息(返回字符串 hello node.js)
    res.end('hello node.js')
})
// 启动服务
server.listen(8080, function() {
    console.log('web服务启动成功')
})
```

### 解决中文乱码问题

```js
// 导入http模块
const http = require('http')
// 创建http实例
const server = http.createServer()
// 绑定函数
server.on('request', function(req, res) {
    console.log("有人访问了我们的网站")
    // 设置响应头
    res.setHeader('Content-Type', 'text/html; charset=utf-8')
    res.end('你好，Node.js')
})
// 启动服务
server.listen(8080, function() {
    console.log('web服务启动成功')
})
```

### 不同 url 响应不同内容·

```js
const { copyFileSync } = require('fs');
const http = require('http')
const server = http.createServer()
server.on('request', function(req, res) {
    let url = req.url;
    console.log(url)
    if(url === '/' || url === '/index.html') res.end('<div>Hello</div>')
    else res.end('<p>404</p>')
})

server.listen(80, function() {
    console.log('Web Server 启动成功')
})
```

## 模块化

### 模块分类

- 系统模块（fs、path、http）
- 第三方模块
- 用户自定义模块（自己写的js文件）

### 模块调用（require函数）

```js
// 当加载模块时，会执行模块的代码，并导入模块内的exports的成员
let t = require('./test.js') // 可以不加js后缀
```

### 模块作用域

- 默认情况模块内的成员只能在模块内访问
- 可以使用modul的exports，将模块内的成员共享出去
  
    ```js
    let age = 18;
    module.exports.age = age
    module.exports.username = "fanfan";
    module.exports.print = function () {
      console.log("hello world");
    };
    ```
    
    ```js
    let age = 18;
    module.exports = {
        age : age,
        print : function() {
            console.log("hello")
        }
    }
    ```
    
- module和module.exports 可替换，但最终引入的对象永远是module.exports
  
    ```js
    let age = 18;
    exports = {
        age : age,
        print : function() {
            console.log("hello")
        }
    }
    // 因为module.exports 为 {} 所以最终加载的模块也为 {}
    ```
    

## Npm

### 安装命令

```bash
npm install 包名 
npm i 包名
```

### moment包使用

```js
const moment = require('moment')
let time = moment().format('YYYY-MM-DD HH:mm:ss')
console.log(time)
```

### 多出的文件结构

- node_modules 包文件
- package-lock.json 包文件下载信息
- package.json 安装了哪些包

### 安装指定版本

```js
npm i 包名@版本号
```

### 版本语义

![](https://pic1.imgdb.cn/item/63404b2116f2c2beb1656498.png)

### 快速生成package.json文件

```js
npm init -y
```

### 一次性安装所有依赖包

```js
npm i
```

### 卸载包

```js
npm uninstall 包名
```

### 安装只在开发阶段用到的包

```js
npm i 包名 -D
```

### 切换为国内源

- npm 命令
  
   ![](https://pic1.imgdb.cn/item/63404ab416f2c2beb1648223.png)
  
- nrm 工具
  
    ![](https://pic1.imgdb.cn/item/63404abc16f2c2beb16492b3.png)

### 包的分类

- 项目包
    - 开发依赖包 -D
    - 核心依赖包
- 全局包 -g
  
    ![](https://pic1.imgdb.cn/item/63404b6716f2c2beb165f65a.png)

- i5ting_top

    ![](https://pic1.imgdb.cn/item/63404b6716f2c2beb165f65e.png)

    

## Express

### 安装

```js
npm i express@4.17.1
```

### 基本流程

```js
// 导入
const express = require('express')
// 创建web服务器
let app = express()
// 启动web服务器
app.listen(80, () => {
    console.log('启动成功')
})
```

### 监听Get和Post请求

```js
// 导入
const express = require('express')
// 创建web服务器
let app = express()
// 添加Get请求监听
app.get('/user', (req, res) => {
    res.send({
        name: 'zs',
        age: 18,
        gender: '男'
    })
})
// 添加Post请求监听
app.post('/admin', (req, res) => {
    res.send('post请求成功')
})
// 启动web服务器
app.listen(80, () => {
    console.log('启动成功')
})

```

### 获取url携带的查询参数

```js
const express = require('express')
let app = express()
app.get('/', (req, res) => {
    // 通过query获取查询参数
    console.log(req.query)
    res.send(req.query)
})
app.listen(80, () => {
    console.log('启动成功')
})
```

### 获取url中的动态参数(相当于赋值)

```js
const express = require('express')
let app = express()
// :id 是动态参数
app.get('/user/:id/:name', (req, res) => {
    console.log(req.params)
    res.send(req.params)
})
app.listen(80, () => {
    console.log('启动成功')
})
```

```bash
启动成功
{ id: '666' , name: 'zs'}
```

### 托管静态资源

```js
const express = require('express')
let app = express()
// 托管login下的所有文件
app.use(express.static('./login'))

app.listen(80, () => {
    console.log('启动成功')
})
// 可以托管多个文件夹，并顺序查找，同一文件在不同文件夹中同时出现，只会显示第一次出现的那个
```

### 添加前缀

```js
const express = require('express')
let app = express()

// 添加前缀 login
app.use('/login' ,express.static('./login'))

app.listen(80, () => {
    console.log('启动成功')
})
```

### 使用nodemon调试程序

- 目的: 不用频繁的开启关闭项目

- 安装

    ```bash
    npm i nodemon -g
    ```

- 使用

    ```bash
    nodemon app.js
    ```

### 路由

前面挂载到app上的get和post请求监听就是路由，但我们一般不这么写，而是实现路由模块化

- 一般流程

    ```js
    const express = require('express')
    // 创建路由对象、R要大写
    const router = express.Router();
    // 添加路由
    router.get('/', (req, res) => {
        res.send('get')
    })
    router.post('/', (req, res) => {
        res.send('post')
    })
    // 共享模块（= 而不是 .）
    module.exports = router
    ```

    ```js
    const express = require('express')
    let app = express()
    // 导入路由模块
    const testRouter = require('./test_router.js')
    // 使用(注册)路由模块
    app.use(testRouter)
    app.listen(80, (req, res) => {
        console.log(req)
    })
    ```
    
- 添加前缀

    ```js
    // 使用路由模块, 并添加前缀
    app.use('/api', testRouter)
    ```

    

### 中间件

- 定义

    ```js
    const express = require('express')
    let app = express()
    
    // 中间件函数
    let mv = function(req, res, next) {
        console.log('这是一个中间件函数')
        next()
    }
    
    app.listen(80, (req, res) => {
        console.log(req)
    })
    ```

- 全局生效的中间件

    ```js
    const express = require('express')
    let app = express()
    
    // 中间件函数
    let mw = function(req, res, next) {
        console.log('这是一个中间件函数')
        next()
    }
    // 添加到app服务上
    app.use(mw)
    
    app.get('/', (req, res) => {
        console.log('get')
    })
    
    app.listen(80, (req, res) => {
        console.log(req)
    })
    ```

    ```bash
    这是一个中间件函数
    get
    ```

- 简化写法

    ```js
    const express = require('express')
    let app = express()
    
    // 简化写法
    app.use(function(req, res, next) {
        console.log('这是一个中间件函数')
        next()
    })
    
    app.get('/', (req, res) => {
        console.log('get')
    })
    
    app.listen(80, (req, res) => {
        console.log(req)
    })
    ```

- 中间件的作用 —— 多个中间件共享同一份 req 和 res

    ```js
    const express = require('express')
    const { data } = require('jquery')
    let app = express()
    
    app.use(function(req, res, next) {
        req.startTime = Date.now();
        next()
    })
    
    app.get('/', (req, res) => {
        console.log(req.startTime)
    })
    
    app.listen(80, (req, res) => {
        console.log(req)
    })
    ```

- 局部生效的中间件

    ```js
    const express = require('express')
    const { data } = require('jquery')
    let app = express()
    
    let mw = function(req, res, next) {
        req.startTime = Date.now();
        next()
    }
    
    // 为该监听添加mw函数
    app.get('/', mw, (req, res) => {
        console.log(req.startTime)
    })
    
    app.listen(80, (req, res) => {
        console.log(req)
    })
    ```

- 使用错误中间件捕获错误信息(必须放在路由之后)

    ```js
    const express = require('express')
    const { data } = require('jquery')
    let app = express()
    
    app.get('/', (req, res) => {
        throw new Error('服务器内部错误')
        console.log('hahaha')
    })
    
    app.use((err, req, res, next) => {
        console.log(err.message)
        res.send(err.message)
        next()
    })
    
    app.listen(80, (req, res) => {
        console.log(req)
    })
    ```

- json中间件

    ```js
    const express = require('express')
    const { data } = require('jquery')
    let app = express()
    
    app.use(express.json())
    
    app.get('/', (req, res) => {
        console.log(req.body)
    })
    
    app.listen(80, (req, res) => {
        console.log(req)
    })
    ```

- urlencoded中间件

    ```js
    const express = require('express')
    const { data } = require('jquery')
    let app = express()
    
    app.use(express.urlencoded({ extended: false }))
    
    app.get('/', (req, res) => {
        console.log(req.body)
    })
    
    app.listen(80, (req, res) => {
        console.log(req)
    })
    
    ```

## 操控数据库

### 安装数据库模块

```bash
npm i mysql
```

### 配置mysql模块

```js
const mysql = require('mysql')
const db = mysql.createPool({
    host: '',       // 数据库ip
    user: '',       // 用户名
    password: '',   // 密码
    database: '',   // 数据库名称
})
```

### 查询users的所有列

```js
let sqlStr = 'SELECT * from users'
db.query(sqlStr, (err, results) => {
    if(err) return console.log(err.message)
    console.log(results)
})
// 返回的结果是数组
```

### 插入数据

```js
// 添加用户
let addUser = (name, passwd) => {
    let user = {
        name: name,
        passwd: passwd,
        register_time: new Date(),
        active_degree: 1
    }
    // ? 是临时占位符，执行时被替换
    let sql = 'INSERT INTO users (user_name, user_passwd, user_register_time, user_active_degree) VALUES (?, ?, ?, ?)'
    db.query(sql, [user.name, user.passwd, user.register_time, user.active_degree],(err, results) => {
        if(err) return console.log(err.message)
        // 影响了一行，代表插入插入数据成功
        if(results.affectedRows === 1) {console.log('用户添加成功')}
    })
}
addUser('疯狂的石头', 'jffjaslkks')
```

```js
// 简化写法(要求列名和变量名一一对应)
let addUser = (name, passwd) => {
    let user = {
        user_name: name,
        user_passwd: passwd,
        user_register_time: new Date(),
        user_active_degree: 1
    }
    let sql = 'INSERT INTO users SET ?'
    db.query(sql, user,(err, results) => {
        if(err) return console.log(err.message)
        if(results.affectedRows === 1) {console.log('用户添加成功')}
    })
}

addUser('疯狂的石头', 'jffjaslkks')
```

### 更新数据

```js
// 更改用户信息
let updateUser = (id, name, passwd) => {
    let user = {
        user_id: id,
        user_name: name,
        user_passwd: passwd
    }
    let sql = 'update users set user_name=?, user_passwd=? where user_id=?'
    db.query(sql, [user.user_name,user.user_passwd, user.user_id],(err, results) => {
        if(err) return console.log(err.message)
        if(results.affectedRows === 1) {console.log('更新成功')}
    })
}

updateUser(6, '小小', 'jfsfks')
```

```js
// 简化写法(要求列名和变量名一一对应)
let updateUser = (id, name, passwd) => {
    let user = {
        user_id: id,
        user_name: name,
        user_passwd: passwd
    }
    let sql = 'update users set ? where user_id = ?'
    db.query(sql, [user, user.user_id],(err, results) => {
        if(err) return console.log(err.message)
        if(results.affectedRows === 1) {console.log('更新成功')}
    })
}
updateUser(6, '大大', 'jfsfks')
```

### 删除数据

```js
// 删除用户
let deleteUser = (id) => {
    let sql = 'delete from users where user_id=?'
    db.query(sql, id,(err, results) => {
        if(err) return console.log(err.message)
        if(results.affectedRows === 1) {console.log('删除成功')}
    })
}

deleteUser(6)
```

### 标记删除

```js
// 一般我们不会真的删除一条数据，而是添加标记，使用update语句
let deleteUser = (id) => {
    let sql = 'update users set user_status=? where user_id=?'
    db.query(sql, [0, id],(err, results) => {
        if(err) return console.log(err.message)
        if(results.affectedRows === 1) {console.log('删除成功')}
    })
}
deleteUser(3)
```

### 数据库函数的异步性

这里不知道数据库函数的异步性会使人十分懵，曾经遇到数据库函数的返回值一直是undefined的情况，让人十分抓狂

```js
// 问题代码
const verifyUser = (userName, time, password) => {
    let sql = 'select * from users where user_name=? and user_register_time=? and user_passwd=?'
    db.query(sql, [userName, time, password],(err, result) => {
        // 如果出错直接返回，并输出错误信息
        if(err) return console.log(err.message)
        // 如果密码正确返回ture
        if(result.length) return true
        // 否者返回false
        else return false
    })
}
var t = verifyUser('fanfan', '2022-10-08', 'fanfanchina')
console.log(t)
```

这是因为

## 身份认证

### 服务端渲染 - Session

- HTTP协议的无状态性

    ![](https://pic1.imgdb.cn/item/634184d816f2c2beb11f4991.jpg)

- 如何突破无状态

    ![](https://pic1.imgdb.cn/item/6341853e16f2c2beb1203832.jpg)

- Cookie是什么？

    ![](https://pic1.imgdb.cn/item/6341862516f2c2beb12242cd.jpg)

- Cookie如何工作

    ![](https://pic1.imgdb.cn/item/634186c116f2c2beb123a868.jpg)

- Cookie不具备安全性

    ![](https://pic1.imgdb.cn/item/6341873116f2c2beb124aefd.jpg)

- Session认证机制

    ![](https://pic1.imgdb.cn/item/634187ba16f2c2beb125ea1f.jpg)

- Session如何工作

    ![](https://pic1.imgdb.cn/item/6341887916f2c2beb1279e72.jpg)

### 使用express-session模块

- 安装session模块

    ```bash
    npm i express-session
    ```

- 使用session模块

    ```js
    const session = require('express-session')
    app.use(
        session({
            secret: fanfan, // 随便写
            resave: false,
            saveUninitialized: true
        })
    )
    ```

- 存入用户信息

    ![](https://pic1.imgdb.cn/item/63418b4a16f2c2beb12e649c.jpg)

- 读取用户信息

    ![](https://pic1.imgdb.cn/item/63418bb916f2c2beb12f6e80.jpg)

- 清空用户信息（登出时使用）

    ![](https://pic1.imgdb.cn/item/63418c2216f2c2beb1305aa5.jpg)

### 前后端分离 - JWT

- 当前端请求后端接口不存在跨域问题时，推荐使用session机制
- 否则推荐使用JWT认证机制

JWT目前写小程序用不到，先不学了哈哈哈
