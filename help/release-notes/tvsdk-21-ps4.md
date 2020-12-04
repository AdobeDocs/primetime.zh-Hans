---
title: TVSDK 2.1 PlayStation 4发行说明
seo-title: TVSDK 2.1 PlayStation 4发行说明
description: TVSDK 2.1 for PlayStation 4发行说明描述了TVSDK 2.1 PlayStation 4中支持的功能和已知问题。
seo-description: TVSDK 2.1 for PlayStation 4发行说明描述了TVSDK 2.1 PlayStation 4中支持的功能和已知问题。
uuid: 494569cf-07e2-476a-b88e-e46c9cca4cdc
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: ebfc8819-f5a9-47a2-b454-0e4e6f9e4640
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6
workflow-type: tm+mt
source-wordcount: '792'
ht-degree: 0%

---


# TVSDK 2.1 PlayStation 4发行说明{#tvsdk-playstation-release-notes}

TVSDK 2.1 for PlayStation 4发行说明描述了TVSDK 2.1 PlayStation 4中支持的功能和已知问题。

## 已解决问题{#resolved-issues}

以下是针对PlayStation 4的TVSDK 2.1的已解决问题：

**版本2.1.0.638**

* **PTPLAY-10439：当**
VMAP包装器和链接断开时，播放器卡在“准备”状态（它未发送） 
`onComplete` )。

* **PTPLAY-10179:**

   `creativeRepackaging` 和 `fallbackOnInvalidCreative` 值现在默认为关闭。此外，当设置`creativeRepackaging`标志但未提供`creativeRepackaging`格式时，调用`onRepackagingComplete`的次数与广告中断中的广告的次数相同，从而多次创建广告中断。

* **Zendesk #10304**:未初始化广告功能开／关变量。现在，我们从`DataSetEntry's`矢量初始化变量。

* **PTPLAY-10318：已**
引入对背景模式的支持。
* **Zendesk # 17409：进**
入特技播放模式后，返回正常播放模式，再进入特技播放模式，播放位置开始跳转。
* **PTPLAY-9552：解**
析响应XML文件后，现在，只要没有广告，错误代码1108就会被ping。
* **PTPLAY-9551:**
当Auditude处理后没有广告中断时，CRS调用 
**** onPrefetchComplete减少groupCount。由于没有广告中断，因此&#x200B;**groupCount**&#x200B;为0并递减1。 以前，**groupCount**&#x200B;是&#x200B;**uint32_t**，因为它用于更改为max值。 现在为&#x200B;**int32_t**。

**版本2.1.0.621**

* **Zendesk #4555**
内存问题即时加载错误- 
`MediaItemLoader` 修复释放时发生的崩溃  `mediaitemloader`

* **Zendesk #17223**
2.x CSAI:并非所有广告跟踪URL都触发
   * 一些VAST广告反过来指向内联广告缺少跟踪URL。
   * 当VAST XML中的广告中有多个印象标记时，只保存第一个印象url，而忽略其余内容。 现在，所有印象URL都将保存并在以后进行ping。
* **Zendesk #17224**
PS4用户代理将黄金时段信息移至UAString末尾
* **Zendesk #17226**
2.x CSAI:并非所有拼接广告。
\
   修复是指出时间轴因insertBy或eraseBy操作而发生更改，并相应地执行期间切换。

* **Zendesk #17284**
   [所有] 平台隐藏式字幕不显示。\
   HLS —— 支持VTT题注文件的`EXT-X-MEDIA-TIME`标记。

* **Zendesk #17889**
在PS4上播放“奶”
\
   应用了正确的yoffset（用于颜色转换）

* **Zendesk #17954广告**
回退逻辑+处理空的海量
\
   修复了当其中一个Vast包装器为空时，用于继续处理包装器的Vast分析器的问题。

* **Zendesk #17807**
无法通过空的大片与Zendesk #3103相同

* **Zendesk #17865**
PS4和XBox One上的回退逻辑
\
   与Zendesk #3103相同

**版本2.1.0.591**

* **Zendesk #3767PS4**
广告代码片断，处理VMAP重定向时广告解析失败。
* **Zendesk #4096**
PS4 CSAI:分段错误修复了在广告库处理VMAP响应时TVSDK引发分段错误时的崩溃。

* **Zendesk #4161**
电影结束时的Trickplay 16x冻结在Trickplay返回到正常播放时发生的固定死锁

* **Zendesk #4208启**
用隐藏式字幕时的随机崩溃启用隐藏式字幕时的固定内存泄漏

* **Zendesk #4213**
PS4 CSAI:更改所有广告相关调用的默认用户代理字符串用户代理字符串是使用浏览器使用+添加Primetime字符串的同一UA字符串创建的

* **PTPLAY-7675** （内部）转码广告在VMAP或VAST响应中调用时不播放Creative Repackaging失败。解决方法是只从广告中阅读媒体文件，而不是在广告大时从资产中阅读。

* **PTPLAY-7895** （内部） `allowMultipleAds=false`当没有广告播放错误修复了参数 `allowMultipleAds` 未正确遵循的问题。

* **PTPLAY-7896** （内部）广告在PS4上的播放顺序不正确修复了广告在XML响应中不按广告显示顺序的问题。

* PS4 TVSDK在小型应用程序（而非游戏）中重新测试。

**版本2.1.0.563**

* **Zendesk #3868**
TVSDK是否支持Playstation SDK 2.5 TVSDK现在使用2.5 Playstation SDK构建。

* **Zendesk #4093**
定位Pt Ads请求中的信息键值对。
\
   添加了分隔键／值对的换行符。

## 支持的功能{#supported-features}

TVSDK 2.1 for PlayStation 4支持以下功能：

**版本2.1.0.621**

* 广告回退，广告选择逻辑中的菊花链(Zendesk #3103)
对于启用回退规则的VAST广告（创意）,TVSDK将MIME类型无效的广告视为空广告并尝试使用回退广告代替广告。您可以配置回退行为的某些方面

**版本2.1.0.538**

* HLS VOD播放，包括播放、暂停、搜索
* 自适应比特率流
* 使用Primetime DRM和香草AES保护的内容进行加密内容回放
* 包含默认广告行为和广告容错的客户端广告插入
* 创意重新打包
* WebVTT隐藏字幕
* 使用自定义开始位置即时启动
* 快进快退的戏法播放
* 302重定向

## 帮助资源{#helpful-resources}

* 请参阅[Adobe Primetime学习和支持](https://helpx.adobe.com/support/primetime.html)页面上的完整帮助文档。