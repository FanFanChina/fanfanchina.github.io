## 目录结构

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

## 基础知识

### 新建页面与设置首页面

- 新建页面
  
    ```json
    # 无需自己建一堆文件，只需在app.json文件内添加页面路径保存即可
    "pages":[
        "pages/index/index",
        "pages/logs/logs",
        "pages/list/list"
      ]
    ```
    
- 修改项目首页(默认渲染全局配置文件内的第一个page)

### 小程序和网页的不同点

- WXML与HTML的不同点
    - 标签名称不同
        - HTML - div, span,  img, a
        - WXML - view, text, image, navigator
    - 属性名称不同
        - <a href=”#”>链接</a>
        - <navigator url=”/pages/home/home”></navigator>
    - 提供类似Vue的语法
        - 数据绑定
        - 列表渲染
        - …
- WXSS与CSS的不同点
    - 新增rpx尺寸单位，不同大小的屏幕会自动换算
    - 提供全局WXSS和局部WXSS
    - 仅支持部分CSS选择器
- JS
    - app.js - 小程序入口文件
    - pages的js文件 -  页面的入口文件
    - utils的js文件 - 自己写的模块、函数

## 组件

### view

### scroll-view

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

### image

```css

```

## 数据绑定

```js
data: {
    info: '你好世界'
	imgSrc: 'www.xxxxx.com',
	randomNum: Math.random() * 10
},
```

```html
<view>{{info}}</view>
<image src="{{imgSrc}}"></image>
<view>{{randomNum >= 5 ? 'haha' : 'nini'}}</view>
```

## 事件绑定

### 点击输出

```html
*<button type="primary" bindtap="btnTapHandler">按钮</button>*
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

### 点击修改页面date的值

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

## input事件绑定

```html
<input bindinput="test_01"></input>
```

```js
Page({
    test_01(e) {
        console.log(e.detail.value);
    }
})
```

### 实现文本框和data数据之间的实时同步

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

P22

## 窗口配置

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

### 云端和本地数据同步问题

- 云端更新 >> 本地重新获取
- 云端数据修改时，和本地数据不处于同一页面时，返回本地数据页面再刷新数据
- 云端数据修改时，和本地数据处于同一页面时，直接刷新

