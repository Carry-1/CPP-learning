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
<font color=red>代码2好像是错的，不知道哪里错了</font>   
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

错误运行结果：
1168231104
1168231104
1168231104
Press any key to continue

运行结果：
6
120
504
Press any key to continue
```
代码2刚开始在VC++6.0和 VS Code上运行都会出现错误的结果，后来不知道怎么结果又对了。

**6.对象指针**   
**(1)指向对象的指针**
```
类名 * 对象指针名
如： Time * p    
	 Time t1;
	p = &t1;	//p中存放着t1的起始地址
	(*p).hour或p->hour 可以引用t1.hour  
```
**（2）指向对象数据成员的指针**
定义指向对象数据成员的指针变量的方法和定义指向普通变量的指针变量的方法相同：   
```
int *p;
p = &t1.hour //把对象成员的地址赋给p，则p指向对象数据成员t1.hour
```
**(3)指向对象成员函数的指针**
定义指向对象成员函数的指针变量的方法和定义指向普通函数的指针变量的方法不同
```
int (*p)(int a, int b);   //指针p是一个普通函数指针
p=fun;      //让p指向函数fun 
```
而定义指向成员函数的指针变量不能简单地将类的成员函数的入口地址赋给p
```
p = t1.gettime;      //错误
```
定义指向公用成员函数的指针变量的一般形式为：
 ```
 数据类型名 （类名::指针变量名）（参数列表）
 void(Time::p)();  //定义一个指向公用成员函数的指针
 
 指针变量名=&类名::成员函数名
 p=&Time::gettime; //把公用成员函数的入口地址赋给指向公用成员函数的指针
                   //在VC++中，也可以不写&，但建议不要省略
 ```   
 # 上代码🙃
 ```
 # include <iostream>
using namespace std;
class Time
{public:
	int hour,min,sec;
	Time(int, int, int);
	void Time::gettime();
};
Time::Time(int h, int m, int s)
{
	hour=h;
	min=m;
	sec=s;
}

void Time::gettime()
{
	cout<<hour<<":"<<min<<":"<<sec<<endl;
}

int main()
{
	Time t1(12,35,46);
	Time *p;
	p=&t1;
	t1.gettime();
	cout<<(*p).hour<<endl;
	cout<<p->hour<<endl;
	void (Time:: *p1)();   //这里后面要加括号
	p1=&Time::gettime;    //这里后面不要加括号，和指向普通函数的指针在赋值时类似
	(t1.*p1)();   //这里要加括号，因为前面一部分只是相当于t1.gettime;
	return 0;
}

运行结果：
12:35:46
12
12
12:35:46
Press any key to continue
 ```
**<font collor=red>注意上面代码的注释中写的什么时候要有括号，什么时候没括号</font>**

在给p1赋值时，是
```
p1=&Time::gettime;
```
而不是
```
p1=&t1::gettime;  //错误  
```
因为如果同时定义了同一个类的多个对象，这些对象公用这个类的成员函数，即成员函数不是存放在对象的空间中的，而是存放在对象外的空间的，附给这个指针的地址应是公用的成员函数代码段的入口地址。

**7.this指针**
在每个成员函数中都包含一个特殊的指针，这个指针的名字是固定的，称为this。它是指向本类对象的指针，它的值是调用本成员函数的对象的起始地址。
学习了this指针之后，应当理解：调用对象t1的成员函数gettime,实际上是在调用成员函数gettime时让this指针指向对象t1.
因为，在声明类时
```
class Time
{
	void gettime();
};
void Time::gettime()
{
	...
}
```
C++编译系统在编译时自动会将其处理为
```
void Time::gettime(Time *this)
{
	...
}
```
同时，在调用时，也是将`t1.gettime()`处理为`t1.gettime(&t1)`
;


**用new运算符新建无名对象**
```
Box *p=new Box; 
```
返回一个指向该对象的指针

**对象的赋值** 
```
Box b1(10,8,9), b2;
 b2=b1;   //对象赋值

```
**对象的复制**
```
Box b1(10,8,9);
Box b2=b1; //正确
```
**复制构造函数**
```
Box::Box(const Box &b)
{
	height=B.height;
	width=b.wdth;
	length=b.length;

}
```
以下三种情况需调用复制构造函数：
**（1）**程序中需建立一个新对象，并用同类对象对它初始化
**（2）**当函数参数是类的对象时，调用该参数时实参是类的对象，需要将该对象的拷贝传给形参，就是按实参复制一个形参，此时调用复制构造函数。
**（3）**函数的返回值是类的对象。
```
Box fun(void)
{
	Box b1;
	...
	return b1;
}
int main ()
{
	...
	Box b2;
	b2 = fun();
}
```
由于退出fun函数时，对象b1占用的空间被释放，因此return返回的肯定不是b1的数据成员的值，而是调用复制构造参数，将b1复制给一个临时对象，并将其传给b2.

**静态数据成员**   

**静态成员函数**

**友元函数**
**友元成员函数**
**类的提前声明**
**友元类**     
友元类的声明是**单向**的，不是**双向**的。如果类A是类B的友元类，则类A可以访问类B中所有的数据成员，同时，友元类的声明损害了信息隐蔽，因此，应该尽量少声明一些友元类。

**转换构造函数**
代码：
```
# include <iostream>
using namespace std;
class Complex
{
public:
	Complex()
	{
		real=0;
		image=0;
	}
	Complex( int r)
	{
		real = r;
		image = 0;
	}
	int real, image;
};
int main()
{
	Complex c1(3);
	cout<<c1.real<<"+"<<c1.image<<"i"<<endl;
	return 0;
}

运行结果：
3+0i
Press any key to continue

```

**类型转换函数**
operator 类型名()
{
	实现转换的语句;
}

如：
```
operator double()
{
	return real;    //可见，类型转换函数应为成员函数。否则，编译系统怎么会知道real是某个对象的数据成员呢
}
```
```
# include <iostream>
using namespace std;
class Complex
{
public:
	Complex()
	{
		real=0;
		image=0;
	}
	Complex(int r, int i):real(r),image(i){}
	operator double()   //定义类型转换函数
	{
		return real;
	}
	int real, image;
};
int main()
{
	Complex c1(3,2);
	double a=3.2;
	double b= a + c1;
	cout<<b<<endl;
	return 0;
}
```

看一段同时有**类型转换函数、转换构造函数、运算符重载函数（重载为成员函数）的代码**
```
# include <iostream>
using namespace std;
class Complex
{
public:
	Complex()
	{
		real=0;
		image=0;
	}
	Complex(int r, int i):real(r),image(i){}
	operator double()    //定义类型转换函数
	{
		return real;
	}
	Complex(double r) //定义转换构造函数
	{ 
		real = r;
      //  image =0;
	}
	Complex operator +(Complex &c2);    //声明运算符重载函数

		
	double real, image;
};

Complex Complex::operator +(Complex &c2)   //定义运算符重载函数
	{
		Complex c;
		c.real= real + c2.real;
		c.image = image + c2.image;
		return c;
	}
		
int main()
{
	Complex c1(3,2), c2(5,4),c3, c4;
	double a=3.2;
	double b= a + c1;   //c1被强制类型转换为double类型
	c3 = c1+c2;   //c1和c2通过重载后的"+"进行相加
	c4 = c1 + a;  
	cout<<"b="<<b<<endl;
	cout<<"c3="<<c3.real<<"+"<<c3.image<<"i"<<endl;
	cout<<"c4="<<c4<<endl;
	return 0;
}
```

派生类的声明方式：
例如已声明：
```
class student
{
	public:
	cout<<"number="<<number<<endl;
	cout<<"name="<<name<<endl;
	cout<<"sex="<<sex<<endl;

	private:
	int number;
	char sex;
	string name;

};

class Student1:public student    //声明派生类
{
	public:
	cout<<"age="<<age<<endl;
	cout<<"address="<<add<<endl;
	
	private:
	int age;
	char add[20];
	

};

在声明派生类时，一般格式为：
class 派生类名：继承方式 基类名
{
	派生类的新增成员；
}；
```
继承方式可选 public private protected,默认为private

继承方式与在派生类中的访问属性对应关系：  
~~首先要清楚，若某个成员是属于某个类的私有成员，则该成员只可被该类的成员函数访问，若~~
|     在基类的访问属性     | 继承方式 |             在派生类的访问属性                |
| ------------ | --- | ------------------------------- |
| public（公用） |  public（公用） | [public（公用） |
| private（私有）     |  public(公用) | 不可访问          |
| protected     |  public(公用) | protected(保护)          |

|     在基类的访问属性     | 继承方式 |             在派生类的访问属性                |
| ------------ | --- | ------------------------------- |
| public（公用） |  private(私有) | [private(私有) |
| private（私有）     |  private(私有) | 不可访问          |
| protected     |   private(私有) |  private(私有)          |

|     在基类的访问属性     | 继承方式 |             在派生类的访问属性                |
| ------------ | --- | ------------------------------- |
| public（公用） |  protected(保护) | [protected(保护) |
| private（私有）     |  protected(保护) | 不可访问          |
| protected     |   protected(保护) |  protected(保护)          |

代码：
```
# include<iostream>
# include<string>
using namespace std;
class student    //定义基类
{
public:
	void get_value()
	{
		cin>>number>>name>>sex;
	}
	void display()
	{
		cout<<"number:"<<number<<endl;
		cout<<"name:"<<name<<endl;
		cout<<"sex:"<<sex<<endl;

	}
private:
	int number;    //学号
	char sex;      //性别
	string name;
};

class student1: public student    //定义派生类
{
public:
	void get_value1()
	{
		cin>>age>>addr;
	}

	void display1()
	{
		cout<<"age:"<<age<<endl;
		cout<<"addr:"<<addr<<endl;
	}
private:
	int age;
	string addr;
};

int main()
{
	student1 std1, std2;   //定义派生类对象
	std1.get_value1();    //派生类对象访问派生类成员函数
	std1.display1();     //派生类对象访问派生类成员函数
	std2.get_value();   //派生类对象访问基类成员函数
	std2.display();     //派生类对象访问基类成员函数
	return 0;
}
```
**派生类构造函数**
```
class student
{
	public:
		int num;
		string name;
		int age;
};

class student1: public student
{
	public:
		char sex;
		string addr;
		student1(int n, string nam, int a, char s string add):student(n, nam, a)
		{
			sex = s;
			addr = add;
		}
};

```
**有子对象的构造函数**
```
# include<iostream>
# include<string>
using namespace std;
 
class student     //基类
{
	public:
		student(int n, string nam)
		{
			number = n;
			name = nam;
		}
		void display()
		{
			cout<<"number="<<number<<endl;
			cout<<"name="<<name<<endl;
		}
	protected:
		int number;    //学号
		string name;   //姓名
};

class student1: public student     //派生类
{
	public:
		student1(int n, string nam, int n1, string nam1, int a, string add): student(n, nam), monitor(n1, nam1) //定义有子对象的派生类构造函数
		{
			age = a;
			addr = add;
		}
		void show()     //派生类的成员函数
		{
			cout<<"information of student is"<<endl;

			display();     //调用基类成员函数，输出学号和姓名
			cout<<"age="<<age<<endl;
			cout<<"addr="<<addr<<endl;
		}
		
		void show_display()     //派生类的成员函数，用于输出班长的学号和姓名
		{
			cout<<"information of monitor is"<<endl;
			monitor.display();   //输出班长的信息
		}
	private:     //派生类的私有成员
		student monitor;       //基类对象作为派生类的成员
		int age;
		string addr;
};
	int main()
{
		student1 stud1(520, "XQS", 1314, "ZMZ", 23, "AHSHFS");
		stud1.show();    //输出学生的信息
		stud1.show_display();    //输出班长的信息

		return 0;
}
```

**多重继承**

**虚基类**

**有效避免了多重继承时引起的二义性问题**

**组合和继承的区别**

**多态**

**异常**
**命名空间**

**new delete**   
如：
new和delete运算符用于动态分配和撤销存储空间。
```
new int(100); //开辟一个用于存放整数的空间，并指定该整数的初值为100，返回一个指向该空间的指针
```
静态数据成员可以初始化，但只能在类体外进行初始化，其一般形式为：数据类型类名::静态数据成员名=初值。

