CMG
=================================
控制力矩陀螺（control moment gyroscope, CMG）是一种航天器姿态控制的惯性执行机构，相对于飞轮执行机构具有力矩放大效应，从框架输人很小的力矩就可以通过转子角动量方向的改变输出较大的姿态控制力矩，且控制精度高。CMG在空间站、高精度空间监测等需要快速机动和高指向精度的航天任务应用日益广泛。

CMG全寿命周期内受到加速度、振动、冲击、泄压、冷热交变等环境应力，工作时还受到反作用力矩（框架转速和转台转速）的作用。因此，关于CMG的试验因子包括以下6项（4、5、6项为重要因子）：

+ 加速度
+ 振动
+ 冲击
+ 温度
+ 框架转速
+ 转台转速

CMG的试验指标为径向间隙减少量

代码示例如下：::
	
    c = CMG()
    CMGdata1,CMGdata2= c.getData(proportion=0.7)
    print(CMGdata1)
    print(CMGdata2)

    print(CMGdata1["input"].shape)
    print(CMGdata2["input"].shape)

    knowlist = c.getKnowledge()
    print(knowlist)
	
运行结果如下：::
	
	{'input': array([[20., 40.,  3.],
       [50.,  5.,  5.],
       [20., 20.,  3.],
		...
       [10., 50.,  2.]]), 
	   'output': array([[46.96155518],
       [50.70059255],
       [35.8137842 ],
		...
       [40.79854655]]), 
	   'title': [['温度', '框架转速', '转台转速'], ['径向间隙减少量']], 
	   'range': [[[0.0, 70.0], [0.0, 50.0], [1.0, 5.0]], [[0.0, 100.0]]]}
	   
	{'input': array([[ 0.,  5.,  1.],
       [ 0.,  5.,  5.],
       [ 0., 10.,  1.],
       ...
       [60., 50.,  5.]]), 
	   'output': array([[15.3063172 ],
       [22.96783484],
       [15.79706343],
       ...
       [67.77268739]]),
	   'title': [['温度', '框架转速', '转台转速'], ['径向间隙减少量']], 
	   'range': [[[0.0, 70.0], [0.0, 50.0], [1.0, 5.0]], [[0.0, 100.0]]]}
	(168, 3)
	(42, 3)
	___________________________________________________________________________
	知识名称:C:\kfsmt算法包\kfsmt\benchmark\CMG\knowledge\CMGMonoKnowledge1.xml
	知识类型:单调型
	变量:温度
	变量范围:[-20.0, 60.0]
	性能:径向间隙减少量
	单调性:单调递增
	协变量1:  协变量参数:框架转速  取值类型:范围  协变量范围:[5.0, 57.3]
	协变量2:  协变量参数:转台转速  取值类型:范围  协变量范围:[0.0, 5.0]
	___________________________________________________________________________
	知识名称:C:\kfsmt算法包\kfsmt\benchmark\CMG\knowledge\CMGMonoKnowledge2.xml
	知识类型:单调型
	变量:框架转速
	变量范围:[5.0, 57.3]
	性能:径向间隙减少量
	单调性:单调递增
	协变量1:  协变量参数:温度  取值类型:范围  协变量范围:[-20.0, 60.0]
	协变量2:  协变量参数:转台转速  取值类型:范围  协变量范围:[0.0, 5.0]
	___________________________________________________________________________
	知识名称:C:\kfsmt算法包\kfsmt\benchmark\CMG\knowledge\CMGMonoKnowledge3.xml
	知识类型:单调型
	变量:转台转速
	变量范围:[0.0, 5.0]
	性能:径向间隙减少量
	单调性:单调递增
	协变量1:  协变量参数:温度  取值类型:范围  协变量范围:[-20.0, 60.0]
	协变量2:  协变量参数:框架转速  取值类型:范围  协变量范围:[5.0, 57.3]
	[{'type': '单调型', 'input_type': ['温度'], 'output_type': ['径向间隙减少量'], 'convar': [{'convar_type': '框架转速', 'convar_RangeOrValue': 'range', 'convar_range': [5.0, 57.3]}, {'convar_type': '转台转速', 'convar_RangeOrValue': 'range', 'convar_range': [0.0, 5.0]}], 'input_range': [[-20.0, 60.0]], 'mapping_relation': ['单调递增']}, {'type': '单调型', 'input_type': ['框架转速'], 'output_type': ['径向间隙减少量'], 'convar': [{'convar_type': '温度', 'convar_RangeOrValue': 'range', 'convar_range': [-20.0, 60.0]}, {'convar_type': '转台转速', 'convar_RangeOrValue': 'range', 'convar_range': [0.0, 5.0]}], 'input_range': [[5.0, 57.3]], 'mapping_relation': ['单调递增']}, {'type': '单调型', 'input_type': ['转台转速'], 'output_type': ['径向间隙减少量'], 'convar': [{'convar_type': '温度', 'convar_RangeOrValue': 'range', 'convar_range': [-20.0, 60.0]}, {'convar_type': '框架转速', 'convar_RangeOrValue': 'range', 'convar_range': [5.0, 57.3]}], 'input_range': [[0.0, 5.0]], 'mapping_relation': ['单调递增']}]


