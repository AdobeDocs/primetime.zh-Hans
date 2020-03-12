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

---


# TVSDK 2.1 PlayStation 4发行说明 {#tvsdk-playstation-release-notes}

TVSDK 2.1 for PlayStation 4发行说明描述了TVSDK 2.1 PlayStation 4中支持的功能和已知问题。

## 已解决的问题 {#resolved-issues}

以下是PlayStation 4的TVSDK 2.1的已解决问题：

**版本2.1.0.638**

* **PTPLAY-10439:**&#x200B;当VMAP包装器和链接断开时，播放器将卡在“准备”状态(它不发送 `onComplete` 给其调用者)。

* **PTPLAY-10179:**
   `creativeRepackaging` 并且 `fallbackOnInvalidCreative` 现在默认情况下，值处于关闭状态。 此外，设置旗 `creativeRepackaging` 标但未提供格 `creativeRepackaging``onRepackagingComplete` 式时，会像广告中断中的广告一样多次调用该广告，从而导致多次创建广告中断。

* **Zendesk #10304**:ad forveness on/off变量未初始化。 我们现在从矢量初始化变 `DataSetEntry's` 量。

* **PTPLAY-10318:**&#x200B;引入了对背景模式的支持。
* **Zendesk # 17409:**&#x200B;当进入特技播放模式时，回到正常播放模式，再进入特技播放模式时，播放位置发生跳转。
* **PTPLAY-9552:**&#x200B;解析响应XML文件后，现在，只要没有广告，就会ping错误代码1108。
* **PTPLAY-9551:**&#x200B;当Auditude处理后没有广告中断时，CRS将调用 **onPrefetchComplete** ，这会减少groupCount。 由于没有广告中断， **groupCount** 为0，递减1。 以前 **groupCount是** uint32_t **** ，因为它用于更改为max值。 现在为 **int32_t**。

**版本2.1.0.621**

* **Zendesk #4555**`MediaItemLoader` Instant on Memory issues leading-loading errors - Fix for crash and being leaseing `mediaitemloader`

* **Zendesk #17223** 2.x CSAI:并非所有广告跟踪URL都触发
   * 一些VAST广告反过来指向内联广告缺少跟踪URL。
   * 当VAST XML中的广告中有多个印象标记时，只保存第一印象URL，而忽略其余内容。 现在，所有印象URL都将保存并在以后平移。
* **Zendesk #17224** PS4用户代理将黄金时段信息移至UAString结束
* **Zendesk #17226** 2.x CSAI:并非所有拼合广告。\
   修复是指示时间轴因insertBy或eraseBy操作而发生更改，并相应地执行周期切换。

* **Zendesk #17284**
   [所有平台] “隐藏式字幕”均不显示。\
   HLS —— 支持VTT题 `EXT-X-MEDIA-TIME` 注文件的标记。

* **Zendesk #17889**&#x200B;在PS4上播放“Michly”\
   应用了正确的yoffset（用于颜色转换）

* **Zendesk #17954广告**&#x200B;回退逻辑+处理空的海量\
   修复了当其中一个Vast包装器为空时，用于继续处理包装器的Vast分析器的问题。

* **Zendesk #17807**&#x200B;无法通过空的广场与Zendesk #3103相同

* **Zendesk #17865** Fallback Logic on PS4 and XBox One\
   与Zendesk #3103相同

**版本2.1.0.591**

* **Zendesk #3767** PS4广告代码片断，在处理VMAP重定向时，广告解析失败。
* **Zendesk #4096** PS4 CSAI:分段错误修复了当广告库处理VMAP响应时TVSDK引发分段错误时的崩溃。

* **Zendesk #4161**&#x200B;电影结束时停止播放的16x修复了在播放返回到正常播放时发生的死锁

* **Zendesk #4208打开隐**&#x200B;藏式字幕时的随机崩溃启用隐藏式字幕时的固定内存泄漏

* **Zendesk #4213** PS4 CSAI:更改所有与广告相关的调用的默认用户代理字符串用户代理字符串是使用浏览器使用+添加Primetime字符串的同一UA字符串创建的

* **PTPLAY-7675** （内部）转码广告不播放在VMAP或VAST响应中调用Creative Repackaging时失败。 解决方法是只从广告中阅读媒体文件，而不是在广告大时从资产中阅读。

* **PTPLAY-7895** （内部） `allowMultipleAds=false`当没有广告播放时，修复了参数未 `allowMultipleAds` 正确跟踪的错误。

* **PTPLAY-7896** （内部）广告在PS4上的播放顺序错误修复了广告在XML响应中不按广告显示顺序的问题。

* PS4 TVSDK在小型应用程序（而非游戏）中重新测试。

**版本2.1.0.563**

* **Zendesk #3868** TVSDK是否支持Playstation SDK 2.5TVSDK现在使用2.5 Playstation SDK构建。

* **Zendesk #4093**&#x200B;定位Pt Ads请求中的信息键值对。\
   添加了分隔键／值对的换行符。

## 支持的功能 {#supported-features}

TVSDK 2.1 for PlayStation 4支持以下功能：

**版本2.1.0.621**

* 广告回退，广告选择逻辑中的菊花链(Zendesk #3103)对于启用回退规则的VAST广告（创意）,TVSDK将MIME类型无效的广告视为空广告并尝试在其位置使用回退广告。您可以配置回退行为的某些方面

**版本2.1.0.538**

* HLS VOD播放，包括播放、暂停、搜索
* 自适应比特率流
* 使用Primetime DRM和受AES保护的加密内容回放
* 包含默认广告行为和广告容错的客户端广告插入
* 创意重新打包
* WebVTT隐藏式字幕
* 使用自定义开始位置即时启动
* 快速前进和快速后退的特技播放
* 302重定向

## 实用资源 {#helpful-resources}

* 请参阅 [Adobe Primetime学习和支持页面上的完整帮助文档](https://helpx.adobe.com/support/primetime.html) 。