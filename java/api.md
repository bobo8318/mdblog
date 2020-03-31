* 1.主页面统计:

  * 请求URL：

    > /mainstat

	* 请求方式：GET

  * 参数:无

  * 返回示例
  
    ```
    {
        totalProduct: 659,
        onSale: 869,
        mobileSale: 911,
        newProduct: 659,
        totalShop: 869,
        onlineShop: 911,
        mobileSaleShop: 659,
        newShop: 869
    }
    ```
  
* 2.主页面大盘数据饼图

  * 请求URL

    > /salePie

  * 请求方式：POST

  * 请求参数

    | 参数名   | 必选 | 类型 | 说明                             |
    | -------- | ---- | ---- | -------------------------------- |
    | statType | 是   | int  | 1 按销售数量，2 按销售金额       |
    | statDays | 是   | int  | 前（1 ，3，7，14，30，60）天数据 |

  * 返回示例

    ```
    [
        ['Firefox',   45.0],
        ['IE',       26.8],
        ['Chrome', 12.8],
        ['Safari',    8.5],
        ['Opera',     6.2],
        ['Others',   0.7]
    ]
    ```

  * 返回参数说明

* 3.主页面上新动态饼图

  * 请求URL：

    > /newPie

  * 请求方式：GET

  * 参数

    | 参数名   | 必选 | 类型   | 说明                             |
    | -------- | ---- | ------ | -------------------------------- |
    | proType  | 否   | String |                                  |
    | statDays | 是   | int    | 前（1 ，3，7，14，30，60）天数据 |

  * 返回示例

    ```
    [
        ['Firefox',   45.0],
        ['IE',       26.8],
        ['Chrome', 12.8],
        ['Safari',    8.5],
        ['Opera',     6.2],
        ['Others',   0.7]
    ]
    ```

  * 参数说明

* 4.趋势图数据

  * 请求URL

    > /lineChartData

* 5.top商品

  * 请求URL

    > /topPro
    
  * 请求方式：POST

  * 请求参数

    | 参数名 | 必选 | 类型 | 说明     |
    | ------ | ---- | ---- | -------- |
    | limit  | 是   | int  | 显示条数 |
    
  * 返回示例

    ```
    {
            yesterdayBest:[{"img":"http://localhost:9000/ceshi/1.jpg","name":"【油污克星】3秒快速去除污渍，车内、卫生间、厨房，1厘米厚的老油垢,一喷净！","salesVolume":"6085"},   
                        ],
            newBest:[{"img":"http://localhost:9000/ceshi/1.jpg","name":"【油污克星】3秒快速去除污渍，车内、卫生间、厨房，1厘米厚的老油垢,一喷净！","salesVolume":"6085"},
                        ],
            everbest:[{"img":"http://localhost:9000/ceshi/1.jpg","name":"【油污克星】3秒快速去除污渍，车内、卫生间、厨房，1厘米厚的老油垢,一喷净！","salesVolume":"6085"},  
                        ]
        }
    ```

  * 返回参数说明

    | 参数名        | 说明     |
    | ------------- | -------- |
    | yesterdayBest | 昨日爆款 |
    | newBest       | 潜力新秀 |
    | everbest      | 常青榜   |
    | img           | 商品图   |
    | name          | 商品名   |
    | salesVolume   | 昨日销量 |

    

* 6.top店铺

  * 请求URL

    > /topShop
    
  * 请求方式：POST

  * 请求参数

    | 参数名 | 必选 | 类型 | 说明     |
    | ------ | ---- | ---- | -------- |
    | limit  | 是   | int  | 显示条数 |

  * 返回示例

    ```
     {
            yesterdayBest:[{"img":"http://localhost:9000/ceshi/1.jpg","name":"【油污克星】3秒快速去除污渍，车内、卫生间、厨房，1厘米厚的老油垢,一喷净！","salesVolume":"6085"},
                        ],
            newBest:[{"img":"http://localhost:9000/ceshi/1.jpg","name":"【油污克星】3秒快速去除污渍，车内、卫生间、厨房，1厘米厚的老油垢,一喷净！","salesVolume":"6085"},  
                        ],
            everbest:[{"img":"http://localhost:9000/ceshi/1.jpg","name":"【油污克星】3秒快速去除污渍，车内、卫生间、厨房，1厘米厚的老油垢,一喷净！","salesVolume":"6085"},  
                        ]
        }
    ```

  * 返回参数说明

    | 参数名        | 说明     |
    | ------------- | -------- |
    | yesterdayBest | 昨日爆款 |
    | newBest       | 潜力新秀 |
    | everbest      | 常青榜   |
    | img           | 店铺品图 |
    | name          | 店铺名   |
    | salesVolume   | 昨日销量 |

* 7.商品列表

  * 请求URL

    > /searchProduct
    
  * 请求方式：POST

  * 请求参数

    | 参数名         | 必选 | 类型   | 说明                    |
    | -------------- | ---- | ------ | ----------------------- |
    | productType    |      |        | 商品类别                |
    | saleDateFrom   |      | String | 上架日期始              |
    | saleDateTo     |      | String | 上架日期止              |
    | priceFrom      |      | int    | 价格始                  |
    | priceTo        |      | int    | 价格止                  |
    | saleVolumeFrom |      | int    | 销量始                  |
    | saleVolumeTo   |      | int    | 销量止                  |
    | status         |      |        | 状态：全部 、上架、下架 |
    | productName    |      | String | 商品名                  |
    |                |      |        |                         |
    | pagesize       |      |        |                         |
    | currentPage    |      |        |                         |
    | ordertype      |      |        |                         |
    |                |      |        |                         |

  * 返回示例

    ```
    [
            {"id":1,'img':"2","name":"【限时买一送一 领10元券】完美日记氨基酸卸妆水送卸妆湿巾1","protype":"化妆品","shop":"Perfect Diary完美日记旗舰店","resource":"鲁班","price":"¥138-¥198","day1":"36","days3":"1876","days7":"6803","salesvolume":"30000+","sales":"50万+","saledate":"2019-12-09","iwatch":"0"},
            {"id":2,'img':"2","name":"【限时买一送一 领10元券】完美日记氨基酸卸妆水送卸妆湿巾2","protype":"化妆品","shop":"Perfect Diary完美日记旗舰店","resource":"鲁班","price":"¥138-¥198","day1":"37","days3":"1875","days7":"6804","salesvolume":"20000+","sales":"51万+","saledate":"2019-12-10","iwatch":"1"},
        ]
    ```

  * 返回参数说明

    | 参数名      | 说明     |
    | ----------- | -------- |
    | id          |          |
    | img         | 图片     |
    | name        | 名字     |
    | protype     | 商品类别 |
    | shop        | 店铺     |
    | resource    | 来源     |
    | price       | 价格     |
    | day1        | 一日销量 |
    | days3       | 3日销量  |
    | days7       | 7日销量  |
    | salesvolume | 累计销量 |
    | sales       | 销售额   |
    | saledate    | 上架时间 |
    |             |          |

* 8.店铺列表

  * 请求URL

    > /searchShop
    
  * 请求方式：POST

  * 请求参数

    | 参数名      | 必选 | 类型   | 说明         |
    | ----------- | ---- | ------ | ------------ |
    | productType | 否   | String | 类别         |
    | shopName    | 否   | String | 店铺名称     |
    | limit       | 是   | int    | 每页显示数量 |
    | currentPage | 是   | int    | 页码         |
    | ordertype   | 是   | int    | 0 升序 1降序 |
    | sortopt     | 是   | String | 排序项 ：    |

  * 返回示例

    ```
    [
       {"id":1,'img':"2","name":"淘天然1","comp":"赣州市星橙电子商务有限公司","main":"生鲜-蔬菜-茄果瓜类","onsale":"17","day1":"3510","days3":"7019","days7":"45501","days30":"45502","allwatch":"122","iwatch":"0"},
        ]
    
    ```

    返回参数说明

    | 参数名   | 说明     |
    | -------- | -------- |
    | id       |          |
    | img      | 图片     |
    | name     | 名字     |
    | comp     | 所属公司 |
    | main     | 主营类目 |
    | onsale   | 在售商品 |
    | days30   | 30日销量 |
    | day1     | 一日销量 |
    | days3    | 3日销量  |
    | days7    | 7日销量  |
    | allwatch | 关注数   |
    |          |          |
    |          |          |
    |          |          |

* 9.收藏商品列表

  * 请求URL

    > /getWatchPro
    
  * 请求方式：POST

  * 请求参数

    | 参数名 | 必选 | 类型   | 说明           |
    | ------ | ---- | ------ | -------------- |
    | proids | 是   | String | 关注商品id列表 |
    
  * 返回示例

    ```
  {"id":1,'img':"2","name":"【限时买一送一 领10元券】完美日记氨基酸卸妆水送卸妆湿巾1","protype":"化妆品","shop":"Perfect Diary完美日记旗舰店","resource":"鲁班","price":"¥138-¥198","day1":"36","days3":"1876","days7":"6803","salesvolume":"30000+","sales":"50万+","saledate":"2019-12-09"}
    ```
    
    

* 10.收藏店铺列表

  * 请求URL

  	> /getWatchShop
  	
  * 请求方式：POST
  
  * 请求参数
  
    | 参数名  | 必选 | 类型   | 说明           |
    | ------- | ---- | ------ | -------------- |
    | shopids | 是   | String | 关注商品id列表 |
  
  * 返回示例
  
    ```
     {"id":1,'img':"2","name":"淘天然1","comp":"赣州市星橙电子商务有限公司","main":"生鲜-蔬菜-茄果瓜类","onsale":"17","day1":"3510","days3":"7019","days7":"45501","days30":"45502","allwatch":"122","iwatch":"0"},
    ```
  
    
  
* 11.获取商品分类

  * 请求URL

    > /getProTypeList

  * 请求方式：POST

  * 请求参数

    | 参数名 | 必选 | 类型 | 说明     |
    | ------ | ---- | ---- | -------- |
    | ftype  | 是   |      | 父级分类 |

  * 返回示例

    ```
    
    ```

    