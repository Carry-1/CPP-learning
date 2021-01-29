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

**对象的引用**    
若已定义了Time 类   
```
Time t1;
Time &t2=t1;//t2是t1的引用
```
则t2.tour=ti.tour
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
(5)可以定义使用默认参数的构造函数。   
**4.析构函数**    
析构函数也是一种成员函数，例如:
```
class Time
{
	~Time()
	{

	}
	...
}
```
析构函数一定无参数，因此不能重载，一个类只有一个析构函数。析构函数不仅还可以用来执行用户在最后一次使用对象之后所执行的任何操作。如果用户没有在类中定义析构函数，则C++编译系统会自动定义一个空的析构函数。
代码🧑：
# include<string>
# include <iostream>
using namespace std;
class Student
{
	public:
		Student(int n, string nam, char s)
		{
			num=n;
			name=nam;
			sex = s;
			cout<<"constructor called."<<endl;
		}
		~Student()
		{
			cout<<"destructor called."<<endl;
		}

		void display();
	private:
		int num;
		string name;
		char sex;
};

void Student::display()
{
	cout<<num<<endl;
	cout<<name<<endl;
	cout<<sex<<endl;

}

int main()
{
	Student st1(100,"Zhao Meng Zhe",'f');
	st1.display();
	Student st2(101,"Xia Qingsheng",'m');
	st2.display();
	return 0;
}

什么时候调用构造函数和析构函数要视情况而定：   
（1）在所有函数之外定义对象：定义对象时调用构造函数，但仅在程序运行结束时才调用析构函数   
（2）在函数中定义局部自动变量：在函数中定义对象时调用构造函数，在退出函数时调用析构函数   
（2）在函数中定义静态局部变量：在函数中定义对象时调用构造函数，但仅在程序运行结束时才调用析构函数

**5.对象数组**    
代码1：
```
# include <iostream>
using namespace std;
class Cube
{
	public:
		Cube(int l=10, int w=12, int h=15):length(l),width(w),height(h){}
	int volume();
	private:
			int length;
			int width;
			int height;
		
};
int Cube::volume()
{
	return(length*width*height);
}

int main()
{
	Cube lifangti[3]=
	{
		Cube(1,2,3),
		Cube(4,5,6),
		Cube(7,8,9)
	};
	cout<<lifangti[0].volume()<<endl;
	cout<<lifangti[1].volume()<<endl;
	cout<<lifangti[2].volume()<<endl;
	return 0;
}

运行结果：
[Running] cd "e:\CPP-learning\" && g++ tempCodeRunnerFile.cpp -o tempCodeRunnerFile && "e:\CPP-learning\"tempCodeRunnerFile
6
120
504

[Done] exited with code=0 in 0.546 seconds

```
代码2：
```
# include <iostream>
using namespace std;
class Cube
{
	public:
		Cube(int l, int w, int h)
		{
			int length=l;
			int width=w;
			int height=h;
		}
	int volume();
	private:
			int length;
			int width;
			int height;
		
};
int Cube::volume()
{
	return(length*width*height);
}

int main()
{
	Cube lifangti[3]=
	{
		Cube(1,2,3),
		Cube(4,5,6),
		Cube(7,8,9)
	};
	cout<<lifangti[0].volume()<<endl;
	cout<<lifangti[1].volume()<<endl;
	cout<<lifangti[2].volume()<<endl;
	return 0;
}

运行结果：
6
120
504
Press any key to continue
```
代码2刚开始在VC++6.0和 VS Code上运行都会出现错误的结果，后来不知道怎么结果又对了。
# 看到了281页
