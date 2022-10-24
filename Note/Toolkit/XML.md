## XML



## DTD

## Schema

### 基本结构

```xml
<?xml version="1.0" encoding="UTF-8"?>
<?xml name space 前缀 - xs, 所以使用schema定义好的类型需要加上前缀xs:?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified" attributeFormDefault="unqualified">
    <xs:element name="city"/>
</xs:schema>
```

**Note: 根元素必须存在且必须是xs:schema**

---

### 数据类型

#### 内置数据类型

```xml
<xs:element name="数字" type="xs:long"/>
<xs:element name="字符串" type="xs:string"/>
<xs:element name="整数" type="xs:integer"/>
```

```bash
string：字符串数据
boolean布尔型：元素只能取真（True）或假（False）的值。
time：时间型，格式为HH:MM:SS，每天是重复的。
date：表示日期，格式是YYYY-MM-DD。
dateTime：日期时间型，其形式为YYYY-MM-DDThh:mm:ss。
duration:表示持续的时间
decimal任意精度和位数的十进制数
float：标准单精度32位浮点数，如12.88
double：表示双精度64位浮点数
anyURI：代表一个URI,用来定位文件
long：整型数-263—+263-1
int： 整型数-231—+231-1（由long导出）
integer：整数
negativeInteger仅包含负值的整数 ( .., -2, -1.)由integer导出
nonNegativeInteger仅包含非负值的整数 (0, 1, 2, ..)
nonPositiveInteger仅包含非正值的整数 (.., -2, -1, 0)
positiveInteger仅包含正值的整数 (1, 2, ..)
```

**Note: 内置数据类型直接用即可，记得带上xs:**

#### 简单数据类型

```xml
<?定义一个0-100的整数?>
<xs:simpleType name="number" >
    <?基于integer?>
    <xs:restriction base="xs:integer">
        <?最小值?>
        <xs:minInclusive value="0"></xs:minInclusive>
        <?最大值?>
        <xs:maxInclusive value="100"></xs:maxInclusive>
    </xs:restriction>
</xs:simpleType>
<?使用上述定义的数据类型?>
<xs:element name="score" type="number"></xs:element>
```

```xml
<?定义一个只能取male or female的枚举类型数据sex?>
<xs:simpleType name="sex">
    <xs:restriction base="xs:string">
        <xs:enumeration value="male"></xs:enumeration>
        <xs:enumeration value="female"></xs:enumeration>
    </xs:restriction>
</xs:simpleType>
```

```xml
<xs:simpleType name="phone">
    <xs:restriction base="xs:string">
        <?长度为8?>
        <xs:length value="8"></xs:length>
        <?匹配模式dddd-ddd?>
        <xs:pattern value="\d{4}-\d{3}"></xs:pattern>
    </xs:restriction>
</xs:simpleType>
```

#### 复杂数据类型

**Note: 复杂类型就是定义子元素和属性，一定要先定义子元素以何种方式出现，如Sequence**

```xml
<?定义一个复杂数据address?>
<xs:complexType name="address">
    <?定义一个序列?>
    <xs:sequence>
        <xs:element name="street" type="xs:string"/>
        <xs:element name="city" type="xs:string"/>
        <xs:element name="state" type="xs:string"/>
        <xs:element name="zip" type="xs:string"/>
    </xs:sequence>
</xs:complexType>
<xs:element name="QDAddress" type="address"/>
```

---

### 元素声明

#### Schema和DTD的区别

![](https://pic1.imgdb.cn/item/634ce7a416f2c2beb1ade993.jpg)

#### 简单样例

```xml
<xs:element name="number" type="xs:string" fixed="001"></xs:element> 
```

#### 复杂样例

```xml
<xs:complexType name="student_type">
    <xs:sequence>
        <xs:element name="stu" type="stu_type"/>
    </xs:sequence>
</xs:complexType>
<xs:element name="students" type="student_type"/>
```

#### 匿名类型样例

**Note: 对于定义在元素内的类型可以不命名**

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified" attributeFormDefault="unqualified">
	<xs:element name="students">
		<xs:complexType>
			<xs:sequence>
				<xs:element name="stu" type="stu_type"/>
			</xs:sequence>
		</xs:complexType>
	</xs:element>
</xs:schema>
```

#### 小练习

```xml
<students> 
    <stu>
        <id>2</id>
        <name>张三</name> 
        <sex>男</sex> 
    </stu> 
    <stu> 
        <id>2</id> 
        <name>李四</name> 
        <sex>女</sex> 
    </stu> 
</students> 
```

```xml
<xs:simpleType name="sex_type">
    <xs:restriction base="xs:string">
        <xs:enumeration value="男"/>
        <xs:enumeration value="女"/>
    </xs:restriction>
</xs:simpleType>
<xs:complexType name="stu_type">
    <xs:sequence>
        <xs:element name="id" type="xs:integer"/>
        <xs:element name="name" type="xs:string"/>
        <xs:element name="sex" type="sex_type"/>
    </xs:sequence>
</xs:complexType>
<xs:complexType name="student_type">
    <xs:sequence>
        <xs:element name="stu" type="stu_type"/>
    </xs:sequence>
</xs:complexType>
<xs:element name="students" type="student_type"/>
```

### 属性声明

```xml
<xs:attribute name=“编号”type=“xs:integer”use=“required”/>
<xs:attribute name =“年龄”type=“xs:string” use=“optional”/>
<xs:attribute name=“电话”type=“xs:string”use=“prohibited”/>
```

### 练习

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified" attributeFormDefault="unqualified">
	<xs:simpleType name="id_type">
		<xs:restriction base="xs:string">
			<xs:length value="8"/>
			<xs:pattern value="[2][0][1][9]\d{4}"/>
		</xs:restriction>
	</xs:simpleType>
	<xs:simpleType name="name_type">
		<xs:restriction base="xs:string">
			<xs:pattern value="[\\u4e00-\\u9fa5]"/>
		</xs:restriction>
	</xs:simpleType>
	<xs:simpleType name="sex_type">
		<xs:restriction base="xs:string">
			<xs:enumeration value="男"/>
			<xs:enumeration value="女"/>
		</xs:restriction>
	</xs:simpleType>
	<xs:simpleType name="tel_type">
		<xs:restriction base="xs:string">
			<xs:length value="11"/>
			<xs:pattern value="/^(13[0-9]|14[01456879]|15[0-35-9]|16[2567]|17[0-8]|18[0-9]|19[0-35-9])\d{8}$/"/>
		</xs:restriction>
	</xs:simpleType>
	<xs:complexType name="stu_type">
		<xs:sequence>
			<xs:element name="id" type="id_type"/>
			<xs:element name="name" type="name_type"/>
			<xs:element name="sex" type="sex_type"/>
			<xs:element name="birthDate" type="xs:date"/>
			<xs:element name="tel" type="tel_type"/>
		</xs:sequence>
	</xs:complexType>
	<xs:complexType name="students_type">
		<xs:all>
			<xs:element name="stu" type="stu_type"/>
		</xs:all>
	</xs:complexType>
	<xs:element name="students" type="students_type"/>
</xs:schema>
```

### 元素和属性限定

#### 元素个数限制

```xml
<xs:complexType name="Orders_type">
	<xs:sequence>
		<xs:element name="Order" type="Order_type" minOccurs="1" maxOccurs="unbounded"/>
	</xs:sequence>
</xs:complexType>
```

#### 元素值唯一

![](https://pic1.imgdb.cn/item/63560a8d16f2c2beb14e8882.png)

#### 属性值唯一

![](https://pic1.imgdb.cn/item/63560a8d16f2c2beb14e8885.png)

### 元素和属性组

#### 元素组

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified" attributeFormDefault="unqualified">
	<xs:group name="myGroup">
		<xs:sequence>
			<xs:element name="haha"/>
			<xs:element name="nihao"/>
		</xs:sequence>
	</xs:group>
	<xs:complexType name="temp">
		<xs:sequence>
			<xs:group ref="myGroup"/>
		</xs:sequence>
	</xs:complexType>
</xs:schema>
```

#### 属性组

```xml
<?xml version="1.0" encoding="UTF-8"?>
<xs:schema xmlns:xs="http://www.w3.org/2001/XMLSchema" elementFormDefault="qualified" attributeFormDefault="unqualified">
	<xs:attributeGroup name="myAttributeGroup">
		<xs:attribute name="press" type="xs:string"/>
		<xs:attribute name="ISBN" type="xs:string"/>
	</xs:attributeGroup>
	<xs:element name="book">
		<xs:complexType>
			<xs:attributeGroup ref="myAttributeGroup"/>
		</xs:complexType>
	</xs:element>
</xs:schema>
```



### 模式重用

#### Include

```xml
<?xml version="1.0" encoding="UTF-8"?>
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="www.a/b">
	<simpleType name="bid">
		<restriction base="string">
			<pattern value="[A]\d{4}"
		</restriction>
	</simpleType>
</schema>
```

```xml
<?xml version="1.0" encoding="UTF-8"?>
<schema xmlns="http://www.w3.org/2001/XMLSchema" targetNamespace="www.a/b">
	<simpleType name="aid">
		<restriction base="string">
			<pattern value="[c]\d{4}"
		</restriction>
	</simpleType>
</schema>
```

```xml
```





#### Import

