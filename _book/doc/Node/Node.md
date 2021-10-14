# 命令行模式 和 Node交互模式的区别
1. 打开mac的 terminal.app || iTerm.app 展现的窗口即为 命令行模式  
在窗口中输入 Node 回车 即可进入Node交互环境，看到 ">"即表示是在Node交互式环境下
2. 此外，在命令行模式使用Node xxx.js命令运行.js文件 和 在Node交互式环境下直接运行JavaScript代码 有所不同，Node交互式环境会把每一行JavaScript代码的结果自动打印出来，但是，直接运行JavaScript文件却不会  
例如，在Node交互式环境下，输入：
```
> 100 + 200 + 300;
600
```
直接可以看到结果600  
但是，写一个calc.js的文件，内容如下：
```
100 + 200 + 300;
```
然后在命令行模式下执行 node calc.js，发现什么输出都没有  