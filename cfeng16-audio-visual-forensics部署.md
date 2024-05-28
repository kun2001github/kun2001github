# 项目地址

[cfeng16/audio-visual-forensics (github.com)](https://github.com/cfeng16/audio-visual-forensics/blob/main/requirements.txt)



# 部署环境

![089cd2bfe1f1cc595d9ba41149b3fde](E:\Users\11755\Documents\WeChat Files\wxid_y4e5iptph7pa22\FileStorage\Temp\089cd2bfe1f1cc595d9ba41149b3fde.jpg)



# 开始部署

## 使用vscode连接autodl服务器

### 升级conda



## 克隆项目

 git clone https://github.com/cfeng16/audio-visual-forensics.git

 cd audio-visual-forensics/



## 克隆环境

 conda create -n py38 --clone base

因为选择的autodl镜像是torch1.9.0的版本，直接克隆他的就好了



 conda activate py38













## 测试

```
CUDA_VISIBLE_DEVICES=0

python detect.py --test_video_path /root/audio-visual-forensics/test_video.mp4 --device cuda:0 --max-len 50 --n_workers 4  --bs 1 --lam 0 --output_dir /root/audio-visual-forensics/save
```

安装

 pip install pandas==1.3.5

 pip install librosa==0.9.1

 pip install torchaudio==0.9.0

 pip install av==9.0.1

 pip install einops==0.4.1