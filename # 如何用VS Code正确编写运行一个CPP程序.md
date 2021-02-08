# 如何用VS Code正确编写运行一个CPP程序
**&emsp;&emsp;最近准备用VS Code来复习一下数据结构的算法题，可是发现写出来的程序总是运行不成功，就算照着书上的程序敲都显示运行问题，那应该是我除了源程序以外，还有一些其他的文件没有配置好了，（因为此时的VSC是可以运行部分CPP程序的）看其他人的帖子要么讲不清楚，要么讲得太复杂，索性自己去看官方文档了。**
## 假设编译器（GCC）和相应的插件已经配置好,步骤如下：
# 1.Create Hello World 
>&emsp;&emsp;From a Windows command prompt, create an empty folder called projects where you can place all your VS Code projects. Then create a sub-folder called helloworld, navigate into it, and open VS Code in that folder by entering the following commands:
```
mkdir projects
cd projects
mkdir helloworld
cd helloworld
code .
```
>The "code ." command opens VS Code in the current working folder, which becomes your "workspace".    

&emsp;&emsp;上面这些话和命令是新建一个文件夹`peojects`，用作工作空间(`workspace`)文件夹，以及在这个文件夹下面新建一个`helloword`文件夹存放源代码，并打开VS Code.
>As you go through the tutorial, you will see three files created in a .vscode folder in the workspace:
```
tasks.json (build instructions)
launch.json (debugger settings)
c_cpp_properties.json (compiler path and IntelliSense settings)
```
&emsp;&emsp;上面这段话和代码的意思是完成上述步骤就会在helloword文件夹下面**自动**生成一个`.vscode`文件夹，并且这个文件夹中包含3个`json`文件
其中
```
tasks.json (build instructions)   //与编译有关的命令
launch.json (debugger settings)   //与调试有关的设置
c_cpp_properties.json (compiler path and IntelliSense settings) //这里面有编译路径和语法提示设置
```


# 2. Build helloworld.cpp
>&emsp;&emsp;Next, you'll create a tasks.json file to tell VS Code how to build (compile) the program. This task will invoke the g++ compiler to create an executable file based on the source code.   
&emsp;&emsp;From the main menu, choose Terminal > Configure Default Build Task. In the dropdown, which will display a tasks dropdown listing various predefined build tasks for C++ compilers. Choose g++.exe build active file, which will build the file that is currently displayed (active) in the editor.



参考文献：[Visual Studio Code 官方文档](https://code.visualstudio.com/docs/cpp/config-mingw)