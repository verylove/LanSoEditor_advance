# LanSoEditor_advance
android  video editor  advance sdk . filter, overlay,remark,mixer and so on安卓平台视频编辑高级版本，可以滤镜，叠加，标记等操作
## 当前版本是2.3.0
*  增加FrameInfo类. 
      您可以很快获取到视频中的所有帧时间戳，并获取到多少个关键帧，每个关键字的位置等。
      从而有针对性的快速提取视频帧和或播放器的精确定位。      
*  摄像头图层和视频图层：增加5级美颜效果。
*  视频图层: 当画面小于视频宽高时,增加一个虚化背景.且虚化程度可调.
*  音频部分: 增加多个音频拼接方法,比如音频A,音频B,音频C,拼接后音频是ABC;
*  其他优化。
*  SDK更改为4部分组成. armeabi-v7a,jar LSResource 和lansosdk文件夹.
*  SDK的限制条件: SDK如果没有授权, 则APP名字一定要是我们demo的名字, 请注意.

## SDK简介
* 像Android系统的UI架构设计了各种按钮, 文本框, 编辑框等各种控件一样. 我们设计了各种图层，如果您对UI架构的各种Button/TextView/ImageView熟悉, 用同样的思路来使用我们的SDK即可, 架构清晰易懂,及其方便调用.
*  或者您懂Photoshop的话， 那图层的思想您更明白了， 就是一层一层的处理，和Photoshop一样的图层操作。
*  采用全新的[画板]+ [图层] 的编程思想.
*  您可以认为我们是设计了一款视频处理开发软件，类似AE和Photoshop一样，可以让您在我们的基础上自由的去开发各种视频效果。
*  每个图层都继承自父类Layer，都支持 移动、缩放、旋转、亮暗、闪烁、滤镜等效果。
*  我们设计了一个容器DrawPad，类似Photoshop的工作区，您可以设置工作区的大小，刷新模式，是否实时录制，并设置每一帧的回调监听，处理完成监听，
*  在Drawpad处理过程中:支持任意时间点的加入,隐藏,显示,退出等图层处理.支持叠加过程中的各种调节,支持图层切换，支持实时保存.
*  我们针对每个图层,各种形式均做了Activity的演示, 大概有30个左右的Activity,这些在com\example\advanceDemo文件夹下,您都可以演示.
*  如果您遇到一些特殊的图层处理方法，也可以在 合作后，我们为您做简单的演示代码。 
*  我们的SDK完全以API的形式呈现,稳定可靠,简单易用,您可以根据项目的个性化而任意的发挥.


## 核心架构
*   一个工程是由多个线程组成, 又由各种类对象组成. 
*   我们把对视频处理的OpenGLGL技术处理后封装成 线程，命名为DrawPad(画板)
*   对视频处理用到的各种素材，封装成类，命名为Layer(图层)
*   这样视频处理的OpenGLGL线程中增加的各种类对象，就被抽象成 画板和图层的关系。和日常画画流程一致，方便您的使用。
*   画板：用来处理各种素材的线程，分为 [画板前台线程] 和 [画板后台线程], 您自由选择使用。
*   图层：编辑会用到的素材。包括：视频，图片，文字，摄像头，裸数据，MV等。这些经过我们的核心技术处理，变成：视频图层， 		图片图层，UI图层，Canvas图层，数据图层，摄像头图层，MV图层,Gif图层等。
*   抽象类Layer：继承它的有：视频图层， 图片图层，UI图层，数据图层，摄像头图层，MV图层；均有：平移/缩放/旋转/隐藏/显示/RGBA调节的功能。
		另外他们各自也有独立的方法。
*   滤镜功能：当前所有的图层均支持滤镜功能。

## 当前具有的图层种类有(8种):
*  视频图层    VideoLayer
*  摄像头图层  CameraLayer
*  图片图层    BitmapLayer
*  MV图层      MVLayer
*  UI图层      UILayer
*  Canvas图层  CanvasLayer
*  Data图层    DataLayer
*  Gif图层     GifLayer
			
## 三步调用（3Step）
*	1， 创建一个容器(DrawPad):  设置容器的宽度和高度,刷新率,码率,设置进度监听,结束监听 各种Listener等
* 2,  开启这个容器,开启后,增加各种图层来实现你的处理效果, 并在处理监听中,来调节图层的各种变化,从而有各种效果.
* 3,  结束容器的执行.
   

## 更仅一步说:
*	1， 您想给视频增加滤镜，则可以在开启Drawpad后,增加一个视频图层,并给图层设置滤镜效果即可. 也可以设置压缩,缩放或其他功能.
* 2,  您想给视频增加图片,文字. 则可以用 视频图层+Canvas图层+ bitmap图层,三个叠加一起,即可完成.当然也可以在指定位置,指定时间增加,也可以增加后旋转移动缩放等操作.
* 3, 您想把多种图层合成视频. 则可以 增加多个 [图片图层], 可以设置图片的各种飞入飞出,旋转,移动等效果.
*	4，你用 【UI图层  ViewLayer或CanvasLayer】在画板上作画， 就是把精美的UI界面转换为视频， 当然我们的设计，也可以后台处理。
* 5， 你用  【视频图层】 + 【MV图层】 在画板上作画， 就是在视频中叠加MV的效果。
* 6， 你用  【视频图层】 + 【Gif图层】 在画板上作画， 就是在视频中叠加Gif动画的效果。
* 7， 我们针对每个图层都做了举例，您可以在我们Demo中找到；
* 8， 可以在前台工作， 也可以在后台处理。
* 9， 此SDK采用为收费授权,公司性质的合作,为了您项目更好的进行,欢迎和我们联系.谢谢!


## 下载地址: 
*  https://github.com/LanSoSdk/LanSoEditor_advance

## 我们有基本视频编辑,以方便您项目中基本需求：
*	https://github.com/LanSoSdk/LanSoEditor_common

## 我们的IOS版本， 欢迎您的使用：
*	https://github.com/LanSoSdk/LanSongEditor_IOS

## 直接下载获取APK:
   下载整个项目后, 在bin文件下有apk, 直接安装后即可演示.


## 联系方式:
*   QQ 1852600324 
*   Email:support@lansongtech.com
*   网址: www.lansongtech.com

*  如果您下载过慢, 可联系我们, 索取最新的工程包