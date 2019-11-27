title:python base
date: 2019-11-9
Category: python
Tags: python
Authors: openui
Summary:python base

* create env

  > conda create --name python36 python=3.6
  > conda create -n python2 python=2.7

  * use env

    > //win
    > activate env_name
    > // linux & mac
    > source activate env_name

  * exit env

    > //win 
    > deactivate
    > //linux & mac
    > source deactivate

  * list env

    > conda env list

  * remove env

    > conda remove --name python36 --all
    > conda env remove -n python36

  * install package

    > conda install package_name
    > conda install numpy=1.14

  * remove package

    > conda remove package_name

  * update package

    > conda update package_name

* beautifulsoup

  > conda install beautifulsoup4
  > from bs4 import BeautifulSoup

* 模块

  ```
  .
  └── mypackage
      ├── __init__.py  #导入包时会执行这里的代码
      ├── subpackage_1
      │   ├── test11.py
      │   └── test12.py
      ├── subpackage_2
      │   ├── test21.py
      │   └── test22.py
      └── subpackage_3
          ├── test31.py
          └── test32.py
  ```
  
  > from mypackage.subpackage_1 import test11

