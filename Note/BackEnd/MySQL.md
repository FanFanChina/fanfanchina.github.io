## MySQL安装

### Windows

**[MySQL 安装](https://www.bilibili.com/video/BV1UE41147KC?p=4)**


## 基本语法

### 普通查询

```sql
-- 选取全部列
use sql_store;				#使用sql_store数据库
select * from customers		 #获取customers的所有列
where customer_id = 1		 #添加限制条件————id = 1
```

```sql
-- 选取多列
use sql_store;
select first_name, last_name from customers
```

```sql
-- 选取时进行运算
use sql_store;
select 
    points,
    points*10+5
    from customers
```

```sql
-- 选取时起别名
use sql_store;
select 
	points as hahaha,
    points * 10 + 5 as ' biubiubiu' -- 附加空格时加上'或"
    from customers
```

### 添加数值条件

```sql
-- 限定整数
use sql_store;
select * from customers
	where points > 2000
```

```sql
-- 限定字符串   
use sql_store;
select * from customers
	where state = 'VA' -- state = 'va'也可以,不分大小写
```

```sql
-- 限定字符串  
use sql_store;
select * from customers
	where state != 'VA'  #state <> 'va'也可以
```

```sql
-- 限定日期
use sql_store;
select * from customers
	where birth_date > '1990-01-01'
```

### 添加多个数值条件

```sql
-- and
use sql_store;
select * from customers
	where birth_date >= '1990-01-01' and points > 1000
```

```sql
-- or
use sql_store;
select * from customers
	where birth_date >= '1990-01-01' or points > 1000
```

```sql
-- and > or
use sql_store;
select * from customers
	where birth_date >= '1990-01-01' or points > 1000 
		  and state = 'VA' 		
```

```sql
-- not
use sql_store;
select * from customers
	where not(birth_date >= '1990-01-01' or points > 1000)
```

### `简化多个数值条件`

####  `OR到IN`

```sql
-- or简化为in
use sql_store;
select * from customers
	where state in ('VA','FL','GA')		  
```

```sql
-- NOT + IN
use sql_store;
select * from customers
	where state not in ('VA','FL','GA')		   		
```

#### `BETWEEN`

```sql
use sql_store;
select * from customers
	where points  between 1000 and 3000
```

```sql
-- 小练习
use sql_store;
select * from customers
	where birth_date  between '1990-01-01' and '2000-01-01'
```

### `添加包含条件` 

#### `LIKE`

```sql
# %
use sql_store;
select * from customers
	where last_name like 'B%' 	#B打头
--  where last_name like '%B%' 	#含B
--  where last_name like '%B' 	#B结尾
```

```sql
# _
use sql_store;
select * from customers
	where last_name like 'b____y' 
```

```sql
# 小练习1
use sql_store;
select * from customers
	where address like '%TRAIL%'  or
		  address like '%AVENUE%' 
```

```sql
# 小练习2
use sql_store;
select * from customers
	where phone like '%9'
```

#### `REGEXP`

```sql
use sql_store;
select *
from customers
where last_name regexp 'field' -- 包含field
where last_name regexp '^field' -- 以field开头
where last_name regexp 'field$' -- 以field结尾
where last_name regexp '^field|mac|rose' -- 包含以field开头 or mac or rose
where last_name regexp '[gim]e[pq]' -- 包含e，且e前为 g or i or m,e后为 p or q
where last_name regexp '[a-h]e' -- 包含e，且e前为a到h
```

```sql
# 小练习
where first_name = 'ELKA' or first_name = 'AMBUR';
where last_name like '%EY' or last_name like '%ON'
where last_name like 'MY%' or last_name regexp 'SE'
where last_name regexp 'B[RU]'
```

### `其他限制条件`

#### `NULL`

```sql
use sql_store;
select *
from customers
where phone is null -- 缺失
where phone is not null -- 非缺失
```

#### `DISTINCT`

```sql
-- 对列去重 
-- distinct + 列名
use sql_store;
select distinct state from customers
```

### `查询后数据处理`

#### `ORDER`

```sql
use sql_store;
select *
from customers
order by first_name -- 按first_name 升序
order by first_name desc -- 按first_name 降序
order by state, first_name -- 按state升序，每一种state的分支按first_name 升序
```

```sql
-- 小练习
select * 
from order_items
where order_id = 2
order by quantity * unit_price desc 
```

#### `LIMIT`

```sql
select *
from customers
limit 3 -- 获取前三位顾客
limit 6, 3 -- 获取7， 8， 9 位顾客 
-- 练习
order by points desc
limit 3
-- limit语句一定要放在select语句的最后面
```

## `进阶语法`

### `表连接`

#### `库内连接`

**同一数据库内的表的连接**

```sql
-- 选取orders和customers的所有列
-- 对齐条件：二表customer_id相等
use sql_store;
select * 
from orders
join customers on orders.customer_id = customers.customer_id 
```

```sql
-- 选取同名列时需要标注表名
-- 可以对二表起别名
-- 对齐条件：customer_id相等
use sql_store;
select o.customer_id, first_name, last_name, order_date
from orders o
join customers c 
on o.customer_id = c.customer_id
```

```sql
-- 小练习
use sql_store;
select order_id, oi.product_id, quantity, oi.unit_price
from order_items oi
join products p
on oi.product_id = p.product_id
```

#### `库间连接`

**不同数据库的表的连接**

```sql
-- 给不在当前数据库的表加上前缀即可
use sql_store;
select *
from order_items oi 
join sql_inventory.products p
	on oi.product_id = p.product_id 
```

```sql
-- 三表连接
-- 加一句jion on即可
use sql_store;
select 
	o.order_id,
    c.customer_id,
    o.order_date,
    os.name as status
from customers c
join orders o
	on c.customer_id = o.customer_id
join order_statuses os
	on  o.status = os.order_status_id
```

#### `自连接`

**表自己连接自己**

```sql
-- 自连接要求表内有自循环
-- 起不同的别名即可
use sql_hr;
select *
from employees e
join employees m
	on e.reports_to = m.employee_id
```

```sql
-- 简化表
use sql_hr;
select 
	e.employee_id, 
	e.first_name, 
    m.first_name as manager
from employees e
join employees m 
	on e.reports_to = m.employee_id
```

#### `复合连接`

```sql
-- 一列不能唯一标识全部行的情况
-- 用and条件使用多列标识全部行
use sql_store;
select *
from order_items oi
join order_item_notes oin
	on oi.order_id = oin.order_id
    and oi.product_id = oin.product_id
```

#### `隐式连接`

```sql
-- 尽量不要使用
use sql_store;
select *
from customers c, orders o
where c.customer_id = o.customer_id
```

#### `外连接`

```sql
-- left join
-- 左边无论符不符合条件都会被返回
use sql_store;
select
	c.customer_id,
	c.first_name,
    o.status
from customers c
left join orders o
	on c.customer_id = o.customer_id
```

```sql
-- right join 右连接
-- 右边无论符不符合条件都会被返回
use sql_store;
select
	c.customer_id,
	c.first_name,
    o.order_id
from  orders o
right join customers c
	on c.customer_id = o.customer_id
-- 转换位置可以使用任意使用左右连接
```

#### `多表外连接`

```sql
-- 多表连接尽量只使用左连接
use sql_store;
select 
	c.customer_id,
    c.first_name,
    o.shipper_id,
    sh.name as shipper
from customers c
left join orders o
	on c.customer_id = o.customer_id
left join shippers sh
	on o.shipper_id = sh.shipper_id
```

#### `自外连接`

**表自己和自己外连接**

```sql
use sql_hr;
select 
	e.employee_id,
    e.first_name,
    m.first_name as manager
from employees e
left join employees m
	on e.reports_to = m.employee_id
```



#### `自然连接`

```sql
-- 不添加连接条件，让软件自己判断
-- 无法控制，比较危险
use sql_invoicing;
select *
from clients c
join invoices i
```

#### `交叉连接`

```sql
-- cross join
-- 一对多连接
-- 显式写法
use sql_store;
select 
	c.first_name as customer,
    p.name as product
from customers c 
cross join products p
order by customer
```

```sql
-- 隐式写法
use sql_store;
select 
	c.first_name as customer,
    p.name as product
from customers c, products p
order by customer
```

### `表连接语法简化`

#### `USING`

```sql
-- using只能在两个表中有相同列名时才能使用
use sql_store;
select 
	c.customer_id,
    c.first_name,
    o.order_id,
    sh.name as shipper
from orders o
join customers c
	using(customer_id)
join shippers sh
	using(shipper_id)
```

```sql
-- 亦可以来替换复合连接
use sql_store;
select *
from order_items oi
join order_item_notes oin
	using(order_id,product_id)
```



### `修改表`

#### `INTERT ROW`

![](https://pic.imgdb.cn/item/626539e8239250f7c5c9f502.jpg)

**AI：自动递增属性，当给插入数据但不给customer_id赋值时，customer_id会自动赋值为上一行 + 1**

```sql
-- 常规插入一行
use sql_store;
insert into customers
values
(
	default, 
	'Jone', 
	'Smith', 
	NULL,
	default,
	'dada',
	'da',
	'CA',
	default
)
```

```sql
-- 选几列插入
-- 未赋值的列默认为default值
use sql_store;
insert into customers
(
	first_name,
    last_name,
    address,
    city,
    state
)
values
(
	'Jone', 
	'Smith', 
	'dada',
	'da',
	'CA'
)
```

```sql
-- 插入多行
use sql_store;
insert into shippers (name)
values ("shipper1"), ("shipper2"), ("shipper3")
```

#### `CREATE TABLE`

```sql
-- 子查询复制orders表，忽略属性
use sql_store;
create table orders_backup as 
select * from orders
```

```sql
-- 子查询复制部分orders的表
use sql_store;
create table orders_backup 
select * 
from orders
where order_date < '2019-01-01'
```

#### `UPDATE ROW`

```sql
-- 更新单行
use sql_invoicing;
update invoices
set payment_total = 10,
	payment_date = '2019-03-01'
where invoice_id = 1  -- 指定列
```

```sql
use sql_invoicing;
update invoices
set payment_total = payment_total * 0.5,
	payment_date = '2019-03-01'
where invoice_id = 1  -- 指定行
```

```sql
-- 更新多行
use sql_invoicing;
update invoices
set payment_total = payment_total * 0.5,
	payment_date = '2019-03-01'
where invoice_id in (1, 2)
```

```sql
-- update子查询
use sql_invoicing;
update invoices
set payment_total = payment_total * 0.5,
	payment_date = '2019-03-01'
where invoice_id = 
	(	select client_id 
		from clients
		where name = 'Myworks'
	)
```

```sql
-- 多条语句时用in合并
use sql_invoicing;
update invoices
set payment_total = payment_total * 0.5,
	payment_date = '2019-03-01'
where invoice_id in 
(	select client_id 
	from clients
	where name in 
	(
		'Myworks',
		'Hahah'
	)
)
```

#### `DELETE ROW`

```sql
use sql_invoicing;
delete from invoices -- 删除整个invoices
```

```sql
use sql_invoicing;
delete from invoices
where invoice_id = 
(
	select *
    from clients
    where name = 'Myworks'
)
```

### `查询的联合`

```sql
-- 表内联合
-- 第一段查询决定列名
use sql_store;
select 
	order_id as id,
    order_date as date,
    'Active' as status
from orders
where order_date >= '2019-01-01'
union
select 
	order_id as id,
    order_date as date,
    'Actived' as status
from orders
where order_date < '2019-01-01'
```

```sql
-- 列数相等即可，第一个查询决定列名
use sql_store;
select 
	first_name
from customers
union
select 
	shipper_id
from shippers
```

## `高阶语法`



### `聚合函数`

**由多个数据传入函数得出单一数据 —— 聚合，聚合函数的参数是列**

#### `常见聚合`

**以下为查询时使用的聚合函数**

```sql
use sql_invoicing;
select
	max(invoice_total) as highest, 	-- 最大值
    min(invoice_total) as lowest,  	-- 最小值
    avg(invoice_total) as average, 	-- 平均值
    sum(invoice_total) as total,  	-- 求和
    count(invoice_total) as count, 	-- 计算行数跳过NULL
    count(*)					  -- 计算行数但不跳过NULL
from invoices
```

**Note：聚合函数传入列名只对非NULL值有效，使用COUNT时不计入NULL的一行，除非使用COUNT（*）**

```sql
-- 也可以加限定条件
use sql_invoicing;
select
	max(invoice_total) as highest,
    min(invoice_total) as lowest,
    avg(invoice_total) as average,
    sum(invoice_total) as total
from invoices
where payment_date > '2017-07-01'
```

```sql
-- 统计并去重
use sql_invoicing;
select
	max(invoice_total) as highest,
    min(invoice_total) as lowest,
    avg(invoice_total) as average,
    sum(distinct client_id) as total
from invoices
where payment_date > '2017-07-01'
```

****

**以下为查询完使用的聚合**

#### `GROUP BY`

**对列内不同同名称的行分到不同组，相同的分到同一组**

```sql
-- 单列分组
use sql_invoicing;
select
	client_id,
    sum(invoice_total) as total
from invoices
group by client_id
order by total desc
```

```sql
-- 多列分组
use sql_invoicing;
select 
	p.date,
    pm.name as payment_method,
    sum(p.amount) as total_payments
from payments p
join payment_methods pm
	on p.payment_method = pm.payment_method_id
group by date, payment_method
order by date
```

#### `HAVING`

**对列进行分组之后我们不知道每一行的数据就无法使用where筛选行，于是我们引入了having对分组后进行筛选**

```sql
use sql_invoicing;
select 
	client_id,
    sum(invoice_total) as total
from invoices
group by client_id
having total > 500
```

**Note：where可以筛选选中表单中任意的列，但having只能筛选分组时select的列**

#### `ROLLUP`

**一、仅对聚合的列进行求和**

**二、可以看成对数据分组进行求和，如果每个分组有子分组时（多列分组的情况），还要对子分组进行求和**

```sql
-- 单列分组ROLLUP
use sql_invoicing;
select 
	client_id,
    sum(invoice_total) as total 
from invoices
group by client_id with ROLLUP
```

```sql
-- 多列分组ROLLUP
use sql_invoicing;
select 
	state,
    city,
    sum(invoice_total) as total 
from invoices i
join clients c using (client_id)
group by state, city with ROLLUP
```


### `复杂查询`

**待更**

### `SQL基本函数`

**待更**

### `视图`

**待更**

### `存储过程`

**待更**

### `触发器`

**待更**