# 项目地址：

[microsoft/scene_graph_benchmark：图像场景图生成基准 --- microsoft/scene_graph_benchmark: image scene graph generation benchmark (github.com)](https://github.com/microsoft/scene_graph_benchmark)

## 参考地址：

[scene_graph_benchmark/INSTALL.md在main · microsoft/scene_graph_benchmark --- scene_graph_benchmark/INSTALL.md at main · microsoft/scene_graph_benchmark (github.com)](https://github.com/microsoft/scene_graph_benchmark/blob/main/INSTALL.md)



## 环境：

系统window 10 家庭版中文

版本号：22H2

安装docker   （到控制面板-程序和功能-启动或关闭Windows功能，开启Winndows 虚拟机监控程序平台、适用于Linux的Windows字系统、虚拟机平台）

安装vscode



我使用win的wsl的ubuntu18.04



# 克隆项目

git clone https://github.com/microsoft/scene_graph_benchmark.git

















# 使用wsl部署 18.04





# 使用anconda win11 









# 使用docker部署

```
#使用cuda11.0和cudnn8 ubuntu18.04
#cuda10.1和cudnn7 ubuntu18.04停止维护了，nvidia/cuda官方删除了，所以pull 不到了

docker pull [nvidia/cuda:11.0.3-cudnn8-devel-ubuntu18.04](app://dd/#) 
```

## 启动容器

```
docker run -it --gups all --name demo nvidia/cuda:11.0.3-cudnn8-devel-ubuntu18.04 /bin/bash
```

## 切换源

```
apt update 

apt install curl

bash <(curl -sSL https://linuxmirrors.cn/main.sh)
```

注意：要跳过软件更新，不然可能会导致显卡方面的问题

> [!WARNING] 
>
> 更新后，会遇到这些报错，会影响到显卡
>
> /sbin/ldconfig.real: File /usr/lib/x86_64-linux-gnu/libnvidia-ptxjitcompiler.so.450.191.01 is empty, not checked. /sbin/ldconfig.real: File 
> /usr/lib/x86_64-linux-gnu/libcuda.so.450.191.01 is empty, not checked. /sbin/ldconfig.real: /usr/lib/x86_64-linux-gnu/libcuda.so.1 is not a symbolic link

## install basics 安装基础包

```
apt-get update -y

apt-get install -y apt-utils git curl ca-certificates bzip2 cmake tree htop bmon iotop g++

apt-get install -y libglib2.0-0 libsm6 libxext6 libxrender-dev libyaml-dev vim zsh wget htop tmux
```

## Install Miniconda 安装miniconda

```
wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda3-latest-Linux-x86_64.sh

bash ./Miniconda3-latest-Linux-x86_64.sh
```

## 创建虚拟环境

```
conda create -y --name py37 python=3.7

conda activate py37

conda install -y ipython h5py nltk joblib jupyter pandas scipy

pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple

pip install requests ninja cython yacs>=0.1.8 numpy>=1.19.5 cython matplotlib opencv-python tqdm protobuf tensorboardx pymongo scikit-learn boto3 scikit-image cityscapesscripts

pip install azureml-defaults>=1.0.45 azureml.core inference-schema

pip install einops==0.6.0  #默认安装了0.7.0，会报错，这里提前解决了

pip --no-cache-dir install --force-reinstall -I pyyaml

安装nltk的预料包等等，因为国内网络的问题
python -m nltk.downloader punkt
执行成功如下：
E:\anaconda3\envs\py37\lib\runpy.py:125: RuntimeWarning: 'nltk.downloader' found in sys.modules after import of package 'nltk', but prior to execution of 'nltk.downloader'; this may result in unpredictable behaviour
  warn(RuntimeWarning(msg))
[nltk_data] Downloading package punkt to
[nltk_data]     C:\Users\HASEEE\AppData\Roaming\nltk_data...
[nltk_data]   Unzipping tokenizers\punkt.zip.



官方文档：https://www.nltk.org/data.html
1解决方法：
export http_proxy="http://10.12.54.198:7890/"
export https_proxy="http://10.12.54.198:7890/"


2解决方法：(我使用了clash挂了代理，我的IP是192.168.42.236，端口是7890，开启了局域网访问)失败
python
import nltk
import os
os.environ["http_proxy"] = "http://192.168.42.236:7890"
os.environ["https_proxy"] = "http://192.168.42.236:7890"
nltk.download()
d
punkt

```

## 安装torch 1.7.1

```
conda install pytorch==1.7.1 torchvision==0.8.2 torchaudio==0.7.2 cudatoolkit=11.0 -c pytorch

conda install -y -c conda-forge timm einops
```

## 安装install pycocotools

```
conda install -y -c conda-forge pycocotools
```

# install cityscapesScripts

```
python -m pip install cityscapesscripts
```

# install Scene Graph Detection

```
git clone https://github.com/microsoft/scene_graph_benchmark
cd scene_graph_benchmark

# the following will install the lib with
# symbolic links, so that you can modify
# the files if you want and won't need to
# re-build it

FORCE_CUDA="1"
FORCE_CUDA=${FORCE_CUDA}

python setup.py build develop

执行后报错（可能是因为我的显卡是4060，而4060是需要最少11.1以上的cuda支持算力8.9，但是torch1.7.1的只支持到cuda11.0，算力只有到8.6）
raise ValueError("Unknown CUDA arch ({}) or GPU not supported".format(arch))
ValueError: Unknown CUDA arch (8.9) or GPU not supported
参考地址：https://blog.csdn.net/zjy_cn/article/details/134360303

原因是cuda（我这里是cuda11.0，最高支持8.6）的版本不支持当前算力（8.9）
解决方法：修改算力
sudo vim ~/.bashrc
# 在配置文件中添加如下一行
export TORCH_CUDA_ARCH_LIST=8.0  # 因为是CUDA11.0，对应的算力为8.6，测试8.6失败，8.0成功
source ~/.bashrc







测试解决方案：（失败）
vim /root/miniconda3/envs/py37/lib/python3.7/site-packages/torch/utils/cpp_extension.py
找到named_arches 和 supported_arches 修改为如下
   named_arches = collections.OrderedDict([
        ('Kepler+Tesla', '3.7'),
        ('Kepler', '3.5+PTX'),
        ('Maxwell+Tegra', '5.3'),
        ('Maxwell', '5.0;5.2+PTX'),
        ('Pascal', '6.0;6.1+PTX'),
        ('Volta', '7.0+PTX'),
        ('Turing', '7.5+PTX'),
        ('Ampere', '8.0;8.6+PTX'),
        ('Hopper', '9.0+PTX'),
    ])

    supported_arches = ['3.5', '3.7', '5.0', '5.2', '5.3', '6.0', '6.1', '6.2',
                        '7.0', '7.2', '7.5', '8.0', '8.6','8.9','9.0']
```



遇到的问题
ImportError: libGL.so.1: cannot open shared object file: No such file or directory

解决方法：apt-get install ffmpeg libsm6 libxext6  -y



win问题1：

AttributeError: module 'Cython.Plex.Actions' has no attribute 'Method'

可能是cython的版本原因，升级就行了

pip install --upgrade cython



win 遇到问题

python setup.py build develop

E:\anaconda3\envs\py37\lib\site-packages\torch\utils\cpp_extension.py:287: UserWarning: Error checking compiler version for cl: [WinError 2] 系统找不到指定的文件。

warnings.warn('Error checking compiler version for {}: {}'.format(compiler, error))
building 'maskrcnn_benchmark._C' extension

error: Microsoft Visual C++ 14.0 or greater is required. Get it with "Microsoft C++ Build Tools": https://visualstudio.microsoft.com/visual-cpp-build-tools/

解决方法，使用conda 安装gcc（linux可以）

另外一篇csdn看到的解决方法：conda install libpython m2w64-toolchain -c msys2   #这是安装gcc的命令，但是还是失败了，卸载它，使用2的方法

[Microsoft Visual C++ 14.0 is required.-CSDN博客](https://blog.csdn.net/qzzzxiaosheng/article/details/125119006)

看到系统安装了gcc的开发环境（visual studio2022） 就使用了这个环境的cmd打开编译安装

  File "E:\anaconda3\envs\py37\lib\site-packages\torch\utils\cpp_extension.py", line 702, in _check_abi
    raise UserWarning(msg)
UserWarning: It seems that the VC environment is activated but DISTUTILS_USE_SDK is not set.This may lead to multiple activations of the VC env.Please set `DISTUTILS_USE_SDK=1` and try again.

set `DISTUTILS_USE_SDK=1`

还是不行，，放弃使用visual c++的环境





2 的方法：使用

下载路径：[MinGW-w 64-用于32位和64位Windows下载|SourceForge.net --- MinGW-w64 - for 32 and 64 bit Windows download | SourceForge.net](https://sourceforge.net/projects/mingw-w64/)

参考文献：[Windows10安装MinGW-W64出现Cannot download repository.txt的一种解决方法 - SZU_黄其才 - 博客园 (cnblogs.com)](https://www.cnblogs.com/zhicungaoyuan-mingzhi/p/12804210.html#:~:text=问题：去官网下载的MinGW-w64安装文件，然后双击安装时出现如下问题： 尝试使用右键管理员权限打开无效之后。 最后我使用的是离线安装的方法。 解决方法：,1、进行离线安装，直接下载文件的方法，我给出链接直接下载即可，64位机器点这里 下载 32位机器自己在这个网站找一下即可。 2、下载好文件之后，直接解压。 3、将解压好的文件，直接拷贝到你所需要的安装的文件夹，文件夹的路径最好不要有中文，复制文件夹路径，进行到这一步所需的文件就全部都下载好了。)

安装

python setup.py build develop



发现成功了



遇到报错3

(py37) PS E:\scene_graph_benchmark> & E:/anaconda3/envs/py37/python.exe e:/scene_graph_benchmark/tools/train_net.py
Traceback (most recent call last):
  File "e:/scene_graph_benchmark/tools/train_net.py", line 31, in <module>
    from apex import amp
ModuleNotFoundError: No module named 'apex'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "e:/scene_graph_benchmark/tools/train_net.py", line 33, in <module>
    raise ImportError('Use APEX for multi-precision via apex.amp')
ImportError: Use APEX for multi-precision via apex.amp



解决方法：pip install apex

报错

WARNING: Building wheel for cryptacular failed: [Errno 2] No such file or directory: 'C:\\Users\\HASEEE\\LOCALS~1\\Temp\\pip-wheel-z76ubbox\\cryptacular-1.6.2-cp37-cp37m-win_amd64.whl'
Failed to build cryptacular
ERROR: Could not build wheels for cryptacular, which is required to install pyproject.toml-based projects

则pip install pyproject

在pip install apex

换一个解决方案：

[Windows系统下安装apex，及错误汇总_warning: building wheel for cryptacular failed: [e-CSDN博客](https://blog.csdn.net/qq_17783559/article/details/127813381)

我又换了一个
使用conda安装 （成功）

```
conda install -c conda-forge nvidia-apex
```



测试跑代码都没有问题



环境：

 [env-conda.yaml](env-conda.yaml) 











# 开始测试-执行训练

### 安装azcopy工具下载数据集

azcopy工具下载官方：[使用AzCopy v10将数据复制或移动到Azure存储|微软学习 --- Copy or move data to Azure Storage by using AzCopy v10 | Microsoft Learn](https://learn.microsoft.com/en-us/azure/storage/common/storage-use-azcopy-v10)

github地址：[Azure/azure-storage-azcopy: The new Azure Storage data transfer utility - AzCopy v10 (github.com)](https://github.com/Azure/azure-storage-azcopy)

wget https://aka.ms/downloadazcopy-v10-linux

mv downloadazcopy-v10-linux  azcopy.tar.gz
tar -zxvf azcopy.tar.gz

/root/azcopy/azcopy copy 'https://penzhanwu2.blob.core.windows.net/sgg/sgg_benchmark/datasets/TASK_NAME' <target folder> --recursive

```
TASK_NAME` **可以是** `visualgenome` **、** `openimages_v5c
```













# 测试提供的demo





发现报错：（我的einops的版本是0.7.0，`einsum` 函数的签名可能已经改变，不再接受 `/` 作为参数分隔符，导致的报错，）

File "/root/miniconda3/envs/py37/lib/python3.7/site-packages/einops/einops.py", line 807

def einsum(tensor: Tensor, pattern: str, /) -> Tensor:

SyntaxError: invalid syntax

解决测试：pip install einops==0.6.0





