



安装amd显卡遇到了问题

![image-20240518001456980](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240518001456980.png)

sudo apt update
wget https://repo.radeon.com/amdgpu-install/23.40.2/ubuntu/jammy/amdgpu-install_6.0.60002-1_all.deb
sudo apt install ./amdgpu-install_6.0.60002-1_all.deb

sudo amdgpu-install -y --usecase=graphics,rocm

下列软件包有未满足的依赖关系：
 rocm-gdb : 依赖: libtinfo5 但无法安装它
            依赖: libncurses5 但无法安装它
            依赖: libpython3.10 但无法安装它 或
                    libpython3.8 但无法安装它
E: 无法修正错误，因为您要求某些软件包保持现状，就是它们破坏了软件包间的依赖关系。

  直接使用apt install 安装这些包，发现根本就找不到，那么就手动安装，参考[Ubuntu 24.04 Preview 版安装 libtinfo5-CSDN博客](https://blog.csdn.net/engchina/article/details/135396971)



到http://archive.ubuntu.com/ubuntu/pool/universe/n/ncurses/里面搜索  libtinfo5  libncurses5   

或者是在[Ubuntu – Ubuntu Packages Search](https://packages.ubuntu.com/)里面搜索



wget http://archive.ubuntu.com/ubuntu/pool/universe/n/ncurses/libtinfo5_6.4-2_amd64.deb
sudo dpkg -i libtinfo5_6.4-2_amd64.deb



wget http://archive.ubuntu.com/ubuntu/pool/universe/n/ncurses/libncurses5_6.4-2_amd64.deb

sudo dpkg -i libncurses5_6.4-2_amd64.deb



安装libpython3.8

wget http://security.ubuntu.com/ubuntu/pool/main/p/python3.8/libpython3.8_3.8.10-0ubuntu1~20.04.9_amd64.deb

sudo dpkg -i libpython3.8_3.8.10-0ubuntu1~20.04.9_amd64.deb