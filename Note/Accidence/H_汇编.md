# `寄存器`

**以下寄存器均为对编程人员可见的可编程寄存器**

## `通用寄存器`

### `数据寄存器`

**AX——累加（Accumulate）**

**BX——基地址（Base）**

**CX——计数（Count）**

**DX——存数据（Date）**

### `特殊寄存器`

**SP——堆栈指针（Stake）**

**BP——基地址指针（Base）**

**SI——源变址（Source Index）**

**DI——目的变址（Destination Index）**

## `专用寄存器`

### `标志寄存器`

**FLAGS**

### `指令指针寄存器`

**IP**

### `段寄存器`

**CS——代码段（Code）**

> CS指明代码段基地址  : IP(指令指针)——当前执行的指令位置

**DS——数据段（Date）**

> 没有特定的寄存器存储数据段的偏移地址，需要自己计算（EA）

**SS——栈段（Stack）**

> SS指明栈段基地址  : SP(堆栈指针)——指明栈顶

**ES——附加段（Extra）**

# `存储器`

## `字节，字和双字`

**8位——字节**

**16位——字**

**32位——双字**

## `编号规则`

**从0开始，直到最大**

eg：IA-32（0-2的32次方（0-FFFFFFFF）H）

> 4个二进制位对应一个16进制位

**每一个地址指向一个字节，如下图：**

![dwad](https://pic.imgdb.cn/item/618787812ab3f51d9173f971.jpg)

## `MMU`

**MMU——Memory Manage Unit（存储管理单元）**、

<img src="https://pic.imgdb.cn/item/618788492ab3f51d9174e2d5.jpg" alt="dwad" style="zoom:80%;" />

## `逻辑地址和物理地址`

**逻辑地址=段基地址：偏移地址**

![](https://pic.imgdb.cn/item/618789122ab3f51d9175fe04.jpg)

**同一个存储单元的不同表示方式，逻辑地址利于我们去编程。**

**逻辑地址——MMU——物理地址**

# `指令分类`

**执行性语句：标号:硬性助记符 操作数，操作数;注释**

**说明性语句：名字 伪指令助记符 参数,参数, ...;注释**

> 执行性语句类似于高级语言中的赋值等（完成具体的功能）
>
> 说明性语句类似于高级语言中的定义变量，结构体，类等（说明一些属性） 

# `操作数`

**（一）立即数——无地址含义，只表示运算数据（请立即给我一个数，不要墨迹）**

**（二）寄存器——运算的数据放在CPU的寄存器组里（最快！！！）**

**（三）存储器——运算的数据放在内存里 [ ] 表示偏移地址**

# `寻址方式`

## `立即寻址`

**指令直接给出，适用于立即数**

## `寄存器寻址`

**大多指的是通用寄存器**

## `存储器寻址`

**使用——[偏移地址]**

> Note:存储器操作数的字长本身不确定，其字长取决于指令中另外一个寄存器的操作数，或通过其他方式指定字长

### `直接寻址`

```asm6502
mov ax,[1200H]		;默认使用Date Segment段基地址
mov ax,ex:[1200H]	;重设为Extra Segment段基地址
```

### `间接寻值`

**使用间址寄存器BX，BP，SI，DI（只有也只能有这4个）**

```asm6502
mov bx,1200H
mov ax,[bx]
```

**BX，SI，DI——默认在数据段**

**BP——默认在堆栈段**

**另：SP——始终指向栈顶**

### `相对寻址`

```asm6502
mov ax,[bx+date];
```

```asm6502
mov ax,2000H	;2000H送给ax
mov ds,ax		;ax送给dx
mov bx,1200H	;1200H送给Bx
mov al,[bx+5]	;在Date Segment基地址偏移1205H个单位的字节送给al寄存器
;其他写法5[bx]、[bx]5
```

**主要用于一维数组的操作，常数作为表头地址，间址寄存器作为相对地址**

### `基址、变址寻址`

**基址寄存器的内容（BX，BP） + 变址寄存器的内容（SI，SP）**

**BX——默认在数据段**

**BP——默认在堆栈段**

```asm6502
mov si,1100H	;si==1100H
mov bx,si		;bx==1100H
mov ax,[bx+si]	;DateSegment段偏移2200H和2201H个单位的地址所指向的字节的数送给ax寄存器
```

### `基址、变址、相对寻址`

**基址寄存器的内容（BX，BP） + 变址寄存器的内容（SI，SP）+位移量**

**主要用于二维数组的操作，表头地址，行地址和列地址**

```asm6502
mov di,1100H
mov bp,di
mov al,[bp][di]5;StackSegment段偏移2205H个单位的地址所指向的字节的数送给al寄存器
```

### `隐含寻址`

```asm6502
mul bl	;equal: ax=al*bl
```
# `寻址方式 Test`

![](https://pic.imgdb.cn/item/6187cce42ab3f51d91f420fa.jpg)

```asm6502
mov ax,bx			;寄存器寻址
mov dl,80H			;立即寻址
mov ax,VAR[bx][si]   ;6000H*16+0050H+0800H+00A0H=608F0H(5位)
mov al,'B'			;立即寻址
mov di,es:[bx]       ;2000H*16+0800H=20800H
mov dx,[bp]			;1500H*16+1200H=16200H
mov bx,20H[bx]		;6000H*16+0800H+20H=60820H
```

**物理地址，偏移地址，基地址针对均为存储器，寄存器的地址是固定的**

# `指令`

## `数据传送类`

### `MOV`

```asm6502
mov al,bx		;错误：字长不等
mov ax,10H		;正确：立即寻址
mov ax,bx		;正确：寄存器寻址
mov ax,[bx]05H	;正确：存储器寻址
mov ds,1000H	;错误：段寄存器不可以用立即寻址赋值
mov [bx][bp],bx ;错误：目的操作数寻址方式错误（bx和bp为不同的两个段）
mov dx,09H	    ;正确：立即数的字长是不确定的，可以补0
mov [1200],[si] ;错误：mov指令不能同时为存储器c
```

**eg: 将(*)的ASCⅡ码2AH送入内存数据段1000H开始的100个单元中**

```asm6502
mov di 1000H		;起始位置
mov cx,64H			;100D=64H
mov al,'*'			; *
AGAIN: mov [di],al
	   inc di		;di++
	   dec cx		;cx--
	   jnz AGAIN	;cx!=0 则继续
	   hlt			;
```

### 	`PUSH、POP`

**特点：先进后出、以字（双字节，16位）为单位**

**note：操作数可以是寄存器或存储器的两个单元，但不能是`立即数`**

**单操作数指令的操作数一定不能是立即数！！！**

### `交换指令`

**(XCHG REG,MEM/REG)**

**note: 两个操作数必须至少有一个寄存器，不允许使用段寄存器**

```asm6502
xchg ax,bx		;寄存器交换
xchg [2000],cl	;内存与寄存器交换
```

### `查表指令(XLAT)`

**表头：BX**

**偏移量：AL**

**值返回对象：AL**

**将BX+AL所指单元的内容送给AL**

### `字位扩展指令`

**note：将有符号数的符号位扩展到高位**

```asm6502
cbw	;将al扩展到ax
;最高位为1，执行后ah为FFH(有符号数)
;最高位为0，执行后ah为00H
cwd	;将ax扩展到dx,ax
;最高位为1，执行后dx为FFFFH
;最高位为0，执行后dx为0000H
```

**上述指令只针对有符号数有意义，无符号数拓展只需要在高位加足够多的0即可！！！**

### `地址传送指令`

**LEA：取偏移地址（近地址指针,当前段内）**

**LDS、LES、远地址指针（用于多模块设计）**

**将变量的16位偏移地址写入到目标寄存器**

```asm6502
mov al,i	;将i变量的内容送给al
lea bx,i	;将i变量的地址送给bx
```

![](https://pic.imgdb.cn/item/618bba3b2ab3f51d910541cb.jpg)

**note: lea是取地址，mov是取值**

**eg:**

![](https://pic.imgdb.cn/item/618bbb552ab3f51d9105a708.jpg)

```asm6502
lea si,MEM1
lea di,MEM2
mov cl,50
AGAIN: 
mov al,[si]
mov [di],al
inc si
inc di
dec cl
jnz AGAIN
HLT
```

![](https://pic.imgdb.cn/item/618bbd3a2ab3f51d91064230.jpg)

### `标志传送指令`

**FLAGS是一个16位的寄存器，一共有9个标志位，其余7个是空闲位**

**LAHF：将FLAGS低8位内容(含5个标志位)装入AH**

![](https://pic.imgdb.cn/item/618bbe852ab3f51d9106ab79.jpg)

**SAHF：将AH的内容写回到FLAGS低8位中**

### `输入输出指令`

**端口：除了在CPU内部有寄存器组，接口处也有寄存器组，为了区分，接口里面的寄存器叫做端口，CPU可以直接读写端口**

**指令格式：**

**IN acc，PORT（port：端口地址）**

**OUT PORT，acc（port：端口地址）**

**acc——al/ax（绝对不能是ah）**

![](https://pic.imgdb.cn/item/6191e6062ab3f51d91110dfc.jpg)



```asm6502
in ax,80H;从80H端口读入一个16bit数据到ax（端口地址8位）
mov dx,2400H
in al,dx;从2400H端口读入一个8bit数据（端口地址16位）
out 35h,ax;将ax的值写到35H端口中去
out ax,35H;格式错误！！！
```

**note：端口地址有两种，其取决于机器的物理架构，地址处对应的寄存器存放的数据可以是8bit也可以是16bit，和地址无关。**



## `算术运算类`

### `加`

**add：普通相加(影响FLAGS)**

```asm6502
mov al,78H;01111000
add al,99h;10011001
;al:00010001
;cf(carry):最高为0，所以向前有进位、cf=1(进位标志)
;sf(senior):最高位为0、sf=0			 (最高位标志)
;af(assist):第3位到第4位有进位、af=1  (半加进位标志)
;zf(zero):结果不为0、zf=0			(为0判断)
;pf():1个数为偶数、pf=1
;of(overflaw):次高位进位状态和最高位进位状态相同、of=0
```

**adc：带进位相加(影响FLAGS)**

**add会使进位丢失，adc会保留进位到下一位上去**

![](https://pic.imgdb.cn/item/6191ee6c2ab3f51d9113499b.jpg)

**Note:运算前cf的值是随机的一个值，需要先清0，防止干扰运算CLC**

**inc：加1指令(只影响5个状态位，不影响cf)**

```asm6502
inc ax;ax++、inc：increase
```

### `减`

**SUB：普通减法(影响FLAGS)**

**SBB：带借位减法(影响FLAGS)**

**DEC：减1指令(只影响5个状态位，不影响cf)**

```asm6502
       mov bl,2
NEXT1: mov cx,0FFFFH;最高位为A-F时需要在前面加0，便于编译器识别
NEXT2: dec cx
	   jnz NEXT2	;ZF=0转到NEXT2
	   dec bl
	   jnz NAXT1	;ZF=0转到NEXT1
	   HLT		    ;暂停
```

**NEG：取负数（negative）**

**操作数为0时，cf=0，其他情况，cf=1（有借位）**

**Note：0减去一个负数——对负数取补码，故又名（求补指令）**

**CMP(比较指令，仅影响标志位)**

```asm6502
cmp ax,bx;无符号
;ax>bx、无借位、cf=0
;ax<bx、有借位、cf=1
;ax=bx、cf=1、zf=1
```

```asm6502
cmp ax,bx;有符号
;of AND sf 状态相同、ax>bx
;of AND sf 状态不同、ax<bx
```



### `乘`

**和加减运算指令的区别：对于有符号数和无符号数有不同的助记符号**

**1.MUL（无符号数）、采用`隐含`寻址**

```asm6502
MUL OPRD
;oprd为8位——al*oprd——>ax
;oprd为16位——ax*oprd——>dxax
```

**例子：**

```asm6502
mul byte ptr[bx];在ds段偏移地址位bx的单元（一个byte）和al相乘
```

**2.IMUL（有符号数）、采用`隐含`寻址**



### `除`

**1.DIV（无符号数）（被除数是除数的双倍字长）**

```asm6502
DIV OPRD
;oprd为8位——ax/oprd——>al：商、ah：余数
;oprd为16位——dxax/oprd——>ax：商、dx：余数
```

**2.IDIV（有符号数）**



### `实例`

```asm6502
mov si,1200h
mov word ptr[si],8765h;数据段偏移si的地方写入一个字
mov al,[si];数据段偏移si的地方的内容（一个字节）写给al
inc si
mul byte pty[si];65h*87h——ax=3543h
```

```asm6502
mov si,1200h
mov word ptr[si],8765h
mov ax,[si];数据段偏移si的地方的内容（一个字）写给ax
mul word ptr[si];8765h*8765h——>dx=479bh、ax=add9h
```

**总结：**

**01.使用存储器操作数时，需要用`PTR`声明操作字长**

**02.乘积是乘数的双倍字长，被除数是除数的双倍字长**

## `逻辑运算类`

**01.非运算要求操作数不能是立即数**

**02.除"非运算"，其余指令的执行都会影响除AF外的标志**

**03.无论执行结果如何，都会使标志位OF=CF=0**

**04.非运算不影响任何标志位**

### `与`

```asm6502
and bl,[si];按位相与，写回bl
and al,0fh;al高四位清零，写回al
and ax,ax;操作数不变，使of和cf清零
```

![](https://pic.imgdb.cn/item/6199eab02ab3f51d91fa1336.jpg)

```asm6502
	mov dx,3f8h	;端口大于一个字节使用dx寄存器
again:
	in al,dx	;从dx端口读入一个字节
	and al,02h	;和00000010与（逻辑乘）
	jz again	;al为0继续循环，否者跳出循环
	mov dx,38fh 
	mov ax,data
	out dx,ax
```

### `或`

```asm6502
or cl,0fh;cl高4不变，cl低4为1（逻辑加）
or ax,ax;ax不变，使of=cf=0
```

**eg：将一个2进制的9，变成字符9**

```asm6502
;二进制的9：00001001
;字符9的ASCii码:30h
mov al,9	;00001001
or al,30h	;00111001-39h
```

### `非`

```asm6502
not byte ptr[bx];数据段偏移bx地方的一个字节内容取反再收送回去
```
### `异或`
**Note：相同为0，不同为1（可以看成`相减取绝对值`）**

```asm6502
xor bl,80h;对bl的最高位取反、80h:10000000
xor ax,ax;对ax清零
```

### `测试指令`

**Note：Test的目的在于修改标志位，不计算的 And**

```asm6502
test al,01h;al和01h相与(and)，但不修改al的值
```



## `移位指令`

### `非循环移位Shift`

**`逻辑`：最高/低位移到CF标志位，高/低位补0，不保留符号**

**01.逻辑左移(无符号数)**

```asm6502
shl oprd,1 ;为1时可以直接给出
shl oprd,cl;>=1时必须用cl
```
**02.逻辑右移(无符号数)**

```asm6502
shr oprd,1 ;为1时可以直接给出
shr oprd,cl;>=1时必须用cl
```

**举个例子：**

```asm6502
mov al,68h
mov cl,2
shr al,cl
```
**`算术`：最高/低位移到CF标志位，高/低位补符号位，保留符号**

**01.算术左移(有符号数、补码)**

```asm6502
sal oprd,1 ;为1时可以直接给出
sal oprd,cl;>=1时必须用cl
```

**02.算术右移(有符号数、补码)**

```asm6502
sar oprd,1 ;为1时可以直接给出
sar oprd,cl;>=1时必须用cl
```
**总结：**

**当运算要求保留符号位时，采用算术移位，否者采用逻辑移位，算术移位和逻辑移位都是线性的。**

### `循环移位Rotate`

**不带进位位的循环: 最高位和最低位来回循环，最高/低位放入CF标志位**

**01.左移**

```asm6502
rol 
```

**02.右移**

```asm6502
ror
```

**带进位位的循环:CF参与循环移位，构成大的循环**
**01.左移**

```asm6502
rcl 
```

**02.右移**

```asm6502
rcr
```

**应用：**

**1.测试某些位的状态**

**2.高低位交换**

```asm6502
mov al,12h
mov cl,4
ror al,cl;12h——>21h
```

**3.与非循环移位指令一起组成32位或更长字长数的移位**

**例题如下：**

**Addendum：压缩BCD码使用4位二进制数表示一位十进制数**

![](https://pic.imgdb.cn/item/619a0bfe2ab3f51d9108f62e.jpg)

```asm6502
lea si,m1
lea di,m2
mov ch,4
Next:
	mov al,[si]
	mov bl,al
	and al,0fh;高4位清零
	or al,30h;高4位变成3，相当于加30h
	mov [di],al
	inc di
	mov al,bl
	mov cl,4
	shr al,cl
	or al,30h
	mov [di],al
	inc di
	inc si
	dec ch
	jnz Next
	hlt
```

## `串操作指令`

![](https://pic.imgdb.cn/item/619a2f762ab3f51d91174bd7.jpg)



**Note：SI——Source、DI——Direction**

### `重复前缀`

**01.无条件重复**

**REP——当cx!=0时REP后的指令将继续重复执行**

**02.条件重复**

**REPE(REPZ)——CX!=0 and zf=1（相等——Equal相减为0——Zero）**

**REPNE(REPNZ)——CX!=0 and zf=0（不相等——NE，相减不为0——NZ）**

![](https://pic.imgdb.cn/item/619a35de2ab3f51d911a5eda.jpg)

### `MOVSB和CMPSB`

```asm6502
lea si,mem1
les di,mem2
mov cx,200
cld ;clear df(destination flag清0)
rep movsb;按字节传送
cld
repe cmpsb
jz stop
dec si
mov al,[si]
mov	bx,al
stop:
	hlt
```

### `SCASB和SCASW`

```asm6502
mov di,2000h
mov bx,di
mov cx,10	;查询次数
mov al,'A'	;待查询字符
CLD			;从上往下搜索
repne scasb	;不相等（不等于零）时继续扫描
jz Found	;相等（等于0）时跳出循环（jz——judge zf）
Found:
	dec di
	mov data2,di
	inc di
	sub di,bx;查询次数为di
```

### `LODSB和LODSW`

```asm6502
lodsb ;al<--[ds:si]
lodsw ;ax<--[ds:si]
```

**一般不加重复前缀**

### `STOSB和STOSW`

```asm6502
stosb ;al-->[es:si]
stosw ;ax-->[es:si]
```

## `程序控制指令`

### `转移指令`

**01.JMP（段内、无条件）**

**Note：地址放在寄存器中（16bit）**

```asm6502
jmp lable;段内直接转移
```

```asm6502
mov bx,1200h
jmp bx	;段内间接转移
mov bx,1200
jmp word ptr[bx]
```

**02.JMP FAR(段间、无条件)**

**Note：地址放在内存中（32bit）**

```asm6502
jmp dword ptr[bx];CS：高字节、IP：低字节
```
**03.条件转移指令**

![](https://pic.imgdb.cn/item/619b74be2ab3f51d91938776.jpg)
![](https://pic.imgdb.cn/item/619b74dc2ab3f51d9193969a.jpg)
**例题：**
![](https://pic.imgdb.cn/item/619b74f12ab3f51d9193a635.jpg)

```asm6502
xor al,al
mov plus,al
mov minus,al
mov zero,al
mov cx,100
cld
check:
	lodsb
	or al,al
	js x1
	jz x2
	
x0:	inc plus
x1: inc minus
x2: inc zero
```



### `循环控制`

### `过程调用`

### `中断控制`







**续行符——" \ "**

**汇编语言默认不区分大小写**

**执行结束——不等于—— 汇编结束**

```asm6502
;inc——increase
;dec——decrease
;jmp——jump
;jc——jump carry
;jnz——jump not zero(cx不为0跳转)
;jnc——jump not carry
;lahf——lay low flags to ah
;sahf——
```

**masm有一个不成文的规定，那就是在定义完数据段后，所定义的变量均向后100h个单元，需要我们将ds段寄存器置位，在程序的start:后面加上如下指令：
mov ax,data
mov ds,ax**

# `程序实例`

## `一`

**向内存0:200-0:23F依次传送数据0-63（3FH）**

```asm6502
date SEGMENT
date ENDS
code SEGMENT
    ASSUME cs:code,ds:date
    start:
        mov ax,0    ;初始化段地址
        mov ds,ax
        mov bx,200h ;初始化偏移地址
        mov cx,64   ;循环64-1、共63次
        mov dx,0    ;传入数据
    C:
        mov [bx],dx
        inc dx
        inc bx
        Loop C
        mov ax,4c00h
        int 21h
code ENDS
    END start
```

## `二`

**编写code段代码，用push指令将a段中的word数据逆序存储到b段中**

![](https://pic.imgdb.cn/item/619d89e42ab3f51d91605c08.jpg)

```asm6502
assume cs:code
code SEGMENT
    a SEGMENT
        dw 1,2,3,4,5,6,7,8
    a ENDS
    b SEGMENT
        dw 0,0,0,0,0,0,0,0
    b ENDS
    start:
        mov ax,b    ;初始化
        mov ss,ax
        mov sp,16
        mov ax,a
        mov ds,ax
        mov bx,0
        mov cx,8
    C: 
        mov dx,word ptr [bx]
        push dx
        add bx,2
        loop C
code ENDS
    END start
```

# `补充`
## `MOV 传送代名字项`

```asm6502
date segment
	m1 db 'ABCDEF$'
date ends
code segment
	assume cs:code,ds:date
	start:
		mov ax,date
		mov ds,ax
		mov ax,m1+2		;将m1+2地址指向的内容往后两个字节传给ax
						;低给低、高给高
code ends
	end start

```

## `数据段定义内容存放`

```asm6502
date segment
	m1 db 'abcdefg';低——>高:abcdefg
	;只有db可以在一个''内合起来定义，其他的不可以合起来
	m2 dw 'AB','CD','EF';低——>高:BADCEF
date ends
```

## `数据段向寄存器传送内容`

**无论数段如何定义，始终低地址给低位，高地址给高位**



