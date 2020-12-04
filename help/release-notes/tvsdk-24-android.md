---
title: 适用于Android的TVSDK 2.4.1发行说明
seo-title: 适用于Android的TVSDK 2.4.1发行说明
description: TVSDK 2.4.1 for Android发行说明描述了TVSDK Android 2.4.1中新增和支持的功能以及已知问题和限制。
seo-description: TVSDK 2.4.1 for Android发行说明描述了TVSDK Android 2.4.1中新增和支持的功能以及已知问题和限制。
uuid: 929fc577-e851-4e03-9201-13280cc6137a
topic-tags: release-notes
products: SG_PRIMETIME
discoiquuid: a6dbcc4a-9e14-4452-9004-b39ed13fad6f
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6
workflow-type: tm+mt
source-wordcount: '1988'
ht-degree: 0%

---


# TVSDK 2.4.1 for Android发行说明{#tvsdk-for-android-release-notes}

TVSDK 2.4.1 for Android发行说明描述了TVSDK Android 2.4.1中新增和支持的功能以及已知问题和限制。

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe正在发布适用于Android的TVSDK 2.4.1。

要使用此版本的TVSDK，请确保您的系统满足[系统要求](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6)中所述的要求。

您可以在此处找到文档：

·适用于Android的在线帮助系统TVSDK 2.4帮助

· [适用于Android Java API的Javadocs TVSDK 2.4](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Javadocs是终极权威，因为它们是直接从TVSDK源代码自动生成的。

· [C++ API文档TVSDK 2.4 for Android C++ API](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

每个Java类都有相应的C++类，而C++文档包含的解释性材料比Javadoc更多，因此请查阅C++文档以进一步了解Java API。

·迁移指南（[TVSDK 2.4 for Android迁移指南](../migration-guides/tvsdk-14-25-android.md)）

本指南解释将基于TVSDK 1.4的应用程序迁移到基于TVSDK 2.4的应用程序时需要修改的内容。

## 新增功能{#new-features}

适用于Android的TVSDK 2.4.1与先前版本相比提供了许多性能改进。 它提供高质量的查看体验。

此版本包含版本2.4和2.4.1的所有功能，不弃用任何功能。

以下是版本2.4.1中的主要新增功能：

* HLS版本4功能

   * **视频播放** （播放、暂停、搜索）与实时、线性和VOD流的播放器控制。
   * **隐藏字幕。** TVSDK可显示608/708隐藏式字幕，其中包含字体、字体大小、颜色和背景选项。它还支持带有滚动字幕的视频，并可在语言轨道之间切换（如果可用）。
   * **技巧播** 放模式支持使用I帧的HLS流的快进和后退。所有视频播放控件对内容起作用。 慢动作（前进）适用于速率介于0和1之间的外部视频回放模式。
   * **自适应比特率(** ABR)允许播放器根据网络和其他条件动态选择要播放的同一内容流的多个版本中的哪一个。您可以动态地或在清单文件中设置参数，以在激进、中和和保守的选择策略中进行选择。
   * **字** 节范围允许单个TS文件包含多个TS段。
   * **替代音** 频再现使播放器能够在可用音轨之间切换。
   * **ID3支持。** TVSDK可以播放包含ID3音频元数据（如艺术家姓名、标题和专辑）的HLS音频和视频流。
   * **故障转移。 **尽管主机服务器、播放列表文件和区段出现故障，TVSDK仍使用策略继续不间断播放。
   * **多渠道音频传输(DD+)。** TVSDK可以将Dolby Digital Plus音频(E-AC3)数据传递给支持硬件。

* 内容保护功能

   * **HLS的DRM。** 所有视频播放API均可处理受Adobe访问保护的加密视频内容。支持以下DRM功能：

      * 许可证轮换
      * 键旋转
      * 许可证缓存
      * 策略时间
      * IV旋转

* **AES 128播放。** TVSDK可播放密钥大小为128位的高级加密标准(AES)HLS内容。
* **受保护的HLS(PHLS)** 提供有限的预建DRM策略集(即Adobe访问提供的子集)，以在HLS上为实时流和VOD流启用轻量DRM。

* 广告／替代内容和货币化功能

   * **跟踪服务器端插入广告。** TVSDK可以跟踪Adobe云广告插入服务插入的广告。它支持VAST2、VAST3和VMAP格式的线性广告，用于VOD和实时／线性流。
   * **自定义HLS标记。** 当流中显示自 `MediaPlayerConfig` 定义HLS标记时，TVSDK使用其类启用通知播放器应用程序。
   * **客户端广告插入。** Auditude广告插入库与Adobe Auditude服务器共同解决广告问题，以便在前置、中置或后置位置动态插入实时、线性和VOD内容。
   * **自定义广告解析器。** 通过 `ContentResolver, OpportunityGenerator,` 和 `MediaPlayerClientFactory` 接口，您可以实现自定义广告／替代内容解析程序并注册自定义机会检测器以与TVSDK一起使用。`TestAdResolver`和`AuditudeResolver`类提供实现内容解析器的C++示例。 您可以在`samples/jspsdk/testapp/psdk.js`找到Javascript示例。
   * **一致的广告行为。** 使用该 `AdPolicySelector` 界面可在所有播放器上实现一致的行为，例如在内容中出现广告时进行搜索和技巧播放。如果您不实施自己的软件，TVSDK将使用`DefaultAdPolicySelector`。
   * **删除／替换C3广告。** 使用适当的TVSDK API删除自定义内容范围并动态插入新广告，无需进行其他准备工作。在广播实时／线性内容后立即按需提供而无需清理时，此功能很方便。

以下是2.4版的主要新增功能：

* **VOD和实时的即** 时启用即时时，TVSDK在播放开始之前初始化和缓冲媒体。由于您可以在后台同时启动多个`MediaPlayerItemLoader`实例，因此可以缓冲多个流。 当用户更改渠道，且流已正确缓冲时，将立即在新渠道开始上播放。 TVSDK 2.4还支持实时流的即时启动。 实时窗口移动时，将重新缓冲实时流。

* **性能改进**新的TVSDK 2.4体系架构带来各种性能改进：

   * **子分段** - TVSDK进一步减小每个片段的大小以尽快开始回放。
   * **并行广告下载** - TVSDK在点击广告中断前预取与内容播放平行的广告，从而实现广告和内容的无缝播放。
   * **延迟广告分辨率** -借助此功能，我们无需等待非预卷广告的分辨率，即可开始播放，从而缩短启动时间。在解决所有广告之前，仍不允许搜索和技巧播放等API。

* **MP4内容播放**

此版本的TVSDK支持将MP4作为主内容回放。

* **永久网络连接**

TVSDK维护一组可重用的网络连接，因此它不会产生为每个网络请求创建和破坏网络连接的开销。

* **基于分辨率的输出保护**

此功能将播放限制与特定分辨率联系起来，提供更精细的DRM控件。

* **自适应比特率(ABR)的特技播放**

此功能允许TVSDK在特技播放模式下在iFrame流之间切换。 您可以使用非iFrame用户档案以较低的速度进行特技播放。

* **更流畅的技巧播放**

这些改进增强了用户体验：

·在特技播放期间，根据带宽和缓冲区用户档案选择自适应比特率和帧速率

·使用主流（而非IDR流）可以快速回放30 fps。

* **改进的ABR逻辑**

新的ABR逻辑基于缓冲区长度、缓冲区长度变化率和测量带宽。 这确保ABR在带宽波动时选择正确的比特率，还通过监视缓冲区长度变化的速率来优化比特率切换的实际发生次数。

* **计费**

TVSDK会自动收集指标，遵守客户销售合同，生成计费所需的定期使用情况报告。 在每个流开始事件中，TVSDK使用Adobe Analytics数据插入API将付费指标（如内容类型、广告插入启用标记和根据收费流的持续时间启用drm的标记）发送到Adobe Analytics黄金时段拥有的报表包。 这不会干扰或包含在客户自己的Adobe Analytics报告套件或服务器调用中。 此计费使用情况报告会按要求定期发送给客户。 这是付费功能的第一阶段，仅支持使用付费。 可以使用文档中描述的API根据销售合同进行配置。

## 支持的功能{#supported-features}

适用于Android 2.4的TVSDK支持许多功能，您可以通过这些功能向视频应用程序添加功能。

>[!NOTE]
>
>在下面的功能矩阵表中，√表示当前版本中支持该功能。

### 核心播放功能{#core-playback-features}

| **功能** | **内容类型** | **HLS** | **虚线** |
|---|---|---|---|
| 常规播放（播放、暂停、搜索） | VOD + Live | √ | √（仅VOD） |
| FER —— 常规播放（播放、暂停、搜索） | FER VOD | √ | 不支持 |
| MP3 | VOD | 不支持 | 不支持 |
| MP4内容播放 | VOD | √ | √ |
| 自适应比特率切换逻辑 | VOD + Live | √ | 不支持 |
| 仅播放音频 | VOD + Live | √ | 不支持 |
| 隐藏式字幕- 608/708 | VOD + Live | √ | √（仅VOD） |
| 隐藏字幕- WebVTT | VOD + Live | √ | √（仅VOD） |
| 清单故障转移 | VOD + Live | √ | √（仅VOD） |
| 高级故障转移 | VOD + Live | √ | √（仅VOD） |
| QoS和播放器通知 | VOD + Live | √ | √（仅VOD） |
| 支持Cookie头 | VOD + Live | √ | √（仅VOD） |
| 支持自定义标题 | VOD + Live | 不支持 | 不支持 |
| 设置缓冲区控制参数 | VOD + Live | √ | √（仅VOD） |
| 设置自适应比特率控件 | VOD + Live | √ | √（仅VOD） |
| 自定义清单标记(HLS)/事件流(DASH) | VOD + Live | √ | √（仅VOD） |
| 延迟绑定音频 | VOD + Live | √ | √（仅VOD） |
| 302重定向 | VOD + Live | √ | √（仅VOD） |

### 高级播放功能{#advanced-playback-features}

<table> 
 <tbody>
  <tr>
   <td><strong>功能</strong></td> 
   <td><strong>内容类型</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>虚线</strong></td> 
  </tr>
  <tr>
   <td>带偏移的播放</td> 
   <td>实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>仅播放音频</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>技巧游戏 </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>平滑技巧播放（使用ABR）</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>ID3解析(HLS)/定时元数据(DASH)</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>封锁 </td> 
   <td>VOD + Live</td> 
   <td>不支持</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>即时启动</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>不连续性标记支持(HLS) </li> 
     <li>多句点(DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>302重定向严谨</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√（仅VOD）</td> 
  </tr>
  <tr>
   <td>缩览图擦洗（Iframe和JPEG）</td> 
   <td>VOD + Live</td> 
   <td>不支持</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>流完整性 </td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
 </tbody>
</table>

### 核心Ad Insertion功能(CSAI){#core-ad-insertion-features-csai}

| **功能** | **内容类型** | **HLS** | **虚线** |
|---|---|---|---|
| 常规播放，支持广告 | VOD + Live | √ | √（仅VOD预滚动） |
| 支持广告的FER内容 | VOD | √ | 不支持 |
| 默认广告行为 | VOD + Live | √ | √（仅VOD预滚动） |
| VAST 2.0/3.0 | VOD + Live | √ | √（仅VOD预滚动） |
| VMAP 1.0 | VOD + Live | √ | √（仅VOD预滚动） |
| MP4广告 | VOD + Live | √（来自CRS） | √（仅来自CRS，预滚动） |

### 高级Ad Insertion功能(CSAI){#advanced-ad-insertion-features-csai}

<table> 
 <tbody>
  <tr>
   <td><strong>功能</strong></td> 
   <td><strong>内容类型</strong></td> 
   <td><strong>HLS</strong></td> 
   <td><strong>虚线</strong></td> 
  </tr>
  <tr>
   <td>支持广告的技巧播放</td> 
   <td>VOD + Live</td> 
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
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√（仅VOD预滚动）</td> 
  </tr>
  <tr>
   <td>自定义参数</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√（仅VOD预滚动）</td> 
  </tr>
  <tr>
   <td>自定义广告行为</td> 
   <td>VOD + Live</td> 
   <td>√</td> 
   <td>√（仅VOD预滚动）</td> 
  </tr>
  <tr>
   <td>自定义广告标记</td> 
   <td>实时</td> 
   <td>√ </td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>自定义广告解析器</td> 
   <td>VOD + Live</td> 
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
   <td>VOD + Live</td> 
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
     <li>不连续标记支持- SSAI(HLS) </li> 
     <li>多句点(DASH)</li> 
    </ul> </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>配套广告、横幅广告和可点击广告</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>√（仅VOD预滚动）</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD + Live</td> 
   <td>√(JS) </td> 
   <td>√（仅VOD预滚动）</td> 
  </tr>
  <tr>
   <td>早期广告退出</td> 
   <td>实时</td> 
   <td>√ </td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>基于规则的创意VOD +实时优先级排序</td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>CRS规则 </td> 
   <td>VOD + Live</td> 
   <td>√ </td> 
   <td>不支持</td> 
  </tr>
 </tbody>
</table>

## 内容保护功能{#content-protection-features}

| **功能** | **内容类型** | **HLS** | **虚线** |
|---|---|---|---|
| AES加密 | VOD + Live | √ | √（仅VOD） |
| 示例AES加密 | VOD + Live | √ |  |
| 标记流 | VOD + Live | √ |  |
| DRM | VOD + Live | 仅限Primetime DRM(未来：Widevine) | 仅限Widevine |
| 外部播放(RBOP) | VOD + Live | 仅限Primetime DRM | 不支持 |
| 许可证轮换 | VOD + Live | 仅限Primetime DRM | 不支持 |
| 键旋转 | VOD + Live | 仅限Primetime DRM | 不支持 |

### 集成功能{#integration-features}

| **功能** | **内容类型** | **HLS** | **虚线** |
|---|---|---|---|
| Adobe AnalyticsVHL集成 | VOD + Live | √ | √ |
| 计费 | VOD + Live | √ | 不支持 |

## 不支持的功能{#features-not-supported}

此版本的TVSDK不支持：

* 广告封锁。
* 在戏法游戏中慢动作。
* 寻找和滴答不漏的MP4内容。
* 使用MP4主内容插入广告。
* 在广告播放时进行搜索。
* 使用纯音频媒体播放广告。

## 已知问题和限制{#known-issues-and-limitations}

此版本的TVSDK有以下问题：

* 特定于设备(Samsung Galaxy Tab 4)，使用auditude使VOD DRM LBA崩溃并单击广告
* 不会为特定内容播放滚动后广告。
* 将关闭题注设置为CJK语言不起作用。
* 视频可以在VOD和实时视频之间自动退出技巧模式。
* VHL —— 当我们从偏移开始内容时，会发送错误的心跳调用。
* 播放VPAID广告时，VHL心跳调用事件:type:play广告缺失。
* 即使选择了adBreakPolicy SKIP，也会播放前置广告。
* 进入“完整”状态播放器后，使用SKIP adBreakPolicy返回到“播放”状态进行后滚广告。

没有视频，就没有视口尺寸，没有视口尺寸，就无法显示任何字幕图形。

## 帮助资源{#helpful-resources}

* 请参阅[Adobe Primetime学习和支持](https://helpx.adobe.com/support/primetime.html)页面上的完整帮助文档。