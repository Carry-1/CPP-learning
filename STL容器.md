STL是C++为读者提供的标准模板库（Standard Template Library）的缩写

一些代码示例😋：
```
# include<cstdio>
# include<string>
# include<queue>
# include<stack>
# include<map>
using namespace std;
//声明一些全局变量
typedef struct
{
   bool flag;
   double num;
   char op;
}node;

string str;  //用于存放中缀表达式
stack<node> s;   //运算符栈
queue<node> q;   //存放操作数
map<char, int> op; 

```