项目地址：[hongwang01/MEPNet: 【MICCAI2023】Equivariant Proximal Network for Joint Sparse-View Reconstruction and Metal Artifact Reduction in CT Images (github.com)](https://github.com/hongwang01/MEPNet)



部署环境

前提条件安装git，安装conda





git clone https://github.com/hongwang01/MEPNet.git

cd MEPNet

conda create -n MEPNetpy36 python=3.6

conda activate MEPNetpy36

```
conda install cudatoolkit=10.1  
conda install pytorch==1.4.0 cudatoolkit=10.1   -c pytorch  #因为找不到torchvision==0.5.0的包

pip install torchvision==0.5.0
```

pip install -r requirements.txt -i https://pypi.tuna.tsinghua.edu.cn/simple some-package  

分开安装，先安装一部分后再安装一部分

出现：找不到这4个包

astra-toolbox==1.9.9.dev0   #win下每个这个版本

odl==1.0.0.dev0

ztensorboardX==1.8

解决方法：

pip install https://github.com/odlgroup/odl/archive/master.zip   安装odl==1.0.0.dev0

pip install  .\tensorboardX-1.8-py2.py3-none-any.whl  

**conda** **install** **-c** **astra-toolbox/label/dev** **astra-toolbox**

手动下载torch1.4.0的GPU版本

[download.pytorch.org/whl/torch_stable.html](https://download.pytorch.org/whl/torch_stable.html)





问题1：

 File "C:\ProgramData\anaconda3\envs\MEPNetpy36\lib\site-packages\scipy\optimize\__init__.py", line 398, in <module>
    from ._nnls import nnls
ImportError: DLL load failed: 找不到指定的模块。

解决方法：

conda remove --force numpy, scipy

pip install -U [numpy](https://so.csdn.net/so/search?q=numpy&spm=1001.2101.3001.7020), scipy  #似乎安装了1.5.4



问题2：

PS C:\Users\Administrator\Desktop\MEPNet-main> & C:/ProgramData/anaconda3/envs/MEPNetpy36/python.exe c:/Users/Administrator/Desktop/MEPNet-main/test.py
Traceback (most recent call last):
  File "C:\ProgramData\anaconda3\envs\MEPNetpy36\lib\site-packages\pywt\_cwt.py", line 15, in <module>
    import scipy.fft
ModuleNotFoundError: No module named 'scipy.fft'

During handling of the above exception, another exception occurred:

Traceback (most recent call last):
  File "c:/Users/Administrator/Desktop/MEPNet-main/test.py", line 8, in <module>
    import odl
  File "C:\ProgramData\anaconda3\envs\MEPNetpy36\lib\site-packages\odl\__init__.py", line 69, in <module>
    from . import tomo
  File "C:\ProgramData\anaconda3\envs\MEPNetpy36\lib\site-packages\odl\tomo\__init__.py", line 13, in <module>
    from .analytic import *
  File "C:\ProgramData\anaconda3\envs\MEPNetpy36\lib\site-packages\odl\tomo\analytic\__init__.py", line 13, in <module>
    from .filtered_back_projection import *
  File "C:\ProgramData\anaconda3\envs\MEPNetpy36\lib\site-packages\odl\tomo\analytic\filtered_back_projection.py", line 14, in <module>
    from odl.trafos import FourierTransform, PYFFTW_AVAILABLE
  File "C:\ProgramData\anaconda3\envs\MEPNetpy36\lib\site-packages\odl\trafos\__init__.py", line 13, in <module>
    from . import backends, util
  File "C:\ProgramData\anaconda3\envs\MEPNetpy36\lib\site-packages\odl\trafos\backends\__init__.py", line 14, in <module>
    from .pywt_bindings import *
  File "C:\ProgramData\anaconda3\envs\MEPNetpy36\lib\site-packages\odl\trafos\backends\pywt_bindings.py", line 21, in <module>
    import pywt
  File "C:\ProgramData\anaconda3\envs\MEPNetpy36\lib\site-packages\pywt\__init__.py", line 24, in <module>
    from ._cwt import *
  File "C:\ProgramData\anaconda3\envs\MEPNetpy36\lib\site-packages\pywt\_cwt.py", line 22, in <module>
    next_fast_len = fftmodule.next_fast_len
AttributeError: module 'scipy.fftpack' has no attribute 'next_fast_len'

pip install scipy==1.2.1



