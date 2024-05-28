# 项目地址：

[TransUrban-UAH/DFSS_Model (github.com)](https://github.com/TransUrban-UAH/DFSS_Model)



项目最后更新是2021.7.16



部署步骤 

#conda 没有3.8.6的版本，所以按照了3.8.8的版本

conda create --name py38 python=3.8.8



pandas== 1.3.0

geopandas==0.7.0

dask==2021.6.0

numpy =1.20.3

statistics 

tqdm==4.60.0

matplotlib==3.4.2 

scipy==1.7.0

scikit-learn==0.24.2

distributed= =2021.6.0

networkx ==2.5.1

openpyxl==3.0.7

pygeos==0.10   #运行neighbours.py遇到的报错解决





### 问题1：vscode里面无法使用conda

```
. : 无法加载文件 C:\Users\HP\Documents\WindowsPowerShell\profile.ps1，因为在此系统上禁止运行脚本。有关详细信息，请参阅
https:/go.microsoft.com/fwlink/?LinkID=135170 中的 about_Execution_Policies。
所在位置 行:1 字符: 3

. 'C:\Users\HP\Documents\WindowsPowerShell\profile.ps1'

CategoryInfo          : SecurityError: (:) []，PSSecurityException

FullyQualifiedErrorId : UnauthorizedAccess
```

解决方法：

通过管理员模式打开powershell,然后输入：
set-executionpolicy RemoteSigned

然后输入A回车即可





### 报错2：运行 neighbours.py 遇到问题

```
(py388) PS D:\my_code\DFSS_Model-main> & C:/Users/HP/.conda/envs/py388/python.exe d:/my_code/DFSS_Model-main/disruptive_simulator/neighbours.py
Executing the script encharged of the generation of neighbouts of each parcel.

Setting working directory in: D:\my_code\DFSS_Model-main\sample_Los_santos\scenario_1

Opening the scenario shapefile: scenario_1.shp

Working with the buffer of 25 meters.
Executing the Spatial Join...
Traceback (most recent call last):
  File "d:/my_code/DFSS_Model-main/disruptive_simulator/neighbours.py", line 151, in <module>
    main()
  File "d:/my_code/DFSS_Model-main/disruptive_simulator/neighbours.py", line 117, in main
    gdf_final = neighbours(gdf, dist_list)
  File "d:/my_code/DFSS_Model-main/disruptive_simulator/neighbours.py", line 64, in neighbours
    spatial_join = sjoin(gdf_geom_buffer, gdf_geom, how="inner", op="intersects",
  File "C:\Users\HP\.conda\envs\py388\lib\site-packages\geopandas\tools\sjoin.py", line 89, in sjoin
    indices = _geom_predicate_query(left_df, right_df, op)
  File "C:\Users\HP\.conda\envs\py388\lib\site-packages\geopandas\tools\sjoin.py", line 179, in _geom_predicate_query
    sindex = right_df.sindex
  File "C:\Users\HP\.conda\envs\py388\lib\site-packages\geopandas\base.py", line 2630, in sindex
    return self.geometry.values.sindex
  File "C:\Users\HP\.conda\envs\py388\lib\site-packages\geopandas\array.py", line 309, in sindex
    self._sindex = _get_sindex_class()(self.data)
  File "C:\Users\HP\.conda\envs\py388\lib\site-packages\geopandas\sindex.py", line 21, in _get_sindex_class
    raise ImportError(
ImportError: Spatial indexes require either `rtree` or `pygeos`. See installation instructions at https://geopandas.org/install.html
```

解决方法：

pip install pygeos==0.10





问题：

(py388) PS D:\my_code\DFSS_Model-main> & C:/Users/HP/.conda/envs/py388/python.exe d:/my_code/DFSS_Model-main/disruptive_simulator/regressions.py
d:/my_code/DFSS_Model-main/disruptive_simulator/regressions.py:381: MatplotlibDeprecationWarning: Case-insensitive properties were deprecated in 3.3 and support will be removed two minor releases later
  axes[axe1, axe2].set_title(ls_titles[ls_uses.index(use)],
d:/my_code/DFSS_Model-main/disruptive_simulator/regressions.py:395: MatplotlibDeprecationWarning: Case-insensitive properties were deprecated in 3.3 and support will be removed two minor releases later   
  axe.set_xlabel('Distance (m)', Fontproperties = font_label, loc = "right")
d:/my_code/DFSS_Model-main/disruptive_simulator/regressions.py:422: MatplotlibDeprecationWarning: 
The 'quality' parameter of print_jpg() was deprecated in Matplotlib 3.3 and will be removed two minor releases later. Use pil_kwargs={'quality': ...} instead. If any parameter follows 'quality', they should be passed as keyword, not positionally.
  figure.savefig("graf_" + xlsx[:-5] + ".jpg", quality = 100, dpi = 500,



解决方法：pip install matplotlib==3.3.0rc1

matplotlib从来3.3版本开始就不支持这种语法，会在未来的2个小版本中删除，然后我就试了3.4的版本也是可以的，一样有这个提示，我又试了3.5的版本，结果真的没有了，直接报错了







问题：

(base) PS D:\my_code> & C:/Users/HP/.conda/envs/py388/python.exe d:/my_code/DFSS_Model-main/disruptive_simulator/initial_attraction.py
C:\Users\HP\.conda\envs\py388\lib\site-packages\geopandas\_compat.py:106: UserWarning: The Shapely GEOS version (3.11.3-CAPI-1.17.3) is incompatible with the GEOS version PyGEOS was compiled with (3.9.1-CAPI-1.14.2). Conversions between both will be slow.
  warnings.warn(
Traceback (most recent call last):
  File "d:/my_code/DFSS_Model-main/disruptive_simulator/initial_attraction.py", line 22, in <module>
    from attraction import attraction
  File "d:\my_code\DFSS_Model-main\disruptive_simulator\attraction.py", line 18, in <module>
    from dask.distributed import Client
  File "C:\Users\HP\.conda\envs\py388\lib\site-packages\dask\distributed.py", line 3, in <module>
    from distributed import *
  File "C:\Users\HP\.conda\envs\py388\lib\site-packages\distributed\__init__.py", line 7, in <module>
    from .actor import Actor, ActorFuture
  File "C:\Users\HP\.conda\envs\py388\lib\site-packages\distributed\actor.py", line 6, in <module>
    from .client import Future, default_client
  File "C:\Users\HP\.conda\envs\py388\lib\site-packages\distributed\client.py", line 44, in <module>
    from .batched import BatchedSend
  File "C:\Users\HP\.conda\envs\py388\lib\site-packages\distributed\batched.py", line 9, in <module>
    from .core import CommClosedError
  File "C:\Users\HP\.conda\envs\py388\lib\site-packages\distributed\core.py", line 23, in <module>
    from .comm import (
  File "C:\Users\HP\.conda\envs\py388\lib\site-packages\distributed\comm\__init__.py", line 25, in <module>
    _register_transports()
  File "C:\Users\HP\.conda\envs\py388\lib\site-packages\distributed\comm\__init__.py", line 17, in _register_transports
    from . import inproc, tcp, ws
  File "C:\Users\HP\.conda\envs\py388\lib\site-packages\distributed\comm\tcp.py", line 8, in <module>
    from ssl import SSLError
  File "C:\Users\HP\.conda\envs\py388\lib\ssl.py", line 98, in <module>
    import _ssl             # if we can't import it, let the error propagate
ImportError: DLL load failed while importing _ssl: 找不到指定的模块。







类似报错1：

在跑initial_attraction.py 提示

C:\Users\HP\.conda\envs\py388\lib\site-packages\geopandas\_compat.py:106: UserWarning: The Shapely GEOS version (3.11.3-CAPI-1.17.3) is incompatible with the GEOS version PyGEOS was compiled with (3.9.1-CAPI-1.14.2). Conversions between both will be slow.

解决方法：pip install geopandas==0.7.0





### 报错3：

PS D:\my_code\DFSS_Model-main> & C:/Users/HP/.conda/envs/py386/python.exe d:/my_code/DFSS_Model-main/disruptive_simulator/regressions.py
Traceback (most recent call last):
  File "d:/my_code/DFSS_Model-main/disruptive_simulator/regressions.py", line 381, in <module>
    axes[axe1, axe2].set_title(ls_titles[ls_uses.index(use)],
  File "C:\Users\HP\.conda\envs\py386\lib\site-packages\matplotlib\axes\_axes.py", line 180, in set_title
    title._internal_update(kwargs)
  File "C:\Users\HP\.conda\envs\py386\lib\site-packages\matplotlib\artist.py", line 1223, in _internal_update
    return self._update_props(
  File "C:\Users\HP\.conda\envs\py386\lib\site-packages\matplotlib\artist.py", line 1197, in _update_props
    raise AttributeError(
AttributeError: Text.set() got an unexpected keyword argument 'FontProperties'

我的matplotlib版本是3.7.5，3.7.0 3.6.0都不行

AttributeError: 'Text' object has no property 'FontProperties'

3.5.0不行，没有这个属性，修改代码即可







### 报错4：

PS D:\my_code\DFSS_Model-main\disruptive_simulator> & C:/Users/HP/.conda/envs/py386/python.exe d:/my_code/DFSS_Model-main/disruptive_simulator/main_run.py
<p>Error: module 'main_set_up_data' has no attribute 'set_up_data'</p>
Traceback (most recent call last):
  File "d:/my_code/DFSS_Model-main/disruptive_simulator/main_run.py", line 53, in main
    msud.set_up_data(wd, scenario_list, z_default, z_urban, z_nonurban,
AttributeError: module 'main_set_up_data' has no attribute 'set_up_data'









