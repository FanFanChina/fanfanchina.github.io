## 布局技巧

### 文字居中

```css
text-align: center;
line-height: = div 高度
```

### 多个div处在同一行

```css
/* 对父元素使用以下样式 */
display: flex;
justify-content: center; /*居中*/
justify-content: space-around; /*分散*/
justify-content: space-between; /*相同间隔*/
```

### 使div居中

```css
margin:0 auto;
```

```css
position: relative;
top: 50%;
left: 50%;
transform: translate(-50%, -50%);
```

### 图片在div中居中

```css
display: flex;
justify-content: center;
align-items: center;
```

### 图片做背景铺满整个div

```css
background: url(../img/yjw_login_default_bg.png) no-repeat;
background-size: cover;
background-size: 100% 100%;
```

