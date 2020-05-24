### 1.conda env install OpenCV

* clone code

  > git clone https://github.com/mbeyeler/opencv-machine-learning.git

* add conda-Forge

  > conda config --add channels conda-forge

* create env

  > conda install -c https://conda.binstar.org/menpo opencv
>
  > pip install opencv-python
  >
  > cv /Users/openui/Documents/gitwb/opencv-machine-learning
>
  > conda create -n Python3CV python=3.6 --file requirements.txt
  >
  > import cv2
  >
  > print(cv2.__version__)
  >
  > http://www.mamicode.com/info-detail-2200546.html?__cf_chl_jschl_tk__=28f6631f38b0ca360203696ccbe0afef5d969354-1589977003-0-AU2YD_KbkoaXX4Y7HnHD-vY4ojaR1AkHO6P2Rue48vmLnsc1agi7yXTrhM7a6jMXktoEpyclPTbIEW8f7i3rL6DVE3zK4DcsGatMXJaUIQbm9k_bth9Lqkip6frbeiH7SS3Ry2LI4G57djL_62CwZ5SjTTRvO90Mayg_qCQe6sabz36tTumUKi9vSmLBUNyLgLcJFN0cInW-P1a-0terDmJyKe5pVdXJcgxsOJrZkoshwz7HZV-HBnFTe7jjKqyjQCKszKHsmVutjVi3nfEGaqCq0O32bTdnukIZaFa3PT4h57P7rVQytrXQsdkCVCp0Ug
  >
  > https://www.cnblogs.com/zuoruining/p/8203162.html
  
  * link
  
    > /Users/openui/opt/anaconda3/envs/python38cv/lib/python3.8/site-packages/cv2/cv2.cpython-38-darwin.so
    >
    > 
    >
    > /usr/local/Cellar/opencv/4.3.0/lib/python3.8/site-packages/cv2/python-3.8/cv2.cpython-38-darwin.so
    >
    > 
    >
    > cd /Users/openui/opt/anaconda3/envs/python38cv/lib/python3.8/site-packages  
    >
    > ln -s /usr/local/Cellar/opencv/4.3.0/lib/python3.8/site-packages/cv2/python-3.8/cv2.cpython-38-darwin.so  cv2.so 
  
    ```
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/ conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
    conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/ conda config --set show_channel_urls yes
  
    //C:\Users\My\.condarc
    channels:
      - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/
      - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/msys2/
      - https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud/conda-forge/
    ssl_verify: true
    show_channel_urls: true
    ```

### 2.base 

* plt

  > import matplotlib.pyplot as plt
  >
  > plt.style.use("ggplot")

  * plt.scatter() 散点图
  
    ```
    matplotlib.pyplot.scatter(x, y, s=None, c=None, marker=None, cmap=None, norm=None, vmin=None, vmax=None, alpha=None, linewidths=None, verts=None, edgecolors=None, *, data=None, **kwargs)
    
    参数的解释：
    
    x，y：表示的是大小为(n,)的数组，也就是我们即将绘制散点图的数据点
    
    s:是一个实数或者是一个数组大小为(n,)，这个是一个可选的参数。
    
    c:表示的是颜色，也是一个可选项。默认是蓝色'b',表示的是标记的颜色，或者可以是一个表示颜色的字符，或者是一个长度为n的表示颜色的序列等等，感觉还没用到过现在不解释了。但是c不可以是一个单独的RGB数字，也不可以是一个RGBA的序列。可以是他们的2维数组（只有一行）。
    
    marker:表示的是标记的样式，默认的是'o'。
    
    cmap:Colormap实体或者是一个colormap的名字，cmap仅仅当c是一个浮点数数组的时候才使用。如果没有申明就是image.cmap
    
    norm:Normalize实体来将数据亮度转化到0-1之间，也是只有c是一个浮点数的数组的时候才使用。如果没有申明，就是默认为colors.Normalize。
    
    vmin,vmax:实数，当norm存在的时候忽略。用来进行亮度数据的归一化。
    
    alpha：实数，0-1之间。
    
    linewidths:也就是标记点的长度。 
    
    示例：
    import numpy as np
    import matplotlib.pyplot as plt
     
    np.random.seed(1)
    x=np.random.rand(10)
    y=np.random.rand(10)
     
    colors=np.random.rand(10)
    area=(30*np.random.rand(10))**2
     
    plt.scatter(x,y,s=area,c=colors,alpha=0.5)
    
    plt.show()
    ```
  
    

### 3.数据分析流程

* 数据预处理

  * 特征选择

    > pandas
    >
    > x = titanic[['pclass','age','sex']]
    >
    > y=titanic['survived']

  * 特征转换

    > from sklearn.feature_extraction import DictVectoriser# 字典特征提取器
    > vec = DictVectorizer(sparse=False) *#sparse=False意思是不产生稀疏矩阵* 
    >
    > data = vec.fit_transform(x_train.to_dict(orient='record'))
    >
    > 1.  将字典数据结构抽和向量化
    > 2.   类别类型特征借助原型特征名称采用0 1 二值方式进行向量化
    > 3.   数值类型特征保持不变

  * 特征标准化

    > form sklearn import preprocessing
    >
    > X_scaled = preprocessing.scale(x)//每行均值等于或接近0
    >
    > 
    >
    > form sklearn.preprocessing  import StandardScaler
    >
    > ss = StandardScaler()
    >
    > x_train = ss.fit_transform(x_train)#均值为0 方差为1
    >
    > x_test = ss.transform(x_test)

  * 特征归一化 拥有单位范数的过程

    > //L1范数 曼哈顿距离
    >
    > x_normalized_l1 = preprocessing.normalize(x,norm='l1')
    >
    > // L2范数 欧氏距离
    >
    > x_normalized_l2 = preprocessing.normalize(x, norm='l2')
    >
    > 

  * 数据降维 主成分分析PCA

  * 缺失值处理

    > data = data.replace(to_replace='?', value=np.nan)#?替换为标准的缺失值
    >
    > data = data.dropna(how='any')#丢弃缺失值
    >
    > x['age'].fillna(x['age'].mean(), inplace=true)#pandas

  * 数据分割

    > from sklearn import model_selection as modsel
    >
    > X_train, X_test, y_train, y_test = modsel.train_test_split(boston.data, boston.target, test_size=0.1, random_state=42)

  * 准确率判断

    > from sklearn.metrics import classification_report
    > y_true = [0, 1, 2, 2, 2]
    > y_pred = [0, 0, 2, 2, 1]
    > target_names = ['class 0', 'class 1', 'class 2']
    > print(classification_report(y_true, y_pred, target_names=target_names))
    >
    >             precision    recall  f1-score   support
    >    
    >     class 0       0.50      1.00      0.67         1
    >     class 1       0.00      0.00      0.00         1
    >     class 2       1.00      0.67      0.80         3
    >
    > avg / total       0.70      0.60      0.61         5
    >
    >  当一个搜索引擎返回30个页面时，只有20页是相关的，而没有返回40个额外的相关页面，其精度为20/30 = 2/3，而其召回率为20/60 = 1/3 

    * 准确性（accuracy）:  分对的样本数除以所有的样本数 
    * 召回率（recall）: 结果如何完整 
    * 精确率（precision）:  分为正例的示例中实际为正例的比例
    * f1:  F1 值是精确度和召回率的调和平均值

* 文本特征表示

  > from sklearn.feature_extraction.text import CountVevtorizer
  >
  > vec = CountVevtorizer()
  >
  > x = vec.fit_transform(sample)
  >
  > x.toarray()# 默认为稀疏矩阵，变为常规矩阵
  >
  > vec.get_feature_names()
  >
  > #TF-IDF 通过衡量单词在整个数据中出现的频率来计算权重
  >
  > from  sklearn.feature_extraction.text import TfidfVevtorizer
  >
  > vec = TfidfVevtorizer()

* 图像表示

  * RGB色彩空间编码图像

    > import cv2
    >
    > import matplotlib.pyplot as plt
    >
    > img = cv2.imread('data/lena.jpg')
    >
    > img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)
    >
    > 
    >
    > plt.figure(figsize=(12,6))
    >
    > plt.subplot(121)
    >
    > plt.imshow(img)
    >
    > img.subplot(122)
    >
    > plt.imshow(img_rgb)
    >
    > plt.show()

  * HSV & HLS

    > cv2.COLOR_BGR2HSV
    >
    > cv2.COLOR_BGR2HLS
    >
    > cv2.COLOR_BGR2LAB
    >
    > cv2.COLOR_BGR2YUV

  * 角点检测

    * Harris角点检测:仅可以处理灰度图像

      > img_gray = cv2.cvtColo(img_bgr, cv2.COLOR_BGR2GRAY)
      >
      > corners = cv2.cornerHarris(img_gray, 2, 3, 0.04)# (灰度图像, 角点检测的像素领域大小, 边缘检测的孔径参数, harris检测器自有参数)
      >
      > plt.imshow(corners, cmap='gray')

    * Shi-Tomasi角点检测

      > cv2.goodFearuresToTrack()

    * 尺度不变特征变换
    
      > sift = cv2.xfeatures2d.SIFT_create()
      >
      > kp = sift.detect(img_bgr) #检测
      >
      > 
      >
      > import numpy as np
      >
      > img_kp = np.zeros_like(img_bgr)
      >
      > img_kp = cv2.drawKeypoints(img_bgr, kp, img_kp, flags=cv2.DRAW_MATCHES_FLAGS_DRAW_RICH_KEYPOINTS)
      >
      > plt.imshow(imgkp)
      >
      > #计算特征描述
      >
      > kp, des = sift.compute(img_bgr, kp)
      >
      > kp2, des2 = sift.detectAndCompute(img_bgr, None)
      >
      > #判断两个方法的结果是否相同
      >
      > np.allclose(des, des2)		
    
    * 加强健壮特征:SURF
    
      > surf = cv2.xfeatures2d.SURF_create()
      >
      > kp = surf.detect(img_bgr)
      >
      > 
      >
      > cv2.ORB 免费的替代方案

### 4. 决策树

* data pre 

  > from sklearn.feature_extraction import DictVectorizer # One-Hot 编码
  >
  > vec = DictVectorizer(sparse=False) #sparse=False意思是不产生稀疏矩阵
  >
  > data_pre = vec.fit_transform(data)
  >
  > # 
  >
  > data_pre = np.array(data_pre, dtype=np.float32)

* split data

  > import numy as np 
  >
  > from sklearn.model_selection as ms
  >
  > x_train, x_test, y_train, y_test = ms.train_test_split(data_pre, target, test_size=5, random_state = 42)

* create decide tree

  > import cv2
  >
  > dtree = cv2.ml.dtree_create()
  >
  > 

* train and predict

  > dtree.train(x_train, cv2.ml.ROW_SAMPLE, y_train) #  cv2.ml.ROW_SAMPLE / cv2.ml.COL_SAMPLE 
  >
  > y_pred = dtree.predict(x_test)

* test

  > from sklearn import metrics
  >
  > metrics.accuracy_score(y_test, y_pred)

* show tree

  > from sklearn import tree # 使用sklearn构造决策树
  >
  > dtc = tree.DecisionTreeClassifier() #空的决策树
  >
  > dtc.fit(x_train, y_train)
  >
  > dtc.score(x_test, y_test)
  >
  > conda install graphviz
  >
  > #导出决策树
  >
  > with open("tree.dot", "w"):
  >
  > ​	f = tree.export_graphviz(clf, out_file=f)

* 决策规则

  > dtc = tree.DecisionTreeClassifier(criterion='entropy ') 

  * gini 基尼 
  * entropy 信息熵

* 决策树复杂度

  > DecisionTreeClassifier参数
  >
  > max_depth
  >
  > max_leaf_nodes
  >
  > min_samples_split 设置一节点中的最小数据点来持续分割

* 决策树进行回归

  > tree.DecisionTreeRegressor()

### 5.SVM

* 生成模拟数据

  > x,y = datasets.make_classification(n_samples=100, n_features=2, n_redundant=0, n_classes=2, random_state=7816)
  >
  > 
  >
  > plt.scatter(x[:, 0], x[:, 1], c=y, s=100)
  >
  > plt.xlabel('x values')
  >
  > plt.ylabel('y values')
  >
  > plt.show()

* 数据预处理

  > x = x.astype(np.float32)
  >
  > y = y*2 - 1 # -1 或 1
  >
  > x_train, x_test, y_train, y_test = ms.train_test_split(x, y, test_size=0.2, random_state=42)

### 6.贝叶斯

* 使用sklearn

  > from sklearn import naive_bayes
  >
  > model_naive = naive_bayes.GaussianNB()
  >
  > model_naive.fit(x_train, y_train)


### 7.kmeans

* 一些基础知识

  > reshape(-1,3) # -1表示由计算机自己下决定行数，行数不直接指定
  >
  > np.array([X[labels==i].mean(axis=0) for i in range(n_clusters)])