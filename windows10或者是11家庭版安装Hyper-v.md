# Windows10/11家庭版开启Hyper-V虚拟机功能



确保电脑启动了虚拟化，没有开启则上网搜索，自己笔记本型号进入bios的教程，开启虚拟化

![image-20240427134643003](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427134643003.png)

## 开启Hpyer-V脚本

### 新建一个名为Hyper-V.txt文件，输入以下内容

```
pushd "%~dp0"

dir /b %SystemRoot%\servicing\Packages\*Hyper-V*.mum >hv.txt

for /f %%i in ('findstr /i . hv.txt 2^>nul') do dism /online /norestart /add-package:"%SystemRoot%\servicing\Packages\%%i"

del hv.txt

Dism /online /enable-feature /featurename:Microsoft-Hyper-V -All /LimitAccess /ALL

Pause
```

输入完成后，保存，并且重命名为Hyper-V.bat，右击，以管理员身份运行即可，执行完成后重启电脑