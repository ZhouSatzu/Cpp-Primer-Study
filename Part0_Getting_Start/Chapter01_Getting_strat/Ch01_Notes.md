# Ch01_Notes

## 1.1 编写一个简单的C++程序

C++程序包含一个或多个函数（function）,必须含有一个**`main`**函数。

一个函数的定义包含四部分：返回类型（return type）、函数名（function name）、由括号包围的且允许为空的形参列表（parameter list）以及函数体（function body）。

main函数的返回类型必须为int。int为一种内置类型（built-in-type）,即语言自身定义的类型。

### 1.1.1 编译、运行程序

**程序源文件命名约定**

源文件指的是程序文件

**从命令行运行编译器**（**MSVC**）

基本编译

```bash
cl source.cpp
# 生成 source.exe 和 source.obj
```

标准编译

```bash
cl /EHsc source.cpp
# /EHsc：启用C++异常处理，是标准做法。
# 生成 source.exe
```

编译多个源文件

```bash
cl /EHsc /Fe:my_app.exe main.cpp helper.cpp utils.cpp
# 将多个.cpp文件一起编译链接成一个可执行文件。
```

运行可执行文件

```bash
.\source.exe
```

## 1.2 初识输入输出

iostream库包含两个基础类型：istream和ostream，表示输入流和输出流。

**标准输入输出对象**

标准库（standard liarbry）定义了4个IO对象。

标准输入：名为`cin`的istream类型的对象。

标准输出：名为`cout` 的ostream类型的对象。

使用`cerr`来输出警告和错误信息，`clog`来输出程序运行时的一般性信息

**一个使用IO库的程序**

```cpp
#include <iostream>

int main()
{
	std::cout << "Enter two numbers: " << std::endl;
	int v1 = 0, v2 = 0;
	std::cin >> v1 >> v2;
	std::cout << "The sum of " << v1 << " and " << v2 << " is " << v1 + v2 << std::endl;
	return 0;
}
```

程序的第一行`#include <iostream>` 告诉编译器使用iostream库。

**向流写入数据**

```cpp
std::cout << "Enter two numbers: " << std::endl;
```

语句执行了一个表达式（expression）。在C++中表达式产生一个计算结果，它由一个或多个运算对象和一个运算符组成。该语句中使用了输出运算符`<<` 在标准输出上打印消息。

`<<` 运算符接受两个运算对象，左侧对象必须是一个ostream对象，右侧对象是要打印的值。此运算符将给定的值写到给定的ostream对象中去。

`endl` 是一个操作符（manipulator）的特殊值，效果是结束当前行，并将设备关联的缓冲区（buffer）中的内容刷到设备中。

**使用标准库中的名字**

前缀`std::`指出cout和endl是定义在名为std的命名空间（namespace）中的，其中`::`是作用运算符。

**从流中读取数据**

```cpp
int v1 = 0, v2 = 0;
```

定义两个int类型的变量（variable）来保存输出，先将其初始化（initialize）为0。

## 1.3 注释简介

**C++中注释的种类**

C++中有两种注释（comments）：单行注释和界定符对注释。

单行注释以`//`开始，以换行符结束。

界定符对注释以`/*`开始，以`*/`结束。注意注释界定符不能嵌套。

## 1.4 控制流

### 1.4.1 while语句

`while`语句会反复执行一段代码，直至给定条件为假为止。其形式为：

```cpp
while(condition)
	statement
```

`while`语句的执行过程是交替的检测`condition`条件和执行关联语句的`statement`，直至condition为假时停止。若condition为真，则执行statement，每当执行statement之后，再次检测condition，直至condition为假为止。

### 1.4.2 for语句

for语句包含两部分：循环头和循环体。

```cpp
for (int val = 1; val <= 10; ++val)
	sum += val;
```

循环头有三部分组成：一个初始化语句（init-statement）、一个循环条件（condition）以及一个表达式。

在本例中，初始化语句为`int val = 1` ，定义了一个名为val的int型变量，只能在for循环内部使用。循环条件`val <= 10` ，循环体每次执行前都会检查循环条件，只要val小于等于10就会执行循环体。表达式为`++val` ，表达式在循环体之后进行。

### 1.4.3 读取数量不定的输入数据

```cpp
#include <iostream>

int main()
{
	int sum = 0, value = 0;
	while (std::cin >> value)
	{
		sum += value;
	}
	std::cout << "Sum is: " << sum << std::endl;
	return 0;
}
```

通过`while`循环读取数据，`std::cin >> value`从标准输入中读取下一个数，保存在`value`中。当我们使用istream对象作为条件是，起效果是检测流的状态，当遇到文件结束符（end-of-file 注：Windows系统中EOF为Ctrl+Z）或遇到无效输入时，istream对象就会处于无效状态，使条件变假。

### 1.4.4 if语句

```cpp
#include <iostream>
//统计每个值连续出现了多少次
int main()
{
	int currVal = 0, val = 0;
	if (std::cin >> currVal) 
	{
		int cnt = 1;
		while (std::cin >> val) 
		{
			if (val == currVal) 
			{
				++cnt;
			} 
			else 
			{
				std::cout << currVal << " occurs " << cnt << " times" << std::endl;
				currVal = val;
				cnt = 1;
			}
		}
		std::cout << currVal << " occurs " << cnt << " times" << std::endl;
	} 
	else
	{
		std::cout << "No data?!" << std::endl;
	}
	return 0;
}
```

`if`是一个判断语句，其中使用了`==`相等运算符。在c++中`=`用于赋值，`==`用于相等判断。

## 1.5 类简介

在C++中，我们通过定义一个类（`calss`）来定义自己的数据结构（data structure）。

通常使用`.h`作为头文件的后缀

### 1.5.1 Sales_item类

每个类都定义了一个新的类型，其类型名就为类名。与内置类型一样，可以定义类类型（class type）的变量。

```cpp
Sales_item item;
```

表达了item是Sales_item类型的对象。

### 1.5.2 初识成员函数

```cpp
item1.isbn() == item2.isbn()
```

调用了名为isbn的成员函数（member function）。成员函数是定义为类的一部分的函数，有时被称为方法（method）。通常使用一个类对象的名义来调用成员函数。`.`点运算符只能用于类类型的对象，左侧是一个类类型的对象，右侧是该类型的一个成员名。