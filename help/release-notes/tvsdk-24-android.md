---
title: TVSDK 2.4.1 for Android发行说明
description: TVSDK 2.4.1 for Android发行说明描述了TVSDK Android 2.4.1中新增和支持的功能以及已知问题和限制。
topic-tags: release-notes
products: SG_PRIMETIME
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '1963'
ht-degree: 0%

---


# TVSDK 2.4.1 for Android发行说明{#tvsdk-for-android-release-notes}

TVSDK 2.4.1 for Android发行说明描述了TVSDK Android 2.4.1中新增和支持的功能以及已知问题和限制。

## TVSDK Android 2.4.1 {#tvsdk-android}

Adobe将发布适用于Android的TVSDK 2.4.1。

要使用此版本的TVSDK，请确保您的系统符合[系统要求](https://helpx.adobe.com/content/dam/help/en/primetime/programming-guides/psdk_android_2.5.pdf#page=6)中描述的要求。

您可以在此处查找文档：

·用于Android帮助的在线帮助系统TVSDK 2.4

· [Javadocs TVSDK 2.4 for Android Java API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.4/index.html)

Javadocs是终极权威，因为它们是直接从TVSDK源代码自动生成的。

· [C++ API文档TVSDK 2.4 for Android C++ API](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.4/namespaces.html)

每个Java类都有相应的C++类，且C++文档包含比Javadoc更多解释性材料，因此请查阅C++文档以更深入地了解Java API。

·迁移指南（[TVSDK 2.4 for Android迁移指南](../migration-guides/tvsdk-14-25-android.md)）

本指南说明了将基于TVSDK 1.4的应用程序迁移到基于TVSDK 2.4的应用程序时需要修改的内容。

## 新增功能{#new-features}

适用于Android的TVSDK 2.4.1比早期版本提供了许多性能改进。 它提供了高质量的观看体验。

此版本包含版本2.4和2.4.1的所有功能，不弃用任何功能。

以下是版本2.4.1中的主要新增功能：

* HLS版本4功能

   * **利用实时** 、线性和VOD流的播放器控件进行视频播放（播放、暂停、搜索）。
   * **隐藏式字幕。** TVSDK可显示608/708隐藏式字幕，其中包含多种字体、字体大小、颜色和背景。它还可支持带有滚动字幕的视频，并可在语言轨道之间切换（如果可用）。
   * **特技播** 放模式支持使用I帧的HLS流的快进和后退。所有视频播放控件都对内容起作用。 慢动作（前进）适用于速率介于0和1之间的外部视频播放模式。
   * **自适应比特率(ABR)** 允许播放器根据网络和其他条件动态选择要播放的同一内容流的多个版本中的哪一个。您可以动态设置参数或在清单文件中设置参数，以在积极、中和和保守的选择策略中进行选择。
   * **字** 节范围允许单个TS文件包含多个TS段。
   * **替代音** 频再现使播放器能够在可用音轨之间切换。
   * **ID3支持。** TVSDK可以播放包含ID3音频元数据（如艺术家姓名、标题和专辑）的HLS音频和视频流。
   * **故障转移。 **尽管主机服务器、播放列表文件和区段出现故障，TVSDK仍使用策略继续不间断播放。
   * **多渠道音频传递(DD+)。** TVSDK可以将杜比数字+音频(E-AC3)数据传递给支持硬件。

* 内容保护功能

   * **HLS的DRM。** 所有视频播放API都可与受Adobe访问保护的加密视频内容配合使用。支持以下DRM功能：

      * 许可证轮换
      * 键旋转
      * 许可证缓存
      * 策略时间
      * 四轮

* **AES 128播放。** TVSDK可以播放密钥大小为128位的高级加密标准(AES)HLS内容。
* **受保护的HLS(PHLS)** 提供有限的预建DRM策略集，即Adobe访问提供的子集，以在HLS上为实时流和VOD流启用轻量DRM。

* 广告/备选内容和货币化功能

   * **跟踪服务器端插入的广告。** TVSDK可以跟踪由Adobe Cloud广告插入服务插入的广告。它支持VOD和实时/线性流的VAST2、VAST3和VMAP格式中的线性广告。
   * **自定义HLS标记。** 当流中显示自 `MediaPlayerConfig` 定义HLS标记时，TVSDK使用其类启用通知播放器应用程序。
   * **客户端广告插入。** Auditude广告插入库与Adobe Auditude服务器一起使用，以解析广告，以便在前置、中置或后置位置动态插入实时、线性和VOD内容。
   * **自定义广告解析器。** 通过 `ContentResolver, OpportunityGenerator,` 和 `MediaPlayerClientFactory` 接口，您可以实现自定义广告/替代内容解析器并注册自定义机会检测器以与TVSDK一起使用。`TestAdResolver`和`AuditudeResolver`类提供了实现内容解析器的C++示例。 您可以在`samples/jspsdk/testapp/psdk.js`找到Javascript示例。
   * **一致的广告行为。** 使用该 `AdPolicySelector` 界面可在所有播放器中实现一致的行为，以执行诸如在内容中显示广告时进行搜索和技巧播放等操作。如果您不实施自己的，TVSDK将使用`DefaultAdPolicySelector`。
   * **删除/替换C3广告。** 使用适当的TVSDK API删除自定义内容范围并动态插入新广告，无需进行其他准备工作。这在广播实时/线性内容后立即按需提供而无需清理时很方便。

以下是2.4版的主要新增功能：

* **VOD和实时的即** 时启用即时启用时，TVSDK在播放开始之前初始化媒体并缓冲媒体。由于您可以在后台同时启动多个`MediaPlayerItemLoader`实例，因此可以缓冲多个流。 当用户更改渠道，且流已正确缓冲时，立即在新的渠道开始上播放。 TVSDK 2.4还支持实时流的即时启动。 在实时窗口移动时重新缓冲实时流。

* **性能改进**新的TVSDK 2.4架构带来了各种性能改进：

   * **子分段** - TVSDK进一步缩小每个片段的大小以尽快播放开始。
   * **并行广告下载** - TVSDK在点击广告中断前预取与内容播放平行的广告，从而实现广告和内容的无缝播放。
   * **延迟广告**  — 利用此功能，我们在开始播放之前无需等待非预卷广告的分辨率，从而缩短了启动时间。搜索和技巧播放等API在所有广告都解决之前仍不允许。

* **MP4内容播放**

此版本的TVSDK支持将MP4作为主要内容回放。

* **永久网络连接**

TVSDK维护一组可重用的网络连接，因此它不会产生为每个网络请求创建和破坏网络连接的开销。

* **基于分辨率的输出保护**

此功能将播放限制与特定分辨率关联起来，提供更精细的DRM控制。

* **使用自适应比特率(ABR)进行特技播放**

此功能允许TVSDK在特技播放模式下在iFrame流之间切换。 您可以使用非iFrame用户档案以较低的速度进行特技播放。

* **更流畅的特技播放**

这些改进增强了用户体验：

·在特技播放期间根据带宽和缓冲区用户档案选择自适应比特率和帧速率

·使用主流（而非IDR流）可以快速回放30 fps。

* **改进的ABR逻辑**

新的ABR逻辑基于缓冲区长度、缓冲区长度变化率和测量带宽。 这确保ABR在带宽波动时选择正确的比特率，还通过监视缓冲区长度变化的速率来优化比特率切换实际发生的次数。

* **帐单**

TVSDK自动收集量度，遵守客户销售合同，以生成计费所需的定期使用情况报告。 在每个流开始事件中，TVSDK使用Adobe Analytics数据插入API向Adobe Analytics Primetime拥有的报表包发送付费量度，如内容类型、广告插入启用标记和drm启用标记（基于可计费流的持续时间）。 这不会干扰或包含在客户自己的Adobe Analytics报表包或服务器调用中。 根据要求，此账单使用情况报告会定期发送给客户。 这是付费功能的第一阶段，仅支持使用付费。 可以使用文档中描述的API根据销售合同进行配置。

## 支持的功能{#supported-features}

适用于Android 2.4的TVSDK支持许多功能，您可以通过这些功能为视频应用程序添加功能。

>[!NOTE]
>
>在以下功能矩阵表中，√表示当前版本支持该功能。

### 核心播放功能{#core-playback-features}

| **功能** | **内容类型** | **HLS** | **虚线** |
|---|---|---|---|
| 常规播放（播放、暂停、搜索） | VOD +实时 | √ | √（仅VOD） |
| FER — 常规播放（播放、暂停、搜索） | FER VOD | √ | 不支持 |
| MP3 | VOD | 不支持 | 不支持 |
| MP4内容播放 | VOD | √ | √ |
| 自适应比特率切换逻辑 | VOD +实时 | √ | 不支持 |
| 仅音频回放 | VOD +实时 | √ | 不支持 |
| 隐藏式字幕 — 608/708 | VOD +实时 | √ | √（仅VOD） |
| 隐藏式字幕 — WebVTT | VOD +实时 | √ | √（仅VOD） |
| 清单故障转移 | VOD +实时 | √ | √（仅VOD） |
| 高级故障转移 | VOD +实时 | √ | √（仅VOD） |
| QoS和播放器通知 | VOD +实时 | √ | √（仅VOD） |
| 支持Cookie头 | VOD +实时 | √ | √（仅VOD） |
| 支持自定义标题 | VOD +实时 | 不支持 | 不支持 |
| 设置缓冲区控制参数 | VOD +实时 | √ | √（仅VOD） |
| 设置自适应比特率控件 | VOD +实时 | √ | √（仅VOD） |
| 自定义清单标记(HLS)/事件流(DASH) | VOD +实时 | √ | √（仅VOD） |
| 延期音频 | VOD +实时 | √ | √（仅VOD） |
| 302重定向 | VOD +实时 | √ | √（仅VOD） |

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
   <td>带偏移的回放</td> 
   <td>实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>仅音频回放</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>Trick Play </td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>流畅的技巧播放（使用ABR）</td> 
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
   <td>即时启动</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>
    <ul> 
     <li>间断标记支持(HLS) </li> 
     <li>多句点(DASH)</li> 
    </ul> </td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>302重定向</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>√（仅VOD）</td> 
  </tr>
  <tr>
   <td>缩览图划动（Iframe和JPEG）</td> 
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

### 核心Ad Insertion功能(CSAI){#core-ad-insertion-features-csai}

| **功能** | **内容类型** | **HLS** | **虚线** |
|---|---|---|---|
| 常规播放，支持广告 | VOD +实时 | √ | √（仅限VOD预滚动） |
| 支持广告的FER内容 | VOD | √ | 不支持 |
| 默认广告行为 | VOD +实时 | √ | √（仅限VOD预滚动） |
| VAST 2.0/3.0 | VOD +实时 | √ | √（仅限VOD预滚动） |
| VMAP 1.0 | VOD +实时 | √ | √（仅限VOD预滚动） |
| MP4广告 | VOD +实时 | √（来自CRS） | √（来自CRS，仅限预滚动） |

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
   <td>支持广告的特技播放</td> 
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
   <td>√（仅限VOD预滚动）</td> 
  </tr>
  <tr>
   <td>自定义参数</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>√（仅限VOD预滚动）</td> 
  </tr>
  <tr>
   <td>自定义广告行为</td> 
   <td>VOD +实时</td> 
   <td>√</td> 
   <td>√（仅限VOD预滚动）</td> 
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
     <li>间断标记支持 — SSAI(HLS) </li> 
     <li>多句点(DASH)</li> 
    </ul> </td> 
   <td>VOD +实时</td> 
   <td>√ </td> 
   <td> </td> 
  </tr>
  <tr>
   <td>配套广告、横幅广告和可点击广告</td> 
   <td>VOD +实时</td> 
   <td>√ </td> 
   <td>√（仅限VOD预滚动）</td> 
  </tr>
  <tr>
   <td>VPAID 2.0</td> 
   <td>VOD +实时</td> 
   <td>√(JS) </td> 
   <td>√（仅限VOD预滚动）</td> 
  </tr>
  <tr>
   <td>早期广告退出</td> 
   <td>实时</td> 
   <td>√ </td> 
   <td>不支持</td> 
  </tr>
  <tr>
   <td>基于规则的创意VOD +实时优先排序</td> 
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

## 内容保护功能{#content-protection-features}

| **功能** | **内容类型** | **HLS** | **虚线** |
|---|---|---|---|
| AES加密 | VOD +实时 | √ | √（仅VOD） |
| 示例AES加密 | VOD +实时 | √ |  |
| 标记流 | VOD +实时 | √ |  |
| DRM | VOD +实时 | 仅限Primetime DRM(未来：Widevine) | 仅限Widevine |
| 外部播放(RBOP) | VOD +实时 | 仅限Primetime DRM | 不支持 |
| 许可证轮换 | VOD +实时 | 仅限Primetime DRM | 不支持 |
| 键旋转 | VOD +实时 | 仅限Primetime DRM | 不支持 |

### 集成功能{#integration-features}

| **功能** | **内容类型** | **HLS** | **虚线** |
|---|---|---|---|
| Adobe Analytics VHL集成 | VOD +实时 | √ | √ |
| 帐单 | VOD +实时 | √ | 不支持 |

## 不支持的功能{#features-not-supported}

此版本的TVSDK不支持：

* 广告封锁。
* 玩特技的慢动作。
* 寻找和细致地处理MP4内容。
* 包含MP4主内容的广告插入。
* 在广告播放时进行搜索。
* 使用纯音频媒体播放广告。

## 已知问题和限制{#known-issues-and-limitations}

此版本的TVSDK有以下问题：

* 特定于设备(Samsung Galaxy Tab 4)，使用auditude并单击广告使VOD DRM LBA崩溃
* 不会为特定内容播放滚动后广告。
* 将关闭题注设置为CJK语言不起作用。
* 视频可以在VOD和实时视频点播之间自动退出特技模式。
* VHL — 当我们从偏移开始内容时，会发送错误的心率调用。
* 播放VPAID广告时，缺少事件:type:play广告的VHL心率调用。
* 即使选择了adBreakPolicy SKIP，也会播放前置广告。
* 进入“完整”状态播放器后，使用SKIP adBreakPolicy（针对后滚广告）返回“播放”状态。

没有视频，就没有视口尺寸，没有视口尺寸，就无法显示字幕的任何图形。

## 有用资源{#helpful-resources}

* 请参阅[Adobe Primetime学习和支持](https://helpx.adobe.com/support/primetime.html)页面上的完整帮助文档。