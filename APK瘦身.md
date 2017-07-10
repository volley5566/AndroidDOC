# APK瘦身
## 1. 下表为Apk目录及文件说明：
* assets/	存放一些静态文件，可以通过AssertManager访问
* lib/	如果该目录存在，一般存放的是NDK编译出来的so
* META-INF/	保存着APK的签名信息
* res/	资源文件所在目录，包含drawable、layout等
* AndroidManifest.xml	程序全局配置文件
* classes.dex	Java Class，被DEX编译后可供Dalvik/ART虚拟机所理解的文件格式
* resources.arsc	编译后生成的二进制资源文件

## 2. 分析APK本身各部分所占大小，来确定好瘦身的主要方向
*　build -> Analyze APK 

一元会购： 分析版本 OneBuy-2.2-beta6.apk
1. res : 占 72.3% 13.1MB
2. classes.dex : 占 19.2% 3.5MB 
3. lib : 占 3.3% 615.2KB

主要的瘦身方向： 
1. 代码部分：冗余代码、无用功能、代码混淆、方法数缩减等；
2. 资源部分：冗余资源、资源混淆、图片处理等；
3. 对So文件的处理等。








## 4. 针对shareSDK 和 appkefu 冗余图片优化
* 两个第三方工程当中涉及的图片，名称不变，将图片内容变成 1 * 1的透明像素点图片

## 5. 删除未使用到xml和图片
如何知道哪些xml和图片未被使用到？使用Android Studio的Lint，步骤：点击菜单栏 Analyze -> Run Inspection by Name -> unused resources -> Moudule ‘app’ -> OK，这样会搜出来哪些未被使用到未使用到xml和图片

## 5. 使用webp格式
对于 res 文件夹，通常占空间最大的就是图片了。如果你的 Android Studio 为 2.3，并且项目的 minSdkVersion 为 18 或以上，应该使用 webp 而不是 png 图片。webp 图片有更小的体积，图片质量还没有什么损失。

我们可以选中 drawable 和 mipmap 文件夹，右键后选择 convert to webp，将图片转为 webp 格式。



## 5. 用使用TinyPng优化Android的资源图片
* 地址 https://tinypng.com/
* 需要注意的是：
1. tinypng支持png和jpg图片的压缩，并且也支持9图的压缩。
2. tinypng的缺点是在压缩某些带有过渡效果（带alpha值）的图片时，图片会失真。
3. tinypng提供了开放接口供开发者开发属于自己的压缩工具，不过这是付费服务，对于普通用户来说，tinypng为每个用户提供的每月图片免费压缩数量已经足够了。

## 6. 使用pngquant来压缩png资源缩小apk
* 使用pngquant来压缩png资源缩小apk http://www.cnblogs.com/soaringEveryday/p/5148881.html  （待测试 ）












## 7. 删除未使用到代码

* 同样使用Android Studio的Lint，步骤：点击菜单栏 Analyze -> Run Inspection by Name -> unused declaration -> Moudule ‘app’ -> OK
但清理效果不太明显










## 8. resConfig和lib
配置resConfigs

如果APP支持中文，可以配置resConfigs，只支持中文

	android {
  	...
    defaultConfig {
      ...
        resConfigs  "en","fr"

        ndk{
        //设置支持的SO库架构
        abiFilters 'armeabi','x86','armeabi-v7a','x86_64','arm64-v8a'
        }
    	}
    }







## AndResGuard资源混淆
* http://www.jianshu.com/p/7ffea26c9fd8













