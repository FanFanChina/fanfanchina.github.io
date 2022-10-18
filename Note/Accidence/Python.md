# `环境搭建`

**[Python](https://www.aliyundrive.com/s/n4xSTi7TAhT) 提取码：`ed8m`**

# `基础语法`

## `注释`

```python
#		单行注释

'''
        多行注释
'''
```

------

## `Hello World`

```python
print("Hello World")
```

------

## `输出`

```python
#1
a=10
print("a=",a)#print()自动换行
#2
age=18
print("我的年龄是%d岁"%age)
#3
s="China"
print("我的年龄是%d岁、我的国籍是%s"%(age,s))
#4
print("我的名字是%s、我来自%s"%("非洲小白孩","非洲"))
'''
    %(替换对象1,替换对象2...)
'''
#5
print("你好！%s，我来自%s，我叫%s，今年%d岁"%("HAQI","China","FanFan",18))
#6
print("www","baidu","com",sep=".")#Separate隔开、用 . 隔开
#7
print("hello ",end="")#为""时不换行
print("world")
#8
print("-"*30)
```

------

## `输入`

```python
#1
password = int(input("please input password："))#"  "内为提示语
print("The password is",password)
print(type(password))
#输入的内容默认的类别是字符串or数字
#2
a = int('10231')
print(type(a))
```

------

## `随机数`

```python
import random
a = random.randint(1,10)
print(a)
```

------

## `if判断语句`

```python
#1
a = 100
b = 101
if a>b:
    print('a > b')#必须要有缩进，且同一范围内必须对齐
else :
    print("a < b")

#2
score = 90
if score >= 90:
    print("优秀")
elif score>70 and score<90:
    print("一般")
else:
    print("不及格")
```

------

## `for循环语句`

```python
#1
for i in range(5):
    print(i,end=" ")
print("")
for i in range(1,5):
    print(i,end=" ")
print("")
for i in range(1,6,2):
    print(i,end=" ")
print("")
#1
for c in "China":
    print(c,end="")
print("")
for d in ["adas","dsadad","sdawd"]:
    print(d,end=" ")
print("")
a = ["dada","dawd","dwad"]
for i in a:
    print(i,end=" ")
print("")
a = ["dada","dawd","dwad"]
for i in range(1,len(a)):
    print("下标:",i,a[i])
print("")
#3
i=0
while i<5:
    print(i)
    i+=2
sum = 0
m = 100
while m:
    sum+=m
    m-=1
else:
    print("求和完毕1-100的和为：",sum)
#4
for i in "Room":
    if i=="o":
        pass
    else:
        print(i)
```

------

## `九九乘法表`

```python
for i in range(1,10):
    for j in range(1,10):
        if j<=i:
            print(i,"*",j,"=",i*j,end="\t")
    print("")

i = j = 1
while i<=9:
    j=1
    while j<=9:
        if j<=i:
             print(i,"*",j,"=",i*j,end="\t")
        j+=1
    i+=1
    print("")
```

------

## `字符串`

```python
#1
word = 'Hello'
sentence = "这是一个句子"
paragraph = '''  嘿嘿
        这是一个段落
        哈哈哈
'''
print(word)
print(sentence)
print(paragraph)

#2
str1 = "I'm a student"#双引号内单引号失去作用
print(str1)

#str2 = 'I'm a student'会报错
str2 = 'I\'m a student'#标识该 ' 无索引字符串地作用
print(str2)

#str3 = "Jack said "I like you""#会报错
str3 = "Jack said \"I like you\""
print(str3)
str4 ='Jack said "I like you"'#单引号内双引号失去作用
print(str4)

#3
string = "China"
print(string[0])
print(string[0:3])#默认跨度为1
print(string[0:3:1])
print(string[0:4:2])#跨度为2
print(string[:3])#第三单元之前的(不包含3)
print(string[3:])#第三单元后的（包含3）
#区间访问时左闭右开！！！

#4
s = "你好"
print(s+"，成都！")#“+”表示字符串相连接
print(s*3)
#5
print("hello\nworld")
print(r"hello\nworld")#r使转义字符失效
```

------

## `运算符`

```python
# ** 乘方运算
a = 2
b = 5
print(a ** b) # a的b次方
```



## `列表`

### `定义列表`

```python
#定义一个空的列表
nameList = []
#定义非空列表
nameList = ["小张","小王","小李"]
print(nameList[0])
#混合类型
nameList = [1,"China",89.2]
print(type(nameList[0]))
print(type(nameList[1]))
print(type(nameList[2]))
print("")
```

### `遍历列表`

```python
#遍历
print("开始For循环遍历nameList")
nameList = ["小张","小王","小李"]
for name in nameList:
    print(name)
print("开始While循环遍历nameList")
i = 0 
while i<len(nameList):
    print(nameList[i])
    i+=1
```

### `增加元素`

```python
#增加单个元素
nameList = ["小张","小王","小李"]
print("------增加前------")
for name in nameList:
    print(name,end = " ")
print("")
nameTemp = input("请输入add的元素：")
nameList.append(nameTemp)
print("------增加后------")
for name in nameList:
    print(name,end = " ")
print("")
PYTHON
#增加一个是列表的元素
a = [1,2]
b = [3,4]
a.append(b)
print(a)
PYTHON
#拓展列表（合并列表）
a = [1,2]
b = [3,4]
a.extend(b)
print(a)
PYTHON
#插入元素（原有元素被挤到下一位）
a = [1,2]
a.insert(1,"China")#1位置插入 China
print(a)
```

### `删除元素`

```python
#删除指定位置元素
a = [1,"China",3,4]
del a[2]
print(a)
PYTHON
#弹出尾部元素
a = [1,"China",3,4]
a.pop()
print(a)
PYTHON
#删除指定内容的元素
a = [1,"China",3,4]
a.remove(1)
print(a)
PYTHON
#clear:清空列表
nameList = ["小张","小王","小李"]
print("-----删除前------")
for name in nameList:
    print(name,end = " ")
print("")
nameList.extend(2)
print("------删除后------")
for name in nameList:
    print(name,end = " ")
print("")
```

### `修改元素`

```python
#指定下标赋值即可
a = [1,"China",3,4]
a[1] = 2
print(a)
```

### `查询元素`

```python
#注意数据类型有数字和字符串
a = [1,"China",3,4]
temp = input("请输入您要查找的数据:")
if temp in a:
    print(temp,"存在")
elif int(temp) in a:
    print(temp,"存在")
else:
    print(temp,"不存在")
```
```python
#输出列表中某一元素的下标
myList = ['a','b','c','d']
print(myList.index('a'))
#我们也可以精确范围
myList = ['a','b','c','d']
print(myList.index('a',0,2))
#如果找不到元素就会报错
myList = ['a','b','c','d']
print(myList.index('a',1,2))
#ValueError: 'a' is not in list
```
```python
#统计元素个数
myList = ['a','b','c','d','a']
print(myList.count('a'))
```
```python
#反转和排序
myList = ['a','b','c','d','a']
myList.reverse()
print(myList)
myList.sort()
print(myList)
myList.sort(reverse=True)#排序后反转（降序）
print(myList)
#办公室分配
import random
offices = [[],[],[]]
names = ["A","B","C","D","E","F","G","H","I"]
for name in names:
    index = random.randint(0,2)
    offices[index].append(name)
i = 0
while i<3:
    print("%d号办公室有%d人，分别为 "%(i+1,len(offices[i])),end="")
    for name in offices[i]:
        print(name,end=" ")
    print("")
    i+=1
```
## `元组`
### `定义元组`
```python
tup = ()
print(type(tup))
tup = (50)#等价于tup = 50
print(type(tup))#<class 'int'>
tup = (50,)
print(type(tup))#<class 'tuple'>
```

### `元组的相关操作`

```python
#可遍历，查找，整体删除
tup =  (1,2,3,4,5)
for i in tup:
    print(i)
print(tup[3])
print(tup[-1])
if 4 in tup:
    print("Yes")
tupx =tup+tup
print(tupx)
tupx.sort()#AttributeError: 'tuple' object has no attribute 
'sort'
print(tupx)
tup =  (1,2,3,4,5)
del tup
print(tup)#NameError: name 'tup' is not defined
```

## `字典`

### `定义`

```python
d = {"name":"吴彦祖","age":18}#键+值
```

### `访问和查找`

```python
#访问
d = {"name":"吴彦祖","age":18}
print(d["name"])
print(d["age"])
print(d["geand"])#键不存在时直接访问会 KeyError: 'geand'
#判断某个key是否存在
print(d.get("grand"))#显示：None
print(d.get("grand",0))#显示：0（初始化为0）
```

### `增加键值对`

```python
key = input("请输入新的键：")
p = input("请输入新键的值：")
d[key] = p
print(d[key])
```

### `删除键值对`

```python
#del
d = {"name":"吴彦祖","age":18}
del d["name"]
print(d["name"])#KeyError: 'name'
#clear
d = {"name":"吴彦祖","age":18}
d.clear()
print(d)#打印结果为 {}
```

### `修改键值对`

```python
d = {"name":"吴彦祖","age":18}
d["name"]="哈哈"
print(d)
```

### `查找与遍历键值对`

```python
d = {"name":"吴彦祖","age":18}
print(d.keys())#['name', 'age']
print(d.values())#['吴彦祖', 18]
print(d.items())#[('name', '吴彦祖'), ('age', 18)]、每一项是一个元组
#遍历
d = {"name":"吴彦祖","age":18}
for key in d.keys():
    print(key)
for value in d.values():
    print(value)
for key,value in d.items():
    print("key=%s value=%s"%(key,value))
```

**在列表中也有类似的表达：**

```python
names = ["A","B","C","D","E","F","G","H","I"]
for i,x in enumerate(names):#对names枚举
    print(i,x)
# 1 B
# 2 C
# 3 D
# 4 E
# 5 F
# 6 G
# 7 H
# 8 I
```

## `集合`

```python

#去重
myList = [1,2,2,3,4]
s = set(myList)
print(s)
```

# `网络爬虫`

## `Request库的使用`

### `基本语法`

```python
import requests
url = 'http://www.santostang.com/'
r = requests.get(url) 
print(r.encoding)       #编码格式
print(r.status_code)    #状态码（200==成功）
print(r.text)           #内容
```

### `url定制`
```python
import requests
url = 'http://www.santostang.com/'
keyDict = {'k1':'v1','k2':'v2'}
r = requests.get(url,params=keyDict)
print(r.url)
print(r.text)
```

### `headers定制`

```python
import requests
url = 'http://www.santostang.com/'
headers={
'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36 Edg/96.0.1054.62' 
}
r = requests.get(url,headers=headers)
print(r.status_code)
```

### `POST请求`

```python
import requests
url = 'http://www.santostang.com/'
submitData = {'k1':'v1','k2':'v2'}
r = requests.post(url,data = submitData)
print(r.status_code)
print(r.text)
#注意是data！！！
```

### `DouBan`

```python
import requests
from bs4 import BeautifulSoup
baseUrl = 'https://movie.douban.com/top250?start='
headers = {
    'User-Agent':'Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36 Edg/96.0.1054.62',
    'Host':'movie.douban.com'
}
movieList = []
for i in range(0,10):
    link = baseUrl+str(i*25)
    r = requests.get(link,headers=headers)
    print('The status of page',str(i+0),'is',r.status_code)
    soup = BeautifulSoup(r.text,'lxml')
    divList = soup.find_all('div',class_='hd')
    for t in divList:   
        movie = t.a.span.text.strip()
        movieList.append(movie)
print(movieList)
```



