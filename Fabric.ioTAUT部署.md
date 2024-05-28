# 项目地址：

[Fabric.IoTAUT/iot-server at master · BamLubi/Fabric.IoTAUT (github.com)](https://github.com/BamLubi/Fabric.IoTAUT)

## 部署环境：ubuntu22.04，nvm(node14.21.3 npm 6.14.18) docker

使用nvm工具来管理node和npm是非常奈斯的，跟anconda一样类似的效果

## 安装依赖项

```
sudo apt update && sudo apt install git curl  make build-essential manpages-dev tree vim
```

在安装server服务的时候需要安装以下依赖

make build-essential manpages-dev

## nvm安装教程：

官方安装教程：[nvm/README.md at master · nvm-sh/nvm (github.com)](https://github.com/nvm-sh/nvm/blob/master/README.md?spm=a2c6h.12873639.article-detail.8.41115f59eolm4I&file=README.md)

### 1.脚本安装：

```
wget -qO- httpcurl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bashs://raw.githubusercontent.com/nvm-sh/nvm/v0.39.7/install.sh | bash
```

### 2.git方式安装（推荐）

```
git clone https://github.com/nvm-sh/nvm.git
```

```
cd nvm/ && ./install.sh 
```

```
cd ../.nvm 
chmod +x nvm.sh && ./nvm.sh
```

重启一个命令行即可使用

```
nvm -v
```

# 安装docker

安装docker19.03的版本，docker24.0最新版是自带compose v2的，我要用v1的版本，项目提供的脚本里面用的是v1的docker-compse ，v2的是docker compose 没有-这个

### 1.一键安装：

```
wget  https://linuxmirrors.cn/docker.sh
```

```
chmod +x docker.sh
```

```
sudo ./docker.sh

n
20.10.13
```

安装20.10.13的版本，他安装的也是compose v2的版本，那我们就手动安装吧

```
sudo apt  install docker-compose -y

docker-compose -v
```

docker-compose version 1.29.2, build unknown

###### **1设置普通用户也能使用docker （不推荐）**

```
sudo groupadd docker			# 有则不用创建 

sudo usermod -aG docker $USER	# USER 为加入 docker 组的用户 

newgrp docker					# 刷新 docker 组 

docker run hello-world			# 测试无 root 权限能否使用 docker

systemctl restart docker
#似乎失败了，可以把newgrp docker 写入到.bashrc里面即可（会死掉）
```

###### **2设置普通用户也能使用docker （不推荐）**

```
先查看一下默认这个文件/var/run/docker.sock的权限是啥 ？
$ sudo ls -al /var/run/docker.sock
srw-rw---- 1 root root 0 Feb 15 03:13 /var/run/docker.sock

#修改文件权限
sudo chmod 666 /var/run/docker.sock

#修改后，再查看一下这个文件的权限
$ sudo ls -al /var/run/docker.sock
srw-rw-rw- 1 root root 0 Feb 15 03:14 /var/run/docker.sock
```

参考地址：[docker权限设置：让非root用户可以操作docker--》附带：linux新增用户添加root权限_linux docker 添加用户权限-CSDN博客](https://blog.csdn.net/ak739105231/article/details/107779778)

# 克隆仓库

```
git clone https://github.com/BamLubi/Fabric.IoTAUT.git
```

```
cd Fabric.IoTAUT/iot-network
# 1. 解压bin文件(fabric工具包)
# bin.tar.gz下载地址：
# 链接：https://pan.baidu.com/s/1K-PgsmqZkr4eKUlMdPGkEQ 
# 提取码：1tdp
$ tar -zxvf ./bin.tar.gz
# 2. 获取docker容器镜像
$ docker pull hyperledger/fabric-peer:2.2.2
$ docker pull hyperledger/fabric-orderer:2.2.2
$ docker pull hyperledger/fabric-ca:1.4.9
$ docker pull hyperledger/fabric-tools:2.2.2
$ docker pull hyperledger/fabric-ccenv:2.2.2

chmod +x -R scripts/
chmod +x -R bin/
chmode +x ./network.sh

# 3. 使用--help查看相关指令
$ ./network.sh --help
# 4. 启动节点并创建通道
$ ./network.sh up createChannel -ca
# 5. 部署链码
$ ./network.sh deployCC
# 6. 停止fabric
$ ./network.sh down

## 除了使用自动化部署工具之外，也可以使用工具包自行部署
## 在./Fabric教程中有提及

## 需要修改的文件夹介绍
# ./chaincode -- 存放链码
# ./configtx -- 通道配置文件
# ./organizations/cryptogen -- 区块链组织架构
# ./docker -- docker节点配置
```

```
$ ./network.sh up createChannel -ca  
#最后的输出
	Anchor peer set for org 'Org2MSP' on channel 'mychannel'
	Channel 'mychannel' joined


$ ./network.sh deployCC  
#最后的输出
	Query successful on peer0.org1 on channel 'mychannel'

```

如果报./network.sh: 行 249: scripts/createChannel.sh: 权限不够，则使用chmod +x scripts/createChannel.sh 或者是 chmod +x -R ./*

## 安装服务端（后端）

使用普通用户，使用root用户报错，不知道什么原因

```
cd Fabric.IoTAUT/iot-server/
```

```
nvm install v14.19.0
```

```
nvm use 14
nvm alias default v14  #设置默认的
```

```
npm config set registry https://registry.npmmirror.com #https://npmmirror.com/
npm install
```

```
npm run serve
```

**重点解决 **：出现了跨域的问题 

在toi-server中的app.js 添加如下内容

```
var express = require('express'); // 引入 Express 框架
var app = express(); // 创建一个新的 Express 应用实例

// 设置 CORS
app.use((req, res, next) => {
  // 设置响应头，允许任何源（'*'）访问资源
  res.setHeader('Access-Control-Allow-Origin', '*');

  // 设置允许的 HTTP 方法
  res.setHeader('Access-Control-Allow-Methods', 'GET, POST, PATCH, PUT, DELETE, OPTIONS');

  // 设置允许的 HTTP 头部
  res.setHeader('Access-Control-Allow-Headers', 'Origin, Content-Type, Accept');

  // 继续处理请求
  next();
});

// 其他路由和中间件...  （这里不需要添加）

app.listen(3000, () => {
  console.log('Server running on port 3000');
});
```

复制到root目录下，然后在启动，因为代码里面写死了，从root目录下访问，当然你也可以去修改代码，我就懒得动了

```
sudo -i

cp -R /home/kante/Fabric.IoTAUT/iot-server .

vim ~/.bashrc

export NVM_DIR="/home/kante/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion

nvm use 14

npm run start
```

# 安装客户端

使用普通用户跑即可，先启动服务器在启动客户端

```shell
cd Fabric.IoTAUT/iot-client/ 
```

```
cd iot-client
```

```
nvm install v14.19.0
```

```
npm install
```



> [!NOTE]
>
> npm WARN optional SKIPPING OPTIONAL DEPENDENCY: fsevents@1.2.9 (node_modules/fsevents):
> npm WARN notsup SKIPPING OPTIONAL DEPENDENCY: Unsupported platform for fsevents@1.2.9: wanted {"os":"darwin","arch":"any"} (current: {"os":"linux","arch":"x64"})
>
> added 1094 packages from 898 contributors and audited 1162 packages in 83.736s
>
> 1 package is looking for funding
>   run `npm fund` for details
>
> found 318 vulnerabilities (13 low, 111 moderate, 134 high, 60 critical)
>   run `npm audit fix` to fix them, or `npm audit` for details

修改客户端，对接后端的IP地址修改：

root/iot-client/src/store.js

修改里面的ip为服务器的IP例如:127.0.0.1 或者是localhost

```
npm run serve

可以npm run build 构建后 npm run test
修改文件 npm run lint

```

启动成功后，端口号是8081

浏览器访问localhost:8081

------------------------------

顺便注册个账号

就会在/Fabrlc.IoTAUT/iot-server/public/wallet里面有用户信息密钥

-----------------------------------------------

测试，其他功能都成功，但是出现了（区块数据-组织信息和设备信息）获取不到数据的原因，肯能是因为没有接到实体设备的原因吧

回出现无法获取到区块数据的问题，提示获取数据失败!

![image-20240430031023044](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240430031023044.png)

![image-20240430031034156](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240430031034156.png)

![image-20240430031047113](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240430031047113.png)

其中服务端的报错如下：

2024-04-29T20:17:59.381Z - info: [NetworkConfig]: buildPeer - Unable to connect to the endorser peer0.org1.njtech.com due to Error: Failed to connect before the deadline on Endorser- name: peer0.org1.njtech.com, url:grpcs://localhost:7051, connected:false, connectAttempted:true     at checkState (/root/iot-server/node_modules/@grpc/grpc-js/build/src/client.js:77:26)     at Timeout._onTimeout (/root/iot-server/node_modules/@grpc/grpc-js/build/src/internal-channel.js:503:17)     at listOnTimeout (internal/timers.js:557:17)     at processTimers (internal/timers.js:500:7) {   connectFailed: true }



# 遇到的报错：（可以忽视，按照上面最新的部署不会出现下面这些问题）

### 问题1：

sh: 1: node-pre-gyp: Permission denied
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: pkcs11js@1.2.2 (node_modules/pkcs11js):
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: pkcs11js@1.2.2 install: `node-gyp rebuild`
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: Exit status 1

npm ERR! code ELIFECYCLE
npm ERR! syscall spawn
npm ERR! file sh
npm ERR! errno ENOENT
npm ERR! grpc@1.24.3 install: `node-pre-gyp install --fallback-to-build --library=static_library`
npm ERR! spawn ENOENT
npm ERR! 
npm ERR! Failed at the grpc@1.24.3 install script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     /root/.npm/_logs/2024-05-01T17_35_57_973Z-debug.log

解决：apt install node-pre-gyp

### 问题2

root@kante-virtual-machine:~/Fabric.IoTAUT/iot-server# npm install 

> pkcs11js@1.2.2 install /root/Fabric.IoTAUT/iot-server/node_modules/pkcs11js
> node-gyp rebuild

sh: 1: node-gyp: Permission denied

> grpc@1.24.3 install /root/Fabric.IoTAUT/iot-server/node_modules/fabric-client/node_modules/grpc
> node-pre-gyp install --fallback-to-build --library=static_library

sh: 1: node-pre-gyp: Permission denied
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: pkcs11js@1.2.2 (node_modules/pkcs11js):
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: pkcs11js@1.2.2 install: `node-gyp rebuild`
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: spawn ENOENT

npm ERR! code ELIFECYCLE
npm ERR! syscall spawn
npm ERR! file sh
npm ERR! errno ENOENT
npm ERR! grpc@1.24.3 install: `node-pre-gyp install --fallback-to-build --library=static_library`
npm ERR! spawn ENOENT
npm ERR! 
npm ERR! Failed at the grpc@1.24.3 install script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     /root/.npm/_logs/2024-05-01T18_04_15_354Z-debug.log
解决方法：npm install -i -g  node-gyp node-pre-gyp

### 问题3

root@kante-virtual-machine:~/Fabric.IoTAUT/iot-server# npm install 

> pkcs11js@1.2.2 install /root/Fabric.IoTAUT/iot-server/node_modules/pkcs11js
> node-gyp rebuild

sh: 1: node-gyp: Permission denied

> grpc@1.24.3 install /root/Fabric.IoTAUT/iot-server/node_modules/fabric-client/node_modules/grpc
> node-pre-gyp install --fallback-to-build --library=static_library

node-pre-gyp ERR! build error 
node-pre-gyp ERR! stack Error: Failed to execute 'node-gyp clean' (Error: spawn node-gyp EACCES)
node-pre-gyp ERR! stack     at ChildProcess.<anonymous> (/usr/share/nodejs/@mapbox/node-pre-gyp/lib/util/compile.js:83:23)
node-pre-gyp ERR! stack     at ChildProcess.emit (events.js:314:20)
node-pre-gyp ERR! stack     at Process.ChildProcess._handle.onexit (internal/child_process.js:274:12)
node-pre-gyp ERR! stack     at onErrorNT (internal/child_process.js:470:16)
node-pre-gyp ERR! stack     at processTicksAndRejections (internal/process/task_queues.js:84:21)
node-pre-gyp ERR! System Linux 6.5.0-28-generic
node-pre-gyp ERR! command "/usr/bin/node" "/usr/bin/node-pre-gyp" "install" "--fallback-to-build" "--library=static_library"
node-pre-gyp ERR! cwd /root/Fabric.IoTAUT/iot-server/node_modules/fabric-client/node_modules/grpc
node-pre-gyp ERR! node -v v12.22.9
node-pre-gyp ERR! node-pre-gyp -v v1.0.8
node-pre-gyp ERR! not ok 
Failed to execute 'node-gyp clean' (Error: spawn node-gyp EACCES)
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: pkcs11js@1.2.2 (node_modules/pkcs11js):
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: pkcs11js@1.2.2 install: `node-gyp rebuild`
npm WARN optional SKIPPING OPTIONAL DEPENDENCY: spawn ENOENT

npm ERR! code ELIFECYCLE
npm ERR! errno 1
npm ERR! grpc@1.24.3 install: `node-pre-gyp install --fallback-to-build --library=static_library`
npm ERR! Exit status 1
npm ERR! 
npm ERR! Failed at the grpc@1.24.3 install script.
npm ERR! This is probably not a problem with npm. There is likely additional logging output above.

npm ERR! A complete log of this run can be found in:
npm ERR!     /root/.npm/_logs/2024-05-01T18_05_48_510Z-debug.log

解决方法： npm install -i -g  node-gyp node-pre-gyp

# 其他（不用理会）

go安装 使用g管理工具可以管理多个版本的gvm环境

sudo apt-get install bison

bash < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)

