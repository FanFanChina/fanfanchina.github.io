# CSS

## 样式定义方式

一、行内样式表（inline style sheet）

```html
<!-- 直接定义在标签的style属性中 -->
<img width="300" height="200" src="/static/images/mountain.jpg" alt="山" />
<img
  src="/static/images/mountain.jpg"
  alt="山"
  style="width: 300px; height: 200px"
/>
```

二、内部样式表（internal style sheet）

```html
<!-- 定义在style标签中，通过选择器影响对应的标签 -->
<!-- 可以对同一个页面中的多个元素产生影响 -->
<style type="text/css">
  p {
    width: 30px;
    height: 30px;
    background-color: aquamarine;
  }
  .big {
    width: 50px;
    height: 50px;
  }
  .blue {
    background-color: lightblue;
  }
</style>
<body>
  <p class="big">1</p>
  <p class="blue">2</p>
  <p class="big blue">3</p>
  <p>4</p>
</body>
```

三、外部样式表（external style sheet）

```html
<!-- 定义在css样式文件中，通过选择器影响对应的标签。可以用link标签引入某些页面 -->
<!-- 可以对多个页面产生影响 -->
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Document</title>
    <link rel="stylesheet" href="/static/css/style.css"> <!-- link stylesheet -->
  </head>
  <body>
    <p class="big">1</p>
    <p class="blue">2</p>
    <p class="big blue">3</p>
    <p>4</p>
  </body>
</html>
```

注释方式（注意不能使用//）

```css
/* 
	.blue {
    background-color: lightblue;
  }
*/
```

## 选择器

- 标签选择器

```css
div {
  width: 20px;
  height: 20px;
  color: blueviolet;
  background-color: #617ce95a;
}
```

- ID选择器

```css
#div2 {
  background-color: black;
}
```

- 类选择

```css
.bigAndblack {
  width: 100px;
  height: 100px;
  background-color: black;
}
```

- 伪类选择器（和类一块使用的状态选择器）
    - :hover：鼠标悬停时的样式
    
    ```css
    .big:hover {
      /* 变大为原来的1.2倍 */
      transform: scale(1.2);
      /* 渐变时间0.2s */
      transition: 0.2s;  
    }
    ```
    
    - :link：链接访问前的样式
    - :visited：链接访问后的样式
    - :active：鼠标点击后长按时的样式
    
    ```css
    .friendlink:link {
      color: lightgrey;
    }
    .friendlink:hover {
      color: blue;
    }
    .friendlink:active {
      color: darkmagenta;
    }
    .friendlink:visited {
    	  color: lightgrey;
    }
    ```
    
    - :focus：聚焦后的样式
    
    ```css
    input:focus {
      background-color: lightskyblue;
      
    }
    input:hover {
      transform: scale(1.01);
    }
    ```
    
    - :nth-child(n)：选择是其父标签第n个子元素的所有元素
    
    ```css
    p {
      width: 30px;
      height: 30px;
      background-color: lightblue;
    }
    p:nth-child(2) {
      background-color: lightcoral;
    }
    p:nth-child(odd) {
      background-color: lightcoral;
    }
    p:nth-child(even) {
      background-color: lightcoral;
    }
    p:nth-child(2n + 1) {
      background-color: lightcoral;
    }
    ```
    
    - :target：当url指向该元素时生效
    
    ```css
    p:target {
      background-color: aquamarine;
      transform: scale(1.2);
      transition: 200ms;
    }
    ```
    
- 复合选择器
    - element1, element2：同时选择元素element1和元素element2（也可以用伪类选着器）
    
    ```css
    div {
      width: 50px;
      height: 50px;
    }
    
    p {
      width: 30px;
      height: 30px;
    }
    
    div, p:hover {
      background-color: lightblue;
    }
    ```
    
    - element.class：选则包含某类的element元素
    
    ```css
    div.haha {
      background-color: lightblue;
    }
    ```
    
    - element1 + element2：选择紧跟element1的element2元素
    
    ```css
    div + p {
      background-color: lightblue;
    }
    ```
    
    - element1 element2：选择element1内的所有element2元素。
    
    ```css
    div p {
      background-color: lightblue;
    }
    ```
    
    - element1 > element2：选择父标签是element1的所有element2元素
    
    ```css
    div > p {
      background-color: lightblue;
    }
    ```
    
- 通配符选择器
    - 选择所有标签
    
    ```css
    * {
      font-size: 100px;
    }
    ```
    
    - [attribute]：选择具有某个属性的所有标签
    
    ```css
    input[required] {
      background-color: lightcoral;
    }
    ```
    
    - [attribute=value]：选择attribute值为value的所有标签
    
    ```css
    input[id="haha"] {
      background-color: lightblue;
    }
    ```
    
- 伪元素选择器
    - ::first-letter：选择第一个字母
    
    ```html
    <p><span>我</span>们的爱情到这刚刚好</p>
    ```
    
    ```css
    p::first-letter {
      color: red;
      font-size: 23px;
    }
    ```
    
    - ::first-line：选择第一行
    
    ```css
    P::first-line {
      color: red;
    }
    ```
    
    - ::selection：选择已被选中的内容
    
    ```css
    p::selection {
      background-color: lightblue;
    }
    ```
    
    - ::before：可以在元素前插入内容
    - ::after：可以在元素后插入内容
    
    ```css
    h1 {
      color: lightblue;
    }
    h1::before {
      content: '《';
      color: lightcoral;
    }
    h1::after {
      content: '》';
      color: lightcoral;
    }
    ```
    
    - 样式渲染优先级
        - 正常情况：后覆盖前
        - 权重大小，越具体的选择器权重越大：`!important` > 行内样式 > ID选择器 > 类与伪类选择器 > 标签选择器 > 通用选择器
        - 权重相同时，后面的样式会覆盖前面的样式
        - 继承自父元素的权重最低

## 颜色

一、RGB表示法

rgb(173, 216, 230)

其中第一个数表示红色，第二个数表示绿色，第三个数表示蓝色。

二、16进制表示法

#ADD8E6。
其中第1-2位表示红色，第3-4位表示绿色，第5-6位表示蓝色

简写方式：#ABC，等价于#AABBCC

三、RGBA表示法

rgba(173, 216, 230, 0.5)

前三个数同上，第四个数表示透明度

四、预置颜色

black、white、red、green、blue、lightblue等

五、取色方式

- 网页里的颜色，可以在chrome的调试模式下获取
- 其他颜色可以使用QQ的截图软件：
    - 直接按c键，可以复制rgb颜色
    - 按住shift再按c键，可以复制16进制颜色值
- 其他工具

## 文本

- text-align CSS 属性定义行内内容（例如文字）如何相对它的块**父元素**对齐。text-align**并不控制块元素自己的对齐**，只控制它的行内内容的对齐 （left、center、right、justify）

```css
div {
  background-color: lightcoral;
  text-align: center;
}
```

- line-height 用于设置多行元素的空间量，如多行文本的间距。对于块级元素，它指定元素行盒（line boxes）的最小高度。对于非替代的 inline 元素，它用于计算行盒（line box）的高度

```css
div {
  line-height: 7em;
  background-color: lightblue;
  text-align: center;
}
```

- 补充知识点：长度单位
    - px	设备上的像素点
    - %	相对于父元素的百分比
    - em	相对于当前元素的字体大小
    - rem 相对于根元素的字体大小
    - vw	相对于视窗宽度的百分比
    - vh	相对于视窗高度的百分比
- letter-spacing 属性用于设置文本字符的间距

```css
div {
  letter-spacing: 1em;
}
```

- text-indent  定义一个块元素首行文本内容之前的缩进量

```css
p {
  text-indent: 2em;
}
```

- text-decoration 用于设置文本的修饰线外观的（下划线、上划线、贯穿线/删除线 或 闪烁）它是 text-decoration-line, text-decoration-color, text-decoration-style, 和新出现的 text-decoration-thickness 属性的缩写

```css
div {
  text-decoration: underline overline dotted red ;
}
```

- text-shadow 为文字添加阴影。可以为文字与 text-decorations 添加多个阴影，阴影值之间用逗号隔开。每个阴影值由元素在X和Y方向的偏移量、模糊半（**模糊程度**）和颜色值组成

```css
div {
  text-shadow: 1px 1px 2px red;
}
```

## 字体

- font-size 字体大小
- font-style  字体样式
    - normal ：正常
    - italic：斜体
- font-width 字体粗细
    - normal：正常
    - bold：加粗
    - lighter：变细
    - 100：变为100
    
    ```css
    		100: The quick brown fox jumps over the lazy dog
        200: The quick brown fox jumps over the lazy dog
        300: The quick brown fox jumps over the lazy dog
        400: The quick brown fox jumps over the lazy dog
        500: The quick brown fox jumps over the lazy dog
        600: The quick brown fox jumps over the lazy dog
        700: The quick brown fox jumps over the lazy dog
        800: The quick brown fox jumps over the lazy dog
        900: The quick brown fox jumps over the lazy dog
    ```
    
- font-family 字体种类

## 背景

- background-color ：背景颜色
- background-image：背景图片

```css
.background {
  width: 200px;
  height: 200px;
  background-color: lightblue;
  background-image: url(/static/images/monster.png);
}
```

```css
/*也可以是渐变色图片*/
.background {
  width: 200px;
  height: 200px;
  background-color: lightblue;
  background-image: linear-gradient(rgba(0, 0, 255, 0.5), rgba(255, 255, 0, 0.5));
}
```

- background-size ：背景图片尺寸

```css
.background {
  width: 200px;
  height: 200px;
  background-color: lightblue;
  background-image: url(/static/images/monster.png);
  background-size: 50%;
}
```

- background-repeat：是否重复填充

```css
background-repeat: repeat;
background-repeat: no-repeat;
background-repeat: repeat-x;
background-repeat: repeat-y;
background-repeat: space;
background-repeat: round;
```

- background-position：初始位置

```css
background-position: top;
background-position: left;
background-position: center;
background-position: 25% 75%;
background-position: bottom 50px right 100px;
background-position: right 35% bottom 45%;
```

- background-attachment：决定背景图像的位置是在视口内固定，或者随着包含它的区块滚动
    - scroll 此关键属性值表示背景相对于元素本身固定，而不是随着它的内容滚动（对元素边框是有效的）
    - fixed 此关键属性值表示背景相对于视口固定。即使一个元素拥有滚动机制，背景也不会随着元素的内容滚动

## 边框

- border-style：边框样式（上右下左）

```css
border-style: none;
border-style: dotted;
border-style: inset;
border-style: dashed solid;
border-style: dashed double none;
border-style: dashed groove none dotted;
```

- border-width：边框宽度（上右下左）

```css
border-width: thick; /*厚的*/
border-width: 1em;
border-width: 4px 1.25em;
border-width: 2ex 1.25ex 0.5ex;
border-width: 0 4px 8px 12px;
```

- border-color：边框颜色（上右下左）

```css
/* border-color: color; 单值语法 */
border-color: red;

/* border-color: vertical horizontal; 双值语法*/
border-color: red #f015ca;

/* border-color: top horizontal bottom; 三值语法 */
border-color: red yellow green;

/* border-color: top right bottom left; 四值语法 */
border-color: red yellow green blue;

border-color: inherit
```

- border-radius：边框圆角

```css
border-radius: 30px;
border-radius: 25% 10%;
border-radius: 10% 30% 50% 70%;
border-radius: 10% / 50%;
border-radius: 10px 100px / 120px;
border-radius: 50% 20% / 10% 40%;
```

- border-collapse：用来决定表格的边框是分开的还是合并的。在分隔模式下，相邻的单元格都拥有独立的边框。在合并模式下，相邻单元格共享边框

```css
border-collapse: collapse;
border-collapse: separate;
```

## 元素展示格式

- display
    - block：独占一行width、height、margin、padding均可控制width默认100%
    
    ```css
    div {
      background-color: lightblue;
      width: 100px;
      height: 100px;
      /* 外边距 */
      margin: 10px; 
      /* 内边距 */
      padding: 10px; 
    }
    ```
    
    - inline：共占一行，**width与height无效**，水平方向的margin与padding有效，竖直方向的margin与padding无效，width默认为本身内容宽度
    
    ```css
    span {
        background-color: lightcoral;
        padding: 10px;
        margin: 10px;
    }
    ```
    
    - inline-block：可以共占一行，width、height、margin、padding均可控制，width默认为本身内容宽度
    
    ```css
    span {
        background-color: lightcoral;
        display: inline-block;
        width: 200px;
        height: 50px;
        padding: 10px;
        margin: 10px;
    }
    ```
    
    - divh和span互换
    
    ```css
    div {
    	display : inline;
    }
    
    span {
    	display : block;
    }
    ```
    
- white-space
    - nowrap 不换行
    
    ```css
    div {
      background-color: lightblue;
      /* 不换行 */
      white-space: nowrap;
      width: 100px;
      height: 100px;
    }
    ```
    
    - pre
    
    ```css
    div {
      background-color: lightblue;
      white-space: pre;
      width: 100px;
      height: 100px;
    }
    ```
    
- overflow：超出部分处理
    - auto：自动添加滚轮
    
    ```css
    div {
      background-color: lightblue;
      width: 100px;
      height: 40px;
      overflow: auto;
    }
    ```
    
    - hidden：隐藏多余部分
    
    ```css
    div {
      background-color: lightblue;
      width: 100px;
      height: 40px;
      overflow:hidden;
    }
    ```
    
    - text-overflow: ellipsis：产出部分用省略号代替
    
    ```css
    div {
      background-color: lightblue;
      width: 100px;
      height: 40px;
      overflow: hidden;
      text-overflow: ellipsis;
    }
    ```
    

## 内外边距

- margin外边距
    - 可以接受1~4个值（上、右、下、左的顺序）
    - 可以分别指明四个方向：margin-top、margin-right、margin-bottom、margin-left
    - 可取值
        - length：固定值
        - percentage：相对于包含块的宽度，以百分比值为外边距。
        - auto：让浏览器自己选择一个合适的外边距。有时，在一些特殊情况下，该值可以使元素居中、
    - 外边距重叠
        - 块的上外边距(margin-top)和下外边距(margin-bottom)有时合并(折叠)为单个边距，其大小为单个边距的最大值(或如果它们相等，则仅为其中一个)，这种行为称为边距折叠
        - 父元素与后代元素：父元素没有上边框和padding时，后代元素的margin-top会溢出，溢出后父元素的margin-top会与后代元素取最大值
- padding 内边距
    - 可以接受1~4个值（上、右、下、左的顺序）
    - 可以分别指明四个方向：padding-top、padding-right、padding-bottom、padding-left
    - 可取值
        - length：固定值
        - percentage：相对于包含块的宽度，以百分比值为内边距

## 盒子模型

- box-sizing：定义了 user agent 应该如何计算一个元素的总宽度和总高度
    - content-box：是默认值，设置border和padding均会增加元素的宽高
    - border-box：设置border和padding不会改变元素的宽高，而是挤占内容区域

## 位置

- position
    - static：正常布局 top, right, bottom, left 和 z-index 属性无效
    - relative：该关键字下，元素先放置在未添加定位时的位置，再在不改变页面布局的前提下调整元素位置（因此会在此元素未添加定位时所在位置留下空白）。top, right, bottom, left等调整元素相对于初始位置的偏移量
    - absolute：元素会被移出正常文档流，并**不为元素预留空间**，通过指定元素相对于最近的非 static 定位祖先元素的偏移，来确定元素位置。绝对定位的元素可以设置外边距（margins），且不会与其他边距合并
    - fixed：元素会被移出正常文档流，并不为元素预留空间，而是通过指定元素相对于**屏幕视口（viewport）的位置（浏览器）**来指定元素位置。元素的位置在屏幕滚动时不会改变
        
        ```css
        .fixed-div {
            background-color: lightcoral;
            position: fixed;
            top:75%;
            right:0px;
            width:20px;
            height:90px;
            padding: 2px;
        }
        ```
        
    - sticky：元素根据正常文档流进行定位，然后相对它的最近滚动祖先（nearest scrolling ancestor）和 containing block (最近块级祖先 nearest block-level ancestor)，包括table-related元素，基于top, right, bottom, 和 left的值进行偏移。偏移值不会影响任何其他元素的位置**（超出设定位置时黏附）**
        
        ```css
        .sticky-div {
            background-color: lightcoral;
            position: sticky;
            top:0px;
        }
        ```
        

## 浮动

- 修改display = inline-block也可以实现，但是会留下间隙
- float：沿其容器的左侧或右侧放置，允许文本和内联元素环绕它。该元素从网页的正常流动(文档流)中移除，尽管仍然保持部分的流动性（与绝对定位相反）
    - left：左对齐
    - right：右对齐
    - 由于float意味着使用块布局，它在某些情况下修改display 值的计算值，display为inline或inline-block时，使用float后会**统一变成block**
- 有时，你可能想要强制元素移至任何浮动元素下方。比如说，你可能希望某个段落与浮动元素保持相邻的位置，但又希望这个段落从头开始强制独占一行。此时可以使用clear
    - left：清除左侧浮动
    - right：清除右侧浮动
    - both：清除左右两侧浮动

## Flex布局（弹性布局）

### 整体布局

- flex-direction：如何摆放，主轴方向
    - row：flex容器的主轴被定义为与文本方向相同。 主轴起点和主轴终点与内容方向相同
    - row-reverse：表现和row相同，但是置换了主轴起点和主轴终点
    - column：flex容器的主轴和块轴相同。主轴起点与主轴终点和书写模式的前后点相同
    - column-reverse：表现和column相同，但是置换了主轴起点和主轴终点
- flex-wrap：是否换行
    - nowrap：默认值。不换行
    - wrap：换行，第一行在上方
    - wrap-reverse：换行，第一行在下方
- flex-flow：flex-direction 和 flex-wrap 的简写。默认值为：row nowrap
- justify-content：主轴对齐方式
    - flex-start：默认值。左对齐
    - flex-end：右对齐
    - space-between：左右两段对齐
    - space-around：在每行上均匀分配弹性元素。相邻元素间距离相同。每行第一个元素到行首的距离和每行最后一个元素到行尾的距离将会是相邻元素之间距离的一半
    - space-evenly：flex项都沿着主轴均匀分布在指定的对齐容器中。相邻flex项之间的间距，主轴起始位置到第一个flex项的间距，主轴结束位置到最后一个flex项的间距，都完全一样
- align-items：交叉轴对齐方式
    - flex-start：元素向主轴起点对齐
    - flex-end：元素向主轴终点对齐
    - center：元素在侧轴居中
    - stretch：弹性元素被在侧轴方向被拉伸到与容器相同的高度或宽度
- align-content：浏览器如何沿着弹性盒子布局的纵轴和网格布局的主轴在内容项之间和周围分配空间
    - flex-start：所有行从垂直轴起点开始填充。第一行的垂直轴起点边和容器的垂直轴起点边对齐。接下来的每一行紧跟前一行
    - flex-end：所有行从垂直轴末尾开始填充。最后一行的垂直轴终点和容器的垂直轴终点对齐。同时所有后续行与前一个对齐
    - center：所有行朝向容器的中心填充。每行互相紧挨，相对于容器居中对齐。容器的垂直轴起点边和第一行的距离相等于容器的垂直轴终点边和最后一行的距离
    - stretch：拉伸所有行来填满剩余空间。剩余空间平均地分配给每一行

> Note：align-items 和 align-content 类似，区别在于单行时align-items生效而align-contents不生效
> 

### 局部布局

- order：定义flex项目的顺序，值越小越靠前
- flex-grow：设置 flex 项主尺寸 的 flex 增长系数。负值无效，默认为 0
- flex-shrink：指定了 flex 元素的收缩规则。flex 元素仅在默认宽度之和大于容器的时候才会发生收缩，其收缩的大小是依据 flex-shrink 的值，负值无效，默认为1
- flex-basis：指定了 flex 元素在主轴方向上的初始大小（可以看成宽度）可以是 <length>; 该值也可以是一个相对于其父弹性盒容器主轴尺寸的百分数 。负值是不被允许的。默认为 auto
- flex：flex-grow、flow-shrink、flex-basis的缩写
    - auto —— flex: 1 1 auto
    - none —— flex: 0 0 auto

## 响应式布局

- media查询：当屏幕宽度满足特定条件时应用css

```css
@media(min-width: 768px) {
    .container {
        width: 960px;
        background-color: lightblue;
    }
}
```

- [bootstrap](https://v5.bootcss.com/)

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Test</title>
    <link
      rel="stylesheet"
      href="/static/third_party/bootstrap-5.1.3-dist/css/bootstrap.min.css"
    />
    <script src="/static/third_party/bootstrap-5.1.3-dist/js/bootstrap.min.js"></script>
  </head>
  <body>
    <div class="container">
      <form>
        <div class="row">
            <div class="col-md-6 col-xs-12">
                <div class="mb-3">
                    <label for="exampleInputEmail1" class="form-label"></label>
                    <input type="text" class="form-control" id="exampleInputEmail1" placeholder="username">
                  </div>
            </div>
            <div class="col-md-6 col-xs-12">
                <div class="mb-3">
                    <label for="exampleInputEmail1" class="form-label" ></label>
                    <input type="password" class="form-control" id="exampleInputEmail1" placeholder="password">
                  </div>
            </div>
        </div>
        <div class="row">
            <div class="col-md-6 col-xs-12">
                <button class="btn btn-success" style="width: 100%; margin-top: 10px;">提交</button>
            </div>
            <div class="col-md-6 col-xs-12">
                <button class="btn btn-light" style="width: 100%; margin-top: 10px;">取消</button>
            </div>
        </div>
      </form>
    </div>
  </body>
</html>
```