# 项目地址

[xmed—lab/CLIPN：ICCV 2023：CLIPN用于零触发OOD检测：教CLIP说不 --- xmed-lab/CLIPN: ICCV 2023: CLIPN for Zero-Shot OOD Detection: Teaching CLIP to Say No (github.com)](https://github.com/xmed-lab/CLIPN)



环境情况：（autodl）a400 ubuntu20.04 cuda11.8



## 更新conda

```
conda init

wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda3-latest-Linux-x86_64.sh

bash ./Miniconda3-latest-Linux-x86_64.sh  -u
```

## 克隆仓库

```
git clone https://github.com/xmed-lab/CLIPN.git
cd CLIPN
conda create -n CLIPN   python=3.8    
#python=3.9 和 3.11报错 python-apt==2.0.0+ubuntu0.20.4.8的报错
conda activate CLIPN
# pip install -r ./requirements.txt     #各种报错，不要使用
```



## 安装torch=2.0.1

```
conda install pytorch==2.0.1 torchvision==0.15.2 torchaudio==2.0.2 pytorch-cuda=11.8 -c pytorch -c nvidia
```



## 安装python模块

```
pip instal cmake==3.27.2

pip install tqdm==4.66.1

pip install ftfy==6.1.1

pip install regex==2023.8.8

pip install braceexpand==0.1.7

pip install pandas==2.0.3

pip instal webdataset==0.2.48

pip install tensorboard==2.14.0

pip install webdataset==0.2.48
```

```
pip install huggingface_hub  #跑的时候会用到这个,是在src/training/pretrained.py #255

pip install wandb  #通过src/training/main.py知道的#238

pip install Horovod #通过src/training/distributed.py 知道的

pip install timm==0.9.5 #src/training/timm_model.py #36

pip install sentencepiece==0.1.99

pip install transformers

pip install git+https://github.com/rwightman/pytorch-image-models  #src/training/timm_model.py #89 #这个会报错，可以不安装
```



## 下载cc3m数据

教程：[img2dataset/dataset_examples/www.example.com at main·rom1504/img2dataset --- img2dataset/dataset_examples/cc3m.md at main · rom1504/img2dataset (github.com)](https://github.com/rom1504/img2dataset/blob/main/dataset_examples/cc3m.md)

下载地址：[概念标题 --- Conceptual Captions (google.com)](https://ai.google.com/research/ConceptualCaptions/download)  划到最后，点击 Training split即可下载（Train_GCC-training.tsv）

sed -i '1s/^/caption\turl\n/' Train_GCC-training.tsv

执行

cd CLIPN/src 

bash ./run.sh   #修改选择的的显卡，和--nproc_pre_node的输入，我这里修改是0 和 1 第0个显卡，1个显卡

会直接下载https://huggingface.co/laion/CLIP-ViT-B-16-laion2B-s34B-b88K/resolve/main/open_clip_pytorch_model.bin 到/root/.cache/huggingface/hub/tmp2d97aewc

等待下载好了后，会出现找不到xxxx.tar文件，可能是因为数据集的原因吧



待更新--------











