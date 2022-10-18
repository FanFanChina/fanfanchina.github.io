# `输入输出`

## `Hello World`

```cpp
#include<iostream>					//i:输入o:输出stream:流
using namespace std;				//使用标准命名空间
int main()
{
	cout << "Hello World" << endl;	//endl结束输入并回车
	cout << endl;					//一个 << 对应一个输出内容
	return 0;
}
```
***
## `IO(整数)`
```cpp
#include<iostream>					//i:输入o:输出stream:流
using namespace std;				//使用标准命名空间
int main()
{
	int a,b;
	cin >> a >> b;
	cout << a <<' '<< b;
	return 0;
}
```
***
## `IO(字符)`
```cpp
#include<iostream>					//i:输入o:输出stream:流
using namespace std;				//使用标准命名空间
int main()
{
	char a,b;
	cin >> a >> b;					//输入时加不加空格都可以(空格不会读入)
	cout << a <<' '<< b;
	return 0;
}
```
***
## `IO(字符串)`
```cpp
#include<iostream>					//i:输入o:输出stream:流
using namespace std;				//使用标准命名空间
int main()
{
	string ch1,ch2;
	cin >> ch1 >> ch2;					
	cout << ch1 <<' '<< ch2;
	return 0;
}
//cin遇到空格、Tab、回车时均会停止读取
```
***
## `IO(混合型)`
```cpp
#include<iostream>					//i:输入o:输出stream:流
using namespace std;				//使用标准命名空间
int main()
{
	string ch;
	double m;
	cin >> ch >> m;					
	cout << ch << ' ' << m << endl;
	return 0;
}
```
***
## `精度控制`
```cpp
#include<iostream>					//i:输入o:输出stream:流
#include<iomanip>					//格式控制！！！
using namespace std;				//使用标准命名空间
int main()
{
	double PI=3.1415926535897;
	cout << PI << endl;				//cout默认输出6位(包含整数位)
	cout << setprecision(10) << PI;	//设置精度为 10(输出10位)
	return 0;
}
```
***
## `输出当前精度`
```cpp
//cout.precision()当前精度大小
#include<iostream>					//i:输入o:输出stream:流
#include<iomanip>					//格式控制！！！
using namespace std;				//使用标准命名空间
int main()
{
	double PI=3.1415926535897;
	cout << PI << endl;						//cout默认输出6位(包含整数位)
	cout << cout.precision()<<endl;			//精度为 6
	cout << setprecision(10) << PI<<endl;	//设置精度为 10(输出10位)
	cout << cout.precision();				//精度为 10
	return 0;
}
```
***
## `设置小数点后精度(定点输出)`
```cpp
//cout.precision()当前精度大小
#include<iostream>					//i:输入o:输出stream:流
#include<iomanip>					//格式控制！！！
using namespace std;				//使用标准命名空间
int main()
{
	double PI = 3.1415926535897;
	cout << fixed;							//定点输出(即小数点前固定不变)
	cout << PI << endl;						//cout默认输出6位
	cout << cout.precision() << endl;		//精度为 6
	cout << setprecision(10) << PI << endl;	//设置精度为 10
	cout << cout.precision();				//精度为 10
	return 0;
}
```
***
## `设置域宽`
```cpp
//cout.width()当前域宽的大小
//setfill()设置填充值，作用效果=1
//setw()设置域宽(默认为0、右对齐,作用效果=1)
#include<iostream>					//i:输入o:输出stream:流
#include<iomanip>					//格式控制！！！
using namespace std;				//使用标准命名空间
int main()
{
	double PI=3.14;
	cout << cout.width()<<endl;						//输出当前域宽
	cout << PI<<endl;								//输出PI
	cout << setw(6)<<PI << endl;					//设置域宽为6并输出
	cout << setfill('*') << setw(6)<< PI << endl;	//设置填充值和域宽并输出
	return 0;
}
```
***
## `左对齐`
```cpp
//cout << left
//对其以后的cout统一左对齐输出
#include<iostream>					//i:输入o:输出stream:流
#include<iomanip>					//格式控制！！！
using namespace std;				//使用标准命名空间
int main()
{
	double PI = 3.14;
	cout << cout.width() << endl;					//输出当前域宽
	cout << PI << endl;								//输出PI
	cout << left;									//设置左对齐
	cout << setw(6) << PI << endl;					//设置域宽为6并输出
	cout << setfill('*') << setw(6) << PI << endl;	//设置填充值和域宽并输出
	return 0;
}
```
***

## **[大佬的博客 CSDN](https://blog.csdn.net/long0801/article/details/76643278?ops_request_misc=&request_id=&biz_id=102&utm_term=cpp输出格式控制&utm_medium=distribute.pc_search_result.none-task-blog-2~all~sobaiduweb~default-6-.first_rank_v2_pc_rank_v29&spm=1018.2226.3001.4187)**

# `基础函数`

## `string相关`

```cpp
// 在字符串s1的第pos个位置前 插入字符串s2
s1.insert(pos，s2);
// 在字符串s1的第pos个位置前 插入字符串s2的从begin开始到end的前一个字符结束的子串
s1.insert(pos,s2,begin,end);
// 从位置pos = 10处开始删除，直到结尾
str.erase(10);
// 从位置pos = 6处开始，删除4个字符
str.erase(6, 4);
```

# `函数高级`

## `默认参数`

**错误示范**

```cpp
void fun(int a, int b=12, int c)
{
	cout << a + b + c << endl;
}
```

**Note：b有了默认参数以后，后面的也必须有默认参数**

```cpp
#include<iostream>
using namespace std;
void fun(int a = 10, int b=90, int c=78);
int main()
{
	fun(1, 2, 3);
	return 0;
}
void fun(int a, int b, int c)
{
	cout << a + b + c << endl;
}
```

**Note：声明和实现只能有一个带默认参数**

## `函数重载`

**01.函数名相同**

**02.同一作用域**

**03.函数参数类型、个数或顺序不同**

**Note：函数返回值不可作为函数重载的条件**

# `对象特征`

## `类对象作为类成员`

**内部其他类先有，自身再有，析构相反**

```cpp
#include<iostream>
using namespace std;
class A
{
public:
	int aa;
	A(int ta) :aa(ta) {}
};
class B
{
public:
	int bb;
	A a;
	//A a=n(隐式类型转换，基本类型—>定义类)
	B(int m, int n) :bb(m), a(n){}
};
void test()
{
	B b(1,2);
}
int main()
{
	test();
	return 0;
}
```

## `静态成员`

### `变量`

**静态变量：储存于全局数据区域的局部变量，效果和全局变量有一拼**

**01.默认赋值**

```cpp
#include<iostream>
using namespace std;
void f()
{
	static int a ;
	cout << a << endl;
}
int main()
{
	f();
	return 0;
}
//输出结果：0（static变量编译器默认赋值为0）
```

```cpp
#include <stdio.h>
int main()
{
    static char str[10];
    printf("string: (begin)%s(end)\n", str);
    return 0;
}
//输出结果：string: (begin)(end)
```

```cpp
#include<iostream>
using namespace std;
void f()
{
	static int a=1 ;
	cout << a << endl;
	a++;
}
int main()
{
	f();
	f();
	return 0;
}
//输出结果
//1
//2（第二次static int a = 1 失去作用，始终只有一个a）
```

**可以看出来这个a是在两个f（）中共同使用，不会因为重新声明而覆盖掉，也不会在第一次f（）函数结束时释放掉，static 变量适用于多模块编程，可以将static型变量理解为`声明在局部区域的全局变量，但其全局性也只对该局部区域开放`。例如上述例子中a对两个f（）函数的区域都开放，若不是同一个局部区域，则无效，例子如下：**

```cpp
#include<iostream>
using namespace std;
void f()
{
	static int a = 1;
	cout << a << endl;
	a++;
}
void p()
{
	static int a = 4;
	cout << a << endl;
	a++;
}
int main()
{
	f();
	p();
	return 0;
}
//输出结果
//1
//4
//f()中的a的局部全局性在f（）内部
//p()中的a的局部全局性在p（）内部
//上述两个a具有不同的局部全局性
```

**和全局变量比起来，static可以控制变量的可见范围（隐藏），即局部全局性**

**一、 static全局变量与普通的全局变量有什么区别 ?
全局变量(外部变量)的说明之前再冠以static 就构成了静态的全局变量。
 全局变量本身就是静态存储方式， 静态全局变量当然也是静态存储方式。 这两者在`存储方式`上并无不同。
 这两者的区别在于非静态全局变量的`作用域`是整个`源程序`， 当一个源程序由多个源文件组成时，非静态的全局变量在`各个源文件`中都是有效的。 而静态全局变量则限制了其作用域， 即只在`定义该变量的源文件内`有效， 在同一源程序的其它源文件中不能使用它。由于静态全局变量的作用域局限于一个源文件内，只能为该源文件内的函数公用，因此可以避免在其它源文件中引起错误。
 static全局变量只初使化一次，防止在其他文件单元中被引用;
二、static局部变量和普通局部变量有什么区别 ？
 把局部变量改变为静态变量后是改变了它的`存储方式`即改变了它的`生存期`。把全局变量改变为静态变量后是改变了它的`作用域`，限制了它的使用范围。      static局部变量只被初始化一次，下一次依据上一次结果值；
三、static函数与普通函数有什么区别？
static函数与普通函数作用域不同,仅在本文件。只在当前源文件中使用的函数应该说明为内部函数(static修饰的函数)，内部函数应该在当前源文件中说明和定义。对于可在当前源文件以外使用的函数，应该在一个头文件中说明，要使用这些函数的源文件要包含这个头文件.
static函数在内存中只有一份，普通函数在每个被调用中维持一份拷贝。
四、static的三条重要作用，首先static的最主要功能是隐藏，其次因为static变量存放在静态存储区，所以它具备持久性和默认值0。**

**02.类内静态变量**

**类内声明、类外初始化**

```cpp
class A
{
public:
	static int a;
};
int A::a = 100;//类型、作用域、名
```

```cpp
#include<iostream>
using namespace std;
class Commodity
{
public:
	Commodity(string n="xxx",int q=0,double p=0)
	{
		num = n;
		quantity = q;
		price = p;
	}
	~Commodity() {};
	void total()
	{
		double discount = 1;
		if (quantity > 10)
			discount = 0.98;
		n += quantity;
		sum += price * quantity * discount * this->discount;
	}
	static double average()
	{
		return sum / n;
	}
	static void display()
	{
		cout << "总个数：" << n << endl << "总售价："
			<< sum << endl << "平均售价：" << average();
	}
private:
	string num;					//编号
	int quantity;				//数量
	double price;				//单价
	static double sum;			//总售价
	static double discount;		//折扣
	static int n;				//总销售量
};
double Commodity::sum = 0;
double Commodity::discount = 0.85;
int Commodity::n = 0;
int main()
{
	Commodity commo[3] =
	{
		Commodity("101",5,23.5),Commodity("102",12,24.56),Commodity("103",100,21.5)
	};
	for (int i = 0; i <= 2; i++)
		commo[i].total();
	Commodity::display();
	return 0;
}
```

**Note：简单而言就是三个售货员共用同一组sum、discount、n**

### `函数`

# `友元`

**01.友元使原本不可访问的成员能够访问，破坏了数据的隐藏性**

## `全局函数`

**复制加分号，放到最上方，加 friend**

```cpp
#include<iostream>
using namespace std;
class A
{
	friend void get(A& a);
public:
	A(string n)
	{
		name = n;
	}
private:
	string name;
};
void get(A& a)
{
	cout << a.name;
}
void test()
{
	A a("张三");
	get(a);
}
int main()
{
	test();
	return 0;
}
```

## `友元类`

**同上**

```cpp
#include<iostream>
using namespace std;
class A
{
	friend class B;
public:
	A(string n)
	{
		name = n;
	}
private:
	string name;
};
class B
{
public:
	void func(A& a)
	{
		cout << a.name;
	}

};
void test()
{
	A a("张三");
	B b;
	b.func(a);
}
int main()
{
	test();
	return 0;
}
```

## `成员函数（待）`



# `运算符重载`

**01.实现自定义数据类型的运算**

**02.不是所有的运算符都可以重载**

**03.'>>'和'<<'只能被友元函数重载（猜测：因为要连续输出）**

## `成员函数重载`

```cpp
//头文件
#include<vector>
#include<string>
#include<iostream>
using namespace std;
class Student
{
public:
	//初始化
	Student(string n="x", double s=0)
	{
		name = n;
		score = s;
	}
	//重载 >
	bool operator>(Student& t)
	{
		return this->score > t.score ? true : false;
	}
	//重载 =
	void operator=(Student& t)
	{
		this->name = t.name;
		this->score = t.score;
	}
	//showStudent
	void showStudent()
	{
		cout << name << ' ' << score << endl;
	}
private:
	string name;
	double score;
};
void sortStudent(vector<Student>& t)
{
	Student tt;
	for(int i=t.size()-1;i>=0;i--)
		for (int j = 0; j < i; j++)
		{
			if (t[j] > t[j + 1])
			{
				tt = t[j];
				t[j] = t[j + 1];
				t[j + 1] = tt;
			}
		}
}
void show(vector<Student>& t)
{
	for (int i = 0; i < t.size(); i++)
		t[i].showStudent();
}
```

```cpp
//源文件
#include"Student.h"
int main()
{
	vector<Student> a;
	cout << "请输入 Name AND Score、输入0 0则退出输入\n";
	while (1)
	{
		string name;
		double score;
		cin >> name >> score;
		if (name == "0" && score == 0)
			break;
		Student t(name, score);
		a.push_back(t);
	}
	sortStudent(a);
	show(a);
	return 0;
}
```

## `友元函数重载（待）`



# `继承`

## `构造和析构顺序`

**先构造后析构（先进后出）**

```cpp
#include<iostream>
using namespace std;
class A
{
public:
	A() 
	{
		cout << "A" << endl;
	}
	~A() { cout << "A析构" << endl; };
};
class B:public A
{
public:
	B()
	{
		cout << "B" << endl;
	}
	~B() { cout << "B析构" << endl; };
};
class C:public B
{
public:
	C()
	{
		cout << "C" << endl;
	}
	~C() { cout << "C析构" << endl; };
};
void test()
{
	C c;
}
int main()
{
	test();
	return 0;
}
//结果如下
//A
//B
//C
//C析构
//B析构
//A析构
```

## 6`派生类构造函数`

**01.如果被派生的类无构造函数，那系统自动分配默认构造函数,子类的构造时不用再去赋值基类，系统分配默认构造函数自动为其赋值**

```cpp
#include<iostream>
using namespace std;
class A
{
	int x;
	int y;
public:
	
};
class B :public A
{
	int z;
public:
	B(int c) :z(c) {}
	void show() { cout <<z; }
};
void test()
{
	B b(3);
	b.show();
}
int main()
{
	test();
	return 0;
}
```

**02.主类拥有构造函数时，系统不在分配默认构造函数，子类的构造函数必须使用基类的构造函数为主类赋值，否者报错！！！**

```cpp
#include<iostream>
using namespace std;
class A
{
	int x;
	int y;
public:
	A(int n, int m) :x(n), y(m) {}
};
class B :public A
{
	int z;
public:
	B(int a,int b,int c) :A(a,b),z(c) {}//a,b虽继承，但B不能访问a,b，所以使用基类构造函数对a,b初始化
	void show() { cout <<z; }
};
void test()
{
	B b(1,2,3);
	b.show();
}
int main()
{
	test();
	return 0;
}
```

**Sum：基类的公有成员成为派生类的公有成员，基类的私有部分也成为派生类的一部分，但只能通过基类的公有和保护方法访问。
派生类需要自己的构造函数，派生类不能访问基类的私有数据，所以派生类构造函数要调用基类构造函数来初始化基类的私有数据。基类对象应在程序进入派生类构造函数前被创建，用初始化列表实现。**



## `同名成员处理`

### `成员属性`

**01.自己的直接用**

**02.基类的加作用域**

```cpp
#include<iostream>
using namespace std;
class A
{
public:
	int a;
	A()
	{
		a = 100;
	}	
};
class B:public A
{
public:
	int a;
	B()
	{
		a = 200;
	}
};
void test()
{
	B b;
	cout << b.a<<endl;
	cout << b.A::a << endl;
}
int main()
{
	test();
	return 0;
}
```

### `成员函数`

**01.自己的直接用**

**02.基类的加作用域**

```cpp
#include<iostream>
using namespace std;
class A
{
public:
	int a;
	void fun()
	{
		cout << "A-fun()" << endl;
	}
	void fun(int t)
	{
		cout << t << endl;
	}
};
class B:public A
{
public:
	int b;
	void fun()
	{
		cout << "B-fun()" << endl;
	}
};
void test()
{
	B b;
	b.fun();
	b.A::fun();
	b.A::fun(100);
}
int main()
{
	test();
	return 0;
}
```

## `同名静态成员处理`

### `静态成员属性`

**自己的直接用，父类的加作用域**

```cpp
#include<iostream>
using namespace std;
class A
{
public:
	static int a;
};
int A::a = 100;
class B:public A
{
public:
	static int a;
};
int B::a = 200;
void test()
{
	//通过对象访问
	B b;
	cout << b.a << endl;
	cout << b.A::a << endl;
	//通过类名来访问
	cout << B::a<<endl;
	cout << B::A::a << endl;
}
int main()
{
	test();
	return 0;
}
```

### `静态成员函数`

**自己的直接用，父类的加作用域**

```cpp
#include<iostream>
using namespace std;
class A
{
public:
	static void func()
	{
		cout << "A-func()" << endl;
	}
};
class B:public A
{
public:
	static void func()
	{
		cout << "B-func()" << endl;
	}
};
void test()
{
	//通过对象访问
	B b;
	b.func();
	b.A::func();
	//通过类名访问
	B::func();
	B::A::func();
}
int main()
{
	test();
	return 0;
}
```

## `多继承语法`

**加对应作用域即可**

```cpp
#include<iostream>
using namespace std;
class A
{
public:
	int t;
	A()
	{
		t = 1;
	}
};
class B
{
public:
	int t;
	B()
	{
		t = 2;
	}
};
class C:public A,public B
{
public:
	int t;
	C()
	{
		t = 3;
	}
};
void test()
{
	C c;
	cout << c.t << endl;
	cout << c.B::t << endl;
	cout << c.A::t << endl;
}
int main()
{
	test();
	return 0;
}
```

## `菱形继承`

**问题：多份继承，资源浪费,实例如下：**

```cpp
#include<iostream>
using namespace std;
//动物
class Animal
{
public:
	int age;
};
//羊
class Sheep:public Animal
{
public:
	
	
};
//驼
class Tuo :public Animal
{
public:
	
};
//羊驼
class SheepTuo :public Sheep, public Tuo
{


};
void test()
{
	SheepTuo sp;
	//继承两个age,资源浪费
	sp.Sheep::age = 1;
	sp.Tuo::age = 2;
}
int main()
{
	test();
	return 0;
}
```

**解决方案：使用虚继承，基类变成虚基类，多继承时自动合并，相当于直接从基类继承。**

```cpp
#include<iostream>
using namespace std;
//动物
class Animal
{
public:
	int age;
};
//羊
class Sheep:virtual public Animal
{
public:
	
	
};
//驼
class Tuo :virtual public Animal
{
public:
	
};
//羊驼
class SheepTuo :public Sheep, public Tuo
{


};
void test()
{
	SheepTuo sp;
	sp.age = 18;		//直接访问
	sp.Sheep::age = 1;	//通过内部virtual base pointer找到从Animal中继承的age
	sp.Tuo::age = 2;	//通过内部virtual base pointer找到从Animal中继承的age
}
int main()
{
	test();
	return 0;
}
```

# `多态`

## `基本概念`

**条件：**

**01.有继承关系**

**02.子类重写（除了{}内其他完全相同）父类虚函数，重写时virtual可不写**

**使用方法：**

**父类指针或引用执行子类对象，例子如下**

```cpp
#include<iostream>
using namespace std;
class Animal
{
public:
	void virtual func() 
	{
		cout << "动物在说话" << endl;
	}
};
class Cat:public Animal
{
public:
	void func()
	{
		cout << "猫在说话" << endl;
	}
};
class Dog :public Animal
{
public:
	void func()
	{
		cout << "狗在说话" << endl;
	}
};
void doSpeak(Animal& a)
{
	a.func();
}
void test()
{
	Dog a;
	doSpeak(a);
}
int main()
{
	test();
	return 0;
}
```

## `底层原理`

**虚函数定义后实际上保留的是一个指向函数的指针，子类继承后如果重写父类虚函数，那么原来的指针会被子类的指针替换掉。在调用时父类指针或引用的地址由重写的虚函数来确认，不同的继承类虚函数，运行不同的重写函数，可以拥有多种运行状态，即：多态性、简单理解可以认为是基类虚函数可以被子类虚函数覆盖掉。**

## `计算器类`

**普通写法**

```cpp
#include<iostream>
using namespace std;
class Calculator
{
public:
	int getResult(char oper)
	{
		if (oper == '+')
			return a + b;
		if (oper == '-')
			return a - b;
		if (oper == '*')
			return a * b;
	}
	int a;
	int b;
};
void test()
{
	Calculator c;
	c.a = 1;
	c.b = 2;
	cout << c.getResult('*') << endl;
}
int main()
{
	test();
	return 0;
}
```

**多态写法**

```cpp
#include<iostream>
using namespace std;
class AbstractCalculator
{
public:
	virtual int getResult()
	{
		return 0;
	}
	int a;
	int b;
};
class Add :public AbstractCalculator
{
public:
	int getResult()
	{
		return a+b;
	}
};
class Sub :public AbstractCalculator
{
public:
	int getResult()
	{
		return a - b;
	}
};
class MUL :public AbstractCalculator
{
public:
	int getResult()
	{
		return a * b;
	}
};
class CU :public AbstractCalculator
{
public:
	int getResult()
	{
		return a / b;
	}
};
void test()
{
	AbstractCalculator* ac = new Add;
	ac->a = 1;
	ac->b = 2;
	cout << ac->getResult() << endl;
	delete ac;
	ac = new Sub;
	ac->a = 1;
	ac->b = 2;
	cout << ac->getResult() << endl;
	delete ac;
	ac = new MUL;
	ac->a = 1;
	ac->b = 2;
	cout << ac->getResult() << endl;
	delete ac;
	ac = new CU;
	ac->a = 1;
	ac->b = 2;
	cout << ac->getResult() << endl;
	delete ac;
}
int main()
{
	test();
	return 0;
}
```

## `纯虚函数和抽象类`

**来源：父类的虚函数的实现是无意义的，主要都是调用子类重写的内容，因此可以将虚函数改为纯虚函数。**

**一个拥有纯虚函数的类也称为抽象类。**

**语法：纯虚函数的基础上加一个=0**

**特点：无法实体化对象，子类必须重写基类的纯虚函数，否者也是抽象类。**

```cpp
//无法实例化
#include<iostream>
using namespace std;
class Base
{
public:
	//纯虚函数
	virtual void func() = 0;
};
void test()
{
	Base b;
	new Base;
    //报错
}
int main()
{
	test();
	return 0;
}
```

```cpp
//子类未重写也无法实例化
#include<iostream>
using namespace std;
class Base
{
public:
	//纯虚函数
	virtual void func() = 0;
};
class Son:public Base
{
public:


};
void test()
{
	Son s;//报错
}
int main()
{
	test();
	return 0;
}
```

```cpp
//正确写法
#include<iostream>
using namespace std;
class Base
{
public:
	//纯虚函数
	virtual void func() = 0;
};
class Son:public Base
{
public:
	void func() 
	{
		cout << "hahaha";
	};//';'和上面的';'一致

};
void test()
{
	Base *b = new Son;
	b->func();
}
int main()
{
	test();
	return 0;
}
```



## `56-59`

# `文件操作`

**头文件：fstream**

**文件分类：文本文件（ASCII）、二进制文件（01）**

**打开方式：**

**ios::in(文件读入、读)**

**ios::out(输出到文件、写)**

**ios::app(追加方式写文件Append)**

```cpp
#include<fstream>
#include<iostream>
using namespace std;

void test()
{
	//写
	ofstream ofs;

	ofs.open("text.txt", ios::out);//会覆盖
	ofs << "张三" << endl;
	ofs.close();

	ofs.open("text.txt", ios::app);//不会覆盖(追加)
	ofs << "张三" << endl;
	ofs.close();

	//读
	ifstream ifs;

	ifs.open("text.txt", ios::in);
	string s;
	ifs >> s;
	cout << s;
	ifs.close();
}
int main()
{
	test();
	return 0;
}
```

# `模板`

**Note：模板只是一个框架，且不是万能的**

## `函数模板`

**基本用法**

```cpp
#include<iostream>
using namespace std;
template <typename T> //template <class T>也可以
void mySwap(T& a, T& b)
{
	T temp = a;
	a = b;
	b = temp;
}
int main()
{
	int a = 10, b = 20;
	mySwap(a, b);//自动类型推导
	cout << a << " " << b << endl;
	double c = 1.1, d = 2.2;
	mySwap<double>(c, d);//显示指定类型
	cout << c << " " << d << endl;
	string e, f;
	e = "哈哈";
	f = "嘿嘿";
	mySwap(e, f);
	cout << e << " " << f << endl;
	return 0;
}
```

**注意事项**

```cpp
void mySwap(T& a, T& b)
{
	T temp = a;
	a = b;
	b = temp;
}
int main()
{
	int a = 10, b = 20;
	char c='c';
	mySwap(a, c);//自动类型推导
	cout << a << " " << c << endl;
}
//类型不一致导致错误
```

```cpp
#include<iostream>
using namespace std;
template <typename T>
void fun()
{
	cout << "fun被调用";
}
int main()
{
	fun<int>();//未用到T时必须指明类型(也可用来强制类型转化)
}
```

**一个模板对应一个函数！！！！**

**排序函数模板**

```cpp
#include<iostream>
using namespace std;
template<class T>
void mySwap(T& a, T& b)
{
	T temp = a;
	a = b;
	b = temp;
}
template <typename T>
void mySort(T a[],int len)
{
	for (int i = 1; i < len; i++)
	{
		int k = i;
		for (int j = i + 1; j < len; j++)
		{
			if (a[j] < a[k])
				mySwap(a[j], a[k]);
		}
	}
}
template<typename T>
void myPrint(T a[], int len)
{
	for (int i = 0; i < len; i++)
		cout << a[i] << " ";
	cout << endl;
}
int main()
{
	int a[] = { 1,4,3,7,6 };
	mySort(a, sizeof(a) / sizeof(int));
	myPrint(a, sizeof(a) / sizeof(int));
	char b[] = "ecdaf";
	mySort(b, sizeof(b)-1);
	myPrint(b, sizeof(b)-1);
}
```
**加<>调用模板函数，否则默认调用普通函数**

```cpp
#include<iostream>
using namespace std;
void fun()
{
	cout << "普通函数" << endl;
}
template<class T>
void fun()
{
	cout << "模板函数" << endl;
}
int main()
{
	fun();		//普通函数
	//fun<>();	//报错
	fun<int>();	//模板函数
	return 0;
}
```

**模板函数也可以重载**

```cpp
#include<iostream>
using namespace std;
void fun(int a,int b)
{
	cout << "普通函数" << endl;
}
template<typename T>
void fun(T a,T b)
{
	cout << "模板函数" << endl;
}
template<typename T>
void fun(T a,T b,T c )
{
	cout << "重载的模板函数" << endl;
}
int main()
{
	int a = 10, b = 20, c = 30;
	fun(a,b);		//普通函数
	fun<>(a,b);		//模板函数
	fun(a, b, c);	//重载的模板函数
	return 0;
}
```

**优先不强转调用模板函数，例子如下：**

```cpp
#include<iostream>
using namespace std;
void fun(int a,int b)
{
	cout << "普通函数" << endl;
}
template<typename T>
void fun(T a,T b)
{
	cout << "模板函数" << endl;
}
int main()
{
	char a = 'a';
	char b = 'b';
	fun(a,b);		//调用模板函数
	return 0;
}
```

**模板的具体化（实现更多功能）**

```cpp
#include<iostream>
using namespace std;
class Person
{
public:
	Person(string na,int nu)
	{
		this->name = na;
		this->number = nu;
	}
	string name;
	int number;
};
template <class T>
bool equal(T a, T b)
{
	return a == b;
}
bool equal(Person a, Person b)//模板具体化，实现Person的比较
{
	if (a.name == b.name && a.number == b.number)
		return true;
	else
		return false;
}
int main()
{
	Person a("张三", 111);
	Person b("张三", 111);
	if (equal(a, b))
		cout << "a==b";
	else
		cout << "a!=b";
	return 0;
}

```

## `类模板`

**语法**

```cpp
template <class T>
class Person
{
    //////
}
```

**简例：**

```cpp
#include<iostream>
using namespace std;
template <class typeName,class typeAge>
class Person
{
public:
	Person(typeName name, typeAge age)
	{
		this->name = name;
		this->age = age;
	}
	void show()
	{
		cout << name << " " << age << endl;
	}
private:
	typeName name;
	typeAge age;
};

int main()
{
	Person <string, int>a("张三", 111);
	a.show();
	return 0;
}
```

**Note：和函数模板相比较，类模板无自动类型推导，例子如下：**

```cpp
#include<iostream>
using namespace std;
template <class typeName,class typeAge>
class Person
{
public:
	Person(typeName name, typeAge age)
	{
		this->name = name;
		this->age = age;
	}
	void show()
	{
		cout << name << endl << age << endl;
	}
private:
	typeName name;
	typeAge age;
};

int main()
{
	Person a("张三", 111);
	a.show();
	return 0;
}
//错误信息：缺少Person模板参数信息
```

**类模板可以设置默认参数，如下**

```cpp
#include<iostream>
using namespace std;
template <class typeName=string,class typeAge=int>
class Person
{
public:
	Person(typeName name, typeAge age)
	{
		this->name = name;
		this->age = age;
	}
	void show()
	{
		cout << name << endl << age << endl;
	}
private:
	typeName name;
	typeAge age;
};

int main()
{
	Person <>a("张三", 111);
	a.show();
	return 0;
}
```

## `176-184`

# `异常处理`

**cpp异常处理由检查try，抛出throw和捕捉catch三部分组成**

```cpp
#include<iostream>
using namespace std;

void func()
{
	int a = 1;
	try
	{
		throw a;
	}
	catch (double)
	{
		cout << "哈哈哈";
	}
}
int main()
{
	try
	{
		func();
	}
	catch(...)
	{
		cout << "hahah";
	}
}
```

# `STL`
## `vector`

### `简介`

**vector：向量**
**一个低维空间的向量可以在无数个高维空间上进行表示，所以一个 vector 的大小是可拓展的**
**vector 可以看成一个单端数组，左闭右开。**

**写法：vector<数据类型> 变量名**

```cpp
vector<int> a;//定义一个放int的向量a
```



> vector 与普通数组区别 在于数组是`静态`空间，而 vector 可以`动态`扩展，且动态扩展并不是在原空间之后续接新空间，而是`找更大的内存空间`，然后将原数据`拷贝`新空间，`释放`原空间！

------

### `CSDN_Voctor`

**[voctor](https://blog.csdn.net/weixin_41743247/article/details/90635931?ops_request_misc=%7B%22request%5Fid%22%3A%22163073130216780366569702%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=163073130216780366569702&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~top_positive~default-1-90635931.first_rank_v2_pc_rank_v29&utm_term=vector&spm=1018.2226.3001.4187)**

***

## `优先队列`

**一、头文件：queue**

**二、写法：priority_queue <数据类型，容器类型，排序方式>**

### 例子（1）

```cpp
cpp
#include<queue>
priority_queue<int, vector<int>, greater<int> >Q;
```

> priority_queue: 优先队列
> 数据类型:int 型
> 容器类型:vector
> 比较方式:greater (更大、升序排列、从 top 到 basic 越来越大)
> vector 容器基本内涵
> vector 数据结构和数组非常相似，也称为单端数组
> vector 与普通数组区别 在于数组是`静态`空间，而 vector 可以`动态`扩展
> 且动态扩展并不是在原空间之后续接新空间，而是`找更大的内存空间`，然后将原数据`拷贝`新空间，`释放`原空间！
> 后两个 >> 之间一定要有`空格`，因为 “>>” 是`位移`运算！！！

**相关链接：[bitMap - 位运算](https://xn--ctta.icu/2021/07/27/1.算法与数据结构/01.算法/05.图论算法/Bit Map/)**

------

### 例子（2）

```cpp
cpp
#include<queue>
#include<iostream>
using namespace std;
priority_queue<int, vector<int>, greater<int> >Q;
int ans;
int main()
{
	int n, x;
	cin >> n;
	while (n--)
	{
		cin >> x;
		Q.push(x);
	}
	while (Q.size()!= 1)
	{
		int a, b;
		a = Q.top();
		Q.pop();
		b = Q.top();
		Q.pop();
		Q.push(a + b);
		ans += a + b;
	}
	cout << ans;
	return 0;
}
```

------

## `sort函数`

**头文件：algorithm**
**写法如下：**

```cpp
#include<algorithm>
sort(起始地址,结束地址,排序方式);
```

### `排序int型`

```cpp
#include<iostream>
#include<algorithm>
using namespace std;
int main()
{
   int a[10]={9,6,3,8,5,2,7,4,1,0};
   for(int i=0;i<10;i++)
   cout<<a[i]<<endl;
   sort(a,a+10);//无第三个参数时默认从小到大排序
   for(int i=0;i<10;i++)
   cout<<a[i]<<endl;
   return 0;
}
```

```cpp
#include<iostream>
#include<algorithm>
using namespace std;
bool complare(int a,int b)//排序规则
{
     return a>b;
}
int main()
{
     int a[10]={9,6,3,8,5,2,7,4,1,0};
     for(int i=0;i<10;i++)
     cout<<a[i]<<endl;
     //从大到小排序
     sort(a,a+10,complare);//在这里就不需要对complare函数传入参数了，这是规则
     for(int i=0;i<10;i++)
        cout<<a[i]<<endl;
     return 0;
}
```

------

### `排序结构体`

```cpp
#include<iostream>
#include<algorithm>
using namespace std;
struct Student
{
	string name;
	double score;
};
bool complare(Student t1,Student t2)
{
	return t1.score < t2.score;
}
int main()
{
	Student s[] = {
		{"zhan",89 },
		{"dwad",92}
	};
	sort(s, s + 2, complare);
	for (int i = 0; i <= 1; i++)
	{
		cout << s[i].name << " " << s[i].score << endl;
	}
	return 0;
}
```

**Note: 在定义排序规则的函数里面，返回的是<就是从小往大排，反之亦然，事实上还可以使用运算符重载的方法来排序结构体，后文将会提到。**

# `细节补充`




## `&的用法`

### `逻辑运算符号：与`

**略**

### `取地址符`

**略**

### `位运算`

**见c语言文章或bitmap算法**

### `引用(换名字)`

**eg1：**

```cpp
class Note {
	public: 
    	f9();

} note;

note.f9()


```



```cpp
#include<iostream>
using namespace std;
int main() {
	int a = 10;
	int &b = a;
	cout << a << b << endl;
	return 0;
}
```

**eg2（函数传入参数时起别名）:**

```cpp
#include<iostream>
using namespace std;
void solve(int& a, int& b)
{
	int temp;
	temp = a; a = b; b = temp;
}
int main()
{
	int a = 10;
	int b = 20;
	solve(a, b);
	cout << a << " " << b;
	return 0;
}
```
**eg3（常量引用）：**

```cpp
#include<iostream>
using namespace std;
int main()
{
	const int &a = 89;
	//等同于 int temp=89;int &a=temp;
	cout << a;
	return 0;
}
```




## `宏`

**C语言中，有两种宏，宏其实是一个代码片段，在用到宏时，会被替换掉。**

### `替换变量`

**eg：**

```cpp
#define MAX 100//简单替换
```

**如果宏的代码依然是宏的话，那么会一直往下替换**

### `替换函数`

**宏还可以来替换函数（可传入参数）**

**eg:(宏定义取大函数)**

```cpp
#define MAX(a,b) ((a)>(b)?(a):(b))
#include<iostream>
using namespace std;
int main()
{
	int a = 1, b = 99999;
	cout << MAX(a, b);
}
```

**eg:(宏定义for循环)**

//

## `宽字符`

```cpp
#include<locale>
#include<iostream>
using namespace std;
int main()
{
	setlocale(LC_ALL, "chs");		//设置中文
	wchar_t s[] = L"好是一个好人";
	unsigned short c = s[0];		//双字节对等，unsigned!!!
	int j = 0;
	for (int i = 19968; i <= 40869; i++)
	{
		j++;
		cout << i << " ";
		wprintf(L"%lc\n", i);
	}
	cout << j << endl;
}

```


## `cerr和clog`

[Cerr和Clog](https://blog.csdn.net/bsmmaoshenbo/article/details/50778068?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522163766738616780255274112%2522%252C%2522scm%2522%253A%252220140713.130102334.pc%255Fall.%2522%257D&request_id=163766738616780255274112&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v1~rank_v31_ecpm-1-50778068.pc_search_result_cache&utm_term=cerr&spm=1018.2226.3001.4187)











## `浅拷贝的问题`

**堆区的内存重复释放！！！**





