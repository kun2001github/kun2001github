vscode 通过ssh远程连接服务器配置C/C++环境



工具vscode 1.89.5

系统ubuntu22.04



系统配置：

```
#安装gcc和g++编译器
sudo apt update
sudo apt install build-essential -y  #默认的 Ubuntu 软件源包含了一个软件包组，名称为 “build-essential”,它包含了 GNU 编辑器集合，GNU 调试器，和其他编译软件所必需的开发库和工具。

#安装gdb调试工具
sudo apt install gdb -y

#安装cmake 和 make 工具
sudo apt install cmake make -y
```

vscode 配置：

安装这个插件C/C++Extension Pack 和 C/C++ Runner

![image-20240508235800455](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240508235800455.png)