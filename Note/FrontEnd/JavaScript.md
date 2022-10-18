# JavaScript

## 运行环境

一、HTML文件的任意位置的Script标签内

```html
<script type="module">
    let x = 3;
    console.log(x);
</script>
```

二、引入整个JS文件

```html
<script type="module" src="/static/js/index.js"></script>
```

三、引入部分JS文件的部分内容

```js
let name = "fanfan";
let age = 18;
function print()
{
    console.log("My name is " + name + '.');
    console.log("I am " + age + '.');
}

export{
    name,
    age,
    print
}
```

```html
<script type="module">
      import {name, print} from "/static/js/index.js";
      console.log(name);
      print();
    </script>
```

Note：type = “module” 可以将变量的作用域由全局限制为局部，防止多变量同名冲突

## 执行顺序

1. 类似于HTML与CSS，按从上到下的顺序执行
2. 事件驱动执行

## HTML, CSS, JS三者之间的关系

1. CSS控制HTML
2. JavaScript控制HTML与CSS
3. 为了方便开发与维护，尽量按照上述顺序写代码。例如：不要在HTML中调用JavaScript中的函数

## 变量与运算符

- 数字

```js
<script type="module">
  let a = 1;
  const b = 2;
  let c = 1.233;
  console.log(a, b, c, typeof c);
</script>
```

- String

```js
let s1 = 'hahaha';
let s2 = 'hahaha';
let name = 'funfan';
// string只可读
let temp = name.substr(0, 1) + 'a' + name.substr(2);
console.log(temp);
```

- 对象

```js
let d = {
    name : 'fanfan',
    'age' : 18,   
}
console.log(d['name']);
console.log(d.age);
// 可以给不存在的键赋值
d['school'] = 'pku'
console.log(d);
	// 删除键 
delete d.school;
console.log(typeof d);
console.log(typeof null);

let a;
console.log(typeof a);
```

- 运算符
    - 与C++、Python、Java类似
    - 不同点
        - 表示乘方
        - 等于与不等于用===和!==

## 输入与输出

- 输入
    - 从HTML与用户的交互中输入信息，例如通过input、textarea等标签获取用户的键盘输入，通过click、hover等事件获取用户的鼠标输入
    
    ```html
    <div>请在方输入火星文</div>
    <div >
      <textarea  class="input" name="" id="" cols="30" rows="10">请输入</textarea>
    </div>
    <div>
      <button class="button">R U N</button>
    </div>
    <div >
      <textarea class="output" name="" id="" cols="30" rows="10">请输入</textarea>
    </div>
    </div>
    <script type="module">
    import {main} from '/static/js/test.js';
    main();
    </script>
    ```
    
    ```js
    let input = document.querySelector('.input');
    let run = document.querySelector('.button');
    let output = document.querySelector('.output');
    
    function main(){
        run.addEventListener('click', function(){
            let s = input.value;
            output.innerHTML = s;
        })
    }
    
    export {
        main
    }
    ```
    
    - 通过Ajax与WebSocket从服务器端获取输入
    - 标准输入
- 输出
    - 调试用console.log，会将信息输出到浏览器控制台
    - 改变当前页面的HTML与CSS
    - 通过Ajax与WebSocket将结果返回到服务器
- 格式化
    - 字符串中填入数值
    
    ```js
    let name = 'yxc', age = 18;
    let s = `My name is ${name}, I'm ${age} years old.`;
    ```
    
    - 定义多行字符串
    
    ```js
    let s = 
    `<div>
        <h2>标题</h2>
        <p>段落</p>
    /div>`
    ```
    
    - 保留两位小数如何输出
    
    ```js
    let x = 1.234567;
    let s = `${x.toFixed(2)}`;
    ```
    
- 练习
    - 控制台输出HelloWorld
    
    ```js
    console.log("Hello World");
    ```
    
    - 输出两个数字的和
    
    ```js
    function main(){
        run.addEventListener('click', function(){
           let[a, b] = input.value.split(' ');
           a = parseInt(a), b = parseInt(b);
           output.innerHTML = a + b;
        });
    }
    ```
    
    - 输入一个小数，返回向零取整之后的结果
    
    ```js
    function main(){
        run.addEventListener('click', function(){
           let t = parseFloat(input.value);
           output.innerHTML = parseInt(t);
        });
    }
    ```
    
    - 输出菱形
    
    ```js
    function main(){
        run.addEventListener('click', function(){
            let s = '';
            s += '  *\n';
            s += ' ***\n';
            s += '*****\n';
            s += ' ***\n';
            s += '  *\n';
           output.innerHTML = s;
        });
    }
    ```
    

## 判断语句

- Note
    - JavaScript中的if-else语句与C++、Python、Java中类似
      
        ```js
        let a = 99;
            if(a < 50)
               output.innerHTML = a;
            else
               output.innerHTML = a - 10;
        ```
        
    - JavaScript中的逻辑运算符也与C++、Java中类似
        - &&表示与
        - ||表示或
        - !表示非
- Practice：判断一个年份是否为闰年

```js
run.addEventListener('click', function(){
let temp = parseInt(input.value);
if(temp % 100 !== 0 && temp % 4 === 0 || temp % 400 === 0) output.innerHTML = 'Yes';
else output.innerHTML = 'No';
});
```

## 循环语句

```js
function main() {
  run.addEventListener("click", function () {
    let n = parseInt(input.value);
    let a = 1, b = 1;
    for(let i = 1; i < n; i ++ )
    {
        let c = a + b;
        a = b;
        b = c;
    }
    output.innerHTML = a;
  });
}
```

## 对象

- 类型

```js
let person = {
  name: "fanfan",
  age: 18,
  money: 100,
  friends: {
    name: "Alice",
    age: 18,
  },
  add_money: function (x) {
    this.money += x; // this 指的是拥有该function函数的主人，即person
  },
};
```

- 使用

```js
person.name;
person['age'];
person.add_money(5);
person['add_money'](5);
```

## 数组

Note：类似于C++中的数组，但是数组中的元素类型可以不同

- 定义

```js
let a = [
  1,
  2,
  3,
  "fanfan",
  ["haha", "heihei"],
  { name: "Alice" },
  function () {
    console.log(this);
  },
];
```

- 使用

```js
function main()
{
  console.log(a);
  console.log(a[0]);
  console.log(a[3][0]);
  console.log(a[4][0]);
  console.log(a[5].name);
  a[6]();
}
```

- 数组常用函数
    - 属性length：返回数组长度。注意length是属性，不是函数，因此调用的时候不要加()
    - 函数push()：向数组末尾添加元素
    - 函数pop()：删除数组末尾的元素
    - 函数splice(a, b)：删除从a开始的b个元素
    - 函数sort()：将整个数组从小到大排序
    - 自定义比较函数：array.sort(cmp)
        - 函数cmp输入两个需要比较的元素，返回一个实数，负数表示第一个参数小于第二个参数，0表示相等，正数表示大于。

```js
console.log(a.length);
a.push("Alice");
a.pop();
a.splice(0, 3);
a.sort();
// 自定义函数排序
a.sort(function (a, b) {
  return b - a;
});
```

## 函数

Note：函数是用对象来实现的，函数也C++中的函数类似

```js
function add(a, b) {
    return a + b;
}

let add = function (a, b) {
    return a + b;
}

let add = (a, b) => {
    return a + b;
}
```

Add：如果未定义返回值，则返回undefined

## 类

与C++中的Class类似。但是不存在私有成员，只能存在一个构造函数

- 定义

```js
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
  toString()
  {
    return `(${this.x}, ${this.y})`;
  }
}

let p = new Point(1, 2);
console.log(p.toString());
```

- 继承

```js
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
  toString() {
    return `(${this.x}, ${this.y})`;
  }
}

class ColorPoint extends Point {
  constructor(x, y, color) {
    super(x, y);        // 父类构造函数
    this.color = color;
  }
  toString() {
    return `${this.color}, ${super.toString()}`; // 这里的super可以看成是一个指向父类的实例的指针
  }
}

function main() {
  let cp = new ColorPoint(1, 2, "red");
  console.log(cp.toString());
}

export { main };
```

- 静态成员函数的访问

```js
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }
  toString() {
    return `(${this.x}, ${this.y})`;
  }

  static printClassName()
  {
    console.log("Point");
  }
}

function main() {
  let p = new Point(1, 2);
  Point.printClassName();
}

export { main };
```

- 静态成员变量的定义

```js
class Point {
  constructor(x, y) {
    this.x = x;
    this.y = y;
    Point.cnt ++ ;
  }
  toString() {
    return `(${this.x}, ${this.y})`;
  }

  static printClassName()
  {
    console.log("Point");
  }
}

Point.cnt = 0;

function main() {
 for(let i = 1; i <= 10; i ++ ) new Point(1, 2);
 console.log(Point.cnt);
}

export { main };
```

Add：静态成员函数可以被继承，静态成员变量可以被子类调用（也相当于继承）

## 事件

JavaScript的代码一般通过事件触发

可以通过addEventListener函数为元素绑定事件的触发函数

- 鼠标
    - click：鼠标左键点击
    - dblclick：鼠标左键双击
    - contextmenu：鼠标右键点击
    - mousedown：鼠标按下，包括左键、滚轮、右键
        - event.button：0表示左键，1表示中键，2表示右键
    - mouseup：鼠标弹起，包括左键、滚轮、右键
        - event.button：0表示左键，1表示中键，2表示右键
    
    ```js
    let btn = document.querySelector("button");
    function main() {
      btn.addEventListener('click', function (event) {
        console.log(event.type);
      });
      btn.addEventListener('dbclick', function (event) {
        console.log(event.type);
      });
      btn.addEventListener('contextmenu', function (event) {
        console.log(event.type);
      });
      btn.addEventListener('mousedown', function (event) {
        console.log(event.type);
      });
      btn.addEventListener('mouseup', function (event) {
        console.log(event.type);
      });
    };
    
    export { main };
    ```
    
- 键盘
    - keydown：某个键是否被按住，事件会连续触发
        - event.code：返回按的是哪个键
        - event.altKey、event.ctrlKey、event.shiftKey分别表示是否同时按下了alt、ctrl、shift键。
    - keyup：某个按键是否被释放
        - event常用属性同上
    - keypress：紧跟在keydown事件后触发，只有按下字符键时触发。适用于判定用户输入的字符。、
        - event常用属性同上
    - Add：shiftkey、altkey、 ctrlkey指的是当前是否在按这几个键
    
    ```js
    let btn = document.querySelector("button");
    function main() {
      // btn.addEventListener('keydown', function (event) {
      //   console.log(event.key, event.shiftKey,event.ctrlKey);
      // });
      btn.addEventListener('keypress', function (event) {
        console.log(event.key);
      });
    };
    
    export { main };
    ```
    
- 表单
    - focus：聚焦某个元素
    - blur：取消聚焦某个元素
    - change：某个元素的内容发生了改变
    
    ```js
    let input = document.querySelector("input");
    function main() {
      input.addEventListener('focus', function(event){
        console.log("Focus");
      });
      input.addEventListener('blur', function(event){
        console.log("Blur");
      });
      input.addEventListener('change', function(event){
        console.log("Change");
      });
      input.addEventListener('focus', function(event){
        console.log(event);
      });
    };
    
    export { main };
    ```
    
- 窗口
    - resize：当窗口大小放生变化
    - scroll：滚动指定的元素
    - load：当元素被加载完成
    
    ```js
    let input = document.querySelector("input");
    function main() {
      window.addEventListener("resize", function (event) {
        console.log(event.type);
      });
      window.addEventListener("scroll", function (event) {
        console.log(event.type);
      });
      window.addEventListener("load", function (event) {
        console.log(event.type);
      });
    }
    
    export { main };
    ```
    

## 常用库

### jQuery

- 基本用法
  
    ```js
    let div = document.querySelector('div');
    let $div = $('div');
    ```
    
- 选着器（类似于CSS选择器）
  
    ```js
    $('div');
    $('.big-div');
    $('div > p')
    ```
    
- 事件
  
    ```js
    // 绑定和取消
    function main(){
      // 选择div
      let $div = $('div');
      // 绑定点击事件
      $div.on("click", function(event){
        console.log(event.type);
        $div.off('click');   // 解绑
      });
    }
    ```
    
    ```js
    // 给相同事件起别名
    function main(){
      let $div = $('div');
      $div.on("click.01", function(){
        console.log('click.01');
        $div.off('click.02');
      });
      $div.on("click.02", function(){
        console.log('click.02');
      });
    }
    ```
    
    ```js
    // return false
    function main(){
      let $div = $('div');
      $div.on("click", function(e){
        console.log('click div');
      });
      $('a').on('click', function(e){
        return false;
      });
    }
    ```
    
    - 在事件触发的函数中的return false等价于同时执行
        - e.stopPropagation()：阻止事件向上传递
          
            ```js
            function main(){
              let $div = $('div');
              $div.on("click", function(e){
                console.log('click div');
              });
              $('a').on('click', function(e){
                e.stopPropagation();
              });
            }
            ```
            
        - e.preventDefault()：阻止事件的默认行为
          
            ```js
            function main(){
              let $div = $('div');
              $div.on("click", function(e){
                console.log('click div');
              });
              $('a').on('click', function(e){
                e.preventDefault()
              });
            }
            ```
    
- 元素的隐藏、展现
    - $A.hide()：隐藏，可以添加参数，表示消失时间
    - $A.show()：展现，可以添加参数，表示出现时间
    - $A.fadeOut()：慢慢消失，可以添加参数，表示消失时间
    - $A.fadeIn()：慢慢出现，可以添加参数，表示出现时间
    
    ```js
    function main(){
      let $div = $('div');
      let $show = $('#button-show');
      let $hide = $('#button-hide');
      $show.click(() => {
        $div.show(2000);
      });
      $hide.on('click', function(){
        $div.hide(2000);
      });
    }
    ```
    
    ```js
    function main(){
      let $div = $('div');
      let $show = $('#button-show');
      let $hide = $('#button-hide');
      $show.click(() => {
        $div.fadeIn(2000);
      });
      $hide.on('click', function(){
        $div.fadeOut(2000);
      });
    }
    ```
    
- 元素的添加、删除
    - $('<div class="mydiv"><span>Hello World</span></div>')：构造一个jQuery对象
    - $A.append($B)：将$B添加到$A的末尾
    - $A.prepend($B)：将$B添加到$A的开头
    - $A.remove()：删除元素$A
    - $A.empty()：清空元素$A的所有儿子
    
    ```js
    function main(){
      let $div = $('div');
      let $a = $('<a href="#" target = "_blank">A</a>');
      $div.append($a);
      let $b = $('<a href="#" target = "_blank">B</a>');
      $div.prepend($b);
    }
    ```
    
- 对类的操作
    - $A.addClass(class_name)：添加某个类（**无需加点**）
    - $A.removeClass(class_name)：删除某个类
    - $A.hasClass(class_name)：判断某个类是否存在
    
    ```js
    function main(){
      let $div = $('div');
      $div.on('click', () => {
        $div.addClass('my-div');
        $div.removeClass('my-div');
        console.log($div.hasClass('my-div'));
      });
    }
    ```
    
- 对CSS的操作
    - $("div").css("background-color")：获取某个CSS的属性
    - $("div").css("background-color","yellow")：设置某个CSS的属性
    - 同时设置多个CSS的属性
    
    ```js
    function main(){
      let $div = $('div');
      $div.click(() => {
        $div.css({
          width : "200px",
          height : "200px",
          "background" : "orange"
        });
      });
    }
    ```
    
- 对标签属性的操作
    - $('div').attr('id')：获取属性
    - $('div').attr('id', 'ID')：设置属性
    
    ```js
    function main(){
      let $div = $('div');
      $div.click(() => {
        console.log($div.attr('id'));
        $div.attr('id', '2');
        console.log($div.attr('id'));
      });
    }
    ```
    
- 对HTML内容、文本的操作（不需要背每个标签该用哪种，用到的时候Google或者百度即可）
    - $A.html()：获取、修改HTML内容
    - $A.text()：获取、修改文本信息
    - $A.val()：获取、修改文本的值
- 查找
    - $(selector).parent(filter)：查找父元素
    - $(selector).parents(filter)：查找所有祖先元素
    - $(selector).children(filter)：在所有子元素中查找
    - $(selector).find(filter)：在所有后代元素中查找
- ajax（在不刷新整个页面的请路况下，只从服务端获取某些数据）
    - GET方法
      
        ```js
        $.ajax({
            url: url,
            type: "GET",
            data: {
            },
            dataType: "json",
            success: function (resp) {
        
            },
        });
        ```
        
    - POST方法
      
        ```js
        $.ajax({
            url: url,
            type: "POST",
            data: {
            },
            dataType: "json",
            success: function (resp) {
        
            },
        });
        ```
        

### setTimeout与setInterval

- setTimeout(func, delay)
  
    ```js
    function main(){
      let $div = $('div');
      $div.click(function(){
        setTimeout(function(){
          console.log('Hello World');
        }, 2000);
      });
    }
    ```
    
- setInterval(func, delay)
  
    ```js
    function main(){
      let $div = $('div');
      $div.click(function(){
        setInterval(function(){
          console.log('Hello World');
        }, 2000);
      });
    }
    ```
    
- clearTimeout
  
    ```js
    function main(){
      let $div = $('div');
      let func_id;
      $div.click(function(){
        if(func_id) return false;
        func_id = setInterval(function(){
          console.log('Hello World');
        }, 500);
      });
      $div.dblclick(() => {
        console.log("dbclick");
        clearTimeout(func_id);
      });
    }
    ```
    

### requestAnimationFrame

```js
function main() {
  let step = () => {
    $("div").width($("div").width() + 1);
    $("div").height($("div").height() + 1);
    requestAnimationFrame(step);
  };
  requestAnimationFrame(step);
}
```

- 与setTimeout和setInterval的区别：
    - requestAnimationFrame渲染动画的效果更好，性能更加。
    - 该函数可以保证每两次调用之间的时间间隔相同，但setTimeout与setInterval不能保证这点
    - setTmeout两次调用之间的间隔包含回调函数的执行时间；setInterval只能保证按固定时间间隔将回调函数压入栈中，但具体的执行时间间隔仍然受回调函数的执行时间影响。
    - 当页面在后台时，因为页面不再渲染，因此requestAnimationFrame不再执行。但setTimeout与setInterval函数会继续执行。

### Map与Set

- Map
    - 定义和常用函数
    
    ```js
    function main() {
      let map = new Map();
      map.set('name', 'fanfan');
      map.set('age', 18);
      console.log(map);
      console.log(map.get('name'));
      console.log(map.size);
      console.log(map.has('name'));
      map.delete('age');
      console.log(map);
      map.clear();
      console.log(map.size);
    }
    export { main };
    ```
    
    - 遍历
      
        ```js
        // For循环
        function main() {
            let map = new Map();
            map.set('name', 'fanfan');
            map.set('age', 18);
            for(let [key, value] of map)
            {
              console.log(key, value);
            }
          }
        // ForEach
        function main() {
          let map = new Map();
          map.set('name', 'fanfan');
          map.set('age', 18);
          map.forEach(function(value, key){
            console.log(key, value);
          });
        }
        ```
    
- Set
    - 定义和常用函数
      
        ```js
        function main() {
          let set = new Set();
          set.add("fanfan");
          set.add(17);
          console.log(set);
          console.log(set.size);
          console.log(set.has("fanfan"));
          set.delete(17);
          console.log(set);
          set.clear();
          console.log(set);
        }
        ```
        
    - 遍历
      
        ```js
        // For 循环
        function main() {
          let set = new Set();
          set.add("fanfan");
          set.add(17);
          for (let i of set) {
            console.log(i);
          }
        }
        // ForEach
        function main() {
          let set = new Set();
          set.add("fanfan");
          set.add(17);
          set.forEach(key => {
            console.log(key);
          });
        }
        ```
        

### localStorage

可以在用户的浏览器上存储键值对

- setItem(key, value)：插入
- getItem(key)：查找
- removeItem(key)：删除
- clear()：清空

```js
function main() {
  localStorage.setItem('name', 'fanfan');
  console.log(localStorage.getItem('name'));
  localStorage.removeItem('name');
}
```

### JSON

- JSON.parse()：将字符串解析成对象
- JSON.stringify()：将对象转化为字符串

```js
function main() {
  let d = {
    name: "fanfan",
    age: 18,
  };
  console.log(d);
  let t = JSON.stringify(d);
  console.log(t);
  t = JSON.parse(t);
  console.log(t);
}
```

### 日期

返回值为整数的API，数值为1970-1-1 00:00:00 UTC（世界标准时间）到某个时刻所经过的毫秒数

- Date.now()：返回现在时刻
- *Date*.parse("2022-07-07T15:30:00.000+08:00")

```js
function main() {
  console.log(Date.now());
  console.log(Date.parse("2022-07-07T15:30:00.000+08:00"))
}
```

与Date对象的实例相关的API

- new Date()：返回现在时刻。
- new Date("2022-04-15T15:30:00.000+08:00")：返回北京时间2022年4月15日 15:30:00的时刻。
- 两个Date对象实例的差值为毫秒数
- getDay()：返回星期，0表示星期日，1-6表示星期一至星期六
- getDate()：返回日，数值为1-31
- getMonth()：返回月，数值为0-11
- getFullYear()：返回年份
- getHours()：返回小时
- getMinutes()：返回分钟
- getSeconds()：返回秒
- getMilliseconds()：返回毫秒

### WebSocket

与服务器建立全双工连接

- new WebSocket('ws://localhost:8080');：建立ws连接。
- send()：向服务器端发送一个字符串。一般用JSON将传入的对象序列化为字符串。
- onopen：类似于onclick，当连接建立时触发。
- onmessage：当从服务器端接收到消息时触发。
- close()：关闭连接。
- onclose：当连接关闭后触发

### Window

- window.open("[https://www.acwing.com](https://www.acwing.com/)")在新标签栏中打开页面。
- location.reload()刷新页面。
- location.href = "[https://www.acwing.com](https://www.acwing.com/)"：在当前标签栏中打开页面。

### Canvas

简介：Canvas是借助js来画图的工具， 它是html的一个标签

文档：[https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial](https://developer.mozilla.org/zh-CN/docs/Web/API/Canvas_API/Tutorial)

例子：

- 创建画布，并使其可以聚焦
  
    ```html
    <canvas width="1280" height="720" tabindex=0></canvas>
    ```
    
- 使用jquary索引canvas标签
  
    ```js
    let $canvas = $("canvas");
    // jquary 库索引canvas时，不可以直接使用$canvas.getContext('2d')
    let ctx = $canvas[0].getContext("2d"); // ctx == context
    ```
    
- 填充矩形
  
    ```js
    ctx.fillStyle = "rgb(200,0,0)";
    // x, y, width, height
    ctx.fillRect(0, 0, 100, 100);
    ```
    
- 清除矩形
  
    ```js
    ctx.clearRect(50, 50, 50, 50);
    ```
    
- 绘制边框
  
    ```js
    ctx.strokeRect(60, 60, 30, 30);
    ```