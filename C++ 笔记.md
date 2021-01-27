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