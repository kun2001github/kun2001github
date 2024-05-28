项目地址：[L-Strobel/jointAnalysis充电：《电动汽车对区域和国家电力系统影响的联合分析——2030年德国县级案例研究》中使用的充电优化模型 --- L-Strobel/jointAnalysisCharging: Charging optimization model used in "Joint Analysis of Regional and National Power System Impacts of Electric Vehicles - A Case Study for Germany on the County Level in 2030" (github.com)](https://github.com/L-Strobel/jointAnalysisCharging)



### 安装软件：vscode 

[Download Visual Studio Code - Mac, Linux, Windows](https://code.visualstudio.com/Download)

#### 下载链接：https://vscode.download.prss.microsoft.com/dbazure/download/stable/e170252f762678dec6ca2cc69aba1570769a5d39/VSCodeUserSetup-x64-1.88.1.exe

#### 安装python插件和jupyter插件

![image-20240424233925361](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240424233925361.png)

![image-20240424233903155](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240424233903155.png)



### 安装conda 这里安装minconda

#### 下载地址：https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/

#### 初始化

![image-20240424234408223](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240424234408223.png)

```
conda init
```

![image-20240424234444808](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240424234444808.png)

### 克隆仓库

git clone https://github.com/L-Strobel/jointAnalysisCharging.git

亦或者下载仓库源码，然后解压也行



### 创建虚拟环境

conda create -n jonpy38 python=3.8



### 安装该项目的包

conda activate jonpy38

cd jointAnalysisCharging

python setup.py install

遇到问题2，请跳转解决方法



### 激活许可Gurobi

1.访问：http://www.gurobi.cn/   （没有账号就自己注册一个）

**Gurobi 免IP验证学术许可申请方法**：[许可申请-Gurobi 中国](http://www.gurobi.cn/NewsView1.Asp?id=4)

2.选择如图，学术申请

![image-20240425002335235](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240425002335235.png)

3.

![image-20240425002527325](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240425002527325.png)

4.这里可以申请，没有的话，需要注册一个账号

![image-20240425002640221](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240425002640221.png)

5.

![image-20240425003112309](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240425003112309.png)

6.

![image-20240425003144671](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240425003144671.png)



7.获取到激活命令后，安装如下图片操作，激活成功

grbgetkey 2f9e8bac-fe83-4803-b4bf-a5b15099be14

![image-20240425004040109](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240425004040109.png)

8.设置环境变量

![image-20240425004227967](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240425004227967.png)

参考地址：[下载安装Gurobi10.0+如何在jupyterLab中使用（python)_gurobi下载-CSDN博客](https://blog.csdn.net/weixin_58587245/article/details/128789954)

### 测试

1.使用vscode打开该项目

2.打开作者提供的example.ipynb

3.设置jupyter内核，选择刚刚创建的环境--jonpy38

![image-20240425000901787](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240425000901787.png)

4.点击全部运行

5.会有弹窗，提示安装ipykernel包，点击安装

![image-20240425001018856](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240425001018856.png)

6.自动安装好后，就会运行，如图，就在运行

![image-20240425004412056](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240425004412056.png)

## 遇到的问题

#### 问题1 

. : 无法加载文件 C:\Users\55057\Documents\WindowsPowerShell\profile.ps1，因为在此系统上    禁止运行脚本。有关详细信息，请参阅 https:/go.microsoft.com/fwlink/?LinkID=135170 中的 a      bout_Execution_Policies。
所在位置 行:1 字符: 3

+ . 'C:\Users\55057\Documents\WindowsPowerShell\profile.ps1'
+   + CategoryInfo          : SecurityError: (:) []，PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess

解决方法：以为管理员身份启动PowerShell，执行：set-ExecutionPolicy RemoteSigned 然后输入Y 即可解决

参考地址：[PowerShell报错：无法加载文件C:\Users\server\Documents\windowsPowerShell\profile.ps1..._powershell启动出错无法加载文件 c:\users\24895\documents\wind-CSDN博客](https://blog.csdn.net/qq_34562959/article/details/120653219)

#### 问题2

error: Couldn't find a setup script in C:\Users\55057\AppData\Local\Temp\easy_install-zjy459xn\pandas-2.2.2.tar.gz

解决方法，可能是网络问题，那么就手动安装该包的依赖：

pip install gurobipy numpy pandas -i https://pypi.tuna.tsinghua.edu.cn/simple some-package