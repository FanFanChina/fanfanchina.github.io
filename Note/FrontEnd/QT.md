# `QT安装下载`

**略**

# `使用介绍`

**01.三大基类：widget派生出mainwindows和diglog**

**02.名称和路径不要中文**

**03.自动对齐 ctrl+i、注释 ctrl+/ **

**04.同名文件切换F4**

# `第一个QT程序`

```c++
#include "mywidget.h"
#include <QApplication>             //应用程序的类

int main(int argc, char *argv[])    //argc命令行变量的数量、argv[]命令行变量数组
{
    QApplication a(argc, argv);     //QApplication a，Q应用程序的对象a，有且仅有一个
    myWidget w;                     //类myWidget的对象w
    w.show();                       //w对象的方法
    return a.exec();                //让a进入消息循环，以便于窗口一直存在
}
```

# `按钮`

```c++
//第一种写法
myWidget::myWidget(QWidget *parent)
    : QWidget(parent)
{
    //创建一个按钮
    QPushButton * btn= new QPushButton;
    //btn->show();//以顶层方式弹出窗口控件
    //设置按钮的依赖对象
    btn->setParent(this);
    //显示文本
    btn->setText("你好啊");
}
```

```c++
//第二种写法+重置窗口大小
myWidget::myWidget(QWidget *parent)
    : QWidget(parent)
{
    QPushButton *btn=new QPushButton("hahaha",this);
    resize(600,400);	//重置窗口大小
}
//弊端：按照控件的大小创造窗口的大小
//解决方法:重置窗口大小
```

```c++
//同时显示两个按钮
myWidget::myWidget(QWidget *parent)
    : QWidget(parent)
{
    QPushButton *btn1=new QPushButton("第一个按钮",this);
    QPushButton *btn2 = new QPushButton("第二个按钮",this);
    btn2->move(100,100); //如果不移动开的话会覆盖掉
    resize(600,400);
}
```
# `窗口`
```c++
//设置窗口标题
myWidget::myWidget(QWidget *parent)
    : QWidget(parent)
{
    QPushButton *btn1=new QPushButton("第一个按钮",this);
    QPushButton *btn2 = new QPushButton("第二个按钮",this);
    btn2->move(100,100);
    resize(600,400);
    setWindowTitle("你好");  //设置窗口标题
}
```

```c++
//设置固定窗口大小
myWidget::myWidget(QWidget *parent)
    : QWidget(parent)
{
    QPushButton *btn1=new QPushButton("第一个按钮",this);
    QPushButton *btn2 = new QPushButton("第二个按钮",this);
    btn2->move(100,100);
    setWindowTitle("你好");
    setFixedSize(600,400);//设置固定窗口大小，这样可以不用重置窗口大小
}
```

```c++
//坐标系:左上角为原点、向右为x轴，向下为y轴
```

```c++
//小练习
myWidget::myWidget(QWidget *parent)
    : QWidget(parent)
{
    setWindowTitle("piupiupiupiu");
    setFixedSize(600,400);
    QPushButton *btn1=new QPushButton("这是一个假的按钮",this);
    QPushButton *btn2 = new QPushButton("你看，╰(*°▽°*)╯我不就是一个button 吗 ？",this);
    btn1->move(100,100);
    btn2->move(100,200);
}
```

```c++
//点击按钮关闭窗口
myWidget::myWidget(QWidget *parent)
    : QWidget(parent)
{
    setWindowTitle("piupiupiupiu");
    setFixedSize(600,400);
    QPushButton *btn = new QPushButton("点击关闭窗口",this);
    btn->move(200,100);
    connect(btn,&QPushButton::clicked,this,&myWidget::close);
}
```

# `自定义信号`

```c++
//老师
class Teacher : public QObject
{
    Q_OBJECT
public:
    explicit Teacher(QObject *parent = nullptr);

signals:
    //自定义信号，返回值为空
    //只需要声明，不需要实现
    //可以有参数，可以重载
    void hungry();

public slots:
};

//学生
class Student : public QObject
{
    Q_OBJECT
public:
    explicit Student(QObject *parent = nullptr);

signals:

public slots:
    //返回值为空,需要声明,需要实现
    void treate();
};

//treat函数实现
void Student::treate()
{
    qDebug()<<"我请客！！！";
}

//窗口定义两个对象
class myWidget : public QWidget
{
    Q_OBJECT        //Q_OBJECT宏，允许对象使用信号和槽机制

public:
    myWidget(QWidget *parent = 0);
    void classIsOver();
    ~myWidget();
    void isOver();
    Teacher *t;
    Student *s;
};

//窗口定义触发函数
void myWidget::isOver()
{
    emit t->hungry();
}

//初始化类、信号连接、触发信号
myWidget::myWidget(QWidget *parent) : QWidget(parent)
{

    setWindowTitle("piupiupiupiu");
    setFixedSize(600,400);

    this->s = new Student(this);
    this->t = new Teacher(this);
    connect(t,&Teacher::hungry,s,&Student::treate);
    isOver();
}
```

