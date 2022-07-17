---
title: 适用于Android的TVSDK 2.4.1发行说明
description: 适用于Android的TVSDK 2.4.1发行说明介绍了TVSDK Android 2.4.1中新增和支持的功能以及已知问题和限制。
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 3de09048-ae32-43b4-a019-34b217931a4c
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 0%

---

# 适用于Android的TVSDK 2.4.1发行说明 {#tvsdk-for-android-release-notes}

适用于Android的TVSDK 2.4.1发行说明介绍了TVSDK Android 2.4.1中新增和支持的功能以及已知问题和限制。

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe将发布适用于Android的TVSDK 2.4.1。

要使用此版本的TVSDK，请确保您的系统满足 [系统要求](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6).

您可以在此处找到文档：

·用于Android的联机帮助系统TVSDK 2.4

· [适用于Android Java API的Javaocs TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Javaoc是最终的权威，因为它们是直接从TVSDK源代码自动生成的。

· [C++ API文档TVSDK 2.4，用于Android C++ API](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

每个Java类都具有相应的C++类，并且C++文档包含比Javaoc更多的解释性材料，因此请查阅C++文档，以更深入地了解Java API。

·迁移指南([适用于Android的TVSDK 2.4迁移指南](../migration-guides/tvsdk-14-25-android.md))

本指南介绍了将基于TVSDK 1.4的应用程序迁移到基于TVSDK 2.4的应用程序时需要进行哪些修改。

## 新增功能 {#new-features}

与早期版本相比，适用于Android的TVSDK 2.4.1提供了许多性能改进。 它提供了高质量的观看体验。

此版本包含版本2.4和2.4.1的所有功能，且未弃用任何功能。

以下是版本2.4.1中的主要新增功能：

* HLS版本4功能

   * **视频播放** （播放、暂停、搜寻）与播放器控件（实时、线性和VOD流）结合使用。
   * **隐藏式字幕。** TVSDK可以显示包含选608/708字体、字体大小、颜色和背景的隐藏式字幕。 它还可以支持带有汇总字幕的视频，并在语言跟踪之间（如果可用）切换。
   * **特技播放模式** 支持使用I帧的HLS流的快速转发和倒带。 所有视频播放控件均可在内容中正常运行。 慢动作（前进）适用于速率介于0和1之间的外部视频播放模式。
   * **自适应比特率(ABR)** 允许播放器根据网络和其他条件动态选择要播放的同一内容流的多个版本中的哪一个。 您可以动态设置参数或在清单文件中设置参数，以在激进的、温和的和保守的选择策略中进行选择。
   * **字节范围** 允许单个TS文件包含多个TS区段。
   * **替代音频演绎版** 使播放器能够在可用的音轨之间切换。
   * **ID3支持。** TVSDK可以播放包含ID3音频元数据（如艺术家姓名、标题和专辑）的HLS音频和视频流。
   * **故障转移。 **尽管主机服务器、播放列表文件和区段出现故障，TVSDK仍使用策略来继续无中断播放。
   * **多声道音频传递(DD+)。** TVSDK可以将杜比数字+音频(E-AC3)数据传递到支持硬件。

* 内容保护功能

   * **HLS的DRM。** 所有视频播放API均可处理受Adobe访问保护的加密视频内容。 支持以下DRM功能：

      * 许可证轮换
      * 键旋转
      * 许可证缓存
      * 策略时间
      * 四轮

* **AES 128播放。** TVSDK可以播放密钥大小为128位的高级加密标准(AES)HLS内容。
* **受保护的HLS(PHLS)** 提供一组有限的预建DRM策略(即Adobe访问提供的子集)，以便在实时流和VOD流的HLS上实现轻量级DRM。

* 广告/备用内容和盈利功能

   * **跟踪服务器端插入的广告。** TVSDK可以跟踪由Adobe云广告插入服务插入的广告。 它支持VAST2、VAST3和VMAP格式中的线性广告，用于VOD和实时/线性流。
   * **自定义HLS标记。** TVSDK使用其 `MediaPlayerConfig` 类，以在流中显示自定义HLS标记时通知播放器应用程序。
   * **客户端广告插入。** Auditude广告插入库可与Adobe Auditude服务器配合使用，以解析广告，以便在前置、中置或后置位置动态插入到实时、线性和VOD内容中。
   * **自定义广告解析器。** 的 `ContentResolver, OpportunityGenerator,` 和 `MediaPlayerClientFactory` 通过界面，您可以实施自定义ad/alternate内容解析程序并注册自定义机会检测器以与TVSDK一起使用。 的 `TestAdResolver` 和 `AuditudeResolver` 类提供了实施内容解析程序的C++示例。 您可以在 `samples/jspsdk/testapp/psdk.js`.
   * **一致的广告行为。** 使用 `AdPolicySelector` 界面，以便当内容中存在广告时，在所有播放器中执行搜寻和特技播放等操作时，能够保持一致的行为。 如果您不实施自己的实施，TVSDK会使用 `DefaultAdPolicySelector`.
   * **删除/替换C3广告。** 使用相应的TVSDK API删除自定义内容范围并动态插入新广告，而无需额外的准备工作。 当直播/线性内容，然后立即按需提供而无需清理时，这会很方便。

以下是2.4版的主要新增功能：

* **适用于VOD和直播的即时视频播放** 启用“即时”时，TVSDK会在播放开始之前初始化和缓冲媒体。 因为您可以启动多个 `MediaPlayerItemLoader` 实例同时位于后台，您可以缓冲多个流。 当用户更改渠道，并且流已正确缓冲时，新渠道上的播放会立即开始。 TVSDK 2.4还支持适用于实时流的即时开启。 当实时窗口移动时，会重新缓冲实时流。

* **性能改进**新的TVSDK 2.4架构改进了各种性能：

   * **子分段** - TVSDK会进一步减小每个片段的大小，以便尽快开始播放。
   * **并行广告下载** - TVSDK在点击广告中断之前预取与内容播放并行的广告，从而实现广告和内容的无缝播放。
   * **延迟广告解析**  — 使用此功能，我们无需等待非前置广告的分辨率即可开始播放，从而缩短启动时间。 在解决所有广告之前，仍不允许使用搜寻和特技播放等API。

* **MP4内容播放**

此版本的TVSDK支持播放MP4作为主内容。

* **永久网络连接**

TVSDK维护一组可重用的网络连接，因此不会产生为每个网络请求创建和销毁网络连接的开销。

* **基于分辨率的输出保护**

此功能将播放限制与特定分辨率绑定，从而提供更细粒度的DRM控件。

* **使用自适应比特率(ABR)进行特技播放**

此功能允许TVSDK在特技播放模式下在iFrame流之间切换。 您可以使用非iFrame配置文件以较低的速度进行特技播放。

* **更流畅的戏法游戏**

这些改进可增强用户体验：

·在特技播放期间，根据带宽和缓冲配置文件选择自适应比特率和帧速率

·使用主流而不是IDR流，可快速播放多达30 fps。

* **改进的ABR逻辑**

新的ABR逻辑基于缓冲长度、缓冲长度变化率和测量的带宽。 这确保ABR在带宽波动时选择正确的比特率，并且还通过监视缓冲长度变化的速率来优化比特率切换实际发生的次数。

* **帐单**

TVSDK会自动收集量度，并遵守客户销售合同，以生成计费所需的定期使用报告。 在每个流开始事件中，TVSDK都使用Adobe Analytics数据插入API将计费量度（如内容类型、广告插入启用标记和基于可计费流持续时间的DRM启用标记）发送到Adobe Analytics Primetime拥有的报表包。 这不会妨碍或包含在客户自己的Adobe Analytics报表包或服务器调用中。 此账单使用情况报表会根据请求定期发送给客户。 这是付费功能的第一阶段，仅支持使用计费。 可以使用文档中描述的API根据销售合同进行配置。

## 支持的功能 {#supported-features}

适用于Android 2.4的TVSDK支持许多可实施的功能，以向视频应用程序添加功能。

>[!NOTE]
>
>在以下功能矩阵表中，√表示当前版本支持该功能。

### 核心播放功能 {#core-playback-features}

| **功能** | **内容类型** | **HLS** | **短划线** |
|---|---|---|---|
| 常规播放（播放、暂停、搜寻） | VOD +实时 | √ | √（仅VOD） |
| FER — 常规播放（播放、暂停、搜寻） | 层VOD | √ | 不支持 |
| MP3 | VOD | 不支持 | 不支持 |
| MP4内容播放 | VOD | √ | √ |
| 自适应比特率切换逻辑 | VOD +实时 | √ | 不支持 |
| 仅音频播放 | VOD +实时 | √ | 不支持 |
| 隐藏式字幕 — 608/708 | VOD +实时 | √ | √（仅VOD） |
| 隐藏式字幕 — WebVTT | VOD +实时 | √ | √（仅VOD） |
| 清单故障转移 | VOD +实时 | √ | √（仅VOD） |
| 高级故障切换 | VOD +实时 | √ | √（仅VOD） |
| QoS和播放器通知 | VOD +实时 | √ | √（仅VOD） |
| 支持Cookie标头 | VOD +实时 | √ | √（仅VOD） |
| 支持自定义标头 | VOD +实时 | 不支持 | 不支持 |
| 设置缓冲控制参数 | VOD +实时 | √ | √（仅VOD） |
| 设置自适应比特率控制 | VOD +实时 | √ | √（仅VOD） |
| 自定义清单标记(HLS)/事件流(DASH) | VOD +实时 | √ | √（仅VOD） |
| 迟到的音频 | VOD +实时 | √ | √（仅VOD） |
| 302重定向 | VOD +实时 | √ | √（仅VOD） |

### 高级播放功能 {#advanced-playback-features}

<table> 
 <tbody>
  <tr>
   <td><strong>功能</strong></td> 
   <td><strong>内容类型</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>短划线</strong></td> 
  </tr>
  <tr>
   <td>带偏移的播放</td> 
   <td>实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>仅音频播放</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>技巧游戏 </td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>平滑技巧播放（使用ABR）</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>ID3解析(HLS)/定时元数据（短划线）</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>封锁 </td> 
   <td>VOD +实时</td> 
   <td>不支持</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>即时启用</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>中断标记支持(HLS) </li> 
     <li>多时段（短划线）</li> 
    </ul> </td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>302重定向粘性</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>√（仅VOD）</td> 
  </tr>
  <tr>
   <td>缩览图推移(Iframe和JPEG)</td> 
   <td>VOD +实时</td> 
   <td>不支持</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>流完整性 </td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
 </tbody>
</table>

### 核心Ad Insertion功能(CSAI) {#core-ad-insertion-features-csai}

| **功能** | **内容类型** | **HLS** | **短划线** |
|---|---|---|---|
| 常规播放，已启用广告 | VOD +实时 | √ | √（仅限VOD预转换） |
| 启用广告的FER内容 | VOD | √ | 不支持 |
| 默认广告行为 | VOD +实时 | √ | √（仅限VOD预转换） |
| VAST 2.0/3.0 | VOD +实时 | √ | √（仅限VOD预转换） |
| VMAP 1.0 | VOD +实时 | √ | √（仅限VOD预转换） |
| MP4广告 | VOD +实时 | √（来自CRS） | √（来自CRS，仅预滚动） |

### 高级Ad Insertion功能(CSAI) {#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>功能</strong></td> 
   <td><strong>内容类型</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>短划线</strong></td> 
  </tr>
  <tr>
   <td>启用广告的特技播放</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>仅限广告 </td> 
   <td>VOD</td> 
   <td>不支持</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>定位参数</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>√（仅限VOD预转换）</td> 
  </tr>
  <tr>
   <td>自定义参数</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>√（仅限VOD预转换）</td> 
  </tr>
  <tr>
   <td>自定义广告行为</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>√（仅限VOD预转换）</td> 
  </tr>
  <tr>
   <td>自定义广告标记</td> 
   <td>实时</td> 
   <td>√ </td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>自定义广告解析器</td> 
   <td>VOD +实时</td> 
   <td>√ </td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>自由轮自定义广告解析程序</td> 
   <td>VOD</td> 
   <td>不支持</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>C3广告替换 </td> 
   <td>VOD +实时</td> 
   <td>√ </td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>延迟广告加载</td> 
   <td>VOD</td> 
   <td>√ </td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>不连续标记支持 — SSAI(HLS) </li> 
     <li>多时段（短划线）</li> 
    </ul> </td> 
   <td>VOD +实时</td> 
   <td>√ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>伴随广告、横幅广告和可点击广告</td> 
   <td>VOD +实时</td> 
   <td>√ </td> 
   <td>√（仅限VOD预转换）</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD +实时</td> 
   <td>√(JS) </td> 
   <td>√（仅限VOD预转换）</td> 
  </tr>
  <tr>
   <td>抢先广告退出</td> 
   <td>实时</td> 
   <td>√ </td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>基于规则的创意VOD +实时优先级设置</td> 
   <td>VOD +实时</td> 
   <td>√ </td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>CRS规则 </td> 
   <td>VOD +实时</td> 
   <td>√ </td> 
   <td>不支持</td> 
  </tr>
 </tbody>
</table>

## 内容保护功能 {#content-protection-features}

| **功能** | **内容类型** | **HLS** | **短划线** |
|---|---|---|---|
| AES加密 | VOD +实时 | √ | √（仅VOD） |
| 示例AES加密 | VOD +实时 | √ |  |
| 标记化流 | VOD +实时 | √ |  |
| DRM | VOD +实时 | 仅限Primetime DRM(未来：维德维内) | 仅限Widevine |
| 外部播放(RBOP) | VOD +实时 | 仅限Primetime DRM | 不支持 |
| 许可证轮换 | VOD +实时 | 仅限Primetime DRM | 不支持 |
| 键旋转 | VOD +实时 | 仅限Primetime DRM | 不支持 |

### 集成功能 {#integration-features}

| **功能** | **内容类型** | **HLS** | **短划线** |
|---|---|---|---|
| Adobe Analytics VHL集成 | VOD +实时 | √ | √ |
| 帐单 | VOD +实时 | √ | 不支持 |

## 不支持的功能 {#features-not-supported}

此版本的TVSDK不支持：

* 广告封锁。
* 玩魔术的慢动作。
* 查找并滴答不漏的MP4内容。
* 包含MP4主内容的广告插入。
* 在广告播放时进行搜寻。
* 使用纯音频媒体播放广告。

## 已知问题和限制 {#known-issues-and-limitations}

此版本的TVSDK存在以下问题：

* 特定于设备(Samsung Galaxy Tab 4)的VOD DRM LBA（带有auditude）崩溃并单击广告
* 不会为特定内容播放后置广告。
* 无法将隐藏式字幕设置为CJK语言。
* 视频可以在VOD和实时视频之间自动脱离特技模式。
* VHL — 当我们从偏移量中启动内容时，发送错误的心率调用。
* 当播放VPAID广告时，事件的VHL心率调用:type:播放广告缺失。
* 即使选择了adBreakPolicy SKIP，也会播放前置广告。
* 进入“完整”状态播放器后，对于后置广告，使用SKIP adBreakPolicy返回到“正在播放”状态。

没有视频，就没有视区尺寸，没有视区尺寸，就无法显示字幕的任何图形。

## 有用资源 {#helpful-resources}

* 请参阅以下完整帮助文档： [Adobe Primetime学习与支持](https://experienceleague.adobe.com/docs/primetime.html) 页面。
