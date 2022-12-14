# Vim

> visual interface improve 可视化界面提升版
> 

## **命令模式**

用户刚刚启动 vi/vim，便进入了命令模式。

此状态下敲击键盘动作会被Vim识别为命令，而非输入字符。比如我们此时按下i，并不会输入一个字符，i被当作了一个命令。

以下是常用的几个命令：

- **i** 切换到输入模式，以输入字符。
- **x** 删除当前光标所在处的字符。
- **:** 切换到底线命令模式，以在最底一行输入命令。

若想要编辑文本：启动Vim，进入了命令模式，按下i，切换到输入模式。

命令模式只有一些最基本的命令，因此仍要**依靠底线命令模式输入更多命令**。

## **输入模式**

在命令模式下按下i就进入了输入模式。

在输入模式中，可以使用以下按键：

- **字符按键以及Shift组合**，输入字符
- **ENTER**，回车键，换行
- **BACK SPACE**，退格键，删除光标前一个字符
- **DEL**，删除键，删除光标后一个字符
- **方向键**，在文本中移动光标
- **HOME**/**END**，移动光标到行首/行尾
- **Page Up**/**Page Down**，上/下翻页
- **Insert**，切换光标为输入/替换模式，光标将变成竖线/下划线
- **ESC**，退出输入模式，切换到命令模式
- **底线命令模式**
  
    在命令模式下按下:（英文冒号）就进入了底线命令模式。
    
    底线命令模式可以输入单个或多个字符的命令，可用的命令非常多。
    
    在底线命令模式中，基本的命令有（已经省略了冒号）：
    
    - q 退出程序
    - w 保存文件
    
    按ESC键可随时退出底线命令模式
    

![](https://pic1.imgdb.cn/item/6340444c16f2c2beb156da80.jpg)

## 快捷键

```bash
# 删除光标所在行
命令模式 + dd
# 删除第当前行以下的3行
命令模式 + 3 dd
# 删除给定范围的行
命令模式 + :3,5d
# 删除所有行
命令模式 + :%d
```

## Vim配置和美化

**先在 ~ 目录下建.vimrc文件**

- **配置**
  
    ```bash
    "编码设置"
    set encoding=utf-8
    set termencoding=utf-8
    set fileencodings=ucs-bom,utf-8,cp936,gb18030,big5,euc-jp,euc-kr
    set fileencoding=utf-8
    "自动缩进"
    set autoindent
    set cindent
    "回车 = 4"
    set tabstop=4
    "显示行号"
    set number
    "代码补全"
    set completeopt=preview,menu
    "共享剪贴板"  
    set clipboard=unnamed
    "突出显示当前行"
    set cursorline
    "语法高亮"
    set syntax=on 
    "启用鼠标"
    set mouse=a
    ```
    
- 美化