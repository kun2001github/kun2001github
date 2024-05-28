# 项目地址

[yjh126yjh/TianChi_Protein-Secondary-Structure-Prediction: 天池蛋白质结构预测大赛 排名3/241 (github.com)](https://github.com/yjh126yjh/TianChi_Protein-Secondary-Structure-Prediction)



## 项目的文件说明

- model.py：定义并生成模型
- evaluate.py：加载训练得到的参数并进行二级结构预测
- preprocess.py：预处理数据
- dataset.py：划分数据集
- whole_sequence-best.hdf5.xz：已经训练好的网络参数，线上成绩0.772
- train.py：训练模型

## 复现结果

1. 下载model.py、evaluate.py、dataset.py，下载whole_sequence-best.hdf5.xz并解压，放在同一个文件夹下。
2. 将evaluate.py中的filepath改成测试数据的路径，然后执行python evaluate.py。

## 环境要求：

anconda、vscode 或者是pycharm



## 环境情况

版本：Windows11家庭版

版本：23H2

显卡：NVIDIA GeForce RTX2060

显卡驱动版本：NVIDIA-SMI 472.19       Driver Version: 472.19       CUDA Version: 11.4

详细情况如图

![image-20240523004311023](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240523004311023.png)



注意：项目是2020年的，注意库的版本。



# 准备环境

### 安装ancodna

安装好了后，记得初始化，初始化命令：conda init，否则无法被系统识别到conda命令

![image-20240522174706182](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240522174706182.png)



### 安装vscode

https://vscode.download.prss.microsoft.com/dbazure/download/stable/dc96b837cf6bb4af9cd736aa3af08cf8279f7685/VSCodeUserSetup-x64-1.89.1.exe

#### 安装插件

![image-20240522162951572](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240522162951572.png)



# 下载项目源码

https://github.com/yjh126yjh/TianChi_Protein-Secondary-Structure-Prediction/archive/refs/heads/master.zip

#### 解压源码

省略（使用常规的工具即解压）

# 创建虚拟环境

```
conda create -n py37 python=3.7
```



### 激活环境

```
conda activate 3.7
```

### 安装tensorflow2.3.0

```text
conda install cudatoolkit==10.1.243
conda install cudnn==7.6.4
conda install tensorflow-gpu==2.3.0
conda install keras==2.4.3

----------------------以下都是测试失败的----无视即可----------------------
conda install cudatoolkit==11.0.3 -c conda-forge
conda install cudnn==8.0.5.39 -c conda-forge
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple  #设置清华源加速
pip install tensorflow-gpu==2.4.0
pip install keras==2.4.3
会报错
pip install numpy==1.19.2
pip install scipy==1.10.0
```

# 使用vscode打开源码，并测试

## 在vscode 中选择虚拟环境

![image-20240522174513565](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240522174513565.png)

注意：如果没有anconda没有初始化，或者是设置环境变量，是无法被vscode找到的

如果实在是找不到，那就手动指定

![image-20240522175133296](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240522175133296.png)



## 解压whole_sequence-best.hdf5.xz

解压已经训练好的网络参数，一样使用常规的解压工具即可解压，解压好了后如图

![image-20240522175916072](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240522175916072.png)



## 执行测试

![image-20240522180125541](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240522180125541.png)

![image-20240522180148208](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240522180148208.png)

![image-20240522180110882](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240522180110882.png)

执行结果如下则表示成功：

```
Hyper Parameters

Learning Rate: 5e-05
Drop out: 0.4
Batch dim: 128
Number of epochs: 300

Loss: categorical_crossentropy

Model: "sequential"
_________________________________________________________________
Layer (type)                 Output Shape              Param #   
=================================================================
conv1d (Conv1D)              (None, 700, 1024)         1440768   
_________________________________________________________________
max_pooling1d (MaxPooling1D) (None, 700, 1024)         0
_________________________________________________________________
dropout (Dropout)            (None, 700, 1024)         0
_________________________________________________________________
conv1d_1 (Conv1D)            (None, 700, 512)          19399168
_________________________________________________________________
max_pooling1d_1 (MaxPooling1 (None, 700, 512)          0
_________________________________________________________________
dropout_1 (Dropout)          (None, 700, 512)          0
_________________________________________________________________
conv1d_2 (Conv1D)            (None, 700, 256)          4849920
_________________________________________________________________
max_pooling1d_2 (MaxPooling1 (None, 700, 256)          0
_________________________________________________________________
dropout_2 (Dropout)          (None, 700, 256)          0
_________________________________________________________________
conv1d_3 (Conv1D)            (None, 700, 8)            75784
=================================================================
Total params: 25,765,640
Trainable params: 25,765,640
Non-trainable params: 0
```



# 可能你会遇到报错（也许不会遇到）

## 问题1：

```
(base) D:\github\TianChi_Protein-Secondary-Structure-Prediction-master>conda create -n py38tf python=3.8
Collecting package metadata (current_repodata.json): done
Solving environment: failed with repodata from current_repodata.json, will retry with next repodata source.
Collecting package metadata (repodata.json): done
Solving environment: failed

PackagesNotFoundError: The following packages are not available from current channels:

  - python=3.8

Current channels:

  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/win-64
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/noarch

To search for alternate channels that may provide the conda package you're
looking for, navigate to

    https://anaconda.org

and use the search bar at the top of the page.


```

### 解决方法：更换conda 的源，这里更换清华源https://mirrors.tuna.tsinghua.edu.cn/help/anaconda/

```
在命令行输入：

conda config --set show_channel_urls yes

打开C:\Users\zjq18\.condarc

替换内容如下：
channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  msys2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  menpo: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  pytorch-lts: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  simpleitk: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  deepmodeling: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/
```



## 问题2

ERROR: pip's dependency resolver does not currently take into account all the packages that are installed. This behaviour is the source of the following dependency conflicts.
tensorflow-intel 2.13.0 requires keras<2.14,>=2.13.1, which is not installed.
tensorflow-intel 2.13.0 requires libclang>=13.0.0, which is not installed.
tensorflow-intel 2.13.0 requires packaging, which is not installed.
tensorflow-intel 2.13.0 requires tensorflow-io-gcs-filesystem>=0.23.1; platform_machine != "arm64" or platform_system != "Darwin", which is not installed.
tensorflow-intel 2.13.0 requires absl-py>=1.0.0, but you have absl-py 0.15.0 which is incompatible.
tensorflow-intel 2.13.0 requires flatbuffers>=23.1.21, but you have flatbuffers 1.12 which is incompatible.
tensorflow-intel 2.13.0 requires numpy<=1.24.3,>=1.22, but you have numpy 1.19.5 which is incompatible.
tensorflow-intel 2.13.0 requires tensorboard<2.14,>=2.13, but you have tensorboard 2.11.2 which is incompatible.
tensorflow-intel 2.13.0 requires tensorflow-estimator<2.14,>=2.13.0, but you have tensorflow-estimator 2.4.0 which is incompatible.

### 解释：

1. **`tensorflow-intel` 2.13.0 需要的 `keras` 版本不在当前环境中**：`tensorflow-intel` 需要的 `keras` 版本为 `<2.14,>=2.13.1`，但环境中未安装。
2. **缺少 `libclang` 和 `packaging`**：这两个库是 `tensorflow-intel` 2.13.0 运行所必需的，但未在当前环境中安装。
3. **`tensorflow-intel` 需要的 `tensorflow-io-gcs-filesystem` 版本不在当前环境中**：这个依赖仅在特定平台条件下需要。
4. **`absl-py` 版本不兼容**：`tensorflow-intel` 需要 `absl-py>=1.0.0`，但环境中安装的是 `absl-py 0.15.0`。
5. **`flatbuffers` 和 `numpy` 版本不兼容**：`tensorflow-intel` 需要的版本分别为 `flatbuffers>=23.1.21` 和 `numpy<=1.24.3,>=1.22`，但环境中安装的版本分别是 `flatbuffers 1.12` 和 `numpy 1.19.5`。
6. **`tensorboard` 和 `tensorflow-estimator` 版本不兼容**：`tensorflow-intel` 需要的版本分别为 `tensorboard<2.14,>=2.13` 和 `tensorflow-estimator<2.14,>=2.13.0`，但环境中安装的版本分别是 `tensorboard 2.11.2` 和 `tensorflow-estimator 2.4.0`。

### 遇到这问题是因为安装的是pip install tensorflow==2.4.1   解决方法：修改pip install tensorflow-gpu==2.4.3



## 问题3

```
. : 无法加载文件 C:\Users\zjq18\Documents\WindowsPowerShell\profile.ps1，因为在此系统上禁止运行脚本。有关详细信息，请参阅 https:/go.microsoft.com/fwlink/
?LinkID=135170 中的 about_Execution_Policies。
所在位置 行:1 字符: 3

+ . 'C:\Users\zjq18\Documents\WindowsPowerShell\profile.ps1'
+ CategoryInfo          : SecurityError: (:) []，PSSecurityException
+ FullyQualifiedErrorId : UnauthorizedAccess
```

### 解决方法：

```
- 原因：windows系统出于安全考虑，默认禁止脚本文件运行的
- 解决办法：设置系统允许脚本运行

1. win + x 以管理员身份运行PowerShell
2. 输入set-executionpolicy remotesigned，设置成Y即可（输入Y回车即可）
```

## 问题4

```
(py38tf) PS D:\my_code\TianChi_Protein-Secondary-Structure-Prediction-master> python .\evaluate.py
RuntimeError: module compiled against API version 0xf but this version of numpy is 0xd
ImportError: numpy.core.multiarray failed to import

The above exception was the direct cause of the following exception:

SystemError: <built-in method __contains__ of dict object at 0x0000022A0BC4A9C0> returned a result with an error set

The above exception was the direct cause of the following exception:

Traceback (most recent call last):
  File "E:\anaconda\envs\py38tf\lib\site-packages\keras\__init__.py", line 3, in <module>
    from tensorflow.keras.layers.experimental.preprocessing import RandomRotation
  File "C:\Users\zjq18\AppData\Roaming\Python\Python38\site-packages\tensorflow\__init__.py", line 38, in <module>
    from tensorflow.python.tools import module_util as _module_util
  File "C:\Users\zjq18\AppData\Roaming\Python\Python38\site-packages\tensorflow\python\__init__.py", line 37, in <module>
    from tensorflow.python.eager import context
  File "C:\Users\zjq18\AppData\Roaming\Python\Python38\site-packages\tensorflow\python\eager\context.py", line 34, in <module>
    from tensorflow.python.client import pywrap_tf_session
  File "C:\Users\zjq18\AppData\Roaming\Python\Python38\site-packages\tensorflow\python\client\pywrap_tf_session.py", line 19, in <module>
    from tensorflow.python.client._pywrap_tf_session import *
ImportError: initialization failed

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File ".\evaluate.py", line 2, in <module>
    import model
  File "D:\my_code\TianChi_Protein-Secondary-Structure-Prediction-master\model.py", line 3, in <module>
    from keras.models import Sequential
  File "E:\anaconda\envs\py38tf\lib\site-packages\keras\__init__.py", line 5, in <module>
    raise ImportError(
ImportError: Keras requires TensorFlow 2.2 or higher. Install TensorFlow via `pip install tensorflow`
```

```
这里有2个报错：

第一个是numpy的版本问题，降低或者是升级版本即可解决

第二个是，可能是因为keras的版本与当前的tensorlfow版本不匹配导致的，尝试解决方案：pip install keras==2.2
```

## 问题4

```
(py38tf) PS D:\my_code\TianChi_Protein-Secondary-Structure-Prediction-master> python.exe .\evaluate.py
2024-05-22 21:09:54.210313: I tensorflow/stream_executor/platform/default/dso_loader.cc:49] Successfully opened dynamic library cudart64_110.dll
Traceback (most recent call last):
  File ".\evaluate.py", line 2, in <module>
    import model
  File "D:\my_code\TianChi_Protein-Secondary-Structure-Prediction-master\model.py", line 3, in <module>
    from keras.models import Sequential
  File "E:\anaconda\envs\py38tf\lib\site-packages\keras\__init__.py", line 21, in <module>
    from keras import models
  File "E:\anaconda\envs\py38tf\lib\site-packages\keras\models\__init__.py", line 18, in <module>
    from keras.engine.functional import Functional
  File "E:\anaconda\envs\py38tf\lib\site-packages\keras\engine\functional.py", line 26, in <module>
    from keras import backend
  File "E:\anaconda\envs\py38tf\lib\site-packages\keras\backend.py", line 32, in <module>
    from keras import backend_config
  File "E:\anaconda\envs\py38tf\lib\site-packages\keras\backend_config.py", line 33, in <module>
    @tf.__internal__.dispatch.add_dispatch_support
AttributeError: module 'tensorflow.compat.v2.__internal__' has no attribute 'dispatch'
```

```
导致这个问题的原因还是因为keras的版本问题
```



# 其他小技巧--pycharm

当pycharm找不到虚拟环境的时候需要配置如下，选择anconda安装的目录，选择condabin下面的conda.bat，然后点击Load Environments即可扫描出来conda有那些环境，这里选择我创建的py37

![image-20240523000839587](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240523000839587.png)



# conda环境导出信息如下

```
name: py37
channels:

  - defaults
    dependencies:
  - _tflow_select=2.3.0=gpu
  - absl-py=1.3.0=py37haa95532_0
  - aiohttp=3.8.3=py37h2bbff1b_0
  - aiosignal=1.2.0=pyhd3eb1b0_0
  - astor=0.8.1=py37haa95532_0
  - astunparse=1.6.3=py_0
  - async-timeout=4.0.2=py37haa95532_0
  - asynctest=0.13.0=py_0
  - attrs=22.1.0=py37haa95532_0
  - blas=1.0=mkl
  - blinker=1.4=py37haa95532_0
  - brotlipy=0.7.0=py37h2bbff1b_1003
  - ca-certificates=2024.3.11=haa95532_0
  - cachetools=4.2.2=pyhd3eb1b0_0
  - certifi=2022.12.7=py37haa95532_0
  - cffi=1.15.1=py37h2bbff1b_3
  - charset-normalizer=2.0.4=pyhd3eb1b0_0
  - click=8.0.4=py37haa95532_0
  - colorama=0.4.6=py37haa95532_0
  - cryptography=39.0.1=py37h21b164f_0
  - cudatoolkit=10.1.243=h74a9793_0
  - cudnn=7.6.4=cuda10.1_0
  - dataclasses=0.8=pyh6d0b6a4_7
  - fftw=3.3.9=h2bbff1b_2
  - flit-core=3.6.0=pyhd3eb1b0_0
  - frozenlist=1.3.3=py37h2bbff1b_0
  - gast=0.3.3=py_0
  - google-auth=2.6.0=pyhd3eb1b0_0
  - google-auth-oauthlib=0.4.4=pyhd3eb1b0_0
  - google-pasta=0.2.0=pyhd3eb1b0_0
  - grpcio=1.42.0=py37hc60d5dd_0
  - h5py=2.10.0=py37h5e291fa_0
  - hdf5=1.10.4=h7ebc959_0
  - icc_rt=2022.1.0=h6049295_2
  - idna=3.4=py37haa95532_0
  - importlib-metadata=4.11.3=py37haa95532_0
  - intel-openmp=2021.4.0=haa95532_3556
  - keras=2.4.3=hd3eb1b0_0
  - keras-applications=1.0.8=py_1
  - keras-base=2.4.3=pyhd3eb1b0_0
  - keras-preprocessing=1.1.2=pyhd3eb1b0_0
  - libprotobuf=3.20.3=h23ce68f_0
  - markdown=3.4.1=py37haa95532_0
  - mkl=2021.4.0=haa95532_640
  - mkl-service=2.4.0=py37h2bbff1b_0
  - mkl_fft=1.3.1=py37h277e83a_0
  - mkl_random=1.2.2=py37hf11a4ad_0
  - multidict=6.0.2=py37h2bbff1b_0
  - numpy=1.21.5=py37h7a0a035_3
  - numpy-base=1.21.5=py37hca35cd5_3
  - oauthlib=3.2.1=py37haa95532_0
  - openssl=1.1.1w=h2bbff1b_0
  - opt_einsum=3.3.0=pyhd3eb1b0_1
  - pip=22.3.1=py37haa95532_0
  - protobuf=3.20.3=py37hd77b12b_0
  - pyasn1=0.4.8=pyhd3eb1b0_0
  - pyasn1-modules=0.2.8=py_0
  - pycparser=2.21=pyhd3eb1b0_0
  - pyjwt=2.4.0=py37haa95532_0
  - pyopenssl=23.0.0=py37haa95532_0
  - pyreadline=2.1=py37_1
  - pysocks=1.7.1=py37_1
  - python=3.7.16=h6244533_0
  - pyyaml=6.0=py37h2bbff1b_1
  - requests=2.28.1=py37haa95532_0
  - requests-oauthlib=1.3.0=py_0
  - rsa=4.7.2=pyhd3eb1b0_1
  - scipy=1.7.3=py37h7a0a035_2
  - setuptools=65.6.3=py37haa95532_0
  - six=1.16.0=pyhd3eb1b0_1
  - sqlite=3.45.3=h2bbff1b_0
  - tensorboard=2.10.0=py37haa95532_0
  - tensorboard-data-server=0.6.1=py37haa95532_0
  - tensorboard-plugin-wit=1.8.1=py37haa95532_0
  - tensorflow=2.3.0=mkl_py37h10aaca4_0
  - tensorflow-base=2.3.0=eigen_py37h17acbac_0
  - tensorflow-estimator=2.6.0=pyh7b7c402_0
  - tensorflow-gpu=2.3.0=he13fc11_0
  - termcolor=2.1.0=py37haa95532_0
  - typing-extensions=4.4.0=py37haa95532_0
  - typing_extensions=4.4.0=py37haa95532_0
  - urllib3=1.26.14=py37haa95532_0
  - vc=14.2=h2eaa2aa_1
  - vs2015_runtime=14.29.30133=h43f2093_3
  - werkzeug=2.0.3=pyhd3eb1b0_0
  - wheel=0.38.4=py37haa95532_0
  - win_inet_pton=1.1.0=py37haa95532_0
  - wincertstore=0.2=py37haa95532_2
  - wrapt=1.14.1=py37h2bbff1b_0
  - yaml=0.2.5=he774522_0
  - yarl=1.8.1=py37h2bbff1b_0
  - zipp=3.11.0=py37haa95532_0
  - zlib=1.2.13=h8cc25b3_1
    prefix: E:\anaconda\envs\py37
```

