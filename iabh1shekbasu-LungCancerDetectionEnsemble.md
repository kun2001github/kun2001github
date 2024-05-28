# 项目介绍：[使用深度学习模型集合从胸部 CT 扫描中检测肺癌 |带代码的论文 --- Lung cancer detection from thoracic CT scans using an ensemble of deep learning models | Papers With Code](https://paperswithcode.com/paper/lung-cancer-detection-from-thoracic-ct-scans)

# 项目地址：[iabh1shekbasu/LungCancerDetectionEnsemble (github.com)](https://github.com/iabh1shekbasu/LungCancerDetectionEnsemble)



部署前提，安装vscode，安装conda，安装git

### 坑逼，没有环境配置



## 克隆仓库：

git clone https://github.com/iabh1shekbasu/LungCancerDetectionEnsemble.git

cd LungCancerDetectionEnsemble

## 下载数据集：

下载好数据集后，存放在data目录下

[data - Google 云端硬盘](https://drive.google.com/drive/folders/1xLB687c_0cuPdQntENGWxvnb92tEAELT)



## 安装环境



conda create --prefix E:\anconda\envs\py38 python=3.8

conda activate E:\anconda\envs\py38

```
conda install pytorch==2.0.1 torchvision==0.15.2 torchaudio==2.0.2 pytorch-cuda=11.7 -c pytorch -c nvidia
```

conda install matplotlib

pip install scikit-learn   

pip install pandas

pip install scikit-[plot](https://so.csdn.net/so/search?q=plot&spm=1001.2101.3001.7020)



```
士大夫


```











遇到的报错

(base) C:\Users\st>conda create --name  py38 python=3.8
Solving environment: failed

CondaHTTPError: HTTP 000 CONNECTION FAILED for url <https://repo.anaconda.com/pkgs/pro/noarch/repodata.json.bz2>
Elapsed: -

An HTTP error occurred when trying to retrieve this URL.
HTTP errors are often intermittent, and a simple retry will get you on your way.

If your current network has https://www.anaconda.com blocked, please file
a support request with your network engineering team.

SSLError(MaxRetryError('HTTPSConnectionPool(host=\'repo.anaconda.com\', port=443): Max retries exceeded with url: /pkgs/pro/noarch/repodata.json.bz2 (Caused by SSLError(SSLError("bad handshake: Error([(\'SSL routines\', \'ssl3_get_server_certificate\', \'certificate verify failed\')])")))'))

解决方案，换源，换清华源就解决了
