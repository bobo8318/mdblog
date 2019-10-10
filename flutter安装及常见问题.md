title:flutter安装及常见问题
date: 2019-08-19
Category: 移动开发
Tags: 移动开发,android
Authors: openui
Summary: flutter安装及常见问题

- 常用命令

  ```
  
  --version
  查看Flutter版本
  
  -h或者--help
  
  打印所有命令行用法信息
  
  analyze
  分析项目的Dart代码。
  
  build
  Flutter构建命令。
  
  channel
  列表或开关Flutter通道。
  
  clean
  删除构建/目录。
  
  config
  配置Flutter设置。
  
  create
  创建一个新的Flutter项目。
  
  devices
  列出所有连接的设备。
  
  doctor
  展示了有关安装工具的信息。
  
  drive
  为当前项目运行Flutter驱动程序测试。
  
  format
  格式一个或多个Dart文件。
  
  fuchsia_reload
  在Fuchsia上进行热重载。
  
  help
  显示帮助信息的Flutter。
  
  install
  在附加设备上安装Flutter应用程序。
  
  logs
  显示用于运行Flutter应用程序的日志输出。
  
  packages
  命令用于管理Flutter包。
  
  precache
  填充了Flutter工具的二进制工件缓存。
  
  run
  在附加设备上运行你的Flutter应用程序。
  
  screenshot
  从一个连接的设备截图。
  
  stop
  停止在附加设备上的Flutter应用。
  
  test
  对当前项目的Flutter单元测试。
  
  trace
  开始并停止跟踪运行的Flutter应用程序。
  
  upgrade
  升级你的Flutter副本。
  ```

- 安装

   git clone -b beta https://github.com/flutter/flutter.git

  * IDE选装插件 dart flutter
  * ANDROID_HONE 环境变量设置

  * 检测
  > flutter doctor

  * 创建项目
  > flutter create demo001

  * 检测手机
  > flutter devices

  * 运行程序
  > flutter run

  *更新flutter
  
  > flutter upgrade


* 快捷键

* 常见问题

  * 更新国内镜像地址，设置环境变量

    > export PUB_HOSTED_URL=https://pub.flutter-io.cn
    >
    > export FLUTTER_STORAGE_BASE_URL=https://storage.flutter-io.cn

