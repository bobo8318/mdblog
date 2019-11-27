### 1.创建机器学习数据集

* 通过scikit-learn

  > from sklearn import datasets
  >
  > X, y = datasets.make_blobs(100, 2, centers=2, random_state=1701, cluster_std=2)#聚类数据生成器
  >
  > 
  >
  > n_samples是待生成的样本的总数。
  > n_features是每个样本的特征数。
  > centers表示类别数。
  > cluster_std表示每个类别的方差，例如我们希望生成2类数据，其中一类比另一类具有更大的方差，可以将cluster_std设置为[1.0,3.0]。
  >