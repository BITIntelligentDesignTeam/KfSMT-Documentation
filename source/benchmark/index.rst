基准测试模块
=================================

基准测试模块提供了一些测试函数和工程案例以供代理模型的训练和测试。其类图如图41所示：

.. image:: image/基准测试模块类图.png
    :align: center
	
在本工具包中，基准测试模块提供了8个基准测试函数，他们分别是：Branin,Easom,GoldsteinPrice,LpNorm,Rastrigin,Rosenbrock,Sphere,ThreeHumpCamel；和一个工程上的案例：CMG。
Benchmark为基准测试模块的基类，在此基类下有着不同的子类，他们分别对应着上述的测试函数和工程案例。

基准测试模块的内容
+++++++++++++++++++++++++++
.. toctree::
   :maxdepth: 2

   Branin/index
   Easom/index
   GoldsteinPrice/index
   LpNorm/index
   Rastrigin/index
   Rosenbrock/index
   Sphere/index
   ThreeHumpCamel/index
   CMG/index
   
**Benchmark中的API**

=========================================================   ============================================
名称                                                           作用
=========================================================   ============================================
__call__(x: np.ndarray, proportion=None)                       利用基准函数生成所给输入对应的输出。
getKnowledge（knowType = None,visual = True）                  生成对应的基准函数或者工程案例对应的知识
getData(proportion= None)                                      生成工程案例对应的数据
=========================================================   ============================================

**__call__(x，proportion = None) → dict**

设置训练代理模型所需要的数据

参数：

* x，类型为np.ndarray，需要利用基准函数计算的输入
* proportion，类型为float，训练集占总数据集的比例，默认为None，意为不进行样本集和训练集的划分

返回：

* dict，数据信息的字典，当proportion为None时返回一个字典，当proportion为0~1之间的float型变量时，返回两个字典，其中第一个为训练集，第二个为测试集

示例：::

	from benchmark.sphere import Sphere
	s = Sphere()
    dataSet = s(x)

**getKnowledge（knowType = None,visual = True） → list**

生成对应的基准函数或者工程案例对应的知识

参数：

* knowType, 类型为list，想要得到的知识的类型组成的list，可选的参数有，单调型，属性型，形状型和空间型
* visual，类型为bool，默认为True，是否查看知识的具体信息

返回：

* knowList，类型为list，多条知识dict组成的list

示例：::

		from benchmark.sphere import Sphere
		s = Sphere()
		know = s.getKnowledge(knowType=["单调型","形状型"])

**getData（knowType = None,visual = True） → list**

生成工程案例对应的数据

参数：

* proportion，类型为float，训练集占总数据集的比例，默认为None，意为不进行样本集和训练集的划分

返回：

* dict，数据信息的字典，当proportion为None时返回一个字典，当proportion为0~1之间的float型变量时，返回两个字典，其中第一个为训练集，第二个为测试集


示例：::

		from benchmark.sphere import Sphere
		s = Sphere()
		trainSet，testSet = s.getData(proportion= 0.9)



