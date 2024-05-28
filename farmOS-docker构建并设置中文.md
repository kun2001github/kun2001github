# farmOS使用docker构建并设置中文

参考地址：[Installing farmOS | farmOS](https://farmos.org/hosting/install/)

翻译参考地址：[Translating farmOS | farmOS](https://farmos.org/hosting/localization/)



前提条件，确保电脑安装了docker，并且能启动docker

如果按照了docker，但是没有启动docker

确保在，控制面板-程序-程序和功能-启动或关闭Windows功能里面的以下3个是开启的

- Windows虚拟机监控程序平台

- 适用于LInux的Windows子系统

- 虚拟机平台

  ![image-20240427141730519](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427141730519.png)



使用管理员身份运行cmd

输入wsl -v 确定是wsl 2的版本，如果不是则 wsl -s 2进行设置

![image-20240427141852576](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427141852576.png)



确保wsl是最性的，更新wsl --update

![image-20240427142019945](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427142019945.png)



安装docker ，并且启动docker



如果docker 还是启动不了，那就考虑安装Hyper-V，确保系统是专业版系统，如果是家庭版，则查看这里      xxxxxx链接，安装启动Hyper-V



然后在重新安装docker ，并且启动docker















## 获取farmOS 的docker镜像

3.x.y    #  填写自己需要的版本

```text
docker pull farmos/farmos:3.x.y
docker run --rm -p 80:80 -v "${PWD}/sites:/opt/drupal/web/sites" farmos/farmos:3.x.y
```

github地址：[farmOS/farmOS: farmOS: A web-based farm record keeping application. (github.com)](https://github.com/farmOS/farmOS)

翻译地址：[Translating farmOS | farmOS](https://farmos.org/hosting/localization/)



访问web，并且安装中文翻译模块，默认是没有安装的，翻译的模块叫farm_l10n

![image-20240427143238383](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427143238383.png)

![image-20240427143603365](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427143603365.png)

![image-20240427143618342](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427143618342.png)

好啦，接下来就是安装翻译模块， 其他默认，往下拉，把这个打勾Transiation/localization features

![image-20240427143728949](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427143728949.png)

等待安装

![image-20240427143800093](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427143800093.png)

可以看到已经检测到了翻译模块

![image-20240427144024634](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427144024634.png)

## 开始配置设置中文，并且使其生效



![image-20240427144319569](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427144319569.png)

往下拉，找到这个

![image-20240427144458472](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427144458472.png)

添加中文

![image-20240427144523467](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427144523467.png)







![image-20240427144207256](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427144207256.png)

![image-20240427144706033](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427144706033.png)

![image-20240427144724051](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427144724051.png)

等待下载

![image-20240427144750973](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427144750973.png)

## 给系统配置中文

![image-20240427145532334](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427145532334.png)



![image-20240427145557619](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427145557619.png)

注意：这里设置了，其实还是不可以的，还需要到用户信息里面去设置才生效

点击右上角头像

![image-20240427145740267](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427145740267.png)



![image-20240427145810133](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427145810133.png)

ok 这样就完成了



翻译不会是很全面

可以自己去修改

路径是：http://127.0.0.1:8080/admin/config/regional/translate













# 遇到的报错

## 报错1

![image-20240427144950023](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240427144950023.png)

应该是网络问题吧，重新试试