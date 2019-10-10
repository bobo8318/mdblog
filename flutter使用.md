* 重要基础内容

  * 风格：material.dart   cupertino.dart

    > ```
    > import 'package:flutter/material.dart'
    > ```

  * 组件:所有元素均为Widget 继承StatelessWidget StatefulWidget

    * StatelessWidget  静态组件

      ```
      class MyApp extends StateLessWidget{
          @overwrite
          Widget build(BuildContext context){
              return MaterialApp(
              title:'',
              theme:ThemeData.light(),
              home:BottomNavigationWidget()
              );
          }
          
      }
      ```

      

    * StatefulWidget 动态组件

      ```
      class BottomNavigationWidget extends StatefulWidget{
          _BottomNavigationWidget createState() => _BottomNavigationWidgetState();
      }
      
      class _BottomNavigationWidgetState extends State<BottomNavigationWidget>{
          int _curentindex = 0;
      
          @overwrite
          Widget build(BuildContext context){
              return Scaffold(
              body:list[_curentindex],
              bottomNavigationBar:BottomNavigationBar(
                  items:[
                      BottomNavigationBarItem(
                          icon:Icon(Icons.home,color:blue),
                          title:Text()
                      )
                  ],
                  currenIndex:_currentIndex,
                  onTap:(int index){
                      setState((){
                          _currentIndex = index;
                      });
                  }
              ));
          }
          
          @overwrite
          void initState(){
              list
                  ..add(Home())
                  ..add()
                  ..add();
              super.initState();
          }
      }
      ```

      

  * ### MaterialApp 代表使用纸墨设计（Material Design）风格的应用

    ```
    title ： 在任务管理窗口中所显示的应用名字
    theme ： 应用各种 UI 所使用的主题颜色
    color ： 应用的主要颜色值（primary color），也就是安卓任务管理窗口中所显示的应用颜色
    home ： 应用默认所显示的界面 Widget
    routes ： 应用的顶级导航表格，这个是多页面应用用来控制页面跳转的，类似于网页的网址
    initialRoute ：第一个显示的路由名字，默认值为 Window.defaultRouteName
    onGenerateRoute ： 生成路由的回调函数，当导航的命名路由的时候，会使用这个来生成界面
    onLocaleChanged ： 当系统修改语言的时候，会触发å这个回调
    navigatorObservers ： 应用 Navigator 的监听器
    debugShowMaterialGrid ： 是否显示 纸墨设计 基础布局网格，用来调试 UI 的工具
    showPerformanceOverlay ： 显示性能标签，https://flutter.io/debugging/#performanceoverlay
    checkerboardRasterCacheImages 、showSemanticsDebugger、debugShowCheckedModeBanner 各种调试开关
    ```

    

  * ### Scaffold 单个页面的脚手架

    ```
    appBar - 显示在界面顶部的一个 AppBar。
    body - 当前界面所显示的主要内容 Widget。
    floatingActionButton - Material 设计中所定义的 FAB，界面的主要功能按钮。
    persistentFooterButtons - 固定在下方显示的按钮，比如对话框下方的确定、取消按钮。
    drawer - 抽屉菜单控件。
    backgroundColor - 内容的背景颜色，默认使用的是 ThemeData.scaffoldBackgroundColor 的值。
    bottomNavigationBar - 显示在页面底部的导航栏。
    resizeToAvoidBottomPadding - 类似于 Android 中的 android:windowSoftInputMode='adjustResize'，控制界面内容 body 是否重新布局来避免底部被覆盖了，比如当键盘显示的时候，重新布局避免被键盘盖住内容。默认值为 true。
    ```

  * 网络请求

    * dio:https://pub.flutter-io.cn/packages/dio

      * pubspec.yaml 文件中添加支持以来 

        > denpendencies 添加依赖
        >
        > dio: ^2.0.9

      * 引入

        > import 'package:dio/dio.dart';
  
      * 简单实用
      
        ```
        void getHttp() async {// 异步
          try {
            Response response = await Dio().get("http://www.google.cn");
            print(response);
          } catch (e) {
            print(e);
          }
        }
        
        // post
        response = await dio.post("/test", data: {"id": 12, "name": "wendu"});
        // form
        FormData formData = new FormData.from({
            "name": "wendux",
            "age": 25,
          });
         
        ```
      
      * 伪造请求头
      
        ```
        // httpdeader.dart
        const headers={
        
        }
        
        // home.dart 
        Future getHttp() async{
        	try{
        		Response response;
        		Dio dio = new Dio();
        		dio.options.headers = httpHeaders;
        		response = await dio.get("");
        		return response.data;
        	}catch(e){
        		return print(e);
        	}
        
        }
        
        void _jike(){
        	getHttp().then((val){
        		setStat((){
        			showtext=val
        		});
        	});
        }
        ```
      
        
  
  * 常用示例
    
    * 导航
      
      * 一般导航
      
    ```text
      Navigator.push(context,new  MaterialPageRoute(
                    builder:(context) =>new SecondScreen())
                  );
                  
      Navigator.pop(context);
      ```
      
      * 底部导航
    
        > BottomNavigationBar(
        >
        > ​        type: BottomNavigationBarType.fixed,
        >
        > ​        items:itemlist,
        >
        > ​        currentIndex: currentIndex,
        >
        > ​        onTap: (index){
        >
        > ​          setState(() {
        >
        > ​            currentIndex = index;
        >
        > ​            currentPage = pagelist[currentIndex];
        >
        > ​          });
        >
        > ​        }
        >
        > ​      )
    
         ```
        
         ```
    
    * 布局
    
      * Column 列布局
    
        ```
        Column(
        	children:<widget[
        		Text(),
        		RaisedButton()
        	]>
        )
        ```
    
        
    
    * Button
    
      | RaisedButton  | Material Design中的button， 一个凸起的材质矩形按钮。         |
      | ------------- | ------------------------------------------------------------ |
      | FlatButton    | Material Design中的button，一个没有阴影的材质设计按钮。      |
      | OutlineButton | Material Design中的button，RaisedButton和FlatButton之间的交叉：一个带边框的背景透明的按钮，当按下按钮时，其高度增加，背景变得不透明。 |
    
      * RaisedButton(onpress:(){},child:Text('finished'))
    
    * showDialog()
    
    * Future:`return await ...`的时候，实际上返回的是一个延迟计算的`Future`对象
    
      > Future.then(funA());
    
    * TextField：输入文本框
    
      ```
      TextField(
              controller: controller,
              maxLength: 30,//最大长度，设置此项会让TextField右下角有一个输入数量的统计字符串
              maxLines: 1,//最大行数
              autocorrect: true,//是否自动更正
              autofocus: true,//是否自动对焦
              obscureText: true,//是否是密码
              textAlign: TextAlign.center,//文本对齐方式
              style: TextStyle(fontSize: 30.0, color: Colors.blue),//输入文本的样式
              inputFormatters: [WhitelistingTextInputFormatter.digitsOnly],//允许的输入格式
              onChanged: (text) {//内容改变的回调
                print('change $text');
              },
              onSubmitted: (text) {//内容提交(按回车)的回调
                print('submit $text');
              },
              enabled: true,//是否禁用
        );
      ```
    
        
    
      * 监听变化
    
        ```
        String value = "";
        TextField(
          onChanged: (text) {
            value = text;
          },
        )
        
        // 使用controller
        TextEditingController controller = TextEditingController();
        TextField(
          controller: controller,
        )
        //监听变化
        controller.addListener(() {
          // Do something here
        });
        // 获取 设置 值
        print(controller.text); // Print current value
        controller.text = "Demo Text"; // Set new value
        ```
    
        * 装饰 textfield
    
          ```
          decoration: InputDecoration(
              icon: Icon(Icons.print),
              contentPadding:EdgeInsets.all(10.0),
              labelText:'hello',
              helperText:'help me'
          )
          
          TextField(
            decoration: InputDecoration(
              prefixIcon: Icon(Icons.print)
            ),
          ),
          ```
    
          
        
      * SingleChildScrollView 解决键盘弹起变形
    
      * swiper:轮播效果插件
    
        > dependencies
        >
        > 	flutter_swiper:^1.1.4