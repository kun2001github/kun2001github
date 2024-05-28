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

conda activate py38

```
conda install pytorch==2.0.1 torchvision==0.15.2 torchaudio==2.0.2 pytorch-cuda=11.7 -c pytorch -c nvidia
```

pip install matplotlib

pip install scikit-learn

pip install pandas

pip install scikit-plot







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



问题2

**OutOfMemoryError**: CUDA out of memory. Tried to allocate 2.00 MiB (GPU 0; 4.00 GiB total capacity; 3.44 GiB already allocated; 0 bytes free; 3.46 GiB reserved in total by PyTorch) If reserved memory is >> allocated memory try setting max_split_size_mb to avoid fragmentation.  See documentation for Memory Management and PYTORCH_CUDA_ALLOC_CONF

Output is truncated. View as a [scrollable element](command:cellOutput.enableScrolling?1c6e06e1-80e9-4d1c-8d2b-48a8dbba12fd) or open in a [text editor](command:workbench.action.openLargeOutput?1c6e06e1-80e9-4d1c-8d2b-48a8dbba12fd). Adjust cell output [settings](command:workbench.action.openSettings?["@tag:notebookOutputLayout"])...

解决方案：这是因为显卡的显存不够了，暂未解决，换了电脑跑（我用docker容器跑了）





问题3







---------------------------------------------------------------------------
RuntimeError                              Traceback (most recent call last)
Cell In[18], line 26
     17 # StepLR Decays the learning rate of each parameter group by gamma every step_size epochs
     18 # Decay LR by a factor of 0.1 every 7 epochs
     19 # Learning rate scheduling should be applied after optimizer’s update
   (...)
     23 #     validate(...)
     24 #     scheduler.step()
     25 step_lr_scheduler = lr_scheduler.StepLR(optimizer, step_size = 10, gamma=0.1)
---> 26 model = train_model(model, criterion, optimizer, step_lr_scheduler, num_epochs=10, model_name = "inception_v3")

Cell In[13], line 23
     20 # forward
     21 # track history if only in train
     22 with torch.set_grad_enabled(phase == 'train'):
---> 23     outputs = model(inputs)
     24     _, preds = torch.max(outputs, 1) #was (outputs,1) for non-inception and (outputs.data,1) for inception
     25     loss = criterion(outputs, labels)

File /opt/conda/lib/python3.10/site-packages/torch/nn/modules/module.py:1501, in Module._call_impl(self, *args, **kwargs)
   1496 # If we don't have any hooks, we want to skip the rest of the logic in
   1497 # this function, and just call forward.
   1498 if not (self._backward_hooks or self._backward_pre_hooks or self._forward_hooks or self._forward_pre_hooks
   1499         or _global_backward_pre_hooks or _global_backward_hooks
...
    458                     _pair(0), self.dilation, self.groups)
--> 459 return F.conv2d(input, weight, bias, self.stride,
    460                 self.padding, self.dilation, self.groups)

RuntimeError: Calculated padded input size per channel: (4 x 4). Kernel size: (5 x 5). Kernel size can't be greater than actual input size







问题4

**## Efficientnet B7 Model**



model = models.efficientnet_b7(pretrained = True)
#num_ftrs = model.classifier[0].in_features
#num_ftrs = model.fc.in_features  ##for googlenet, resnet18
#num_ftrs = model.classifier.in_features  ## for densenet169
num_ftrs = model.classifier[1].in_features   ## for efficientnet_b7
print("Number of features: "+str(num_ftrs))
#model.classifier = nn.Linear(num_ftrs, num_classes) ## for vgg19
#model.fc = nn.Linear(num_ftrs, num_classes)  ##for googlenet, resnet18
model.classifier = nn.Linear(num_ftrs, num_classes) ## for densenet169, efficientnet_b7
model = model.to(device)
criterion = nn.CrossEntropyLoss( weight = torch.tensor([1, 4.7]).to(device))
# Observe that all parameters are being optimized
optimizer = optim.Adam(model.parameters(), lr=0.0001)
# StepLR Decays the learning rate of each parameter group by gamma every step_size epochs
# Decay LR by a factor of 0.1 every 7 epochs
# Learning rate scheduling should be applied after optimizer’s update
# e.g., you should write your code this way:
# for epoch in range(100):
#     train(...)
#     validate(...)
#     scheduler.step()
step_lr_scheduler = lr_scheduler.StepLR(optimizer, step_size = 10, gamma=0.1)
model = train_model(model, criterion, optimizer, step_lr_scheduler, num_epochs=10, model_name = "efficientnet_b7")model = models.efficientnet_b7(pretrained = True)
#num_ftrs = model.classifier[0].in_features
#num_ftrs = model.fc.in_features  ##for googlenet, resnet18
#num_ftrs = model.classifier.in_features  ## for densenet169
num_ftrs = model.classifier[1].in_features   ## for efficientnet_b7
print("Number of features: "+str(num_ftrs))
#model.classifier = nn.Linear(num_ftrs, num_classes) ## for vgg19
#model.fc = nn.Linear(num_ftrs, num_classes)  ##for googlenet, resnet18
model.classifier = nn.Linear(num_ftrs, num_classes) ## for densenet169, efficientnet_b7
model = model.to(device)
criterion = nn.CrossEntropyLoss( weight = torch.tensor([1, 4.7]).to(device))
# Observe that all parameters are being optimized
optimizer = optim.Adam(model.parameters(), lr=0.0001)
# StepLR Decays the learning rate of each parameter group by gamma every step_size epochs
# Decay LR by a factor of 0.1 every 7 epochs
# Learning rate scheduling should be applied after optimizer’s update
# e.g., you should write your code this way:
# for epoch in range(100):
#     train(...)
#     validate(...)
#     scheduler.step()
step_lr_scheduler = lr_scheduler.StepLR(optimizer, step_size = 10, gamma=0.1)
model = train_model(model, criterion, optimizer, step_lr_scheduler, num_epochs=10, model_name = "efficientnet_b7")



RuntimeError: DataLoader worker (pid 9541) is killed by signal: Bus error. It is possible that dataloader's workers are out of shared memory. Please try to raise your shared memory limit.





修改共享内存 --shm-size="1g"

使用docker 跑

docker run -it -p 2222:22  --name demo11 --shm-size="4g" --gpus all -v C:\Users\11755\Downloads\LungCancerDetectionEnsemble-main:/workspace  torch201cuda117cudnn8ssh:1.0 /bin/bash





args = parser.parse_args(*args*=['--root_train', '.data/train',

​                '--train_labels', '.data/train_labels.csv',

​                '--root_test', '.data/test',

​                '--test_labels', '.data/test_labels.csv'])





parser = argparse.ArgumentParser(*description*='Process some CSV files.')





