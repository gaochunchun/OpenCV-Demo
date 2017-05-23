## <center> Android中使用OpenCV </center>
<br/>
之前比较早的时候写了一篇博文： [AndroidStudio中配置及使用OpenCV示例](http://blog.csdn.net/gao_chun/article/details/49359535) ，主要介绍了如何在AS中使用OpenCV，基本的配置介绍及使用示例，上传的示例也比较潦草，使用的版本是 <font color=Crimson size=2> OPENCV_VERSION_2_4_9 </font>，各个版本号在OpenCV的SDK包中是可以看到的：
<font color=Crimson size=2>OpenCV-android-sdk\sdk\java\src\org\opencv\android\OpenCVLoader.java</font>
```
package org.opencv.android;
import android.content.Context;

/**
 * Helper class provides common initialization methods for OpenCV library.
 */
public class OpenCVLoader
{
    /**
     * OpenCV Library version 2.4.2.
     */
    public static final String OPENCV_VERSION_2_4_2 = "2.4.2";

    /**
     * OpenCV Library version 2.4.3.
     */
    public static final String OPENCV_VERSION_2_4_3 = "2.4.3";

    /**
     * OpenCV Library version 2.4.4.
     */
    public static final String OPENCV_VERSION_2_4_4 = "2.4.4";

    /**
     * OpenCV Library version 2.4.5.
     */
    public static final String OPENCV_VERSION_2_4_5 = "2.4.5";

    /**
     * OpenCV Library version 2.4.6.
     */
    public static final String OPENCV_VERSION_2_4_6 = "2.4.6";

    /**
     * OpenCV Library version 2.4.7.
     */
    public static final String OPENCV_VERSION_2_4_7 = "2.4.7";

    /**
     * OpenCV Library version 2.4.8.
     */
    public static final String OPENCV_VERSION_2_4_8 = "2.4.8";

    /**
     * OpenCV Library version 2.4.9.
     */
    public static final String OPENCV_VERSION_2_4_9 = "2.4.9";

    /**
     * OpenCV Library version 2.4.10.
     */
    public static final String OPENCV_VERSION_2_4_10 = "2.4.10";

    /**
     * OpenCV Library version 2.4.11.
     */
    public static final String OPENCV_VERSION_2_4_11 = "2.4.11";

    /**
     * OpenCV Library version 2.4.12.
     */
    public static final String OPENCV_VERSION_2_4_12 = "2.4.12";

    /**
     * OpenCV Library version 2.4.13.
     */
    public static final String OPENCV_VERSION_2_4_13 = "2.4.13";

    /**
     * OpenCV Library version 3.0.0.
     */
    public static final String OPENCV_VERSION_3_0_0 = "3.0.0";

    /**
     * OpenCV Library version 3.1.0.
     */
    public static final String OPENCV_VERSION_3_1_0 = "3.1.0";

    /**
     * OpenCV Library version 3.2.0.
     */
    public static final String OPENCV_VERSION_3_2_0 = "3.2.0";

    /**
     * Loads and initializes OpenCV library from current application package. Roughly, it's an analog of system.loadLibrary("opencv_java").
     * @return Returns true is initialization of OpenCV was successful.
     */
    public static boolean initDebug()
    {
        return StaticHelper.initOpenCV(false);
    }

    /**
     * Loads and initializes OpenCV library from current application package. Roughly, it's an analog of system.loadLibrary("opencv_java").
     * @param InitCuda load and initialize CUDA runtime libraries.
     * @return Returns true is initialization of OpenCV was successful.
     */
    public static boolean initDebug(boolean InitCuda)
    {
        return StaticHelper.initOpenCV(InitCuda);
    }

    /**
     * Loads and initializes OpenCV library using OpenCV Engine service.
     * @param Version OpenCV library version.
     * @param AppContext application context for connecting to the service.
     * @param Callback object, that implements LoaderCallbackInterface for handling the connection status.
     * @return Returns true if initialization of OpenCV is successful.
     */
    public static boolean initAsync(String Version, Context AppContext,
            LoaderCallbackInterface Callback)
    {
        return AsyncServiceHelper.initOpenCV(Version, AppContext, Callback);
    }
}

```
由于之前使用的OpenCV版本比较老，并且随着手机配置的增强，处理器越来越牛逼，Android的版本也在不断的更新，在配置过程中很多朋友留言说报出来各种乱七八糟的问题，不知道如何去处理，而且折腾了半天配置完还运行不起来，内心一万头草泥马~，所以我抽时间又整理了下，示例这次上传完整的，不管多大。

OpenCV介绍
OpenCV是一个基于BSD许可（开源）发行的跨平台计算机视觉库，可以运行在Linux、Windows、Android和Mac OS操作系统上。这里你只需要知道它是一个视觉库就可以了，更加详细介绍可以去查阅相关资料。

OpenCV官网：http://opencv.org/，目前最新版本是3.2，下载链接：
**Android**：https://nchc.dl.sourceforge.net/project/opencvlibrary/opencv-android/3.2.0/opencv-3.2.0-android-sdk.zip
**iOS**：https://nchc.dl.sourceforge.net/project/opencvlibrary/opencv-ios/3.2.0/opencv-3.2.0-ios-framework.zip
**GitHub下载**：https://github.com/opencv/opencv/releases/tag/3.2.0

在之前那篇文章的基础上，我们就更换一下OpenCV的版本还有总结下之前问题的出现及解决方案。
我在下载了之前的旧版本示例后，尝试将新的3.2版本的 native--->Libs--->每个目录中的 <font color=Crimson size=2>libopencv_java3.so </font>复制到项目中时，很糟糕，出现了如下问题：

<center>![bug-1](http://img.blog.csdn.net/20170523145725508?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZ2FvX2NodW4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)</center>
程序闪退，我或许不该这么干，因为从2.4.9到3.2.0也许更新了太多的东西，他们库里的方法或许是不能兼容的，这时，我还是乖乖按照 [第一篇文章](http://blog.csdn.net/gao_chun/article/details/49359535) 中的方式将sdk ---> java ---> src下的代码Copy到项目中，OK，直接Run了一下看会不会成功，结果也很糟糕，报错信息如下：
<center>![bug-2](http://img.blog.csdn.net/20170523151305611?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZ2FvX2NodW4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)</center>
这次比上次要好有点，起码它告诉我这条信息：<font color=red size=2>dlopen failed: "/data/app/org.opencv.engine-1/lib/arm/libopencv_java3.so" is 32-bit instead of 64-bit</font>
而且在手机中运行程序的提示信息：
<center>![bug-4](http://img.blog.csdn.net/20170523151909819?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZ2FvX2NodW4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)</center>
Google一番之后，发现问题和使用的targetSDKVersion版本有关，也就是手机系统的版本，5.0？ 6.0？Ok，那这个问题就引刃而解了。错误解决方案：

[libopencv_java3.so is 64-bit instead of 32-bit Android/Eclipse error](https://github.com/opencv/opencv/issues/6124)

[Android 6.0: Load 32-bit OpenCV library on 64-bit arch](https://github.com/opencv/opencv/issues/5862)

[Error Opencv4Android: Caused by: java.lang.IllegalArgumentException: Service Intent must be explicit](http://answers.opencv.org/question/54450/error-opencv4android-caused-by-javalangillegalargumentexception-service-intent-must-be-explicit/)

[OpenCV Service Intent must be explicit, Android 5.0 Lolipop](https://stackoverflow.com/questions/27470313/opencv-service-intent-must-be-explicit-android-5-0-lolipop)
<br/>
也就是在Activity的onResume()方法中初始化OpenCV时，加入了一个判断，OpenCVLoader.initDebug() 可以跟踪进去看看代码。
<center>![demo](http://img.blog.csdn.net/20170523161141093?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZ2FvX2NodW4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)</center>


若需要 OpenCV Manager支持可以到APP应用市场下载，这里我已经一并上传至项目apk目录下了，安装后的界面：
<center>![OpenCV Manager](http://img.blog.csdn.net/20170523173344957?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZ2FvX2NodW4=/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)</center>


#### 配置介绍：
<font color=Blue size=3>测试机360 N4
系统版本6.0
OpenCV版本3.2.0
targetSdkVersion 25
</font>

### GitHub：https://github.com/gaochunchun/OpenCV-Demo