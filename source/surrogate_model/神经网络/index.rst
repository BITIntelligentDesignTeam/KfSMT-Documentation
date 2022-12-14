
神经网络
=================================

代码示例：::

    from knowledge.KnowledgeSet import KnowledgeSet
    from benchmark.sphere import Sphere
    from utils.normalization import Normalization


    ndim = 2
    trainNum = 100
    testNum = 10

    x = np.ones((trainNum, ndim))
    x[:, 0] = np.linspace(-10, 10.0, trainNum)
    x[:, 1] = np.linspace(-10, 10.0, trainNum)

    xt = np.ones((testNum, ndim))
    xt[:, 0] = np.linspace(-10, 10.0, testNum)
    xt[:, 1] = np.linspace(-10, 10.0, testNum)

    s = Sphere()
    trainSet = s(x)
    testSet = s(xt)

    # 获取知识
    k = KnowledgeSet("C:\data\sphereMonoKnowledge1.xml", "C:\data\sphereMonoKnowledge2.xml")
    knowList = k.readKnowledge()

    # k.visualKnowledge()
    x_test = testSet["input"]

    # 对知识和数据进行归一化操作
    n = Normalization()
    trainSet, knowList = n(trainSet, knowList)
    print(knowList)
    xt = n.transform(xt)

    nnModel = EDaKnow()
	
    # nnModel.iterationTime = 10000

    nnModel.setData(trainSet)  # 设置数据

    nnModel.setKnowledge(knowList=knowList)  # 设置知识

    nnModel.train()  # 训练

    yp = nnModel.predict(xt)  # 预测
    print(yp)

    plt.plot(trainSet["input"][:, 0], trainSet["output"][:, 0], label="真实", color="red")
    plt.plot(xt[:, 0], yp[:, 0], label="预测", color='green')
    plt.legend()
    plt.xlabel("x")
    plt.ylabel("y")
    plt.show()

    # b = nnModel.score(testSet, index="RSME")  # 评价代理模型 ，"RSME", "R2", "MAE", "Confidence"
    # print(b)

    nnModel.save(r"C:\data\代理模型训练\高斯过程代理模型.pkl")  # 保存模型文件