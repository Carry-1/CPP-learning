Lambda函数是C++11引入的一种新特性。常见形式如下：    
**1.**
```

void main () {
    auto l = [] {
    std::cout<<"Lambda example"<<std::endl;
    };    //先定义变量，再执行
    l();
}

```
**2.**
```

void main () {
     [] {
    std::cout<<"Lambda example"<<std::endl;
    }();    //直接执行
  

```