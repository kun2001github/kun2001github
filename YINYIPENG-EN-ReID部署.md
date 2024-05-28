# 项目地址：[YINYIPENG-EN/ReID: ReID行人重识别，可做图像检索，陌生人检索等项目 (github.com)](https://github.com/YINYIPENG-EN/ReID)

···



## 前提条件：安装anconda，安装vscode，安装git



## 坑比项目，没有提供requirements，要根据代码，一个一个包的去尝试



# 第一次测试--结果--失败



```
conda create  -n reidpy38 python=3.8

conda deactivate

conda activate reidpy38
```

__运行tools/train.py__

#### 问题1：缺少torch

```
conda install pytorch==1.7.0 torchvision==0.8.0 torchaudio==0.7.0 cudatoolkit=11.0 -c pytorch
```

#### 问题2：ModuleNotFoundError: No module named 'torchsnooper'

参考地址：[（已解决）ModuleNotFoundError: No module named ‘torchsnooper_modulenotfounderror: no module named 'torchsnooper-CSDN博客](https://blog.csdn.net/BetrayFree/article/details/132487988)

```
pip install torchsnooper -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
```



#### 问题3：ModuleNotFoundError: No module named 'IPython'

参考地址：[Python缺少库IPython的解决办法_no module named 'ipython-CSDN博客](https://blog.csdn.net/m0_56401749/article/details/130908527)

```
pip install ipython -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
```



#### 问题4：ModuleNotFoundError: No module named 'yacs'

参考地址：[Py之yacs：yacs的简介、安装、使用方法之详细攻略_pip yacs-CSDN博客](https://blog.csdn.net/qq_41185868/article/details/103881451)

```
pip install yacs  -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
```



#### 问题5：ModuleNotFoundError: No module named 'ignite.engine'

ModuleNotFoundError: No module named 'ignite'

参考地址：[No module named ignite.engine 解决方案_no module named 'ignite-CSDN博客](https://blog.csdn.net/weixin_44273380/article/details/109272186)

```
pip install pytorch-ignite -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
```

```
pip install pytorch-ignite==0.3.0.dev20190909 -i https://pypi.tuna.tsinghua.edu.cn/simple some-package
```



#### 问题6：

#### OSError: [WinError 1455] 页面文件太小，无法完成操作。 Error loading "D:\Anaconda\envs\reidpy38\lib\site-packages\torch\lib\cudnn_adv_infer64_8.dll" 
or one of its dependencies.

参考地址：[解决OSError: [WinError 1455\] 页面文件太小,无法完成操作的问题-百度开发者中心 (baidu.com)](https://developer.baidu.com/article/details/3269672)

把虚拟内存调大





#### 问题7：

2024-04-28 00:05:06,794 reid_baseline.train INFO: Start training
D:\Anaconda\envs\reidpy38\lib\site-packages\torch\optim\lr_scheduler.py:131: UserWarning: Detected call of `lr_scheduler.step()` before `optimizer.step()`. In PyTorch 1.1.0 and later, you should call them in the opposite order: `optimizer.step()` before `lr_scheduler.step()`.  Failure to do this will result in PyTorch skipping the first value of the learning rate schedule. See more details at https://pytorch.org/docs/stable/optim.html#how-to-adjust-learning-rate
  warnings.warn("Detected call of `lr_scheduler.step()` before `optimizer.step()`. "

解决方法：安装1.1.0之前的版本，但是好像能跑起来，就不管他了



#### 问题8：

噩梦来了，虽然忽视了问题6是可以跑起来，但是跑完出现了这个报错

Engine run is terminating due to exception: 'int' object is not callable Traceback (most recent call last):  File "d:/PycharmProjects/ReID/tools/train.py", line 190, in <module>    main()  File "d:/PycharmProjects/ReID/tools/train.py", line 186, in main    train(cfg)  File "d:/PycharmProjects/ReID/tools/train.py", line 62, in train    do_train(  File "D:\PycharmProjects\ReID\.\engine\trainer.py", line 226, in do_train    trainer.run(train_loader, max_epochs=epochs)  File "D:\Anaconda\envs\reidpy38\lib\site-packages\ignite\engine\engine.py", line 889, in run    return self._internal_run()  File "D:\Anaconda\envs\reidpy38\lib\site-packages\ignite\engine\engine.py", line 932, in _internal_run    return next(self._internal_run_generator)  File "D:\Anaconda\envs\reidpy38\lib\site-packages\ignite\engine\engine.py", line 990, in _internal_run_as_gen    self._handle_exception(e)  File "D:\Anaconda\envs\reidpy38\lib\site-packages\ignite\engine\engine.py", line 644, in _handle_exception    raise e  File "D:\Anaconda\envs\reidpy38\lib\site-packages\ignite\engine\engine.py", line 962, in _internal_run_as_gen    self._fire_event(Events.EPOCH_COMPLETED)  File "D:\Anaconda\envs\reidpy38\lib\site-packages\ignite\engine\engine.py", line 431, in _fire_event    func(*first, *(event_args + others), **kwargs)  File "D:\Anaconda\envs\reidpy38\lib\site-packages\ignite\handlers\checkpoint.py", line 1009, in __call__    super(ModelCheckpoint, self).__call__(engine)  File "D:\Anaconda\envs\reidpy38\lib\site-packages\ignite\handlers\checkpoint.py", line 408, in __call__    priority = self.score_function(engine) TypeError: 'int' object is not callable

解决方法：回归到问题7，第二次尝试部署，因为torch1.1.0之前的版本是需要python<=3.7





# 第二次测试--结果-待测试



conda create  -n reidpy36 python=3.6

conda deactivate

conda activate reidpy36

conda install  cudatoolkit=10.0

conda install cudnn=7.6.5

在这个网址里面[download.pytorch.org/whl/cu100/torch_stable.html](https://download.pytorch.org/whl/cu100/torch_stable.html)

下载torch-1.0.0和torchvision-0.2.0 

torch-1.0.0-cp36-cp36m-win_amd64.whl

torchvision-0.2.0-py2.py3-none-any.whl

下载完成后使用pip安装

pip install torch-1.0.0-cp36-cp36m-win_amd64.whl

pip install torchvision-0.2.0-py2.py3-none-any.whl

参考地址：[记录安装pytorch1.0.0和torchvision0.2.0 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/636607358)

安装完成后，测试是否能调用GPU

python

>>> import torch
>>> import torchvision
>>> torch.__version__
>>> '1.0.0'
>>> torch.backends.cudnn.version()
>>> 7401
>>> torch.cuda.is_available()
>>> True



python .\tools\train.py

## 报错1：

  WEIGHT: D:\PycharmProjects\ReID\weights\test_0.6990556451333768.pth
Traceback (most recent call last):
  File "d:/PycharmProjects/ReID/tools/test.py", line 67, in <module>
    main()
  File "d:/PycharmProjects/ReID/tools/test.py", line 59, in main
  File ".\data\build.py", line 16, in make_data_loader
    train_transforms = build_transforms(cfg, is_train=True)
  File ".\data\transforms\build.py", line 17, in build_transforms
    T.RandomHorizontalFlip(p=cfg.INPUT.PROB),
TypeError: object() takes no parameters



问题：我安装的torchvision是2.0.0的，好像是太低了，不支持

解决方法：安装2.1.0版本，下载链接[火炬愿景 ·PyPI的 --- torchvision · PyPI](https://pypi.org/project/torchvision/0.2.1/#files)

pip install .\torchvision-0.2.1-py2.py3-none-any.whl



报错2

  WEIGHT: D:/ReID/weights/test_0.6990556451333768.pth
Traceback (most recent call last):
  File "d:/PycharmProjects/ReID/tools/train.py", line 190, in <module>
    main()
  File "d:/PycharmProjects/ReID/tools/train.py", line 186, in main
    train(cfg)
  File "d:/PycharmProjects/ReID/tools/train.py", line 29, in train
    train_loader, val_loader, num_query, num_classes = make_data_loader(cfg)   # 加载数据集
  File ".\data\build.py", line 16, in make_data_loader
    train_transforms = build_transforms(cfg, is_train=True)
  File ".\data\transforms\build.py", line 17, in build_transforms
    T.RandomHorizontalFlip(p=cfg.INPUT.PROB),
TypeError: object() takes no parameters



卸载，重新安装pip install .\torchvision-0.2.1-py2.py3-none-any.whl













运行tarin.py 完全没有问题了 等待结果

















