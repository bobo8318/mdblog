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