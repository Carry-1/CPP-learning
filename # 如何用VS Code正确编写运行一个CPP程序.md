# 如何用VS Code正确编写运行一个CPP程序
**&emsp;&emsp;最近准备用VS Code来复习一下数据结构的算法题，可是发现写出来的程序总是运行不成功，就算照着书上的程序敲都显示运行问题，那应该是我除了源程序以外，还有一些其他的文件没有配置好了，（因为此时的VSC是可以运行部分CPP程序的）看其他人的帖子要么讲不清楚，要么讲得太复杂，索性自己去看官方文档了。**



## 假设此时你的编译器（GCC）和相应的扩展已经配置好,编写一个源程序，编译调试并成功运行的步骤如下：

# 1.编写源程序
&emsp;&emsp;打开cmd，输入以下命令，
```
mkdir projects
cd projects
mkdir helloworld
cd helloworld
code .   //注意不要忽略后面这个点
```  

&emsp;&emsp;上面这些命令是新建一个文件夹`projects`，用作工作空间(`workspace`)文件夹，以及在这个文件夹下面新建一个`helloword`文件夹存放源代码，并打开VS Code.（当然，你也可以直接打开VS Code手动建立🙃，更方便）



# 2.编译源程序

&emsp;&emsp;第2步，创建`tasks.json`文件，它的作用是告诉VS Code如何编译源程序（即建立一个编译任务）。这项任务会使g++编译器创建一个可执行文件。我们只需选择 Terminal > Configure Default Build Task，之后会出现一个下拉菜单，里面有各种提前定义好的编译任务，选择其中的`g++.exe build active file`,VS Code会自动帮我们创建一个`tasks.json`文件，并编译active file（即当前编辑窗口中打开的源文件）。

**此时已经生成了可执行文件，故可以运行程序啦。**
但通常我们都需要调试代码，因此我们还需要进行第3步：

# 3.调试程序
&emsp;&emsp;在主菜单中选择`Run > Add Configuration... 之后选择 C++ (GDB/LLDB).` 之后再在出现的下拉菜单中选择选择`g++.exe build and debug active file.`再返回helloworld.cpp，这样它就又是active file了，按F5就可以开始调试啦。调试时可以按`F9,F10,F11`(用处和在VC++6.0里一样🙃)。并且可以在左侧边栏中的`VARIABLE`下面监测变量的变化。也可以在`WATCH`中添加你想要观察的某个变量，点击它旁边的`+`号即可。
**调试后源程序若没问题，且已经编译生成可执行文件，按`CTRL+Shift+N`运行即可**

&emsp;&emsp;至此，一个简单的源程序的编写、编译、调试和运行已经完成。

&emsp;&emsp;如果你想要控制更多的C/C++扩展，也可以创建一个`c_cpp_properties.json`文件，（这个也会在.vscode文件夹中自动生成，anyway，一般不会有太大影响）你可以在其中修改使用的C/C++标准，以及指明一些你在编程时用到的一些不在工作空间和标准库中的头文件的路径。或者你直接在`C/C++ configuration UI`中做出的修改也会自动写入到这个文件中。    


&emsp;&emsp;最终你会发现自己打开的工作空间（即你用open folder 打开的文件夹）下有一个`.vscode`文件夹，里面有3个.json文件：

```
tasks.json (build instructions)   //与编译有关的命令
launch.json (debugger settings)   //与调试有关的设置
c_cpp_properties.json (compiler path and IntelliSense settings) //这里面有编译器路径和你所用的C/C++标准...
```

<font color=red>另外，强烈建议路径名即文件名均使用英文，否则在调试时可能识别不出调试路径，最后返回给你一个'no such file or directory.'     
launch.json文件中 Console：...改为： "externalConsole": true,</font>


# 参考文献：[Visual Studio Code 官方文档](https://code.visualstudio.com/docs/cpp/config-mingw)