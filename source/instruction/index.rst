使用说明
=================================


该部分介绍了工具包使用过程中的一些简单示例，用于帮助用户上手使用工具包


知识模块
-------------
本工具包中目前支持的知识类别有单调型知识、属性型知识、形状型知识和空间型知识。
单调型主要表示产品的变量和性能指标，即输入参数与输出参数之间的正负相关性，包括参数间是正相关还是负相关，或是分段的正负相关关系。
形状型知识主要表示产品的变量和性能指标，即输入参数与输出参数之间的形状性关系。该类型的采用贝塞尔曲线的方式进行表征，通过一组贝塞尔曲线的控制点坐标来表征曲线的形状。
属性型知识主要表示产品的变量和性能指标，即输入参数与输出参数之间的基本属性，定义域和值域信息等。
空间型知识主要表示产品的变量对于性能指标在某个区域上的影响关系，即输入参数与输出参数之间的具备的优劣区域关系。


知识新建
>>>>>>>>>>>>>>>>
该部分的内容为将知识新建成为xml文件并储存起来，调用的方法为writeKnowledge（）。

单调型知识新建
::::::::::::::::::::::::

单调型知识对应的类为MonotonicityKnowledge，新建单调型知识的流程如下：

+ 第一步，导入MonotonicityKnowledge类；
+ 第二步，传入需要保存的知识xml文件路径，并将MonotonicityKnowledge实例化；
+ 第三步，调用MonotonicityKnowledge类中writeKnowledge（）方法，新建知识。MonotonicityKnowledge类中writeKnowledge（）方法，方法内的参数类型及含义如下表所示。其中convar代表的是该条知识的协变量信息组成的list，而协变量信息是指该条知识成立的前提条件。

================= ============================   =========
参数                     含义                     格式
================= ============================   =========
input_type            输入的参数名称               list
output_type           输出的参数名称               list
input_range           输入参数的范围               list
mapping_relation   映射关系，在此指单调性关系      list
convar                知识的协变量信息             list
================= ============================   =========

convar字典中的键值对:

====================    ========================   ====================================
key                           含义                    value格式
====================    ========================   ====================================
convar_type               协变量的参数名称            list
convar_RangeOrValue       协变量参数范围的类型        str，可接受“value”或“range”
convar_range              协变量参数的值              float
convar_value              协变量参数的范围            list
====================    ========================   ====================================

新建一条单调型知识的代码示例如下：::
	
	from kfsmt.knowledge.MonotonicityKnowledge import MonotonicityKnowledge
	path = “C:\data\单调型知识1.xml”
	know1 = ShapeKnowledge(path)
	know_dict = know1.writeKnowledge(input_type=['变量1'],
                         output_type=['指标1'],
                         input_range=[[3.0, 10.0]],
                         mapping_relation=['单调递增'],
                         convar=[{'convar_type': '变量2', 
	'convar_RangeOrValue': 'value', 
	'convar_value': 4.0},
                                 {'convar_type': '变量2', 
	'convar_RangeOrValue': 'range', 
	'convar_range': [3.0, 5.0]}])

属性型知识新建
::::::::::::::::::::::::

属性型知识对应的类为AttributeKnowledge，新建属性型知识的流程如下：

+ 第一步，导入AttributeKnowledge类；
+ 第二步，传入需要保存的知识xml文件路径，并将AttributeKnowledge实例化；
+ 第三步，调用AttributeKnowledge类中writeKnowledge（）方法，新建知识。AttributeKnowledge类中writeKnowledge（）方法，方法内的参数类型及含义如下表所示。其中convar代表的是该条知识的协变量信息组成的list，而协变量信息是指该条知识成立的前提条件。

============= ================== ======================
参数             含义              格式
============= ================== ======================
input_type     输入的参数名称      list
output_type    输出的参数名称      list
input_range    输入参数的范围      list
output_range   输出参数的范围      list
convar         知识的协变量信息    list，默认为None
============= ================== ======================

新建一条属性型知识的代码示例如下：::

	from kfsmt.knowledge.AttributeKnowledge import AttributeKnowledge
	path = “C:\data\属性型知识1.xml”
	know1 = AttributeKnowledge (path)
	know_dict = know1.writeKnowledge(input_type=['变量1'],
                                    output_type=['指标1'],
                                  input_range=[[3.0, 10.0]],
                                  output_range =[[2.0, 10.0]])
	
形状型知识新建
::::::::::::::::::::::::

形状型知识对应的类为ShapeKnowledge，新建形状型知识的流程如下：

+ 第一步，导入ShapeKnowledge类；
+ 第二步，传入需要保存的知识xml文件路径，并将ShapeKnowledge实例化；
+ 第三步，调用ShapeKnowledge类中writeKnowledge（）方法，新建知识。ShapeKnowledge类中writeKnowledge（）方法，方法内的参数类型及含义如下表所示。其中convar代表的是该条知识的协变量信息组成的list，而协变量信息是指该条知识成立的前提条件。

==================  ================================== ======================
参数                  含义                              格式
==================  ================================== ======================
input_type           输入的参数名称                     list
output_type          输出的参数名称                     list
input_range          输入参数的范围                     list
output_range         输出参数的范围                     list
mapping_relation     映射关系，在此指贝塞尔曲线控制点   list
convar              知识的协变量信息                    list，默认为None
==================  ================================== ======================

新建一条形状型知识的代码示例如下：::

	from kfsmt.knowledge. ShapeKnowledge import ShapeKnowledge
	path = “C:\data\形状型知识1.xml”
	know1 = ShapeKnowledge (path)
	know_dict = know1.writeKnowledge(input_type=['变量1'],
                         output_type=['指标1'],
                         input_range=[[3.0, 10.0]],
                         output_range =[[2.0, 10.0]], 
	mapping_relation=[[1.0, 2.0], [2.1, 3.5], [2.7, 3.8]],
	convar=[{'convar_type': '变量2', 'convar_RangeOrValue': 'value', 'convar_value': 4.0},
            {'convar_type': '变量2', 'convar_RangeOrValue': 'range','convar_range': [3.0, 5.0]}])

空间型知识新建
::::::::::::::::::::::::

空间型知识对应的类为SpaceKnowledge，新建空间型知识的流程如下：

+ 第一步，导入SpaceKnowledge类；
+ 第二步，传入需要保存的知识xml文件路径，并将SpaceKnowledge实例化；
+ 第三步，调用SpaceKnowledge类中writeKnowledge（）方法，新建知识。SpaceKnowledge类中writeKnowledge（）方法，方法内的参数类型及含义如下表所示。其中space_relation代表的是该条空间型知识代表的空间关系。

=============== ================= ===========
参数             含义                格式
=============== ================= ===========
input_type       输入的参数名称       list
output_type      输出的参数名称       list
space_relation   空间关系             list
=============== ================= ===========

space_relation字典中的键值对：

============  ========================= ===================
key             含义                          value格式
============  ========================= ===================
id             空间区域的编号                   int
area_type      空间区域的类型                   str
area_level     空间区域的程度                   str 
input_type     空间区域输入参数的名称           list
input_range    空间区域输入参数的范围           list
============  ========================= ===================

新建一条空间型知识的代码示例如下：::

	from kfsmt.knowledge. ShapeKnowledge import ShapeKnowledge
	path = “C:\data\空间型知识1.xml”
	s2 = SpaceKnowledge(path)
	s2.writeKnowledge(input_type=['马赫数', '攻角'],
                   output_type=['压心系数'],
                   space_relation=[{'ID': '1', 'area_type': '复杂区域', 'area_level':'较复杂','input_type':['攻角','马赫数'],'input_range': [[0.0, 10.0], [3.0, 4.0]]},
                                      {'ID': '2', 'area_type': '复杂区域', 'area_level': '很复杂', 'input_type': ['攻角', '马赫数'],'input_range': [[0.0, 0.0], [3.0, 3.0]]}])


知识的读取和查看
>>>>>>>>>>>>>>>>

该部分的内容为将已经新建好的知识xml文件读取为dict，也可查看知识的具体内容。

查看和读取知识文件的方法有两种，第一种，对于已经知道知识具体类型的单条知识xml文件，可以直接调用该类知识类下的readKnowledge( )函数用于读取知识，直接调用该类知识类下的visualKnowledge( )函数用于查看知识；第二种，对于还未知道知识具体类型的多条知识xml文件，可以调用KnowldgeSet类下的readKnowledge( )函数用于读取知识，直接调用KnowldgeSet类下的visualKnowledge( )函数用于查看知识。
第一种的应用场景下的流程如下：

第一种的应用场景下的流程如下：

+ 第一步，导入想要读取和查看知识xml文件知识类型对应的类；
+ 第二步，传入想要读取和查看的知识xml文件路径，并将类实例化；
+ 第三步，调用类中readKnowledge( )方法，读取知识，返回包含知识信息的dict；
+ 第三步，调用类中visualKnowledge( )方法，查看知识的具体信息。

以一条形状型知识为例，代码示例如下：::

	from kfsmt.knowledge.ShapeKnowledge import ShapeKnowledge
	path = “C:\data\形状型知识2.xml”
	know1 = ShapeKnowledge(path)
	know_dict = know1.readKnowledge()
	know1.visualKnowledge()

第二种的应用场景下的流程如下：

+ 第一步，导入KnowldgeSet类；
+ 第二步，传入想要读取和查看的知识xml文件路径，并将KnowldgeSet类实例化，实例化过程中可传入的其他参数如下；
+ 第三步，调用类中readKnowledge( )方法，读取知识，返回包含知识信息的dict组成的list；
+ 第三步，调用类中visualKnowledge( )方法，查看知识的具体信息。

==============  ========================================================      ===========================
参数             含义                                                           格式
==============  ========================================================      ===========================
*args            单个知识的路径，可以重复输入                                   str
folder           使用该参数意味着可以对某个文件夹下的所有知识进行操作           list，默认为None
knowledgeList    需要操作的多条知识路径组成的集合                               list，默认为None
knowType         需要筛选的知识类型                                             list，默认为None
knowInput        需要筛选的知识输入参数名称                                     list，默认为None
knowOutput       需要筛选的知识输出参数名称                                     list，默认为None
==============  ========================================================      ===========================

代码示例如下：::

	from kfsmt.knowledge. KnowledgeSet import KnowledgeSet
	set = Knowledge("C:\data\测试1.txt", "C:\data\测试2.txt", "C:\data\测试3.txt",knowledgeList = ["C:\data\测试4.txt", "C:\data\测试5.txt", "C:\data\测试6.txt"],knowType=["单调型","形状型"])
	list = set.readknowledge()
	set.visualKnowledge()

知识筛选
>>>>>>>>>>>>>>>>

该部分的内容为以不同的指标对知识进行筛选，并返回通过筛选后的知识。目前工具包内有着两种筛选指标，分别是梯度一致性，即数据与知识的一致性度量和豪斯多夫距离，即知识与知识之间的一致性度量。他们分别对应着KnowldgeSet类下的函数gradientSelect( )和hausdorffSelect( )。其中gradientSelect( )使用时需要传入数据信息，hausdorffSelect( )则不用。

知识的筛选过程流程如下：

+ 第一步，导入KnowldgeSet类；
+ 第二步，传入想要筛选的知识xml文件路径，并将KnowldgeSet类实例化，实例化过程中可传入的其他参数同上；
+ 第三步，根据想要使用的筛选指标，决定调用gradientSelect( )或hausdorffSelect( )，并返回通过筛选的知识dict组成的list。

=============   ================================  =====================
参数               含义                             格式
=============   ================================  =====================
x_t              用于梯度一致性筛选的数据输入       numpy.ndarray
y_t              用于梯度一致性筛选的数据输入       numpy.ndarray
printPicture     是否打印出知识筛选的可视化结果     bool，默认为None
savePath         保存知识筛选可视化结果的路径       str，默认为None
=============   ================================  =====================

==============  =====================================    ===========================
参数             含义                                       格式
==============  =====================================    ===========================
printPicture    是否打印出知识筛选的可视化结果             bool，默认为None
savePath        保存知识筛选可视化结果的路径               str，默认为None
==============  =====================================    ===========================

知识筛选的代码示例如下：::
	from kfsmt.knowledge. KnowledgeSet import KnowledgeSet
	set = Knowledge(folder=["C:\data\筛选测试"])
	passList = set.hausdorfSelect()

知识融合
>>>>>>>>>>>>>>>>

该部分的内容为以不同的融合方式对多条知识进行融合，并返回通过融合后的新知识。目前工具包内有着两种知识融合算法，分别是基于费马点的知识融合算法和基于遗传算法知识融合算法。他们分别对应着KnowldgeSet类下的函数fermatPointsFuse( )和gaFuse( )。

知识的筛选过程流程如下：

+ 第一步，导入KnowldgeSet类；
+ 第二步，传入想要融合的知识xml文件路径，并将KnowldgeSet类实例化，实例化过程中可传入的其他参数同上；
+ 第三步，根据想要使用的知识融合算法，决定调用fermatPointsFuse( )或gaFuse( )，并返回融合后的新知识dict。

=============  ====================================================    ================================================
参数              含义                                                   格式
=============  ====================================================    ================================================
select            选择将知识直接融合还是通过所选的筛选方式后再融合       str，默认为None，可选“hausdorff”或“gradient”
x_t               用于梯度一致性筛选的数据输入                           numpy.ndarray，默认为None
y_t               用于梯度一致性筛选的数据输入                           numpy.ndarray，默认为None
printPicture      是否打印出知识融合的可视化结果                         bool，默认为None
savePath          保存知识融合可视化结果的路径                           str，默认为None
=============  ====================================================    ================================================

知识融合的代码示例如下：::

	from kfsmt.knowledge. KnowledgeSet import KnowledgeSet
	set = Knowledge(folder=["C:\data\筛选测试"])
	knowNew = k.fermatPointsFuse(select="hausdorff")

数据模块
-------------

数据模块的主要功能为读取从试验得到的文件中读取数据，和通过采样的方式生成新的数据，其中，利用动态采样这一采样方法可以获得质量更好的数据。

数据读取
>>>>>>>>>>>>>>>>

该部分的主要内容为从3.1部分定义好的数据模板csv文件中读取数据信息，并返回对应的数据dict，此外还可以调用CsvData类下的divide( )函数，进行训练集和测试集的划分。具体的流程如下：

+ 第一步，导入CsvData类；
+ 第二步，传入想要读取的数据csv文件路径，并将CsvData类实例化； 
+ 第三步，调用read( )函数，并返回读取到的数据dict；
+ 第四步，调用divide( )函数，按照一定比例划分训练集和测试集。

数据读取的代码示例如下：::
	from kfsmt.data.CsvData import CsvData
	datapath = “C:\data\测试1.csv”
	D = CsvData (datapath)
	dataSet= D.read ()
	trainSet，testSet = D.divide(proportion = 0.7)

采样
>>>>>>>>>>>>>>>>

工具包内包含的采样方法有两大类，分别是传统的一次采样方法和融合知识的序贯式采样方法。其中传统的一次采样方法其他同类型的工具包中也有涉及，而融合知识的序贯式采样方法为本工具包中原创。

工具包中传统的一次采样方法有简单随机采样（对应RandomSampling类）、拉丁超立方采样（对应LatinHypercubeSampling类）和全因素采样（对应FullFactorialSampling类）。采样的流程如下。

+ 第一步，导入想要使用的采样方法对应的类
+ 第二步，设置采样空间，并将上一步中导入的类实例化
+ 第三步，调用sample( )函数，生成采样点。sample( )函数中的参数如下：

===========  =========================  ========================   
参数          含义                              格式
===========  =========================  ========================   
nt            想要生成采样点的数量             int
tablePath     生成采样表的路径                str，默认为None
===========  =========================  ======================== 
  
以拉丁超立方采样为例，传统的一次采样方法代码示例如下：::

	from kfsmt.data.sampling import LatinHypercubeSampling
	xlimts = {“x1”: [0,60], “x2”: [0,40] , “x3”: [0,15]}
	lhs = LatinHypercubeSampling (xlimts)
	points = lhs.sample (100)
	
工具包中融合知识的序贯式采样方法对应的类为DynamicSampling类，在采样的过程中，需要用到知识和数据，其采样的流程如下：

+ 第一步，导入KnowldgeSet类、CsvData类、DynamicSampling类，并直接将该类实例化；
+ 第二步，利用KnowldgeSet类获取知识； 
+ 第三步，调用setKnowldge ( )函数，设置获取到的知识list；
+ 第四步，利用CsvData类获取数据；
+ 第五步，调用setData( )函数设置获得的数据dict；
+ 第六步，调用sample( )函数，生成采样点和对应的采样表。sample( )函数中的参数同上；
+ 第七步，调用score( )函数，评价当前采样效果的好坏，并根据此结果决定是否结束采样，若继续采样，填写完整采样表之后，回到第4步；若结束采样，则由此结束。

代码示例如下：::

	from kfsmt.data.CsvData import CsvData
	from kfsmt.knowledge. KnowledgeSet import KnowledgeSet
	from kfsmt.data.Dysampling import DynamicSampling
	dataPath = r"C:\data\动态采样多目标.csv"
	knowPath = r'C:\ data \空间型知识1.txt’
	s = KnowledgeSet (knowPath)            # 获取知识
	space = s.readKnowledge()
	d = CsvData(dataPath)            # 获取数据
	dataSet = d.read()
	xlimts = {"x1": [0, 10], "x2": [0, 8]}
	dy = DynamicSampling(xlimts)
	dy.setKnowledge(space)
	dy.setData(dataSet)
	points = dy.sample(20, tablePath=r"C:\data\动态采样表示例.csv")
	score = dy.score( )


代理模型模块
-------------

代理模型模块的功能为利用知识和数据训练代理模型和使用代理模型预测。也是工具包中的核心内容。

代理模型的构建
>>>>>>>>>>>>>>>>

本部分的内容为，利用知识和数据完成代理模型的构建。工具包中包含的代理模型种类分为高斯过程类代理模型和神经网络类的代理模型。高斯过程类代理模型包含普通高斯过程（对应GP类）和融合知识的高斯过程（对应GPK类），神经网络类的代理模型包含融合知识的进化神经网络（对应EDaKnow类）和融合知识的贝叶斯神经网络（对应EBNN类）。构建融合知识代理模型流程如下：

+ 第一步，导入KnowldgeSet类、CsvData类，导入想要构建的代理模型对应的类,并直接将该类实例化；
+ 第二步，利用KnowldgeSet类获取知识； 
+ 第三步，调用setKnowledge( )函数，设置获取到的知识list；
+ 第四步，利用CsvData类获取数据；
+ 第五步，调用setData( )函数，设置获得的数据dict；
+ 第六步，调用导入的代理模型类下的train( )函数，完成代理模型的训练

以融合知识的高斯过程（GPK）为例，代码示例如下：::

	from kfsmt.surrogate_model.gp import GPK
	from kfsmt.data.CsvData import CsvData
	from kfsmt.knowledge. KnowledgeSet import KnowledgeSet
	dataPath = r"C:\data\数据示例1.csv"
	knowPath = r'C:\ data \知识示例1.txt’
	s = KnowledgeSet (knowPath)            # 获取知识
	know = s.readKnowledge()
	d = CsvData(dataPath)            # 获取数据
	dataSet = d.read()
	model =GPK()
	model.setData(dataSet) 
	model.setKnowledge(knowList = know) 
	model.train()

代理模型的预测和测试
>>>>>>>>>>>>>>>>>>>>>>>>>>>

本部分的内容为利用训练好的代理模型，进行测试和预测工作。测试和预测的步骤如下：

+ 第一步：根据上一部分的内容完成代理模型部分的训练；
+ 第二步，利用predict( )函数，输入想要预测的数据点进行预测（由于预测的数据点为numpy.ndarray格式的，需要先导入numpy包）；
+ 第三步，利用score( )函数，输入之前准备好的测试集，选择好评价模型要使用的指标进行代理模型的评价。

代码示例如下：::

	…       #代理模型的构建部分，具体在上一个部分已经进行过展示
	import numpy as np
	x = np.linspace(0.0, 4.0, 100)          #生成待预测点
	y = model.predict(x,variance = True)
	confidence = model.score(testSet, index = “Confidence”，error = 0.03)      #这里的testSet为从数据模块中生成的数据dict，前面对应模块处已经详细做过介绍，这里不过多解释。Index为评价代理模型的指标，可以选的指标为可选项有“RSME”、“R2”、“Confidence”。评价代理模型时所使用到的指标，“RSME”为均方误差根，“R2”为R-平方，“Confidence”为一定误差水平下的置信度。


代理模型的保存和加载
>>>>>>>>>>>>>>>>>>>>>>>>>>>
本部分的内容为将训练好的代理模型保存为pkl文件。模型的pkl文件可以通过python自带的pickle包进行加载，加载后的模型无需重复训练，可以直接进行预测等工作。保存和加载的步骤如下：

+ 第一步，按照上一部分的步骤，完成代理模型的训练；
+ 第二步，调用save( )函数，将模型保存为pkl文件；
+ 第三步，导入python自带的pickle包；
+ 第四步，新建一个模型对象，利用pickle包中的load（）将该对象实例化，实例化后的对象即可进行预测等操作。

代码示例如下：::

	…       #代理模型的构建部分，具体在上一个部分已经进行过展示
	model.save(r"C:\data\代理模型.pkl")    #保存模型文件
	import pickle 
	gpModel2 = None                            #加载模型文件
	filename = r"C:\data\代理模型.pkl"
	with open(filename, "rb") as f:
		gpModel2 = pickle.load(f)
	p = gpModel2.predict(x_test)


基准测试模块
-------------
基准测试模块目前提供了8个测试函数和1个工程案例，以供进行代理模型和动态采样的测试工作。

基准测试模块的基类为BenchMarkBase类，8个测试函数和1个工程案例均为BenchMarkBase类的子类，8个测试函数分别为Branin 类、Easom类、GoldsteinPrice类、LpNorm类、Rastrigin类、Rosenbrock类、Sphere类和ThreeHumpCamel类；一个工程案例为CMG类，即控制力矩陀螺（control moment gyroscope）。

BenchMarkBase类中的方法如下

==================================     ===========================================
名称                                     作用
==================================     ===========================================
__call__(x，proportion = None)           利用基准函数生成所给输入对应的输出
getKnowledge(knowType)                   生成该基准函数或工程案例的知识
getData(proportion=None)                 生成该工程案例的数据
==================================     ===========================================

基准测试函数
>>>>>>>>>>>>>>>>

使用基准函数可以为所给输入生成对应的完整数据集，同时也可以获取该条测试函数下对应的知识。使用步骤如下：

+ 第一步，导入所需要使用到的测试函数类；
+ 第二步，通过numpy生成想要完整数据集的数据点；
+ 第三步，通过调用类中的__call__( )函数获得完整的数据集，_call__( )函数中的参数列表如下
+ 第四步，通过调用类中的getKnowledge函数获得知识dict组成的list。

==============  =============================  =====================
参数              含义                           格式
==============  =============================  =====================
x                想要生成完整数据集的数据点     numpy.ndarray
proportion       划分训练集和测试的比例         float，默认为None
==============  =============================  =====================

代码示例如下：::

	import numpy as np
	from kfsmt.benchmark import Sphere
	ndim = 2
	problem = Sphere( )
	num = 100
	x = np.ones((num, ndim))
	x[:, 0] = np.linspace(-10, 10.0, num)
	x[:, 1] = 0.0
	y = problem(x)
	know = problem.getKnowledge([“单调型”,”形状型”])

工程案例
>>>>>>>>>>>>>>>>

使用基准函数可以为所给输入生成对应的完整数据集，同时也可以获取该条测试函数下对应的知识。使用步骤如下：

+ 第一步，导入所需要使用到的工程案例类；
+ 第二步，通过调用类中的getData( )函数获得完整的数据集；
+ 第三步，通过调用类中的getKnowledge( )函数获得知识dict组成的list。

代码示例如下：::

	import numpy as np
	from kfsmt.benchmark import CMG
	problem = CMG( )
	dataSet = problem.getData ()
	know = problem.getKnowledge([“单调型”,”形状型”])

