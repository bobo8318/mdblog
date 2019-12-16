title:sklearn入门基本知识
date: 2018-10-25
Category: 机器学习
Tags: 机器学习,sklearn
Authors: openui
Summary: sklearn入门基本知识

* preprocessing.LabelBinarizer 标签二值化
### 数据标准化
* 特征值归化
```
from sklearn import preprocessing
from sklearn.datasets.samples_generator import make_classification


X, y = make_classification(
    n_samples=300, n_features=2,
    n_redundant=0, n_informative=2,
    random_state=22, n_clusters_per_class=1,
    scale=100)

#X = preprocessing.scale(X)#-1到1范围
X = preprocessing.minmax_scale(X,feature_range=(-1,1))

# 1. 基于mean和std的标准化
scaler = preprocessing.StandardScaler().fit(X)
X scaler.transform(X)

```
### 数据值拆分
```
from sklearn.mode_selection import train_test_split

X_train, X_test, y_train, y_test = train_test_split(X, y, test_size=0.3, random_state=42)

"""
参数
---
arrays：样本数组，包含特征向量和标签

test_size：
　　float-获得多大比重的测试样本 （默认：0.25）
　　int - 获得多少个测试样本

train_size: 同test_size

random_state:
　　int - 随机种子（种子固定，实验可复现）
　　
shuffle - 是否在分割之前对数据进行洗牌（默认True）

返回
---
分割后的列表，长度=2*len(arrays),
　　(train-test split)
"""

```

### 定义模型
```
# 拟合模型
model.fit(X_train, y_train)
# 模型预测
model.predict(X_test)

# 获得这个模型的参数
model.get_params()
# 为模型进行打分
model.score(data_X, data_y) # 线性回归：R square； 分类问题： acc
```

### 线性回归
```
rom sklearn.linear_model import LinearRegression
# 定义线性回归模型
model = LinearRegression(fit_intercept=True, normalize=False,
    copy_X=True, n_jobs=1)
"""
参数
---
    fit_intercept：是否计算截距。False-模型没有截距
    normalize： 当fit_intercept设置为False时，该参数将被忽略。 如果为真，则回归前的回归系数X将通过减去平均值并除以l2-范数而归一化。
     n_jobs：指定线程数
"""
```
### 逻辑回归LR
```
from sklearn.linear_model import LogisticRegression
# 定义逻辑回归模型
model = LogisticRegression(penalty=’l2’, dual=False, tol=0.0001, C=1.0,
    fit_intercept=True, intercept_scaling=1, class_weight=None,
    random_state=None, solver=’liblinear’, max_iter=100, multi_class=’ovr’,
    verbose=0, warm_start=False, n_jobs=1)

"""参数
---
    penalty：使用指定正则化项（默认：l2）
    dual: n_samples > n_features取False（默认）
    C：正则化强度的反，值越小正则化强度越大
    n_jobs: 指定线程数
    random_state：随机数生成器
    fit_intercept: 是否需要常量
"""
```
### 朴素贝叶斯算法NB
```
from sklearn import naive_bayes
model = naive_bayes.GaussianNB() # 高斯贝叶斯
model = naive_bayes.MultinomialNB(alpha=1.0, fit_prior=True, class_prior=None)
model = naive_bayes.BernoulliNB(alpha=1.0, binarize=0.0, fit_prior=True, class_prior=None)
"""
文本分类问题常用MultinomialNB
参数
---
    alpha：平滑参数
    fit_prior：是否要学习类的先验概率；false-使用统一的先验概率
    class_prior: 是否指定类的先验概率；若指定则不能根据参数调整
    binarize: 二值化的阈值，若为None，则假设输入由二进制向量组成
"""
```
### 决策树DT
```
rom sklearn import tree
model = tree.DecisionTreeClassifier(criterion=’gini’, max_depth=None,
    min_samples_split=2, min_samples_leaf=1, min_weight_fraction_leaf=0.0,
    max_features=None, random_state=None, max_leaf_nodes=None,
    min_impurity_decrease=0.0, min_impurity_split=None,
     class_weight=None, presort=False)
"""参数
---
    criterion ：特征选择准则gini/entropy
    max_depth：树的最大深度，None-尽量下分
    min_samples_split：分裂内部节点，所需要的最小样本树
    min_samples_leaf：叶子节点所需要的最小样本数
    max_features: 寻找最优分割点时的最大特征数
    max_leaf_nodes：优先增长到最大叶子节点数
    min_impurity_decrease：如果这种分离导致杂质的减少大于或等于这个值，则节点将被拆分。
"""
```
### 支持向量机SVM
```
rom sklearn.svm import SVC
model = SVC(C=1.0, kernel=’rbf’, gamma=’auto’)
"""参数
---
    C：误差项的惩罚参数C
    gamma: 核相关系数。浮点数，If gamma is ‘auto’ then 1/n_features will be used instead.
"""
```
### k近邻算法KNN
```
from sklearn import neighbors
#定义kNN分类模型
model = neighbors.KNeighborsClassifier(n_neighbors=5, n_jobs=1) # 分类
model = neighbors.KNeighborsRegressor(n_neighbors=5, n_jobs=1) # 回归
"""参数
---
    n_neighbors： 使用邻居的数目
    n_jobs：并行任务数
"""
```
###  多层感知机（神经网络）
```
rom sklearn.neural_network import MLPClassifier
# 定义多层感知机分类算法
model = MLPClassifier(activation='relu', solver='adam', alpha=0.0001)
"""参数
---
    hidden_layer_sizes: 元祖
    activation：激活函数
    solver ：优化算法{‘lbfgs’, ‘sgd’, ‘adam’}
    alpha：L2惩罚(正则化项)参数。
"""
```
### 模型评估与选择
    * 交叉验证  用于特征选择 模型选择
    ```
        from sklearn.model_selection import cross_val_score
        cross_val_score(model, X, y=None, scoring=None, cv=None, n_jobs=1)
        """参数
        ---
            model：拟合数据的模型
            cv ： k-fold
            scoring: 打分参数-‘accuracy’、‘f1’、‘precision’、‘recall’ 、‘roc_auc’、'neg_log_loss'等等
        """



        import numpy as np
        from sklearn import datasets
        from sklearn.cross_validation import train_test_split
        from sklearn.neighbors import KNeighborsClassifier
        from sklearn.cross_validation import cross_val_score

        # 加载iris数据集
        iris = datasets.load_iris()
        # 读取特征
        X = iris.data
        # 读取分类标签
        y = iris.target
        # 定义分类器
        knn = KNeighborsClassifier(n_neighbors = 5)
        # 进行交叉验证数据评估, 数据分为5部分, 每次用一部分作为测试集
        scores = cross_val_score(knn, X, y, cv = 5, scoring = 'accuracy')
        # 输出5次交叉验证的准确率
        print scores




        import numpy as np
        import matplotlib.pyplot as plt
        from sklearn import datasets
        from sklearn.cross_validation import train_test_split
        from sklearn.neighbors import KNeighborsClassifier
        from sklearn.cross_validation import cross_val_score

        # 确定knn中k的取值

        # 加载iris数据集
        iris = datasets.load_iris()
        # 读取特征
        X = iris.data
        # 读取分类标签
        y = iris.target
        # 定义knn中k的取值, 0-10
        k_range = range(1, 30)
        # 保存k对应的准确率
        k_scores = []
        # 计算每个k取值对应的准确率
        for k in k_range:
            # 获得knn分类器
            knn = KNeighborsClassifier(n_neighbors = k)
            # 对数据进行交叉验证求准确率
            scores = cross_val_score(knn, X, y, cv = 10, scoring = 'accuracy')
            # 保存交叉验证结果的准确率均值
            k_scores.append(scores.mean())

        # 绘制k取不同值时的准确率变化图像
        plt.plot(k_range, k_scores)
        plt.xlabel('K Value in KNN')
        plt.ylabel('Cross-Validation Mean Accuracy')
        plt.show()
        ```

    * 检验曲线
    ```
    from sklearn.model_selection import validation_curve
    train_score, test_score = validation_curve(model, X, y, param_name, param_range, cv=None, scoring=None, n_jobs=1)
    """参数
    ---
        model:用于fit和predict的对象
        X, y: 训练集的特征和标签
        param_name：将被改变的参数的名字
        param_range： 参数的改变范围
        cv：k-fold

        返回值
    ---
    train_score: 训练集得分（array）
    test_score: 验证集得分（array）
    """
    ```
* 随机森林
```
criterion: ”gini” or “entropy”(default=”gini”)是计算属性的gini(基尼不纯度)还是entropy(信息增益)，来选择最合适的节点。

splitter: ”best” or “random”(default=”best”)随机选择属性还是选择不纯度最大的属性，建议用默认。

max_features: 选择最适属性时划分的特征不能超过此值。

当为整数时，即最大特征数；当为小数时，训练集特征数*小数；

if “auto”, then max_features=sqrt(n_features).

If “sqrt”, thenmax_features=sqrt(n_features).

If “log2”, thenmax_features=log2(n_features).

If None, then max_features=n_features.

max_depth: (default=None)设置树的最大深度，默认为None，这样建树时，会使每一个叶节点只有一个类别，或是达到min_samples_split。

min_samples_split:根据属性划分节点时，每个划分最少的样本数。
min_samples_leaf:叶子节点最少的样本数。

max_leaf_nodes: (default=None)叶子树的最大样本数。

min_weight_fraction_leaf: (default=0) 叶子节点所需要的最小权值

verbose:(default=0) 是否显示任务进程
关于随机森林特有的参数：
n_estimators=10：决策树的个数，越多越好，但是性能就会越差，至少100左右（具体数字忘记从哪里来的了）可以达到可接受的性能和误差率。
bootstrap=True：是否有放回的采样。  
oob_score=False：oob（out of band，带外）数据，即：在某次决策树训练中没有被bootstrap选中的数据。多单个模型的参数训练，我们知道可以用cross validation（cv）来进行，但是特别消耗时间，而且对于随机森林这种情况也没有大的必要，所以就用这个数据对决策树模型进行验证，算是一个简单的交叉验证。性能消耗小，但是效果不错。  

n_jobs=1：并行job个数。这个在ensemble算法中非常重要，尤其是bagging（而非boosting，因为boosting的每次迭代之间有影响，所以很难进行并行化），因为可以并行从而提高性能。1=不并行；n：n个并行；-1：CPU有多少core，就启动多少job

warm_start=False：热启动，决定是否使用上次调用该类的结果然后增加新的。  

class_weight=None：各个label的权重。  


进行预测可以有几种形式：
predict_proba(x)：给出带有概率值的结果。每个点在所有label的概率和为1.  

predict(x)：直接给出预测结果。内部还是调用的predict_proba()，根据概率的结果看哪个类型的预测值最高就是哪个类型。  

predict_log_proba(x)：和predict_proba基本上一样，只是把结果给做了log()处理。  
```
### 保存模型
* 保存为pickle文件
```
import pickle

# 保存模型
with open('model.pickle', 'wb') as f:
    pickle.dump(model, f)

# 读取模型
with open('model.pickle', 'rb') as f:
    model = pickle.load(f)
model.predict(X_test)
```
* sklearn自带方法joblib
```
from sklearn.externals import joblib

# 保存模型
joblib.dump(model, 'model.pickle')

#载入模型
model = joblib.load('model.pickle')
```
