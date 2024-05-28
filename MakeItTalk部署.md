项目地址：

https://github.com/yzhou359/MakeItTalk/tree/main/examples



环境是autodl 的ubuntu16.04  cuda 9.0 ，实际上我使用了conda安装了cuda11.3





升级minconda，新版的有mababa加速

wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda3-latest-Linux-x86_64.sh

bash Miniconda3-latest-Linux-x86_64.sh -u







获取到仓库 

sudo apt update

git clone https://github.com/yzhou359/MakeItTalk.git



创建环境

```
conda create -n makeittalk_env python=3.6
conda activate makeittalk_env
```

```
sudo apt-get install ffmpeg

有毛病
ffmpeg: error while loading shared libraries: libopenh264.so.5: cannot open shared object file: No such file or directory
```

cd ~/MakeItTalk

pip install -r requirements.txt

目前已知版本

```
ffmpeg-python==0.2.0
opencv-python==4.2.0.32
torchvision==0.11.2       #这里安装这个就会自动安装torch==1.10.1，face_alignment的依赖  #肯能是错误，在MakeItTalk/thirdparty/AdaptiveWingLoss中看到的torch是1.3.0
安装torch==1.3.0
torchvision==0.4.1
face_alignment==1.2.0
pysptk==0.1.18
pip install face_alignment==1.3.1

tensorboardX

其他的默认就好了
```





使用国内的源下载，建议：[wine-builds | 镜像站使用帮助 | 清华大学开源软件镜像站 | Tsinghua Open Source Mirror](https://mirrors-i.tuna.tsinghua.edu.cn/help/wine-builds/)  (不适用ubuntu16.04的)

sudo apt-get update
sudo apt-get install software-properties-common

sudo dpkg --add-architecture i386
wget -nc https://dl.winehq.org/wine-builds/winehq.key
sudo apt-key add winehq.key          #国内的网络，要挂加速器
sudo apt-add-repository 'deb https://dl.winehq.org/wine-builds/ubuntu/ xenial main'  或者是

```
sudo apt-add-repository 'deb https://mirrors4.tuna.tsinghua.edu.cn/wine-builds/ubuntu/ bionic main'        对于ubuntu16.04不要使用这个，这个只有从18.04开始的包
```

sudo apt update
sudo apt install --install-recommends winehq-stable



运行quick_demo.ipynb 

即可一键 项目设置+预训练模型的下载

(或者是安装这个操作来也行）

![image-20240520010810369](C:\Users\11755\AppData\Roaming\Typora\typora-user-images\image-20240520010810369.png)



运行的时候出现了

(makeittalk_env) (base) root@autodl-container-19b1118252-0d3514a9:~/MakeItTalk# python main_end2end.py  --jpg /root/MakeItTalk/examples/paint_boy2.jpg
/root/miniconda3/envs/makeittalk_env/lib/python3.6/site-packages/torch/cuda/__init__.py:143: UserWarning: 
NVIDIA GeForce RTX 3080 with CUDA capability sm_86 is not compatible with the current PyTorch installation.
The current PyTorch install supports CUDA capabilities sm_37 sm_50 sm_60 sm_70.
If you want to use the NVIDIA GeForce RTX 3080 GPU with PyTorch, please check the instructions at https://pytorch.org/get-started/locally/

  warnings.warn(incompatible_device_warn.format(device_name, capability, " ".join(arch_list), device_name))
Traceback (most recent call last):
  File "main_end2end.py", line 72, in <module>
    shapes = predictor.get_landmarks(img)
  File "/root/miniconda3/envs/makeittalk_env/lib/python3.6/site-packages/face_alignment/api.py", line 100, in get_landmarks
    return self.get_landmarks_from_image(image_or_path, detected_faces)
  File "/root/miniconda3/envs/makeittalk_env/lib/python3.6/site-packages/torch/autograd/grad_mode.py", line 28, in decorate_context
    return func(*args, **kwargs)
  File "/root/miniconda3/envs/makeittalk_env/lib/python3.6/site-packages/face_alignment/api.py", line 127, in get_landmarks_from_image
    if image.ndim == 2:
AttributeError: 'NoneType' object has no attribute 'ndim'



解决方法torch报了算力问题：

```
conda install pytorch==1.10.1 torchvision==0.11.2 torchaudio==0.10.1 cudatoolkit=11.3 -c pytorch -c conda-forge
```

解决问题2：

pip install face_alignment==1.3.0

或者是因为图片的有问题的原因，或者是，图片不出现



还有就是不需要加绝对路径，只需要确保图片的保存在examples里面，运行只需要 python main_end2end.py  --jpg paint_boy2.jpg 即可，注意图片是需要256*256，因为是wav格式的，，，，只需要指定图片，不需要指定音频，会自动寻找音频，把所有的因为都配上去。



遇到的问题

W: GPG error: https://dl.winehq.org/wine-builds/ubuntu xenial InRelease: The following signatures couldn't be verified because the public key is not available: NO_PUBKEY 76F1A20FF987672F
E: The repository 'https://dl.winehq.org/wine-builds/ubuntu xenial InRelease' is not signed.
N: Updating from such a repository can't be done securely, and is therefore disabled by default.
N: See apt-secure(8) manpage for repository creation and user configuration details.









(makeittalk_env) (base) root@autodl-container-19b1118252-0d3514a9:~/MakeItTalk# python main_end2end.py --jpg trump.jpg
Traceback (most recent call last):
  File "main_end2end.py", line 72, in <module>
    shapes = predictor.get_landmarks(img)
  File "/root/miniconda3/envs/makeittalk_env/lib/python3.6/site-packages/face_alignment/api.py", line 89, in get_landmarks
    return self.get_landmarks_from_image(image_or_path, detected_faces)
  File "/root/miniconda3/envs/makeittalk_env/lib/python3.6/site-packages/torch/autograd/grad_mode.py", line 28, in decorate_context
    return func(*args, **kwargs)
  File "/root/miniconda3/envs/makeittalk_env/lib/python3.6/site-packages/face_alignment/api.py", line 108, in get_landmarks_from_image
    detected_faces = self.face_detector.detect_from_image(image.copy())
  File "/root/miniconda3/envs/makeittalk_env/lib/python3.6/site-packages/face_alignment/detection/sfd/sfd_detector.py", line 44, in detect_from_image
    bboxlist = detect(self.face_detector, image, device=self.device)[0]
  File "/root/miniconda3/envs/makeittalk_env/lib/python3.6/site-packages/face_alignment/detection/sfd/detect.py", line 26, in detect
    return batch_detect(net, img, device)
  File "/root/miniconda3/envs/makeittalk_env/lib/python3.6/site-packages/face_alignment/detection/sfd/detect.py", line 41, in batch_detect
    img_batch = img_batch - torch.Tensor([104, 117, 123]).view(1, 3, 1, 1)
RuntimeError: Expected all tensors to be on the same device, but found at least two devices, cuda:0 and cpu!









face_alignment==1.3.1

























conda导出环境

```
name: makeittalk_env
channels:

  - pytorch
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - conda-forge
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/pytorch/
  - defaults
    dependencies:
  - _libgcc_mutex=0.1=conda_forge
  - _openmp_mutex=4.5=2_gnu
  - argon2-cffi=21.1.0=py36h8f6f2f9_0
  - async_generator=1.10=py_0
  - attrs=22.2.0=pyh71513ae_0
  - backcall=0.2.0=pyh9f0ad1d_0
  - backports=1.0=pyhd8ed1ab_3
  - backports.functools_lru_cache=2.0.0=pyhd8ed1ab_0
  - blas=2.16=mkl
  - bleach=6.1.0=pyhd8ed1ab_0
  - bzip2=1.0.8=hd590300_5
  - ca-certificates=2024.3.11=h06a4308_0
  - certifi=2021.5.30=py36h06a4308_0
  - cudatoolkit=11.3.1=hb98b00a_13
  - dataclasses=0.8=pyh787bdff_2
  - defusedxml=0.7.1=pyhd8ed1ab_0
  - entrypoints=0.4=pyhd8ed1ab_0
  - ffmpeg=4.3=hf484d3e_0
  - freetype=2.10.4=h0708190_1
  - gmp=6.3.0=h59595ed_1
  - gnutls=3.6.13=h85f3911_1
  - importlib-metadata=4.8.1=py36h5fab9bb_0
  - intel-openmp=2022.1.0=h9e868ea_3769
  - ipykernel=5.5.5=py36hcb3619a_0
  - ipython=7.16.1=py36he448a4c_2
  - ipython_genutils=0.2.0=py_1
  - ipywidgets=7.7.4=pyhd8ed1ab_0
  - jbig=2.1=h7f98852_2003
  - jedi=0.17.2=py36h5fab9bb_1
  - jinja2=3.0.3=pyhd8ed1ab_0
  - jpeg=9e=h0b41bf4_3
  - jsonschema=4.1.2=pyhd8ed1ab_0
  - jupyter=1.0.0=pyhd8ed1ab_10
  - jupyter_client=7.1.2=pyhd8ed1ab_0
  - jupyter_console=6.5.1=pyhd8ed1ab_0
  - jupyter_core=4.8.1=py36h5fab9bb_0
  - jupyterlab_pygments=0.1.2=pyh9f0ad1d_0
  - jupyterlab_widgets=1.1.1=pyhd8ed1ab_0
  - lame=3.100=h166bdaf_1003
  - lcms2=2.12=hddcbb42_0
  - ld_impl_linux-64=2.38=h1181459_1
  - lerc=2.2.1=h9c3ff4c_0
  - libblas=3.8.0=16_mkl
  - libcblas=3.8.0=16_mkl
  - libdeflate=1.7=h7f98852_5
  - libffi=3.3=he6710b0_2
  - libgcc-ng=13.2.0=h77fa898_7
  - libgfortran-ng=7.5.0=h14aa051_20
  - libgfortran4=7.5.0=h14aa051_20
  - libgomp=13.2.0=h77fa898_7
  - libiconv=1.17=hd590300_2
  - liblapack=3.8.0=16_mkl
  - liblapacke=3.8.0=16_mkl
  - libpng=1.6.37=h21135ba_2
  - libsodium=1.0.18=h36c2ea0_1
  - libstdcxx-ng=13.2.0=hc0a3c3a_7
  - libtiff=4.3.0=hf544144_1
  - libuv=1.48.0=hd590300_0
  - libwebp-base=1.4.0=hd590300_0
  - lz4-c=1.9.3=h9c3ff4c_1
  - markupsafe=2.0.1=py36h8f6f2f9_0
  - mistune=0.8.4=pyh1a96a4e_1006
  - mkl=2020.2=256
  - nbclient=0.5.9=pyhd8ed1ab_0
  - nbconvert=6.0.7=py36h5fab9bb_3
  - nbformat=5.1.3=pyhd8ed1ab_0
  - ncurses=6.4=h6a678d5_0
  - nest-asyncio=1.6.0=pyhd8ed1ab_0
  - nettle=3.6=he412f7d_0
  - notebook=6.3.0=py36h5fab9bb_0
  - numpy=1.19.5=py36hfc0c790_2
  - olefile=0.46=pyh9f0ad1d_1
  - openh264=2.1.1=h780b84a_0
  - openjpeg=2.4.0=hb52868f_1
  - openssl=1.1.1w=h7f8727e_0
  - packaging=21.3=pyhd8ed1ab_0
  - pandoc=2.19.2=ha770c72_0
  - pandocfilters=1.5.0=pyhd8ed1ab_0
  - parso=0.7.1=pyh9f0ad1d_0
  - pexpect=4.8.0=pyh1a96a4e_2
  - pickleshare=0.7.5=py_1003
  - pip=21.2.2=py36h06a4308_0
  - prometheus_client=0.17.1=pyhd8ed1ab_0
  - prompt-toolkit=3.0.36=pyha770c72_0
  - prompt_toolkit=3.0.36=hd8ed1ab_0
  - ptyprocess=0.7.0=pyhd3deb0d_0
  - pycparser=2.21=pyhd8ed1ab_0
  - pygments=2.14.0=pyhd8ed1ab_0
  - pyparsing=3.1.2=pyhd8ed1ab_0
  - pyrsistent=0.17.3=py36h8f6f2f9_2
  - python=3.6.13=h12debd9_1
  - python_abi=3.6=2_cp36m
  - pytorch=1.10.1=py3.6_cuda11.3_cudnn8.2.0_0
  - pytorch-mutex=1.0=cuda
  - pyzmq=22.3.0=py36h7068817_0
  - qtconsole-base=5.2.2=pyhd8ed1ab_1
  - qtpy=2.0.1=pyhd8ed1ab_0
  - readline=8.2=h5eee18b_0
  - send2trash=1.8.2=pyh41d4057_0
  - setuptools=58.0.4=py36h06a4308_0
  - six=1.16.0=pyh6c4a22f_0
  - sqlite=3.45.3=h5eee18b_0
  - terminado=0.12.1=py36h5fab9bb_0
  - testpath=0.6.0=pyhd8ed1ab_0
  - tk=8.6.14=h39e8969_0
  - torchaudio=0.10.1=py36_cu113
  - tornado=6.1=py36h8f6f2f9_1
  - traitlets=4.3.3=pyhd8ed1ab_2
  - typing_extensions=4.1.1=pyha770c72_0
  - wcwidth=0.2.10=pyhd8ed1ab_0
  - webencodings=0.5.1=pyhd8ed1ab_2
  - wheel=0.37.1=pyhd3eb1b0_0
  - widgetsnbextension=3.6.1=pyha770c72_0
  - xz=5.4.6=h5eee18b_1
  - zeromq=4.3.5=h59595ed_1
  - zipp=3.6.0=pyhd8ed1ab_0
  - zlib=1.2.13=h5eee18b_1
  - zstd=1.5.0=ha95c52a_0
  - pip:
    - appdirs==1.4.4
    - audioread==3.0.1
    - beautifulsoup4==4.12.3
    - cffi==1.15.1
    - charset-normalizer==2.0.12
    - cycler==0.11.0
    - cython==3.0.10
    - decorator==4.4.2
    - face-alignment==1.3.1
    - ffmpeg-python==0.2.0
    - filelock==3.4.1
    - future==1.0.0
    - gdown==4.7.3
    - idna==3.7
    - imageio==2.15.0
    - importlib-resources==5.4.0
    - joblib==1.1.1
    - kiwisolver==1.3.1
    - librosa==0.9.2
    - llvmlite==0.36.0
    - matplotlib==3.3.4
    - mutagen==1.45.1
    - networkx==2.5.1
    - numba==0.53.1
    - opencv-python==3.4.0.12
    - pillow==8.4.0
    - pooch==1.6.0
    - protobuf==4.21.0
    - pydub==0.25.1
    - pynormalize==0.1.4
    - pysocks==1.7.1
    - pysptk==0.1.18
    - python-dateutil==2.9.0.post0
    - pywavelets==1.1.1
    - pyworld==0.3.4
    - requests==2.27.1
    - resampy==0.4.3
    - resemblyzer==0.1.3
    - scikit-image==0.17.2
    - scikit-learn==0.24.2
    - scipy==1.5.4
    - soundfile==0.12.1
    - soupsieve==2.3.2.post1
    - tensorboardx==2.6.2.2
    - threadpoolctl==3.1.0
    - tifffile==2020.9.3
    - torch==1.10.1
    - torchvision==0.11.2
    - tqdm==4.64.1
    - typing==3.7.4.3
    - urllib3==1.26.18
    - webrtcvad==2.0.10
      prefix: /root/miniconda3/envs/makeittalk_env
```









pip的环境

```
appdirs==1.4.4
argon2-cffi @ file:///home/conda/feedstock_root/build_artifacts/argon2-cffi_1633990451307/work
async-generator==1.10
attrs @ file:///home/conda/feedstock_root/build_artifacts/attrs_1671632566681/work
audioread==3.0.1
backcall @ file:///home/conda/feedstock_root/build_artifacts/backcall_1592338393461/work
backports.functools-lru-cache @ file:///home/conda/feedstock_root/build_artifacts/backports.functools_lru_cache_1702571698061/work
beautifulsoup4==4.12.3
bleach @ file:///home/conda/feedstock_root/build_artifacts/bleach_1696630167146/work
certifi==2021.5.30
cffi==1.15.1
charset-normalizer==2.0.12
cycler==0.11.0
Cython==3.0.10
dataclasses @ file:///home/conda/feedstock_root/build_artifacts/dataclasses_1628958435052/work
decorator==4.4.2
defusedxml @ file:///home/conda/feedstock_root/build_artifacts/defusedxml_1615232257335/work
entrypoints @ file:///home/conda/feedstock_root/build_artifacts/entrypoints_1643888246732/work
face-alignment==1.3.1
ffmpeg-python==0.2.0
filelock==3.4.1
future==1.0.0
gdown==4.7.3
idna==3.7
imageio==2.15.0
importlib-metadata @ file:///home/conda/feedstock_root/build_artifacts/importlib-metadata_1630267465156/work
importlib-resources==5.4.0
ipykernel @ file:///home/conda/feedstock_root/build_artifacts/ipykernel_1620912934572/work/dist/ipykernel-5.5.5-py3-none-any.whl
ipython @ file:///home/conda/feedstock_root/build_artifacts/ipython_1609697613279/work
ipython-genutils==0.2.0
ipywidgets @ file:///home/conda/feedstock_root/build_artifacts/ipywidgets_1679421482533/work
jedi @ file:///home/conda/feedstock_root/build_artifacts/jedi_1605054537831/work
Jinja2 @ file:///home/conda/feedstock_root/build_artifacts/jinja2_1636510082894/work
joblib==1.1.1
jsonschema @ file:///home/conda/feedstock_root/build_artifacts/jsonschema_1634752161479/work
jupyter @ file:///home/conda/feedstock_root/build_artifacts/jupyter_1696255489086/work
jupyter-client @ file:///home/conda/feedstock_root/build_artifacts/jupyter_client_1642858610849/work
jupyter-console @ file:///home/conda/feedstock_root/build_artifacts/jupyter_console_1676328545892/work
jupyter-core @ file:///home/conda/feedstock_root/build_artifacts/jupyter_core_1631852698933/work
jupyterlab-pygments @ file:///home/conda/feedstock_root/build_artifacts/jupyterlab_pygments_1601375948261/work
jupyterlab-widgets @ file:///home/conda/feedstock_root/build_artifacts/jupyterlab_widgets_1655961217661/work
kiwisolver==1.3.1
librosa==0.9.2
llvmlite==0.36.0
MarkupSafe @ file:///home/conda/feedstock_root/build_artifacts/markupsafe_1621455668064/work
matplotlib==3.3.4
mistune @ file:///home/conda/feedstock_root/build_artifacts/mistune_1673904152039/work
mutagen==1.45.1
nbclient @ file:///home/conda/feedstock_root/build_artifacts/nbclient_1637327213451/work
nbconvert @ file:///home/conda/feedstock_root/build_artifacts/nbconvert_1605401832871/work
nbformat @ file:///home/conda/feedstock_root/build_artifacts/nbformat_1617383142101/work
nest_asyncio @ file:///home/conda/feedstock_root/build_artifacts/nest-asyncio_1705850609492/work
networkx==2.5.1
notebook @ file:///home/conda/feedstock_root/build_artifacts/notebook_1616419146127/work
numba==0.53.1
numpy @ file:///home/conda/feedstock_root/build_artifacts/numpy_1626681920064/work
olefile @ file:///home/conda/feedstock_root/build_artifacts/olefile_1602866521163/work
opencv-python==3.4.0.12
packaging @ file:///home/conda/feedstock_root/build_artifacts/packaging_1637239678211/work
pandocfilters @ file:///home/conda/feedstock_root/build_artifacts/pandocfilters_1631603243851/work
parso @ file:///home/conda/feedstock_root/build_artifacts/parso_1595548966091/work
pexpect @ file:///home/conda/feedstock_root/build_artifacts/pexpect_1667297516076/work
pickleshare @ file:///home/conda/feedstock_root/build_artifacts/pickleshare_1602536217715/work
Pillow==8.4.0
pooch==1.6.0
prometheus-client @ file:///home/conda/feedstock_root/build_artifacts/prometheus_client_1689032443210/work
prompt-toolkit @ file:///home/conda/feedstock_root/build_artifacts/prompt-toolkit_1670414775770/work
protobuf==4.21.0
ptyprocess @ file:///home/conda/feedstock_root/build_artifacts/ptyprocess_1609419310487/work/dist/ptyprocess-0.7.0-py2.py3-none-any.whl
pycparser @ file:///home/conda/feedstock_root/build_artifacts/pycparser_1636257122734/work
pydub==0.25.1
Pygments @ file:///home/conda/feedstock_root/build_artifacts/pygments_1672682006896/work
pynormalize==0.1.4
pyparsing @ file:///home/conda/feedstock_root/build_artifacts/pyparsing_1709721012883/work
pyrsistent @ file:///home/conda/feedstock_root/build_artifacts/pyrsistent_1610146795286/work
PySocks==1.7.1
pysptk==0.1.18
python-dateutil==2.9.0.post0
PyWavelets==1.1.1
pyworld==0.3.4
pyzmq @ file:///home/conda/feedstock_root/build_artifacts/pyzmq_1631793305981/work
qtconsole @ file:///home/conda/feedstock_root/build_artifacts/qtconsole-base_1640876679830/work
QtPy @ file:///home/conda/feedstock_root/build_artifacts/qtpy_1643828301492/work
requests==2.27.1
resampy==0.4.3
Resemblyzer==0.1.3
scikit-image==0.17.2
scikit-learn==0.24.2
scipy==1.5.4
Send2Trash @ file:///home/conda/feedstock_root/build_artifacts/send2trash_1682601222253/work
six @ file:///home/conda/feedstock_root/build_artifacts/six_1620240208055/work
soundfile==0.12.1
soupsieve==2.3.2.post1
tensorboardX==2.6.2.2
terminado @ file:///home/conda/feedstock_root/build_artifacts/terminado_1631128154882/work
testpath @ file:///home/conda/feedstock_root/build_artifacts/testpath_1645693042223/work
threadpoolctl==3.1.0
tifffile==2020.9.3
torch==1.10.1
torchaudio==0.10.1
torchvision==0.11.2
tornado @ file:///home/conda/feedstock_root/build_artifacts/tornado_1610094701020/work
tqdm==4.64.1
traitlets @ file:///home/conda/feedstock_root/build_artifacts/traitlets_1631041982274/work
typing==3.7.4.3
typing_extensions @ file:///home/conda/feedstock_root/build_artifacts/typing_extensions_1644850595256/work
urllib3==1.26.18
wcwidth @ file:///home/conda/feedstock_root/build_artifacts/wcwidth_1699959196938/work
webencodings @ file:///home/conda/feedstock_root/build_artifacts/webencodings_1694681268211/work
webrtcvad==2.0.10
widgetsnbextension @ file:///home/conda/feedstock_root/build_artifacts/widgetsnbextension_1655939017940/work
zipp @ file:///home/conda/feedstock_root/build_artifacts/zipp_1633302054558/work
```

