# 实验要求

使用VMware Workstation 创建

win11

windows server2022  DC



windows server 2022 clone DBC





其中DC就是AD的主控制域，而DBC是副控制域







## 安装win10 

省略

## 安装windows server 2022 DC

省略

### 设置计算机名

![image-20240527152516195](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527152516195.png)

![image-20240527152542175](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527152542175.png)

![image-20240527152551999](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527152551999.png)



### 配置IP地址





DC

![image-20240527155033488](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527155033488.png)



 DBC

![image-20240527155154359](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527155154359.png)

win 11 

![image-20240527164701503](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527164701503.png)





## 安装windows server 2022 clone DBC

克隆windows server 2022即可



### 设置计算机名---跟windows server 2022 DC一样的

## 安装服务

### 在DC和DBC上执行以下操作，进行安装

1.添加角色和功能

![image-20240527150509537](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527150509537.png)

2.下一步

![image-20240527150534267](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527150534267.png)



3.下一步

![image-20240527150557100](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527150557100.png)

4.下一步

![image-20240527150619116](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527150619116.png)



![image-20240527150740695](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527150740695.png)



![image-20240527150717952](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527150717952.png)

![image-20240527150754682](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527150754682.png)



![image-20240527150809645](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527150809645.png)

![image-20240527150823651](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527150823651.png)

![image-20240527150839831](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527150839831.png)

![image-20240527150850358](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527150850358.png)





## 在DC上创建

![image-20240527151228423](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527151228423.png)

![image-20240527151244494](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527151244494.png)

![image-20240527151336881](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527151336881.png)

设置DSRM密码（可以同计算机密码一样）

![image-20240527151514606](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527151514606.png)

![image-20240527151534377](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527151534377.png)

等待识别NetBIOS域名（尽量默认）

![image-20240527151719719](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527151719719.png)

![image-20240527151915391](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527151915391.png)

![image-20240527151931450](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527151931450.png)

![image-20240527153642116](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527153642116.png)

![image-20240527153821026](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527153821026.png)

![image-20240527154539272](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527154539272.png)

## 在DBC上创建

#### 首先配置

![image-20240527160053032](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527160053032.png)

![image-20240527160113266](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527160113266.png)

![image-20240527160124358](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527160124358.png)



### 好啦后，就正式开始配置啦

![image-20240527152334037](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527152334037.png)

![image-20240527154615669](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527154615669.png)

![image-20240527154716037](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527154716037.png)

![image-20240527155329405](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527155329405.png)

![image-20240527155359131](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527155359131.png)

设置DSRM密码（可以和相同:我这里设置Lkh2001，，）

![image-20240527155733321](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527155733321.png)

![image-20240527155743118](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527155743118.png)

![image-20240527155805411](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527155805411.png)

![image-20240527155815123](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527155815123.png)

![image-20240527155829403](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527155829403.png)

![image-20240527155906468](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527155906468.png)

![image-20240527161527561](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527161527561.png)

![image-20240527161547436](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527161547436.png)

![image-20240527162117671](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527162117671.png)





出现报错
![image-20240527155948771](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527155948771.png)

解决方法：
![image-20240527160053032](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527160053032.png)

![image-20240527160113266](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527160113266.png)

![image-20240527160124358](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527160124358.png)



解决好啦后，在重新安装就行了。安装好啦自动重启，重启后会出现这个配置页面（直接按住正常的配置即可）

![image-20240527160658231](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527160658231.png)







## 把win11 添加到我创建的AD域里面去

![image-20240527164753301](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527164753301.png)

![image-20240527164820566](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527164820566.png)

输入该域的用户名和密码

![image-20240527165026699](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527165026699.png)

![image-20240527165059655](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527165059655.png)

![image-20240527165111519](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527165111519.png)

![image-20240527165141827](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527165141827.png)



## 查看加入该域的电脑

![image-20240527165606709](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527165606709.png)

![image-20240527165648058](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527165648058.png)

## 在域中创建用户，测试

首先创建组

![image-20240527165606709](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527165606709.png)

![image-20240527170356970](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527170356970.png)

![image-20240527170439573](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527170439573.png)



在组织单位里面创建组

![image-20240527170506406](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527170506406.png)

![image-20240527170607271](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527170607271.png)

在组织单位里面创建用户

![image-20240527170720301](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527170720301.png)

![image-20240527170804746](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527170804746.png)

密码是：Lkh2001，，

![image-20240527170837513](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527170837513.png)

![image-20240527171137438](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527171137438.png)

#### 把组添加进去这个用户

![image-20240527171226784](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527171226784.png)

![image-20240527171248615](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527171248615.png)

![image-20240527171258102](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527171258102.png)

### 开始测试

![image-20240527171407149](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527171407149.png)

![image-20240527171604695](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527171604695.png)

![image-20240527171623695](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527171623695.png)

![image-20240527171734440](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527171734440.png)

![image-20240527171811109](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527171811109.png)

  创建一个快捷方式

![image-20240527172019420](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527172019420.png)

![image-20240527172116084](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527172116084.png)

![image-20240527172132058](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527172132058.png)





## 使用win11 登录AD域创建的用户

账号：ikun

密码：Lkh2001，，

![image-20240527172657865](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527172657865.png)![image-20240527172659400](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527172659400.png)



![image-20240527172711029](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527172711029.png)

可以看到，在AD域里面的用户ikun，已经有这个快捷方式了

![image-20240527173149312](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527173149312.png)





## 其他-安装winmail

前提条件

创建一个win10虚拟机

![image-20240527174830710](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240527174830710.png)

### 安装winmail



