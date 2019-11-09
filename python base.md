title:python base
date: 2019-11-9
Category: python
Tags: python
Authors: openui
Summary:python base

* * create env

    > conda create --name python36 python=3.6
  >
    > conda create -n python2 python=2.7
  
  * use env

    > //win
  >
    > activate env_name
    >
    > // linux & mac
    >
    > source activate env_name
  
  * exit env

    > //win 
  >
    > deactivate
    >
    > //linux & mac
    >
    > source deactivate
  
  * list env

    > conda env list

  * remove env

    > conda remove --name python36 --all
  >
    > conda env remove -n python36
  
  * install package

    > conda install package_name
  >
    > conda install numpy=1.14
  
  * remove package

    > conda remove package_name

  * update package

    > conda update package_name

* beautifulsoup

  > conda install beautifulsoup4
  >
  > from bs4 import BeautifulSoup