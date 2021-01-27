**1.作用域限定符：** 在类体外定义成员函数时，需要加作用域限定符，用它来声明变量是属于哪个类的。如,假设已声明了一个Time类：
```
void Time::set_time()
{
  ...  
}
```
**2.分清作用域限定符(::)和成员运算符（.）的区别：**  作用域限定符是在类体外定义成员函数是用的，紧跟在它之前的是类名，而成员运算符是在主函数中访问对象的成员时用的，紧跟在它之前是对象名。
**上代码🙃**
```
# include <iostream>
using namespace std;
class Array_Max
{
	private:
	int a[10], max;

	public:
	void set_value();
	void max_value();
	void show_value();
};

void Array_Max::set_value()
{
	for (int i=0; i<10; i++)
		cin>>a[i];
}
void Array_Max::max_value()
{
	int i;
	max=a[0];
	for (i=0; i<10; i++)
		max = (max>a[i] ? max:a[i]);
}
void Array_Max::show_value()
{
	cout<<"max="<<max<<endl;
}


int main()
{
	Array_Max Arr;
	Arr.set_value();
	Arr.max_value();
	Arr.show_value();
	return 0;	
}
```

**3.构造函数**    
*示例代码：*
```
# include<iostream>
using namespace std;
class Time
{
	private:
		int hour,min,sec;

	public:
		Time()
		{
			 hour=0;
			 min=0;
			 sec=0;
		}
		void set_time();
		void show_time();
}; 

int main()
{
	Time t1;
	t1.set_time();
	t1.show_time();
	Time t2;
	t2.show_time();
	return 0;
}
void Time::set_time()
{
	cin>>hour;
	cin>>min;
	cin>>sec;
}
void Time::show_time()
{
	cout<<hour<<":"<<min<<":"<<sec<<endl;
}

运行结果：
14 23 56
14:23:56
0:0:0
Press any key to continue
```
（1）构造函数是一种特殊的成员函数,与其它成员函数不同，它不需要用户调用，而是在建立对象时自动执行。构造函数不能任意命名，必须与类名相同，以便编译系统能够识别它并把它当作构造函数来处理。构造函数一般声明为`public`。   
如果用户没有定义构造函数，则编译系统会自动定义一个空的构造函数，它不进行初始化。当然，也可以在类中声明构造函数，在类外定义。`Time::Time(){...}`    

（2）带参数的构造函数：
```
# include <iostream>
using namespace std;
class rectangle
{
	private:
		float length, width, height;
	public:
		rectangle(float , float , float);
		float volume1();
};

rectangle::rectangle(float l, float w, float h)
{
	length=l;
	width=w;
	height=h;
}

float rectangle::volume1()
{
	
	cout<<"volume="<<length*width*height<<endl;
	return length*width*height;
}

int main()
{
	rectangle rec1(2.1,2.5,1.3);
	rec1.volume1();
	rectangle rec2(3.3,2.6,1.5);
	rec2.volume1();
	return 0;
}
```   
（3）带参数初始化表的构造函数：   
如上例子中定义构造函数可改为：   
`
rectangle::rectangle(float l, float w, float h)：length(l),width(w),height(h){}
` 这样就可以直接在类体中（而不是类外）定义构造函数。   
(4)构造函数也可以重载。
（5）可以定义使用默认参数的构造函数。
# 看到了275页
