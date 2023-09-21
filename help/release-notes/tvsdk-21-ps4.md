---
title: TVSDK 2.1 PlayStation 4发行说明
description: 《适用于PlayStation 4的TVSDK 2.1发行说明》介绍了TVSDK 2.1 PlayStation 4中支持的功能和已知问题。
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# TVSDK 2.1 PlayStation 4发行说明 {#tvsdk-playstation-release-notes}

《适用于PlayStation 4的TVSDK 2.1发行说明》介绍了TVSDK 2.1 PlayStation 4中支持的功能和已知问题。

## 已解决的问题 {#resolved-issues}

以下是适用于PlayStation 4的TVSDK 2.1的已解决的问题：

**版本2.1.0.638**

* **PTPLAY-10439：**
当VMAP包装器广告链接断开时，播放器卡在准备状态（未发送） `onComplete` 致其调用方)。

* **PTPLAY-10179：**
  `creativeRepackaging` 和 `fallbackOnInvalidCreative` 值现在默认为off。 此外，当 `creativeRepackaging` 已设置标志，但未设置 `creativeRepackaging` 提供了格式， `onRepackagingComplete` 多次被调用，因为广告时间中存在广告，从而导致多次创建广告时间。

* **Zendesk #10304**：未初始化ad forveness on/off变量。 我们现在从以下位置初始化变量 `DataSetEntry's` ctor。

* **PTPLAY-10318：**
还引入了后台模式支持。
* **Zendesk # 17409：**
进入特技播放模式，然后返回正常播放模式，再次进入特技播放模式时，播放位置发生跳跃。
* **PTPLAY-9552：**
现在，在分析响应XML文件后，只要没有广告，就会固定错误代码1108。
* **PTPLAY-9551：**
当Auditude处理之后没有广告时间时，CRS调用 **onPrefetchComplete** 会减少groupCount。 由于没有广告时间， **组计数** 为0，递减1。 以前的 **组计数** 是 **uint32_t** 因此，它以前会更改为最大值。 这是现在 **int32_t**.

**版本2.1.0.621**

* **Zendesk #4555**
Instant on Memory问题导致加载错误 —  `MediaItemLoader` 修复了在释放时发生崩溃的问题 `mediaitemloader`

* **Zendesk #17223**
2.x CSAI：并非所有广告跟踪URL都会触发
   * 某些VAST广告反过来指向内联广告，因此缺少跟踪URL。
   * 当VAST XML中的广告具有多个展示标记时，仅保存第一印象URL，并且忽略其余部分。 现在，将保存所有展示URL，并稍后执行Ping操作。
* **Zendesk #17224**
PS4用户代理将primetime信息移动到UAString的结尾
* **Zendesk #17226**
2.x CSAI：并非所有广告都已拼合。\
  修复是指时间轴因insertBy或eraseBy操作而发生更改，并相应地执行周期切换。

* **Zendesk #17284**
  [所有平台] 隐藏式字幕不显示。\
  HLS — 支持 `EXT-X-MEDIA-TIME` VTT描述文件的标记。

* **Zendesk #17889**
在PS4上播放“Milky”\
  已应用正确最小值（用于颜色转换）

* **Zendesk #17954**
广告回退逻辑+处理空的vast\
  修复了以下问题：如果其中一个Vast包装为空，则使用Vast解析器继续处理包装器。

* **Zendesk #17807**
无法通过empty vast与Zendesk #3103相同

* **Zendesk #17865**
PS4和XBox One上的回退逻辑\
  与Zendesk #3103相同

**版本2.1.0.591**

* **Zendesk #3767**
PS4广告代码段，处理VMAP重定向时广告解析失败。
* **Zendesk #4096**
PS4 CSAI：分段错误修复了在广告库处理VMAP响应时，TVSDK引发分段错误时的崩溃。

* **Zendesk #4161**
影片末尾的Trickplay 16x冻结修复了在点击播放恢复正常播放时发生死锁的问题

* **Zendesk #4208**
打开隐藏式字幕时的随机崩溃启用隐藏式字幕时的固定内存泄漏

* **Zendesk #4213**
PS4 CSAI：更改所有与广告相关的调用的默认用户代理字符串用户代理字符串是使用与浏览器相同的UA字符串创建的，并添加黄金时间字符串

* **PTPLAY-7675** （内部）转码广告不会播放创意重新打包在VMAP或VAST响应中调用时失败。 Fix是在出现大量广告时，从广告读取媒体文件，而不是从资产读取。

* **PTPLAY-7895** （内部）时间 `allowMultipleAds=false`，无广告播放修复了以下错误： `allowMultipleAds` 参数未正确跟随。

* **PTPLAY-7896** （内部）广告在PS4上按顺序播放修复了广告在XML响应中不按顺序显示的问题。

* PS4 TVSDK已在小型应用程序而非游戏中重新测试。

**版本2.1.0.563**

* **Zendesk #3868**
TVSDK是否支持Playstation SDK 2.5 TVSDK现在使用2.5 Playstation SDK构建。

* **Zendesk #4093**
Pt广告请求中的targetingInfo键值对。\
  添加了分隔键/值对的新行字符。

## 支持的功能 {#supported-features}

适用于PlayStation 4的TVSDK 2.1支持以下功能：

**版本2.1.0.621**

* 广告回退，在广告选择逻辑(Zendesk #3103)中链接雏菊对于启用了回退规则的VAST广告（创意），TVSDK会将具有无效MIME类型的广告视为空广告，并尝试在其位置使用回退广告。您可以配置回退行为的某些方面

**版本2.1.0.538**

* HLS VOD播放，包括播放、暂停、搜寻
* 自适应比特率流
* 使用Primetime DRM和受AES保护的原型内容进行加密内容播放
* 带有默认广告行为和广告宽恕的客户端Ad Insertion
* 创意重新打包
* WebVTT隐藏式字幕
* 使用自定义起始位置立即打开
* 具有快速前进和快速倒带的特技游戏
* 302重定向

## 有用资源 {#helpful-resources}

* 请参阅完整的帮助文档，网址为 [Adobe Primetime学习与支持](https://experienceleague.adobe.com/docs/primetime.html) 页面。
