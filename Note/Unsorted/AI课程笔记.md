## 引入

**Q1. AI和机器学习和深度学习的关系是什么？**

人工智能 > 机器学习 > 深度学习

人工智能（ArtificialIntelligence，AI）是最宽泛的概念，是研发用于模拟、延伸和扩展人的智能的理论、方法、技术及应用系统的一门新的技术科学。由于这个定义只阐述了目标，而没有限定方法，因此实现人工智能存在的诸多方法和分支，导致其变成一个“大杂烩”式的学科。机器学习（MachineLearning，ML）是当前比较有效的一种实现人工智能的方式。深度学习（DeepLearning，DL）是机器学习算法中最热门的一个分支，近些年取得了显著的进展，并替代了大多数传统机器学习算法。

**Q2. 机器学习的方法论是什么？**

假设 > 评价 > 优化

## 波士顿房价预测

### 导包

```python
import json
import numpy as np
```

### 数据处理

```python
# 数据处理(得到训练集和测试集)
def loadData():
    # 读入数据
    dataFile = 'housing.data'
    # numpy的fromfile 和 tofile 函数可以实现数组读写到磁盘中
    data = np.fromfile(dataFile, sep=' ')  
    # 形状转化
    featureNames = ['CRIM', 'ZN', 'INDUS', 
                    'CHAS', 'NOX', 'RM', 
                    'AGE', 'DIS', 'RAD', 
                    'TAX', 'PTRATIO', 'B', 
                    'LSTAT', 'MEDV']
    featureNumber = len(featureNames)  # len = 14
    data = data.reshape([data.shape[0] // featureNumber, featureNumber])  # 506 * 14
    # data.shape 行数:列数
    # data.shape[0] 行数
    # data.shape[1] 列数
    # 数据集划分
    ratio = 0.8     # 训 : 测 = 8 : 2
    offset = int(data.shape[0] * ratio)
    trainingData = data[:offset]  # 从第一行截取到第offset行
    # 求极值和均值
    maxMums, minMums, avgs = \
        trainingData.max(axis=0), \
        trainingData.min(axis=0), \
        trainingData.sum(axis=0) / trainingData.shape[0]
    # 归一化处理
    for i in range(featureNumber):
        data[:, i] = (data[:, i] - avgs[i] / (maxMums[i] / minMums[i]))
    trainData = data[:offset]
    testData = data[offset:]
    return trainData, testData
```

