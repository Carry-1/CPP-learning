&emsp;&emsp;**使用关键字`explicit`的一条黄金法则是：
对于所有只需提供一个参数就能调用的构造函数，除非你想要利用它进行隐式转换，否则一律将该构造函数声明为explicit。**    
&emsp;&emsp;下面来解释以下为什么要这样做：   
&emsp;&emsp;编译器在调用函数时如果传入实参与函数形参类型不一致时可以采用隐式转换来转换实参类型使其与形参保持一致。这意味着编译器可以使用构造函数(其形参表中只有一个参数)来进行隐式转换以得到正确的参数类型。
举个例子：
```
//Foo 类有一个可以用于隐式转换的构造函数
class Foo   
{
public:
  // single parameter constructor, can be used as an implicit conversion
  Foo (int foo) : m_foo (foo) //ctor
  {
  }

  int GetFoo () { return m_foo; }

private:
  int m_foo;
};

//DoBar函数有一个Foo类型的形参
void DoBar (Foo foo)
{
  int i = foo.GetFoo ();
}

//在main函数中调用DoBar函数
int main ()
{
  DoBar (42);
}
```
&emsp;&emsp;上例中，在main函数中调用DoBar函数时传入的实参不是Foo类的对象，而是一个int型整数。然而，因为Foo类存在一个构造函数，它可以将int型整数作为参数用于构造一个Foo类对象，而这个Foo类对象刚好可以作为DoBar的实参。编译器允许进行上述操作。    
&emsp;&emsp;但是，如果在上例中的构造函数前面加上`explicit`,编译器就会被禁止进行隐式转换，因此再次执行DoBar(42)就会发生编译错误，此时要想正确调用DoBar函数，还能这样：DoBar(Foo(42))。    
&emsp;&emsp;有人可能会问：什么时候需要禁止这种隐式类型转换(意外地调用了构造函数)呢？看一个下面这样的例子：    
&emsp;&emsp;你有一个`MyString`类，它有一个这样的构造函数：构造一个给定长度的字符串。同时你有这样的函数：`print(const MyString&)`，还有一个重载它的函数:`print(char *string)`.这时，你想要执行`print("3")`语句，但是由于粗心，你错误地执行了`printf(3)`。你想要打印3，但结果却打印了一个空字符串(其长度为3)。



参考文献：
1. [stack overflow explict](https://stackoverflow.com/questions/121162/what-does-the-explicit-keyword-mean)
2. [cplusplus reference forum](http://www.cplusplus.com/forum/general/168292/)

