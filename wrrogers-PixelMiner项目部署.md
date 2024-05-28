# 项目地址：

[PixelMiner/train_PixelMiner.py at main · wrrogers/PixelMiner (github.com)](https://github.com/wrrogers/PixelMiner)



# 失败   似乎是项目不完整





这个项目是2021年10月14日 最开始是9月17





conda create --name  py37 python=3.7

conda activate py37



pip install numpy==1.19.5

2021.01.06



```
conda install pytorch==1.6.0 torchvision==0.7.0 cudatoolkit=10.2 -c pytorch

2021.04发布 1.6.0
2022.02发布1.7.0
2023.03发布1.8.0
```



pip install  numpy opencv-python matplotlib tqdm scipy scikit-image pandas pillow scikit-learn kivy



pip install nvgpu

pip install SimpleITK==2.2.1

pip install pyradiomics==3.1.0

顺序

pip install wandb

 pip install requests

pip install urllib3  的2.0.7版本提示没有：ModuleNotFoundError: No module named 'urllib3.exceptions'

使用conda install urllib3解决





报错

Traceback (most recent call last):
  File "c:/Users/DELL/Desktop/my_code/PixelMiner-main/train_PixelMiner.py", line 23, in <module>       
    import wandb
  File "X:\anaconda3\envs\py37\lib\site-packages\wandb\__init__.py", line 27, in <module>
    from wandb import sdk as wandb_sdk
  File "X:\anaconda3\envs\py37\lib\site-packages\wandb\sdk\__init__.py", line 24, in <module>
    from . import wandb_helper as helper
  File "X:\anaconda3\envs\py37\lib\site-packages\wandb\sdk\wandb_helper.py", line 6, in <module>       
    from .lib import config_util
  File "X:\anaconda3\envs\py37\lib\site-packages\wandb\sdk\lib\config_util.py", line 10, in <module>   
    from wandb.util import load_yaml
  File "X:\anaconda3\envs\py37\lib\site-packages\wandb\util.py", line 53, in <module>
    import requests
  File "X:\anaconda3\envs\py37\lib\site-packages\requests\__init__.py", line 106, in <module>
    urllib3.__version__, chardet_version, charset_normalizer_version
  File "X:\anaconda3\envs\py37\lib\site-packages\requests\__init__.py", line 86, in check_compatibility
    raise Exception("You need either charset_normalizer or chardet installed")
Exception: You need either charset_normalizer or chardet installed



解决方法：python -m pip install requests chardet



(py37) PS C:\Users\DELL\Desktop\my_code\PixelMiner-main> & X:/anaconda3/envs/py37/python.exe c:/Users/DELL/Desktop/my_code/PixelMiner-main/train_PixelMiner.py
Traceback (most recent call last):
  File "c:/Users/DELL/Desktop/my_code/PixelMiner-main/train_PixelMiner.py", line 31, in <module>
    from pixelcnnpp import sample_from_discretized_mix_logistic, PSNR
ModuleNotFoundError: No module named 'pixelcnnpp'



解决方法： 







固定版本

(py37) PS C:\Users\DELL\Desktop\my_code\PixelMiner-main> python .\generate_whole_image.py
Traceback (most recent call last):
  File ".\generate_whole_image.py", line 17, in <module>
    from skimage.measure import compare_ssim
ImportError: cannot import name 'compare_ssim' from 'skimage.measure' (X:\anaconda3\envs\py37\lib\site-packages\skimage\measure\__init__.py)

pip install scikit-image==0.15.0

[ImportError：无法从“skimage.measure”导入名称“compare_ssim” ·问题 #150 ·williamfzc/stagesepx --- ImportError: cannot import name 'compare_ssim' from 'skimage.measure' · Issue #150 · williamfzc/stagesepx (github.com)](https://github.com/williamfzc/stagesepx/issues/150)





(py37) PS C:\Users\DELL\Desktop\my_code\PixelMiner-main> python .\generate_whole_image.py
Traceback (most recent call last):
  File ".\generate_whole_image.py", line 15, in <module>
    from skimage.metrics import peak_signal_noise_ratio
ModuleNotFoundError: No module named 'skimage.metrics'

pip install scikit-image==0.16.1





问题：

WARNING: Retrying (Retry(total=4, connect=None, read=None, redirect=None, status=None)) after connection broken by 'ProtocolError('Connection aborted.', RemoteDisconnected('Remote end closed connection without response'))': /simple/opencv-python/



```
pip config set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple
```





 Traceback (most recent call last):
   File ".\Qualitative Assessment App.py", line 45, in <module>
     from kivy.garden.matplotlib.backend_kivyagg import FigureCanvasKivyAgg
 ModuleNotFoundError: No module named 'kivy.garden.matplotlib'



 pip uninstall matplotlib

conda install matplotlib



还是不行

pip uninstall kivy

pip uninstall kivy-garden

codna install kivy

conda install kivy-garden



遇到

   File ".\Qualitative Assessment App.py", line 45, in <module>
     from kivy.garden.matplotlib.backend_kivyagg import FigureCanvasKivyAgg
   File "<frozen importlib._bootstrap>", line 983, in _find_and_load
   File "<frozen importlib._bootstrap>", line 967, in _find_and_load_unlocked
   File "<frozen importlib._bootstrap>", line 668, in _load_unlocked
   File "<frozen importlib._bootstrap>", line 640, in _load_backward_compatible
 KeyError: 'kivy.garden.matplotlib'



参考：[成功解决from kivy.garden.matplotlib.backend_kivyagg import FigureCanvasKivyAgg出错_from kivy.garden.matplotlib import figurecanvaskiv-CSDN博客](https://blog.csdn.net/wangxinshero/article/details/94040733)

使用这个项目安装

[kivy-garden/matplotlib: Matplotlib backends using kivy (migration a WIP) (github.com)](https://github.com/kivy-garden/matplotlib)

python setup.py build 

python setup.py install