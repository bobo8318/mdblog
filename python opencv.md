### 1.conda env install OpenCV

* clone code

  > git clone https://github.com/mbeyeler/opencv-machine-learning.git

* add conda-Forge

  > conda config --add channels conda-forge

* create env

  > conda create -n Python3CV python=3.6--file requirements.txt

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

  * 特征标准化

    > form sklearn import preprocessing
    >
    > X_scaled = preprocessing.scale(x)//每行均值等于或接近0

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

  > from sklearn import tree
  >
  > dtc = tree.DecisionTreeClassifier()
  >
  > dtc.fit(x_train, y_train)
  >
  > dtc.score(x_test, y_test)
  >
  > conda install graphviz