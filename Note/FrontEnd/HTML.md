# 软件准备

- VS Code
    - Live Server
    - Auto Rename Tag
    - 设置Format On Save

# HTML

## 文件结构

- 文本类型声明

```html
<！-- 声明文件类型 -->
<!DOCTYPE html> 
```

- HTML文件是一个树形结构

```bash
HTML
   |-- Body
   |   |-- H1
   |   `-- H2
   `-- HEAD
       |-- meta
       `-- title
```
```
- <html>表示一个 HTML 文档的根（顶级元素），所以它也被称为根元素。所有其他元素必须是此元素的后代
- <head>HTML head 元素 规定文档相关的配置信息（元数据），包括文档的标题，引用的文档样式和脚本等
- <body>：HTML body 元素表示文档的内容。document.body 属性提供了可以轻松访问文档的body 元素的脚本
- <title>：定义文档的标题，显示在浏览器的标题栏或标签页上。它只应该包含文本，若是包含有标签，则它包含的任何标签都将被忽略
- <meta>：表示那些不能由其它 HTML 元相关（meta-related）元素（(<base>、<link>, <script>、<style> 或 <title>）之一表示的任何元数据信息
```

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="description" content="这是一个神奇的网站" />
    <meta name="keywords" content="神奇,智慧" />
    <title>hey ! welcome to my website</title>
    <link rel="icon" href="/images/logo.png" />
  </head>
  <body>
    <h1>Welcome to my website !!!</h1>
  </body>
</html>
```

## 文本标签

文本标签虽然很多，但大部分可看成是预定好样式的div和span

```
- <div>：块状元素带换行，衍生元素<h1>, <p>, <pre>, <ul>, <ol>, <table>
- <span>：行内元素，衍生元素<i>, <b>, <del>, <ins>, <td>, <a>
```
```html
<div>Hello</div>
<div>World</div>
<span>Hello</span>
<span>World</span>
```

一、div的衍生元素
```
- <h>：标题，特定的大小粗细的div
- <p>：段落，div加上段落间距、忽略回车空格
- <pre>：段落，div加上段落间距、不忽略回车空格
```
```html
<pre>
    #include &lt;iostream&gt;
    using namespace std;
    int main()
    {
        cout &lt;&lt; "Hello World" &lt;&lt; endl;
        return 0;
    }
</pre>

<!--
	特殊字符
	&lt; 左尖括号 less
	&gt; 右尖括号 grater
-->
```
```
- <br>：回车
- &nbsp; 空格
- <hr>：水平线
- <i>：斜体
- <b>：粗体

<aside>
💡 这个元素过去被认为是粗体（Boldface）元素，并且大多数浏览器仍然将文字显示为粗体。尽管如此，你不应将 <b> 元素用于显示粗体文字；替代方案是使用 CSS font-weight 属性来创建粗体文字
</aside>

- <del>：删除线
- <ins>：下划线
- <strong>：加粗
- <mark>：高亮
```
## 图片标签

代码格式

```html
<img src="" width="500" height="600" alt="">
```

- src：该属性是必须的，它包含了你想嵌入的图片的文件路径（在线/网络）
- alt：图像描述（当图片无法显示时会显示alt）这不是强制性的，但对可访问性而言，它难以置信地有用——屏幕阅读器会将这些描述读给需要使用阅读器的使用者听，让他们知道图像的含义。如果由于某种原因无法加载图像，普通浏览器也会在页面上显示alt 属性中的备用文本：例如，网络错误、内容被屏蔽或链接过期时

实例：

```html
<img src="/images/mount.jpg" width="500" height="600" alt="This is a mount.">
```

Note：如果只设定宽度或者高度那么图片会等比放缩，img隶属于行内元素

## 音频标签

格式一

```html
<audio src="/audios/bgm.mp3" controls>无法播放</audio>
```

格式二

```html
<audio controls>
    <source src="/audios/sound1.mp3" type="audio/mpeg" />
    <source src="/audios/sound2.mp3" type="audio/mpeg" />
</audio>
```

Note：当前音源无法播放时，自动播放下一个，audio隶属于行内元素

## 视频标签

格式一

```html
<video controls src="/videos/video2.mp4">无法播放</video>
```

格式二

```html
<video width="1500" controls>
    <source src="/videos/video1.mp4" type="video/mp4">
    <source src="/videos/video2.mp4" type="video/mp4">
    无法播放
</video>
```

Note：当前视频源无法播放时，自动播放下一个，video隶属于行内元素

## 超链接元素

```html
<!-- 外链 -->
<a href="https://www.acwing.com">AcWing</a>
<!-- 内链 -->
<a href="/test.html">Test</a> 
<!-- 打开新页面 -->
<a href="https://ww.baidu.com" target="_blank">Baidu</a>
<-- 嵌入图片 -->
<a href="">
  <img src="" alt="">
</a>
```

Note：a隶属于行内元素，可以插入任意元素

## 表单元素

HTML 中form元素表示文档中的一个区域，此区域包含交互控件，用于向 Web 服务器提交信息
```
- <input> 用来填写内容
```
```html
<!-- form提交结果：跳转到 test 网页 -->
<form action="/test.html">
	<!-- name -->
  <label for="username">姓名</label>
  <input maxlength="10" type="text" name="username" id="username" />
  <br />
  <!-- age -->
  <label for="age">年龄</label>
  <input placeholder="age" required type="number" name="age" id="age" />
  <br />
  <!-- email -->
  <label for="email"></label>
  <input placeholder="email" type="email" name="email" id="email" />
  <br />
  <!-- password -->
  <label for="password"></label>
  <input
    placeholder="password"
    type="password"
    name="password"
    id="password"
  />
  <br />
  <!-- radio 多选一 -->
  <div>最喜欢的语言</div>
  <input type="radio" name="lang" value="cpp" id="cpp" />
  <label for="cpp">cpp</label>
  <br />
  <input type="radio" name="lang" value="java" id="java" />
  <label for="java">java</label>
  <br />
  <input type="radio" name="lang" value="python" id="python" />
  <label for="python">python</label>
  <br />
  <!-- file -->
  <label for="file">上传程序</label>
  <input type="file" name="file" id="file" />
  <br />
  <!-- textarea -->
  <div>在下面文字框内写入你的个人介绍</div>
  <label for=""></label>
  <textarea name="comment" id="eomment" cols="35" rows="5"> </textarea>
  <br />
  <!-- button -->
  <button type="submit">提交</button>
</form>
```

Note：submit按钮可以提交该form下的所有的input信息
```
- <select> 元素表示一个提供选项菜单的控件
```
```html
<!--  默认为空 -->
<label for="lang">语言</label>
<select name="lang" id="lang">
  <option value=""></option>
  <option value="cpp">C++</option>
  <option value="java">Java</option>
  <option value="python">Python</option>
</select>
```

```html
<!-- 请选择 -->
<label for="lang">语言</label>
<select name="lang" id="lang">
  <option value="">请选择</option>
  <option value="cpp">C++</option>
  <option value="java">Java</option>
  <option value="python">Python</option>
</select>
```

```html
<!-- 默认选择一个 -->
<label for="lang">语言</label>
<select name="lang" id="lang">
  <option value="">请选择</option>
  <option selected value="cpp">C++</option>
  <option value="java">Java</option>
  <option value="python">Python</option>
</select>
```

## 列表元素
```
- <li>  list 列表
- <ul> unorder list
- <ol> order list
```
```html
<ul>
  <li>first item</li>
  <li>second item</li>
  <li>third item</li>
</ul>
```

```html
<ol>
  <li>first item</li>
  <li>second item</li>
  <li>third item</li>
</ol>
```

```html
<!-- 多级列表 -->
<ul>
  <li>a</li>
  <ul>
    <li>b</li>
      <ul>
        <li>c</li>
      </ul>
  </ul>
</ul>
```
```
- <dl> 是一个包含术语定义以及描述的列表，通常用于展示词汇表或者元数据 (键 - 值对列表)
- <dt>  键
- <dd> 值
```
```html
<dl>
  <dt>爱情</dt>
  <dd>love</dd>
  <dt>元素</dt>
  <dd>meta</dd>
  <dt>纸巾</dt>
  <dd>tissue</dd>
</dl>
```

## 表格元素
```
- <table>元素表示表格数据 — 即通过二维数据表表示的信息
- <caption> 展示一个表格的标题， 它常常作为 <table> 的第一个子元素出现，同时显示在表格内容的最前面，但是，它同样可以被 CSS 样式化，所以，它同样可以出现在相对于表格的任意位置
- <thead> 元素定义了一组定义表格的列头的行
- <tbody> 元素定义一组数据行
- <tr>  元素定义表格中的行。 同一行可同时出现<td> 和<th> 元素
- <th> 元素定义表格内的表头单元格
- <td> 元素 定义了一个包含数据的表格单元格
```
```html
<table>
  <caption>
    <b>Transcript</b>
  </caption>
  <thead>
    <tr>
      <th>Name</th>
      <th>Math</th>
      <th>English</th>
      <th>PE</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>fanfan</td>
      <td>100</td>
      <td>100</td>
      <td>100</td>
    </tr>
    <tr>
      <td>Alice</td>
      <td>90</td>
      <td>89</td>
      <td>92</td>
    </tr>
  </tbody>
</table>
```

## 语义标签
```
- <header> 元素用于展示介绍性内容，通常包含一组介绍性的或是辅助导航的实用元素。它可能包含一些标题元素，但也可能包含其他元素，比如 Logo、搜索框、作者名称，等等
- <nav> 元素表示页面的一部分，其目的是在当前文档或其他文档中提供导航链接。导航部分的常见示例是菜单，目录和索引
- <section> 元素表示一个包含在 HTML 文档中的独立部分，它没有更具体的语义元素来表示，一般来说会有包含一个标题
- <figure> 元素代表一段独立的内容，经常与说明（caption）<figcaption> 配合使用，并且作为一个独立的引用单元。当它属于主内容流（main flow）时，它的位置独立于主体。这个标签经常是在主文中引用的图片，插图，表格，代码段等等，当这部分转移到附录中或者其他页面时不会影响到主体
- <figcaption> 元素 是与其相关联的图片的说明/标题，用于描述其父节点 <figure> 元素里的其他数据、
- <article> 元素表示文章
- <aside>  元素表示一个和其余页面内容几乎无关的部分，被认为是独立于该内容的一部分并且可以被单独的拆分出来而不会使整体受影响。其通常表现为侧边栏或者标注框
- <footer>  元素表示最近一个章节内容或者根节点（sectioning root ）元素的页脚。一个页脚通常包含该章节作者、版权数据或者与文档相关的链接等信息
```
```html
<header><h1>我的收藏</h1></header>
<hr>
<nav>
  <ul>
    <li>音乐</li>
    <li>图片</li>
    <li>视频</li>
  </ul>
</nav>
<hr>
<figure>
  <img width="100" src="/images/logo.png" alt="logo">
</figure>
<figcaption>Logo</figcaption>
<hr>
<article>
  <h3>春</h3>
  <p>春春春春春春春春春春春春春春春春春春春春春春春春春</p>
</article>
<hr>
<footer>&copy;2018-2020fanfan版权所有</footer>
```

## 特殊符号

![](https://pic1.imgdb.cn/item/63402b7316f2c2beb11db0dd.png)