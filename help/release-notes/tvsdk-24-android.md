---
title: 适用于Android的TVSDK 2.4.1发行说明
description: 适用于Android的TVSDK 2.4.1发行说明介绍了TVSDK Android 2.4.1中的新增功能和受支持功能，以及已知问题和限制。
topic-tags: release-notes
products: SG_PRIMETIME
exl-id: 3de09048-ae32-43b4-a019-34b217931a4c
source-git-commit: 3b051c3188c81673129e12dfeb573aaf85c15c97
workflow-type: tm+mt
source-wordcount: '1962'
ht-degree: 0%

---

# 适用于Android的TVSDK 2.4.1发行说明 {#tvsdk-for-android-release-notes}

适用于Android的TVSDK 2.4.1发行说明介绍了TVSDK Android 2.4.1中的新增功能和受支持功能，以及已知问题和限制。

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe将发布适用于Android的TVSDK 2.4.1。

要使用此版本的TVSDK，请确保您的系统满足中所述的要求。 [系统要求](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6).

您可以在此处找到文档：

·适用于Android的联机帮助系统TVSDK 2.4帮助

· [适用于Android的Javadocs TVSDK 2.4 Java API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Javadocs是最终权威，因为它们是直接从TVSDK源代码自动生成的。

· [适用于Android C++ API的C++ API文档TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

每个Java类都有一个相应的C++类，并且C++文档包含比Javadocs更多的说明性材料，因此请参阅C++文档以更深入地了解Java API。

·迁移指南([适用于Android的TVSDK 2.4迁移指南](../migration-guides/tvsdk-14-25-android.md))

本指南说明了将基于TVSDK 1.4的应用程序迁移到基于TVSDK 2.4的应用程序时需要修改的内容。

## 新增功能 {#new-features}

与早期版本相比，适用于Android的TVSDK 2.4.1提供了许多性能改进。 它提供了高品质的观看体验。

此版本包含版本2.4和2.4.1的所有功能，并且没有已弃用的功能。

以下是版本2.4.1中的主要新增功能：

* HLS版本4功能

   * **视频播放** （播放、暂停、搜寻），播放器可控制实时、线性和VOD流。
   * **隐藏字幕。** TVSDK可以显示608/708隐藏式字幕，其中包含字体、字体大小、颜色和背景选择。 它还可以支持带汇总字幕的视频，并在语言跟踪之间切换（如果可用）。
   * **特技播放模式** 支持使用I-Frame的HLS流的快速前进和倒带。 所有视频播放控制对内容起作用。 慢动作（前进）可用于速率介于0和1之间的外部视频播放模式。
   * **自适应比特率(ABR)** 允许播放器根据网络和其他条件，动态选择要播放的同一内容流的多个版本。 您可以动态地或在清单文件中设置参数，以便在积极的、温和的和保守的选择策略中进行选择。
   * **字节范围** 启用单个TS文件以包含多个TS区段。
   * **替代音频演绎版** 使播放器能够在可用音轨之间切换。
   * **ID3支持。** TVSDK可以播放包含ID3音频元数据的HLS音频和视频流，例如艺人姓名、标题和专辑。
   * **故障转移。 尽管主机服务器、播放列表文件和区段出现故障，**TVSDK仍使用策略继续不间断播放。
   * **多声道音频直通(DD+)。** TVSDK可以将Dolby Digital Plus音频(E-AC3)数据传递给支持硬件。

* 内容保护功能

   * **HLS的DRM。** 所有视频播放API都可与受Adobe访问保护的加密视频内容配合使用。 支持以下DRM功能：

      * 许可证轮换
      * 密钥轮替
      * 许可证缓存
      * 策略时间
      * IV旋转

* **AES 128播放。** TVSDK可以播放密钥大小为128位的高级加密标准(AES) HLS内容。
* **受保护的HLS (PHL)** 提供一组有限的预建DRM策略(Adobe访问提供的策略子集)，以便为实时流和VOD流启用基于HLS的轻量级DRM。

* 广告/替代内容和盈利功能

   * **跟踪服务器端插入的广告。** TVSDK可以跟踪Adobe云广告插入服务插入的广告。 它支持用于VOD和实时/线性流的VAST2、VAST3和VMAP格式的线性广告。
   * **自定义HLS标记。** TVSDK使用其 `MediaPlayerConfig` 类，用于在自定义HLS标记出现在流中时通知播放器应用程序。
   * **客户端广告插入。** Auditude广告插入库可与Adobe Auditude服务器配合使用，以解决广告问题，以便在前置、中置或后置位置动态地插入实时、线性和VOD内容。
   * **自定义广告解析程序。** 此 `ContentResolver, OpportunityGenerator,` 和 `MediaPlayerClientFactory` 通过界面，您可以实施自定义广告/替代内容解析器，并注册自定义机会检测器以与TVSDK配合使用。 此 `TestAdResolver` 和 `AuditudeResolver` 类提供了实施内容解析器的C++示例。 您可以在Javascript示例中找到 `samples/jspsdk/testapp/psdk.js`.
   * **一致的广告行为。** 使用 `AdPolicySelector` 界面，当内容中存在广告时，启用所有播放器的一致行为，以执行搜寻和特技播放等操作。 如果您不实施自己的解决方案，TVSDK会使用 `DefaultAdPolicySelector`.
   * **删除/替换C3广告。** 使用相应的TVSDK API删除自定义内容范围并动态插入新广告，而无需额外的准备工作。 当直播/线性内容播出，然后立即按需提供而无需清理时，这会很方便。

以下是版本2.4的主要新增功能：

* **即时打开以进行VOD和直播** 启用“即时打开”后，TVSDK会在播放开始之前初始化并缓冲媒体。 因为您可以启动多个 `MediaPlayerItemLoader` 在后台同时执行实例时，可以缓冲多个流。 当用户更改频道，并且流已正确缓冲时，新频道上的播放立即开始。 TVSDK 2.4还支持实时流的Instant On。 当实时窗口移动时，实时流将被重新缓冲。

* **性能改进**新的TVSDK 2.4架构带来了各种性能改进：

   * **子分段** - TVSDK进一步减小了每个片段的大小，以尽快开始播放。
   * **并行广告下载** - TVSDK会在点击广告时间之前与内容播放并行预取广告，从而实现广告和内容的无缝播放。
   * **延迟广告分辨率**  — 利用此功能，我们无需等待非前置广告解析后再开始播放，从而缩短了启动时间。 直到解决所有广告之后，才允许使用搜寻和特技播放等API。

* **MP4内容播放**

此版本的TVSDK支持播放MP4作为主要内容。

* **永久网络连接**

TVSDK维护一组可重用的网络连接，因此不会产生为每个网络请求创建和销毁网络连接的开销。

* **基于分辨率的输出保护**

此功能将播放限制绑定到特定分辨率，从而提供更细粒度的DRM控制。

* **具有自适应比特率(ABR)的特技播放**

此功能允许TVSDK在特技播放模式中切换iFrame流。 您可以使用非iFrame配置文件以较低的速度进行特技播放。

* **更流畅的戏法游戏**

这些改进增强了用户体验：

·在特技播放期间基于带宽和缓冲器配置文件的自适应比特率和帧速率选择

·使用主流而不是IDR流获得最高30 fps的快速播放。

* **改进了ABR逻辑**

该逻辑基于缓冲区长度、缓冲区长度变化率和测量带宽。 这样可以确保ABR在带宽波动时选择正确的比特率，并通过监控缓冲区长度变化的速率来优化比特率切换的实际次数。

* **计费**

TVSDK根据客户销售合同自动收集量度，以生成计费所需的定期使用情况报告。 在每个流开始事件上，TVSDK使用Adobe Analytics数据插入API将计费指标（如内容类型、启用广告插入的标记和启用drm的标记）根据计费流的持续时间发送到Adobe Analytics Primetime拥有的报表包。 这不会干扰客户自己的Adobe Analytics报表包或服务器调用或使其包含在内。 根据请求，定期向客户发送此计费使用情况报告。 这是仅支持使用计费的计费功能的第一个阶段。 可以使用文档中描述的API，根据销售合同对其进行配置。

## 支持的功能 {#supported-features}

适用于Android 2.4的TVSDK支持许多您可实施以向视频应用程序添加功能的功能。

>[!NOTE]
>
>在下面的功能矩阵表中，√表示当前版本支持该功能。

### 核心播放功能 {#core-playback-features}

| **功能** | **内容类型** | **HLS** | **短划线** |
|---|---|---|---|
| 常规播放（播放、暂停、搜寻） | VOD +实时 | √ | √（仅限VOD） |
| FER — 常规播放（播放、暂停、搜寻） | FER VOD | √ | 不支持 |
| MP3 | VOD | 不支持 | 不支持 |
| MP4内容播放 | VOD | √ | √ |
| 自适应比特率切换逻辑 | VOD +实时 | √ | 不支持 |
| 纯音频播放 | VOD +实时 | √ | 不支持 |
| 隐藏字幕 — 608/708 | VOD +实时 | √ | √（仅限VOD） |
| 隐藏式字幕 — WebVTT | VOD +实时 | √ | √（仅限VOD） |
| 清单故障转移 | VOD +实时 | √ | √（仅限VOD） |
| 高级故障切换 | VOD +实时 | √ | √（仅限VOD） |
| QoS和播放器通知 | VOD +实时 | √ | √（仅限VOD） |
| 支持Cookie标头 | VOD +实时 | √ | √（仅限VOD） |
| 支持自定义标头 | VOD +实时 | 不支持 | 不支持 |
| 设置缓冲区控制参数 | VOD +实时 | √ | √（仅限VOD） |
| 设置自适应比特率控制 | VOD +实时 | √ | √（仅限VOD） |
| 自定义清单标记(HLS)/事件流(DASH) | VOD +实时 | √ | √（仅限VOD） |
| 晚到的音频 | VOD +实时 | √ | √（仅限VOD） |
| 302重定向 | VOD +实时 | √ | √（仅限VOD） |

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
   <td>带有偏移的播放</td> 
   <td>实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>纯音频播放</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>特技游戏 </td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>Smooth Trick Play（使用ABR）</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>ID3解析(HLS)/定时元数据(DASH)</td> 
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
   <td>即时打开</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>间断标记支持(HLS) </li> 
     <li>多周期（短划线）</li> 
    </ul> </td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>302重定向粘性</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>√（仅限VOD）</td> 
  </tr>
  <tr>
   <td>缩略图清理(Iframe和JPEG)</td> 
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
| 常规播放，启用广告 | VOD +实时 | √ | √（仅限VOD前置式广告） |
| 启用了广告的FER内容 | VOD | √ | 不支持 |
| 默认广告行为 | VOD +实时 | √ | √（仅限VOD前置式广告） |
| VAST 2.0/3.0 | VOD +实时 | √ | √（仅限VOD前置式广告） |
| VMAP 1.0 | VOD +实时 | √ | √（仅限VOD前置式广告） |
| MP4广告 | VOD +实时 | √（来自CRS） | √（来自CRS，仅限预装） |

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
   <td>启用广告的Trick Play</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>仅广告 </td> 
   <td>VOD</td> 
   <td>不支持</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>定位参数</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>√（仅限VOD前置式广告）</td> 
  </tr>
  <tr>
   <td>自定义参数</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>√（仅限VOD前置式广告）</td> 
  </tr>
  <tr>
   <td>自定义广告行为</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>√（仅限VOD前置式广告）</td> 
  </tr>
  <tr>
   <td>自定义广告标记</td> 
   <td>实时</td> 
   <td>√ </td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>自定义广告解析程序</td> 
   <td>VOD +实时</td> 
   <td>√ </td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>Freewheel自定义广告解析程序</td> 
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
     <li>中断标记支持 — SSAI (HLS) </li> 
     <li>多周期（短划线）</li> 
    </ul> </td> 
   <td>VOD +实时</td> 
   <td>√ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>伴随广告、横幅广告和可点击广告</td> 
   <td>VOD +实时</td> 
   <td>√ </td> 
   <td>√（仅限VOD前置式广告）</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD +实时</td> 
   <td>√ (JS) </td> 
   <td>√（仅限VOD前置式广告）</td> 
  </tr>
  <tr>
   <td>早期广告退出</td> 
   <td>实时</td> 
   <td>√ </td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>基于规则的创意VOD +实时优先处理</td> 
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
| AES加密 | VOD +实时 | √ | √（仅限VOD） |
| 示例AES加密 | VOD +实时 | √ |  |
| 标记化的流 | VOD +实时 | √ |  |
| DRM | VOD +实时 | 仅限Primetime DRM（未来：Widevine） | 仅限Widevine |
| 外部播放(RBOP) | VOD +实时 | 仅限Primetime DRM | 不支持 |
| 许可证轮换 | VOD +实时 | 仅限Primetime DRM | 不支持 |
| 密钥轮替 | VOD +实时 | 仅限Primetime DRM | 不支持 |

### 集成功能 {#integration-features}

| **功能** | **内容类型** | **HLS** | **短划线** |
|---|---|---|---|
| Adobe Analytics VHL集成 | VOD +实时 | √ | √ |
| 计费 | VOD +实时 | √ | 不支持 |

## 不支持的功能 {#features-not-supported}

此版本的TVSDK不支持：

* 广告被封锁。
* 戏法游戏中的慢动作。
* 通过MP4内容进行搜寻和点播。
* 包含MP4主内容的广告插入。
* 在广告播放时搜寻。
* 使用纯音频媒体播放广告。

## 已知问题和限制 {#known-issues-and-limitations}

此版本的TVSDK存在以下问题：

* 特定于设备(Samsung Galaxy Tab 4)的VOD DRM LBA崩溃（包含审核和点击广告）
* 不会为特定内容播放后置广告。
* 将隐藏字幕设置为CJK语言不起作用。
* 视频可以从VOD和实时视频之间的特技模式中自动退出。
* VHL — 从偏移开始内容时，会发送错误的心率调用。
* 播放VPAID广告时，事件的VHL心率调用:type:播放广告缺失。
* 即使选择了adBreakPolicy SKIP，也会播放前置广告。
* 进入完整状态后，播放器会返回至播放状态，并为后置广告使用SKIP adBreakPolicy。

如果没有视频，则没有视区尺寸；如果没有视区尺寸，则无法显示任何用于字幕的图形。

## 有用资源 {#helpful-resources}

* 请参阅完整的帮助文档，网址为 [Adobe Primetime学习与支持](https://experienceleague.adobe.com/docs/primetime.html) 页面。
