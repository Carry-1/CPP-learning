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
C++的规定。并且：若=  ()  [ ]  ->可被重载为友元函数，那么这样的语句会被视为合法：
```
Time t1;
...  //重载=为友元函数

1=t1;   //会被视为合法，但编译过程中出现错误，因为试图将一个变量的值赋给一个字面常量 
```
算符重载的一些规则：①一般情况下，单目运算符最好重载为类的成员函数，双目运算符则最好重载为类的友元函数；②双目运算符=、()、[]、->不能重载为类的友元函数；③类型转换函数只能定义为一个类的成员函数，而不能定义为类的友元函数；**④若一个运算符的操作需要修改对象的状态，选择重载为成员函数较好；⑤若运算符所需的操作数(尤其是第一个操作数)希望有隐式类型转换，则只能选用友元函数；（为什么？）**⑥当运算符函数是一个成员函数时，最左边的操作数(或者只有最左边的操作数)必须是运算符类的一个类对象(或者是对该类对象的引用)；

```
9. 下列关于函数重载的叙述中，错误的是   
答案：B
A）重载函数的参数列表必须不同   //对
B）重载函数的返回值类型必须不同   
C）重载函数的参数可以带有默认值  
D）函数重载就是用相同的函数名定义多个函数   //对
```
<font color=red>注意：运算符重载函数的参数不能有默认参数，并且，一个函数不能既作为重载函数又作为带有默认参数的函数</font>**所以C不也应该是错的嘛？**
例如：
```
void fun(int);            //重载函数之一
void fun(int，int = 2);     //重载函数之二，带有默认参数
void fun(int = 1，int = 2);  //重载函数之三，带有默认参数
fun(3);    //error: 到底调用3个重载函数中的哪个？
fun(4,5)   //error：到底调用后面2个重载函数的哪个？
```

```
11. 在下列原型所示的C++函数中，按“传值”方式传递参数的是
答案：C
A）void f4(int &x);
B）void f2(int *x);
C）void f1(int x);
D）void f3(const int *x);
```
分析：指针作为形参不应该也是按值传递参数么，因为实参是变量地址或指针，
而形参是引用确实是按址传递参数，因为实参是变量名。传递给形参的是实参的地址。

```
12. 将前缀运算符“--”重载为非成员函数，下列原型中，能正确用于类中说明的是
答案：A
A）friend Decr& operator --(Decr&);
B）Decr& operator --(int);
C）friend Decr operator --(Decr&,int);
D）Decr operator --(Decr&,int);
```
分析：“++”和“--”既可以前置也可以后置，重载时是有区别的，如果在重载函数的参数表列中多加一个形参`int`则表示重载后置自增（自减）运算符函数，否则为前置。

```
常对象的成员函数不一定都是常成员函数，只需保证其数据成员是常数据成员即可
```
```
this作用域是在类内部，当在类的非静态成员函数中访问类的非静态成员时，编译器会自动将对象本身的地址作为一个隐含参数传递给函数。另外，全局函数和静态函数都不能使用this指针。故本题答案是类的非静态成员函数都有this指针。
```

# include <iostream>
using namespace std;
class A{
	public:
		static int a;
		void init()
		{
			a=1;
		}
		A(int a = 2)
		{
			init();
			a++;
		}
};
int A::a = 0;
A obj;
int main()
{
	cout<<obj.a;
	return 0;
}

注意构造函数，它没能实现对数据成员a的初始化，相反，在默认构造函数中，形参a会屏蔽掉静态数据成员a，而在函数中对形参a的任何改变都不影响函数作用域外的静态数据成员a          
```
A(int a = 2)
		{
			init();
			a++;
		}
```
```
#include<iostream>
using std::cout;
using std::endl;
class Sample{
    public:
    Sample(){}
    ~Sample(){cout<<"*";}
};

int main()
{
    Sample temp[2], *ptemp[2];
    return 0;
}
```
上述代码在运行时只输出2个*号，原因是只建立了两个对象`（Sample temp[2]）`。`Sample *ptemp[2]`用于建立两个对象指针，<font color=red>并不是对象</font>，对象指针是指针，它的值是地址，它的建立不需要调用构造函数。

字面常量4.2的默认类型是double型。
枚举常量的默认值依次为0,1,2,3...