C++刷题
```
2. 下列语句中，错误的是
答案：B
A）const double *point;
B）const int temp;
C）const double *rt=new double(5.5);
D）const int buffer=256;
```
在定义变量时，如果加上关键字const，则这种变量就是常变量，常变量在定义时必须要同时初始化。

```
4. 有如下程序：
   #include <iostream>
   using namespace std;
   int main()
   {
       int *p;
       *p = 9;
       cout << "The value at p: " << *p;
       return 0;
   }
编译运行程序将出现的情况是
答案：B
A）编译时出现语法错误，不能生成可执行文件
B）运行时有可能出错
C）运行时一定输出：The value at p:*9
D）运行时一定输出：The value at p:9
```
在VC++ 6.0中，上述程序可以编译，但不可以运行。 
不能将一个常量用于给指针变量赋初值，0除外。
```
# include<iostream>
using namespace std;
int main()
{	
	int *p1;
	int *p2;
	p1=NULL;
	p2=0;
	if(p1==p2)
		cout<<1<<endl;
	else cout<<0<<endl;
	return 0;
}

运行结果：
1
Press any key to continue
```
```
7. 下列语句中，错误的是
答案：C
A）int const buffer=256;
B）const double *point;
C）double * const point;
D）const int buffer=256;
```
分析： const限定的变量在定义时就需要初始化。B选项表示指针所指向的变量是一个常变量，故这个变量需要初始化，指针不需要初始化。C选项表示常指针，故这个指针在定义时就需要初始化。
```
# include<iostream>
using namespace std;
int main()
{	
	const int *p;
	int a=3;
	p=&a;
	return 0;
}
运行结果：
--------------------Configuration: test - Win32 Debug--------------------
Compiling...
test.cpp
Linking...

test.exe - 0 error(s), 0 warning(s)

```

```
# include<iostream>
using namespace std;
int main()
{	
	int a=3;
	int * const p =&a;
	return 0;
}
运行结果：
--------------------Configuration: test - Win32 Debug--------------------
Compiling...
test.cpp
Linking...

test.exe - 0 error(s), 0 warning(s)

```
而：
```
# include<iostream>
using namespace std;
int main()
{	
	int a=3;
	int * const p;
	return 0;
}

运行结果：
--------------------Configuration: test - Win32 Debug--------------------
Compiling...
test.cpp
E:\CPP-learning\test.cpp(6) : error C2734: 'p' : const object must be initialized if not extern
执行 cl.exe 时出错.

test.exe - 1 error(s), 0 warning(s)
```
```
10. 有如下程序段：

   int i = 0, j = 1;
   int &r = i;    // ①
   r = j;         // ②
   int *p = &i;   // ③
   *p = &r;       // ④
其中会产生编译错误的语句是
答案：C
A）①
B）③
C）④
D）②
```
分析，*p已经表示一个值了，而编译器将&r视为一个指针，故④是在将一个指针的值赋给一个值，错误。

```
12. 字面常量42、4.2、42L的数据类型分别是
答案：B
A）int、float、long
B）int、double、long
C）long、float、int
D）long、double、int

运行结果：
编译器会将常量4.2视为double型变量而不是float型变量
# include<iostream>
using namespace std;
int main()
{	
	cout<<sizeof(5.2)<<endl;
	cout<<sizeof(float)<<endl;
	cout<<sizeof(double)<<endl;
	return 0;
}

运行结果：

8
4
8
Press any key to continue

```

```
3. 下列关于内联函数的叙述中，正确的是
答案：BA）内联函数函数体的最后一条语句必须是return语句
B）内联函数是通过编译器来实现的
C）内联函数必须通过关键字inline来定义
D）内联函数在调用时发生控制转移
```
当类的成员函数的函数体不长时，C++编译系统自动将其视为内联函数。在用inline关键字声明内联函数时，只是建议性的，不是指令性的。

```
4. 下列运算符不能重载为友元函数的是
答案：D
A）+=  -=  *=  /=
B）+  -  ++  --
C）>  <  >=  <=
D）=  ()  [ ]  ->
```
C++的规定。