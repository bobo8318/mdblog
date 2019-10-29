#### chapter 1

#### chapter2 python base

* import lib

  > import math
  >
  > import math as m
  >
  > from math import exp as e
  >
  > from math import * 

* data structer

  * List

    > a = [1,2,3]
    >
    > b = [i+2 for i in a]
    >
    > list('ab') # ['a','b']

  * Tuple: can not modify

    > a = (4,5,6)
    >
    > tuple([1,2])# (1,2)

  * Dictionary

    > d = {'today':20,'tomorrow':30}
    >
    > d['today'] # 20
    >
    > dict([['today',20],['tomorrow',30]])
    >
    > dict.fromleys({'today','tomorrow'},20)

  * Set

* functional programming

  * lambda

    > f = lambda x : x+2 

  * map

    > b = map(lambda x:x+2,a)
    >
    > b = list(b)

  * reduce

  * filter

*  tools

   *  Numy

      > import numpy as np
      >
      > np.array([2,0,1,5])
      >
      > np.array([[2,0,1,5],[4,5,7,8]])
      >
      > print[:3]
      >
      > print(a*b)

   *  Scipy

      > from scipy.optimize import fsolve

   * Matplotlib

     > import matplotlib.pyplot as plt
  >
     > plt.rcParams['font.sans-serif'] = ['SimHei']
  >
     > plt.rcParams['axes.unicode_minus'] = False
  >
     > plt.figure(figsize = (7,5))

   * pandas
   
     > base 
     >
     > sum mean var std corr  cov skew/kurt
     >
     > graph
     >
     > plot pie hist boxplot plot(logy=True) plot(yerr = eorro)
     >
     > 
     >
     > \# line figure
     >
     > x = np.linspace(0,2*np.pi,50)
     >
     > y = np.sin(x)
     >
     > plt.plot(x,y,'bp--')
     >
     > plt.show()
     >
     > 
     >
     > \# pie figure 
     >
     > lablels = ['Frogs','Hogs','Dogs','Logs']
     >
     > sizes = [15,30,45,10]
     >
     > colors = ['yellowgreen','gold','lightskyblue','lightcoral']
     >
     > explorde = (0,0.1,0,0)
     >
     > plt.pie(sizes,explode=explorde,labels=lablels,colors=colors,autopct='%1.1f%%',shadow=True,startangle=90)
     >
     > plt.axis('equal')
     >
     > plt.show();
   
   *  StatsModels
   
   *  Scikit-Learn
   
   *  Keras
   
   *  Gensim