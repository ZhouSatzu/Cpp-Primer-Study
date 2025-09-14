# Ch01_Exercise

## Exercise1.1

> 查阅你使用的编译器的文档，确定它所使用的文件名约定。编译并运行第2页的main程序。
> 

[GCC and File Extensions - Development with GNU/Linux - labor-liber](http://labor-liber.org/en/gnu-linux/development/index.php?diapo=extensions)

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

## Exercise 1.2

> 改写程序，让它返回-1。返回值-1通常被当做程序错误的标识。重新编译并运行你的程序，观察你的系统如何处理main返回的错误标识。
> 

.exe (进程 41100)已退出，代码为 -1 (0xffffffff)

## Exercise 1.3

> 编写程序，在标准输出上打印Hello, World。
> 

```cpp
#include <iostream>

int main()
{
	std::cout << "Hello, World" << std::endl;
	return 0;
}
```

## Exercise 1.4

> 我们的程序使用加法运算符`+`来将两个数相加。编写程序使用乘法运算符`*`，来打印两个数的积。
> 

```cpp
#include <iostream>

int main()
{
    std::cout << "Enter two numbers:" << std::endl;
    int v1 = 0, v2 = 0;
    std::cin >> v1 >> v2;
    std::cout << "The product of " << v1 << " and " << v2
              << " is " << v1 * v2 << std::endl;
}        
```

## Exercise 1.5

> 我们将所有的输出操作放在一条很长的语句中，重写程序，将每个运算对象的打印操作放在一条独立的语句中。
> 

```cpp
#include <iostream>

int main()
{
    std::cout << "Enter two numbers:" << std::endl;
    int v1 = 0, v2 = 0;
    std::cin >> v1 >> v2;
    std::cout << "The product of ";
    std::cout << v1;
    std::cout << " and ";
    std::cout << v2;
    std::cout << " is ";
    std::cout << v1 * v2;
    std::cout << std::endl;
}
```

## Exercise 1.6

> 解释下面程序片段是否合法。
> 
> 
> ```cpp
> std::cout << "The sum of " << v1;
>           << " and " << v2;
>           << " is " << v1 + v2 << std::endl;
> ```
> 
> 如果程序是合法的，它的输出是什么？如果程序不合法，原因何在？应该如何修正？
> 

不合法。第二行和第三行则是以流插入操作符`<<`开始的，但是它们前面没有提供输出流对象（例如`std::cout`）

## Exercise 1.7

> 编译一个包含不正确的嵌套注释的程序，观察编译器返回的错误信息。
> 
> 
> ```cpp
> /* 正常注释 /* 嵌套注释 */ 正常注释*/
> ```
> 

错误	C2143	语法错误: 缺少“;”(在“*”的前面)
错误	C4430	缺少类型说明符 - 假定为 int。注意: C++ 不支持默认 int	
错误	C2059	语法错误:“/”	

## Exercise 1.8

> 指出下列哪些输出语句是合法的（如果有的话）：
> 
> 
> ```cpp
> std::cout << "/*";
> std::cout << "*/";
> std::cout << /* "*/" */;
> std::cout << /* "*/" /* "/*" */;
> ```
> 
> 预测编译这些语句会产生什么样的结果，实际编译这些语句来验证你的答案(编写一个小程序，每次将上述一条语句作为其主体)，改正每个编译错误。
> 

第三行为错，改正：

```cpp
std::cout << /* "*/" */";
```

## Exercise 1.9

> 编写程序，使用`while`循环将50到100整数相加。
> 

```cpp
#include <iostream>
int main()
{
    int sum = 0, val = 50;
    while (val <= 100){
        sum += val;
        val += 1;
    }
    std::cout << "Sum of 50 to 100 inclusive is "
              << sum << std::endl;
}
```

## Exercise 1.10

> 除了`++`运算符将运算对象的值增加1之外，还有一个递减运算符`--`实现将值减少1.编写程序与，使用递减运算符在循环中按递减顺序打印出10到0之间的整数。
> 

```cpp
#include <iostream>
int main()
{
    int val = 10;
    while (val >= 0){
        std::cout << val << " ";
        val -= 1;
    }
    std::cout << std::endl;
}
```

## Exercise 1.11

> 编写程序，提示用户输入两个整数，打印出这两个整数所指定的范围内的所有整数。
> 

```cpp
#include <iostream>

int main()
{
    int start = 0, end = 0;
    std::cout << "Please input two num: ";
    std::cin >> start >> end;
    if (start <= end) {
        while (start <= end){
            std::cout << start << " ";
            ++start;
        }
        std::cout << std::endl;
    }
    else{
        std::cout << "start should be smaller than end !!!";
    }
}  
```

## Exercise 1.12

> 下面的for循环完成了什么功能？sum的终值是多少？
> 
> 
> ```cpp
> int sum = 0;
> for (int i = -100; i <= 100; ++i)
> 	sum += i;
> ```
> 

从-100加到100，sum的终值是0。

## Exercise 1.13

> 使用for循环重做1.4.1节中的所有练习（练习1.9到1.11）。
> 

**练习1.9**

```cpp
#include <iostream>
int main()
{
    int sum = 0;
    for (int val = 50; val <= 100; ++val){
        sum += val;
    }
    std::cout << "Sum of 50 to 100 inclusive is "
              << sum << std::endl;
}
```

**练习1.10**

```cpp
#include <iostream>
int main()
{
    for (int val = 10; val >=0; --val){
        std::cout << val << " ";
    }
    std::cout << std::endl;
}
```

**练习1.11**

```cpp
#include <iostream>
int main()
{
    int start = 0, end = 0;
    std::cout << "Please input two num: ";
    std::cin >> start >> end;
    if (start <= end) {
        for (; start <= end; ++start){
            std::cout << start << " ";
        }
        std::cout << std::endl;
    }
    else{
        std::cout << "start should be smaller than end !!!";
    }
}
```

## Exercise 1.14

> 对比for循环和while循环，两种形式的优缺点各是什么？
> 

两种循环的选择主要是取决于循环是基于计数器还是基于条件

## Exercise 1.15

> 编写程序，包含第14页“再探编译”中讨论的常见错误。熟悉编译器生成的错误信息。
> 

编译器可以检查出的错误有：语法错误、类型错误、声明错误

## Exercise 1.16

> 编写程序，从cin读取一组数，输出其和。
> 

```cpp
#include <iostream>

int main()
{
    int sum = 0;
    for (int value = 0; std::cin >> value; )
        sum += value;
    std::cout << sum << std::endl;
    return 0;
}
```

## Exercise 1.17-18

> 编译并运行本节的程序，给它输入全都相等的值。再次运行程序，输入没有重复的值。
> 

全部重复：

```cpp
1 1 1 1 1
1 occurs 5 times
```

没有重复：

```cpp
1 2 3 4 5
1 occurs 1 times 
2 occurs 1 times 
3 occurs 1 times 
4 occurs 1 times 
5 occurs 1 times 
```

## Exercise 1.19

> 修改你为1.4.1节练习1.11（第11页）所编写的程序（打印一个范围内的数），使其能处理用户输入的第一个数比第二个数小的情况。
> 

```cpp
#include <iostream>
int main()
{
    int start = 0, end = 0;
    std::cout << "Please input two num: ";
    std::cin >> start >> end;
    if (start <= end) {
        while (start <= end){
            std::cout << start << " ";
            ++start;
        }
        std::cout << std::endl;
    }
    else{
        std::cout << "start should be smaller than end !!!";
    }
}
```