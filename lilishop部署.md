项目：[Lilishop开源商城系统 - Lilishop开源商城系统 (gitee.com)](https://gitee.com/beijing_hongye_huicheng)

项目地址：[lilishop商城-前端（管理端-商家端-PC端）: lilishop商城基于SpringBoot 全端开源 电商商城系统 商城前端。包含买家PC端、商家PC端以及管理端 (gitee.com)](https://gitee.com/beijing_hongye_huicheng/lilishop-ui)

项目文档：[项目介绍 · LILISHOP-开发者中心 (pickmall.cn)](https://docs.pickmall.cn/项目介绍.html)

部署的是：管理端-商家端-PC端

# 项目要求：

centos7.6（推荐）

docker compose  v19

nodejs v14.16.0

vscode



# 第一步：环境要求：

```
jdk >= 1.8

Mysql 8.x.x

Redis >= 6.2.5

elasticsearch >= 7.3.0 需要IK分词器

rocket-server >= 4.7.0

xxl-job >= 2.3.0
```

## 环境要求解决方法1：

### 使用docker 一键部署这些中间件

获取docker脚本

```
git clone https://gitee.com/beijing_hongye_huicheng/docker.git
```

Rocketmq 需要特殊配制一下节点ip

```
 在 config/broker.conf 文件中，将brokerIP1修改为部署docker的局域网ip
```

运行脚本（第一行为部署环境包括Mysql、mq、redis、xxljob等所有中间件） **必须保证es本地挂载目录权限为 777 否则es启动不成功。默认es本地挂载目录为docker项目上一级的volumes/data**

```
docker-compose up -d
```

校验(查看进程是否启动，如果反复启动的程序，可以使用*docker logs* 镜像id 查看日志)

```
docker ps
```

## 环境要求解决方法2：

```
1.如果所有基础设施+API+UI全部启动 ，电脑内存至少在16G及以上。最好是2核16G内存服务器一台
本文档电脑操作系统：Windows10 专业版

Git https://git-scm.com/download/win

jdk1.8 https://www.oracle.com/java/technologies/downloads/#java8

Maven https://maven.apache.org/download.cgi

Nodejs v14.16.0 https://nodejs.org/download/release/v14.16.0/

————————————————————————————————————————————————————

Mysql 8.0.25

Redis 6.2.5

elasticsearch 7.3.0 需要IK分词器

rocket-server 4.7.0

xxl-job 2.3.0

2.修改Rocketmq 节点
在 config/broker.conf 文件中，将brokerIP1修改为部署docker的局域网ip。
```

![image-20240426210447545](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240426210447545.png)



# 第二步部署api（后端）



下载源码

```
cd /home/source
git clone https://gitee.com/beijing_hongye_huicheng/lilishop.git
```

编辑运行api脚本

```
#版本 注意，需要跟随版本号进行调整
version=4.3
#代码目录
code_path=/home/source/lilishop
#运行目录
run_path=/home/source/api/

mkdir -p ${code_path}
mkdir -p ${run_path}
cd ${code_path}
git checkout master
git pull
mvn clean install -DskipTests

ps -ef |grep java |grep buyer  |grep -v 'grep'|awk '{print $2}'  | xargs kill -9
ps -ef |grep java |grep seller  |grep -v 'grep'|awk '{print $2}'  | xargs kill -9
ps -ef |grep java |grep manager  |grep -v 'grep'|awk '{print $2}'  | xargs kill -9
ps -ef |grep java |grep common  |grep -v 'grep'|awk '{print $2}'  | xargs kill -9
ps -ef |grep java |grep consumer  |grep -v 'grep'|awk '{print $2}'  | xargs kill -9
ps -ef |grep java |grep im  |grep -v 'grep'|awk '{print $2}'  | xargs kill -9

rm -rf ${run_path}*.jar
mv ${code_path}/common-api/target/common-api-$version.jar ${run_path}
mv ${code_path}/buyer-api/target/buyer-api-$version.jar ${run_path}
mv ${code_path}/consumer/target/consumer-$version.jar ${run_path}
mv ${code_path}/manager-api/target/manager-api-$version.jar ${run_path}
mv ${code_path}/seller-api/target/seller-api-$version.jar ${run_path}
mv ${code_path}/im-api/target/im-api-$version.jar ${run_path}

cd ${run_path}

mkdir logs

nohup java -Xmx256m -Xms128m -Xss256k  -jar manager-api-$version.jar> logs/manager.out  &
nohup java -Xmx256m -Xms128m -Xss256k  -jar common-api-$version.jar> logs/common.out  &
nohup java -Xmx256m -Xms128m -Xss256k  -jar buyer-api-$version.jar> logs/buyer.out  &
nohup java -Xmx256m -Xms128m -Xss256k  -jar consumer-$version.jar> logs/consumer.out  &
nohup java -Xmx256m -Xms128m -Xss256k  -jar im-api-$version.jar> logs/im.out  &
nohup java -Xmx256m -Xms128m -Xss256k  -jar seller-api-$version.jar> logs/seller.out  &

```

执行脚本

```
chmod +x start-api.sh
sh start-api.sh
```

# 第三步：部署前端

商城UI （lilishop-ui）项目下3个文件夹 

buyer：买家PC端

seller：商家端

manager：后台管理端



下载源码

```
cd /home/source
git clone https://gitee.com/beijing_hongye_huicheng/lilishop-ui.git
```

安装node yarn

```
yum update
yum install -y nodejs
yum install -y npm
npm install -g yarn
#   #设置镜像
#   yarn config set registry https://registry.npmmirror.com --global
#   yarn config set disturl https://registry.npmmirror.com/dist --global
#NPM配置淘宝镜像加速（可选）
#	npm config set registry https://registry.npmmirror.com

# 升级node
npm install -g n
n install v14.16.0
```

编辑脚本

```
#代码目录
code_path=/home/source/lilishop-ui

cd ${code_path}
git checkout master
git pull

cd ${code_path}/manager
yarn install
yarn build

cd ${code_path}/seller
yarn install
yarn build


cd ${code_path}/buyer
yarn install
yarn build
```

执行脚本

```
chmod +x start-ui.sh
sh start-ui.sh
```

# 运行项目

编辑脚本

```
#代码目录
code_path=/home/source/lilishop-ui

cd ${code_path}/manager
yarn run de

cd ${code_path}/seller
yarn run dev

cd ${code_path}/buyer
yarn run dev
```

# 测试

127.0.0.1:1000

127.0.0.1:1002

127.0.0.1:1003



用户名：admin

密码：123456



xxljob默认

用户：admin

密码: 111111