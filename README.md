## <center> Android中使用OpenCV </center>
<br/>
OpenCV介绍
OpenCV是一个基于BSD许可（开源）发行的跨平台计算机视觉库，可以运行在Linux、Windows、Android和Mac OS操作系统上。这里你只需要知道它是一个视觉库就可以了，更加详细介绍可以去查阅相关资料。

之前比较早的时候写了一篇博文： [AndroidStudio中配置及使用OpenCV示例](http://blog.csdn.net/gao_chun/article/details/49359535) ，
主要介绍了如何在AS中使用OpenCV，基本的配置介绍及使用示例，上传的示例也比较潦草，使用的版本是 OPENCV_VERSION_2_4_9 ，各个版本号在OpenCV的SDK包中是可以看到的：
OpenCV-android-sdk\sdk\java\src\org\opencv\android\OpenCVLoader.java

由于之前使用的OpenCV版本比较老，并且随着手机配置的增强，处理器越来越牛逼，Android的版本也在不断的更新，在配置过程中很多朋友留言说报出来各种乱七八糟的问题，
不知道如何去处理，而且折腾了半天配置完还运行不起来，内心一万头草泥马~，所以我抽时间又整理了下。


OpenCV官网：http://opencv.org/，目前最新版本是3.2，
下载链接：
Android：https://nchc.dl.sourceforge.net/project/opencvlibrary/opencv-android/3.2.0/opencv-3.2.0-android-sdk.zip
iOS：https://nchc.dl.sourceforge.net/project/opencvlibrary/opencv-ios/3.2.0/opencv-3.2.0-ios-framework.zip
GitHub下载：https://github.com/opencv/opencv/releases/tag/3.2.0

项目开发配置：
测试机360 N4
系统版本6.0
OpenCV版本3.2.0
targetSdkVersion 25

GitHub：https://github.com/gaochunchun/OpenCV-Demo