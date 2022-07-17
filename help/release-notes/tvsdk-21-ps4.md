---
title: TVSDK 2.1 PlayStation 4发行说明
description: 适用于PlayStation 4的TVSDK 2.1发行说明介绍了TVSDK 2.1 PlayStation 4中受支持的功能和已知问题。
contentOwner: dekalra
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 32af3fe4-c730-41f6-a558-987bd14c9bae
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '772'
ht-degree: 0%

---

# TVSDK 2.1 PlayStation 4发行说明 {#tvsdk-playstation-release-notes}

适用于PlayStation 4的TVSDK 2.1发行说明介绍了TVSDK 2.1 PlayStation 4中受支持的功能和已知问题。

## 已解决的问题 {#resolved-issues}

以下是适用于PlayStation 4的TVSDK 2.1的已解决问题：

**版本2.1.0.638**

* **PTPLAY-10439:**
当VMAP包装器广告链接断开时，播放器陷入“正在准备”状态（未发送） 
`onComplete` )。

* **PTPLAY-10179:**

   `creativeRepackaging` 和 `fallbackOnInvalidCreative` 默认情况下，值处于关闭状态。 此外，当 `creativeRepackaging` 已设置标志，但无 `creativeRepackaging` 格式， `onRepackagingComplete` 被调用的次数与广告时间中的广告次数相同，从而导致多次创建广告时间。

* **森德克#10304**:未初始化广告发送打开/关闭变量。 我们现在从初始化变量 `DataSetEntry's` 矢量。

* **PTPLAY-10318:**
引入了对后台模式的支持。
* **Zendesk # 17409:**
进入特技播放模式后，再回到正常播放模式，再进入特技播放模式时，播放位置出现跳转。
* **PTPLAY-9552:**
现在，解析响应XML文件后，当没有广告时，就会对错误代码1108进行ping。
* **PTPLAY-9551:**
当Auditude处理后没有广告时间时，CRS调用 
**onPrefetchComplete** 这会减少groupCount。 因为没有广告时间， **groupCount** 为0，减1。 以前， **groupCount** was **uint32_t** 因此，它会更改为最大值。 现在 **int32_t**.

**版本2.1.0.621**

* **森德克#4555**
内存问题即时导致加载错误 —  
`MediaItemLoader` 修复了在释放时发生崩溃的问题 `mediaitemloader`

* **森德克#17223**
2.x CSAI:并非所有广告跟踪URL都触发
   * 一些VAST广告反过来指向内联广告，缺少跟踪URL。
   * 当VAST XML中的广告中存在多个展示标记时，只会保存第一次展示URL，而其余的则会被忽略。 现在，将保存所有展示url，并稍后对其进行ping。
* **森德克#17224**
PS4用户代理将黄金时段信息移至UAString的末尾
* **森德克#17226**
2.x CSAI:并非所有广告都拼合在中。
\
   修复是指由于insertBy或eraseBy操作，时间轴已发生更改，并相应地执行期间切换。

* **森德克#17284**
   [所有平台] 隐藏式字幕不显示。\
   HLS — 支持 `EXT-X-MEDIA-TIME` 标记。

* **森德克#17889**
在PS4上播放“乳状”
\
   应用了正确的yoffset（用于颜色转换）

* **森德克#17954**
广告回退逻辑+处理空vast
\
   修复了当其中一个Vast包装器为空时，用于继续处理包装器的Vast解析器的问题。

* **森德克#17807**
无法与Zendesk #3103一样通过空的vast

* **森德克#17865**
PS4和XBox One上的回退逻辑
\
   与森德克一样#3103

**版本2.1.0.591**

* **森德克#3767**
PS4广告代码段，处理VMAP重定向时，广告解析失败。
* **森德克#4096**
PS4 CSAI:分段错误修复了在广告库处理VMAP响应时，TVSDK引发分段错误时的崩溃。

* **森德克#4161**
影片结尾的trickplay 16x冻结修复了trickplay返回正常播放时出现的死锁

* **森德克#4208**
启用隐藏式字幕时随机崩溃固定内存泄漏启用隐藏式字幕时

* **森德克#4213**
PS4 CSAI:更改所有与广告相关的调用的默认用户代理字符串使用浏览器使用+添加Primetime字符串的相同UA字符串创建用户代理字符串

* **PTPLAY-7675** （内部）转码广告在VMAP或VAST响应中调用时，未播放Creative Repackaging失败。 修复是，在广告广告中，只从广告中读取媒体文件，而不是从资产中读取。

* **PTPLAY-7895** （内部） `allowMultipleAds=false`，无广告播放修复了 `allowMultipleAds` 参数未正确跟踪。

* **PTPLAY-7896** （内部）广告在PS4上的播放顺序不正确的问题修复了广告未按广告在XML响应中显示的顺序播放的问题。

* PS4 TVSDK在微型应用程序（而不是游戏）中重新测试。

**版本2.1.0.563**

* **森德克#3868**
TVSDK是否支持Playstation SDK 2.5现在，TVSDK是通过2.5 Playstation SDK构建的。

* **森德克#4093**
targetingInfo键值对。
\
   添加了分隔键/值对的换行符。

## 支持的功能 {#supported-features}

适用于PlayStation 4的TVSDK 2.1支持以下功能：

**版本2.1.0.621**

* 广告回退，在广告选择逻辑中以菊花链(Zendesk #3103)对于启用回退规则的VAST广告（创意），TVSDK会将MIME类型无效的广告视为空广告，并尝试使用回退广告来替换广告。您可以配置回退行为的某些方面

**版本2.1.0.538**

* HLS VOD播放，包括播放、暂停、搜寻
* 自适应比特率流
* 使用Primetime DRM和原有AES保护内容的加密内容播放
* 具有默认广告行为和广告原理的客户端广告插入
* 创意重新打包
* WebVTT隐藏式字幕
* 具有自定义开始位置的即时启动
* 快进快退的特技游戏
* 302重定向

## 有用资源 {#helpful-resources}

* 请参阅以下完整帮助文档： [Adobe Primetime学习与支持](https://experienceleague.adobe.com/docs/primetime.html) 页面。
