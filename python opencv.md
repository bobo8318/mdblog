### 1.conda env install OpenCV

* clone code

  > git clone https://github.com/mbeyeler/opencv-machine-learning.git

* add conda-Forge

  > conda config --add channels conda-forge

* create env

  > conda create -n Python3CV python=3.5 --file requirements.txt

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

