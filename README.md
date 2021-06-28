# OC_Flutter
iOS原生项目混编flutter 文档说明+小demo演示
## 一、创建Flutter模块
#### 1-1、需要在项目同级目录创建
#### 1-2、通过命令行创建flutter模块
> flutter create -t module hello_modu
le

## 二、创建iOS原生项目
#### 2-1、进入到OC_Flutter的iOS 主工程目录。
> cd /Users/weiyouyou/Desktop/OC_Flutter/OC_Flutter


#### 2-2、使用Cocoapods创建podfile文件。
> pod init

#### 2-3、打Podfile文件
> open Podfile

#### 2-4、在Podfile文件中添加代码 （flutter_application_path填入相对路径）
```
  # Comment the next line if you don't want to use dynamic frameworks
  use_frameworks!
 
  # Pods for OC_Flutter
 
  flutter_application_path = '../hello_module' 
  load File.join(flutter_application_path, '.ios', 'Flutter', 'podhelper.rb')
  install_all_flutter_pods(flutter_application_path)
 
 end
```
#### 2-5、执行pod install
> pod install

可以看到 安装成功
#### 2-6、Flutter 暂时不支持Bitcode，在Build Settings->Build Options->Enable Bitcode 设置为NO

## 三、iOS原生界面跳转到Flutter界面
#### 3-1、在iOS原生工程里导包
```
#import <Flutter/Flutter.h>
#import <FlutterPluginRegistrant/GeneratedPluginRegistrant.h> // 如果你需要用到Flutter插件时
```

#### 3-2、flutter界面弹出，这里使用模态视图
```
    FlutterViewController *flutterViewController = [FlutterViewController new];
    //GeneratedPluginRegistrant.register(with: flutterViewController);//如果你需要用到Flutter插件时
    [flutterViewController setInitialRoute:@"route1"];
    [self presentViewController:flutterViewController animated:true completion:nil];
```


#### 3-3、用Android studio 打开 hello_module

#### 3-4、在main.dart 文件中添加如下代码，进行路由配置
```
import 'dart:ui';
void main() => runApp(_widgetForRoute(window.defaultRouteName));
​
Widget _widgetForRoute(String route) {
switch (route) {
case 'route1':
return MyApp();
default:
return Center(
child: Text('Unknown route: $route', textDirection: TextDirection.ltr),
);
}
}
```

原生工程成功集成了flutter module ,撒花花~~😄

