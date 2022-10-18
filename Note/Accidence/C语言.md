## `引言`

**本文主要记录一些 C 语言的细节问题**

------

## `EOF`

**对于 `scanf("%d%d", &a, &b);` 而言**
**如果 `a` 和 `b` 都被`成功读入`，那么 scanf 的`返回值`就是 `2`**
**如果`只有a` 被成功读入，返回值为 `1`**
**如果 a 和 b `都未被`成功读入，返回值为 `0`**
**如果遇到`错误`或遇到 `end of file`，返回值为 `EOF`，且返回值为 `int` 型**
**当`读文件`操作时，遇到`文件结束位置`或`读数据出错`均会返回 `EOF`**
**C 语言中所有的输入输出操作均是按`读文件`的思想来设计的，或者说是文件操作的一种`特例`，如 getchar（）就是 fgetc (stdin) 的一个`宏`**

------

## `文件操作`

**[大佬的博客 - CSDN](http://topurl.cn/7jq)**

------

## `内存分配`

```c
int* f()
{
	int *p = malloc(100);
	return p;
}
```

**malloc 为`动态分配`，p 为`静态分配`（用变量名）**
**`f（）`函数运行`结束`后，malloc 分配的 `100字节的空间`依旧存在，而`变量p` 则不存在了（编译器可能会保存一次）**

------

## `字符串`

**在 `C语言`中这样会报错，但在 `Java` 中可以这么用**
![一个图](https://pic.imgdb.cn/item/6114f65c5132923bf8ea5470.jpg)

**`C语言`的正确写法**

```c
#include<stdio.h>
#include<string.h>
int main()
{
	char ch[20] = "China";
	strcpy(ch, "Lisi");
	printf("%s", ch);
	return 0;
}
```

------

## `结构体与指针`

```c
struct note
{
	int date;
	char name[20];
};
struct note Std;
printf("%d",std.date);
struct note *p=&Std;
printf("%d",p->date);
//p->date == (*p).date == Std.date
```

------

## `无名结构体`

**一、编译器对无名结构体的处理是随机生成一个不重复的变量名**

**二、无类型名的结构体变量在声明结构体时就得定义（后续去用的话不知道名字）**

**三、因为名字是随机的，所以不可以相互赋值，例子如下：**

```c
struct{
  int x;
}a;
struct{
  int x;
}b;
b = a; //报 incompatible type error
```

**四、结构体的指针也无法使用，例子如下：**

```c
#include<stdio.h>
struct
{
	int x;
}a, * pa;
void main()
{
	pa->x = 1; //报 pa 是 NULL
	printf("%d", pa->x);
}
```

**五、用 typedef 处理后可以正常使用，例子如下：**

```c
#include<stdio.h>
typedef struct
{
	int x;
}a, * pa;
void main()
{
	a b;
	pa l;
	l = &b;
	b.x = 1;
	printf("%d", l->x);
}
```

**六、对于多个内部相同属性的结构体可以用无名结构体方式处理，更方便。**

------

## `scanf和gets`

**scanf 遇到`空格`停止读取，gets 遇到`回车`停止读取**

------

## `字符串截取函数`

```c
#include<stdio.h>
#include<malloc.h>
#define MAX 100
//p：待截取的字符串头指针
//s：截取的起始位点
//n：截取长度
char* Intercept_String(char *p, int s, int n)
{
	char* h; int j = 0;
	h = (char*)malloc((n + 1) * sizeof(char));
	for (int i = s; i < n + s; i++)
	{
		*(h+j)= *(p+i);
		j++;
	}
	*(h + j) = '\0';
    return h;
}
int main()
{
	char ch[MAX];
	gets_s(ch);
	printf("%s", Intercept_String(ch, 2, 3));
	return 0;
}
```

------

## `0x3f3f3f3f`

**0x3f3f3f3f 的十进制是 1061109567，是 109 级别的，而一般场合下的数据都是小于 109 的，所以它可以作为`无穷大`使用而不致出现数据大于无穷大的情形**

## `memset`
**[相关链接](https://blog.csdn.net/xp178171640/article/details/115751021?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522163212541216780269835428%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=163212541216780269835428&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-2-115751021.pc_search_result_hbase_insert&utm_term=c%2B%2Bmemset&spm=1018.2226.3001.4187)**
**memset 实现原理是根据`字节`来设置的**
**对于int而言有四个字节我们这样memset**
```c++
memset(map, 0x3f, sizeof(map));
```

## `随机数`

**1.头文件**

stdlib.h

**2.设置随机数种子(Set Rand)**

srand(unsigned int(time(NULL)))

**3.Rand函数**

rand()%100【0-99】

rand()%100+1【1-100】

**4.实例：洗牌**

```c
#include<stdlib.h>
#include<iostream>
using namespace std;
int main()
{
	int a[10], n;
	cin >> n;
	for (int i = 1; i <= n; i++)
	{
		cin >> a[i];
		srand((unsigned int)time(NULL));
		int r = rand()%i+1;
		int t;
		t = a[r]; a[r] = a[i]; a[i] = t;
	}
	for (int i = 1; i <= n; i++)
		cout << a[i]<<' ';
}
```

## `New用法`



## `异或的用法`

```c
#include<stdio.h>
int main()
{
	int a, b;
	scanf_s("%d%d", &a, &b);
	a = a ^ b;
	b = a ^ b;
	a = a ^ b;
	printf("%d %d", a, b);
	return 0;
}
```

## `printf补零输出`

```c
#include<stdio.h>
int main()
{
	int a = 1;
	//宽度已知
	printf("%02d\n", a);
	//宽度未知
	int b = 2;
	int l = 3; //宽度
	printf("%0*d",l,b);
	return 0;
}
```

