# 微信小程序

## 基础知识

### 和网页的不同点

- WXML与HTML的不同点
    - 标签名称不同
        - HTML - div, span,  img, a
        - WXML - view, text, image, navigator
        
    - 属性名称不同
    
    ```html
    <a href="#">链接</a>
    <navigator url="/pages/home/home"></navigator>
    ```
    
    - 提供类似Vue的语法
        - 数据绑定
        - 列表渲染
        - …
    
- WXSS与CSS的不同点
    - 新增 rpx 尺寸单位，不同大小的屏幕会自动换算
    - 提供全局WXSS和局部WXSS
    - 仅支持部分CSS选择器
    
- JS
    - app.js - 小程序入口文件
    - pages的js文件 -  页面的入口文件
    - utils的js文件 - 自己写的模块、函数

### 小程序文件目录结构

- **pages  - 小程序的页面**
    - wxml - 骨架
    - wxss  - 样式
    - js - 页面交互的函数
    - json - 页面配置文件(优于全局配置文件)
- utils - 工具性质的模块
- **app.js - 小程序的入口模块**
- **app.json - 小程序的全局配置文件**
    - pages - 页面路径
    - windows - 全局窗口样式
    - style - 样式组件版本
    - sitemapLocation - 指明sitemap.json的位置
- app.wxss - 小程序全局样式文件
- project.config.json - 小程序开发工具的个性化配置
    - setting.json - 项目编译配置
    - projectname - 项目名称(非小程序名称)
    - appid - 小程序ID
- sitemap.json 用来配置小程序页面是否能被微信索引

### WXML组件

- scroll-view

```html
<scroll-view class="container1" scroll-y>
    <view>A</view>
    <view>B</view>
    <view>C</view>
</scroll-view>
```

```css
.container1 view {
    width: 100px;
    height: 100px;
    text-align: center;
    line-height: 100px;
}

.container1 view:nth-child(1) {
    background-color: blanchedalmond;
}

.container1 view:nth-child(2) {
    background-color: lightcoral;
}

.container1 view:nth-child(3) {
    background-color: lightpink;
}

.container1 {
    border: 1px solid red;
    width: 100px;
    height: 120px;
}
```

### wx:if 控制显示页面组件显示

```html
<view class="show" wx:if="{{!showBack}}" bindtap="showCardBack">显示答案</view>
```

### 数据绑定

在页面的html页面可以通过**Mustache**语法直接引用data中的变量值
```html
<view>{{info}}</view>
<image src="{{imgSrc}}"></image>
<view>{{randomNum >= 5 ? 'haha' : 'nini'}}</view>
```

### 事件绑定

- 点击输出

```html
<button type="primary" bindtap="btnTapHandler">按钮</button>
```

```js
Page({
    // 页面数据
    data: {
    },
    // 事件处理函数
    btnTapHandler(e) {
        console.log(e);
    }
})
```

- 点击修改页面date的值

```js
Page({
    // 页面数据
    data: { count: 1 },
    // +1 函数
    addOne() {
        this.setData({ count: this.data.count + 1 });
        console.log(this.data.count);
    }
})
```

### 事件传参

**Note01: 小程序在绑定事件的同时不可以在函数后面传参数，而需要使用data-参数的方法传**

**Note02: 使用data-传参时，只能用小写，不能用大写**

```html
<button type="primary" bindtap="add" data-t1="{{2}}">Add</button>
<button type="primary" bindtap="add" data-t2="2">Add</button>
```

```js
Page({
    // 页面数据
    data: { count: 1 },
    // +1 函数
    add(e) {
        console.log(e);
    }
})

Page({
    data: { 
        count: 1
    },
    add(e) {
        this.setData({ count: this.data.count + e.target.dataset.t1 });
    }
})
```

## 页面相关

### 新建页面

```json
# 无需自己建一堆文件，只需在app.json文件内添加页面路径保存即可
"pages":[
    "pages/index/index",
    "pages/logs/logs",
    "pages/list/list"
  ]
```

### 设置首页

修改项目首页(默认渲染全局配置文件内的第一个page)

### 页面跳转

- 跳转到导航栏页面

```js
wx.switchTab({
    url: '../home/home'
})
```
- 跳转到非导航栏页面

```js
wx.navigateTo({
    url: '/pages/home-search/home-search',
})
```
- 跳转到非导航栏页面，并传参

```html
<view bindtap="toRepositoryDetail" id='{"userName":"{{rep.user_name}}", "repositoryName":"{{rep.repository_name}}"}' class="home-bottom-rep">
```

```js
toRepositoryDetail(e) {
    wx.navigateTo({
        url: '/pages/repositoryDetail/repositoryDetail?rep=' + e.currentTarget.id,
    })
}
```

- 返回上一个页面

```js
wx.navigateBack({
	delta: 0,
})
```

​    

### 刷新页面

```js
this.onLoad()
// 如果作用域不同，需要先获取到外部的this, 再调用onLoad()函数
that.onLoad()
```

## 数据相关

### 页面数据

小程序页面的js文件中含有对象(键)**data**，其属性(值)代表该页面的全部**数据**

```js
data: {
    info: '你好世界'
	imgSrc: 'www.xxxxx.com',
	randomNum: Math.random() * 10
},
```

### 全局数据

定义在app.js 中的数据 —— globalData中的变量可以被其他页面所引用

```js
globalData: {
    color: '#28BFA0',
    userName: '',
    password: '',
    userStatus: 0,
    // 00b -- 0 -- 未登录
    // 01b -- 1 -- 用户不存在 0 注册登录成功 1
    // 10b -- 2 -- 用户存在 1 密码错误, 登陆失败 0
    // 11b -- 3 -- 用户存在 1 密码正确, 登陆成功 1
    userRegisterTime: '',
    userRepositories: []
},
```

为了方便其他页面引用，我们一般在其他页面中先定义一个app作为app.js的索引

```js
const app = getApp()
let userName = app.globalData.userName
let userRegisterTime = app.globalData.userRegisterTime
```

### 修改页面数据

在页面的js文件中，不能直接给data中的对象赋值，要调用内置函数setData才能成功修改data中对象的值

```javascript
// 修改对象的值
this.setData({info : "世界你好"})
// 修改对象属性的值

```

### 修改全局数据

```js
// 可以直接赋值
getUserName(e) {
    app.globalData.userName = e.detail.value
}
```

### 修改上一页页面数据

```js
// 获取当前页码
let currentPages = getCurrentPages()
// 获取前一页数据
let prePage = currentPages[currentPages.length - 2]
prePage.setData({['repData.cardNumber'] : Number(prePage.data.repData.cardNumber) + 1})
```

### 获取输入框的数据

```html
<input bindinput="getAddRepositoryName" type="text" maxlength="20" placeholder="请输入记忆库名称" />
```

```js
getAddRepositoryName(e) {
    this.setData({
        repositoryName: e.detail.value
    })
}
```

### 获取文本框的数据

```html
<input value="{{msg}}" bindinput="test_01"></input>
```

```css
input {
    border: 1px solid red;
    padding: 5px;
    margin: 5px;
    border-radius: 13px;
}
```

```js
Page({
    data: {
        msg: "请输入内容"
    },
    test_01(e) {
        this.setData({ msg : e.detail.value });
        console.log(this.data.msg);
    }
})
```

### 循环渲染数组数据

```html
<!-- for循环遍历userRepositories数组，每一项都赋值给rep，指定主键为repository_name -->
<view wx:for="{{userRepositories}}" wx:for-item="rep" wx:key="repository_name">
```

### 处理其它页面传入的数据

```js
onLoad(options) {
    let rep = JSON.parse(options.rep)
    this.setData({
        repData: rep
    })
}
```

## 窗口相关

### 导航栏

```json
"navigationBarTitleText": "hahah"
"navigationBarBackgroundColor": "#efefef"
"navigationBarTextStyle": "white"
```

### 下滑刷新

```json
"enablePullDownRefresh": true
```

### 背景图片

```json
"backgroundColor": "#efefee" 
"backgroundTextStyle": "dark"
```

### 上拉触底

```json
# 没有特殊需求，无需修改
"onReachBottomDistance": 50
```

### TabBar

![](https://pic1.imgdb.cn/item/6341956416f2c2beb1450039.png)

## 网络数据请求

### 请求限制

- 只能请求Https类型的接口
- 必须将接口域名添加到信任列表当中
- 域名不能是IP
- 域名必须经过ICP备案
- 域名一个月最多修改5次

### Get请求

```js
wx.request({
    url: 'http://47.96.186.213:',
    method: 'GET',
    data: {
        userName : this.userName,
        password : this.password,
        time: new Date()
    },
    success: (res) => {
        console.log(res)
    }
})
```

### Post请求

```js
wx.request({
    url: 'http://47.96.186.213:',
    method: 'POST',
    data: {
        userName : this.userName,
        password : this.password,
        time: new Date()
    },
    success: (res) => {
        console.log(res)
    }
})
```

## 开发经验总结

### JS中的日期对象转化

```js
// 转化为MySQL支持的格式 - 2000-01-01 12:00:00
let learnTime = new Date().toISOString().slice(0, 19).replace('T', ' ')
// 获取毫秒数
new Date().getTime()
// 使用毫秒数定义日期对象
new Date(86400000)
// 计算两个日期相差天数
let days = parseInt((new Date().getTime() - new Date(userRegisterTime).getTime()) / 86400000)
```

### 云端和本地数据同步问题

- 云端更新 >> 本地重新获取
- 云端数据修改时，和本地数据不处于同一页面时，返回本地数据页面再刷新数据
- 云端数据修改时，和本地数据处于同一页面时，直接刷新
