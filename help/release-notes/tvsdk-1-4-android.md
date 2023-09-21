---
title: 适用于Android的TVSDK 1.4发行说明
description: 适用于Android的TVSDK 1.4发行说明介绍了TVSDK Android 1.4中的新增或更改内容、已解决的问题和已知问题以及设备问题。
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '7802'
ht-degree: 0%

---

# 适用于Android的TVSDK 1.4发行说明 {#tvsdk-for-android-release-notes}

适用于Android的TVSDK 1.4发行说明介绍了TVSDK Android 1.4中的新增或更改内容、已解决的问题和已知问题以及设备问题。

## 新增功能 {#new-features}

**版本1.4.43**

**通过HTTPS安全加载广告**

Adobe Primetime提供了一个选项，用于请求通过HTTPS对primetime广告服务器和CRS的首次调用。

**MediaPlayer类中的alwaysUseAudioOutputLatency(boolean val)**

如果设置了此参数，请在音频时间戳计算中使用音频输出滞后。

它接受布尔参数val。 如果其值为 `True`，客户端在音频时间戳计算中使用音频输出滞后。

**版本1.4.42**

**部分广告时间插入：**
类似于电视的体验：在广告中间加入，而不触发部分观看广告的跟踪。
示例：用户在包含三个30秒广告的90秒广告时间的中间（40秒）加入。 此时是插播中第二个广告的10秒。
* 第二个广告将播放剩余的时长（20秒），随后是第三个广告。
* 对于播放的部分广告（第二个广告），不会触发广告跟踪器。 仅触发第三个广告的跟踪器。

**版本1.4.41**

无新功能。

**版本1.4.40**

无新功能。

>[!NOTE]
>
>如果您使用的版本低于1.4.39，则无需更改API。

**版本1.4.39**

* TVSDK已通过VHL 2.0.1和VHL 2.0.1与Nielsen一起认证。
* Android TVSDK已更新，可从新的Akamai主机发出CRS请求 `primetime-a.akamaihd.net`.
* 新的主机名配置在更大范围内通过HTTP和HTTPS (SSL)提供CRS资产交付。
* TVSDK支持Android Oreo版本。
* 将新函数添加到 `AdClientFactory` 支持注册多个机会检测器的类：

  ```
  public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
  ```

  这应该会返回PlacementOpportunityDetector数组。 现在，您可以注册多个机会检测器。 例如，对于提前广告退出功能，需要两个Opportunity检测器 — 一个用于广告插入，另一个用于提前退出广告。 只有在您已实施自己的AdvertisingFactory（并且未使用DefaultAdvertisingfactory）的情况下，才需要实施此新功能。 要获得现有行为 — 您需要创建一个Opportunity Detector ，如createOpportunityDetector()函数中所示，并将其放入数组中，然后返回：

  ```
  public class MyAdvertisingFactory extends AdvertisingFactory {  
  …  
  @Override  
  public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {  
  List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();  
  opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));  
  return opportunityDetectors;  
  } }
  ```

>[!NOTE]
>
>如果您使用的版本低于1.4.39，则无需更改API。

**版本1.4.36**

修复了Android上内容跳过的错误。

**版本1.4.35**

* **网络广告信息**

  TVSDK API现在提供有关第三方VAST响应的其他信息。 广告ID、广告系统和VAST广告扩展在NetworkAdInfo类中提供，可通过广告资产上的networkAdInfo属性访问该类。 此信息可用于与其他广告分析平台集成，例如 **Moat Analytics**.

**版本1.4.31**

**CRS广告的多CDN支持**
* 默认情况下，所有转码资源将托管在Akamai的Adobe拥有的CDN上。 在最新版本中，AdobeCreative Repackaging Service (CRS)允许将转码创意上传到客户指定的多个CDN。
* 新的API会添加到TVSDK中，以便能够在不使用默认url时指定最终CRS创意url。 请参阅文档以了解如何使用这些新API。

**版本1.4.18**
Primetime Android TVSDK现在支持VPAID 2.0 Javascript创意，以实现丰富的交互式流中广告体验。 有关VPAID 2.0的更多信息，请参阅 [VPAID广告支持](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md).

**版本1.4.17**

只有Amazon FireTV支持AC-3 5.1。

**版本1.4.11**

* **广告回退，在广告选择逻辑中进行Daisy链接(Zendesk #3103** 对于启用了回退规则的VAST广告（创意），TVSDK会将MIME类型无效的广告视为空广告，并尝试使用回退广告来替换该广告。 您可以在某些方面配置回退行为。

有关更多信息，请参阅 [VAST和VMAP广告的广告回退](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md).

* **视频心率库(VHL)已更新至版本1.5**
   * 能够将带有视频开始和/或视频/广告/章节开始的图像作为上下文数据发送元数据
   * 网络流量更少 — 心跳平均更少，大小更小

**版本1.4.7**

* **内部部署个性化支持**&#x200B;支持AdobeIndividualization Server的内部部署，以自定义客户端的个性化请求，从而转到其他端点。

**版本1.4.6**

* **示例AES加密(需要Flash Player版本17.0.0.134)**现在支持基于示例的AES加密。

**版本1.4.2**

* **视频心率库(VHL)已更新至版本1.4.0.1**

   * 添加了将其他SDK或播放器中的不同Analytics用例捆绑到Adobe Analytics Video Essentials的功能。
   * 通过删除trackAdBreakStart和trackAdBreakComplete方法，广告跟踪已得到优化。 从trackAdStart和trackAdComplete方法调用中推断出广告时间。
   * 跟踪广告时不再需要播放头属性。

* **Nielsen SDK集成** TVSDK现在支持将用户跟踪信息发送到Nielsen SDK，而无需任何自定义集成。

**版本1.4.0**

* **使用替代内容替换发出中断信号** 作为1.4 TVSDK更新的一部分，TVSDK现在还支持进入线性内容并从区域封锁返回。 TVSDK现在可以并行处理两个清单文件（主文件和备用文件），以监控中断信号，即使备用程序正在代替原始程序显示时也是如此。

* **删除/替换C3广告** 现在，无需额外的准备工作即可将新广告动态插入到从C3窗口出来的视频点播(VOD)资产中。 TVSDK现在提供了一个API，用于删除自定义内容范围并动态插入新广告。 在广播期间播放实时/线性内容，并且在不用适当时间“清理”资产的情况下立即提取内容作为按需内容时，这项强大的新功能也很有用。

* 接口PlaybackEventListener有一个名为onReplaceMediaPlayerItem的新方法，您可以使用该方法来侦听新事件， `ITEM_REPLACED`. 每当在MediaPlayer上替换MediaPlayeritem实例时，都会调度此事件。 实现此PlaybackEventListener的客户端应用程序必须实现或覆盖此新方法。
* AdClientFactory在类中添加了一个新函数，用于注册多个机会检测器：

  ```
  public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem item);
  
  For example for early ad exit feature, you need two Opportunity Detectors - one for ad insertion and another for  early  exit from  `ad`.
  
  To override this new function create a single Opportunity Detector, and put into an array and return:
  
  @Override
  
  public List&lt;PlacementOpportunityDetector&gt; createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {
  
  List&lt;PlacementOpportunityDetector&gt; opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector&gt;();
  
  opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));
  
  return opportunityDetectors;
  }
  
  }
  ```

## 适用于1.4的TVSDK更改 {#tvsdk-changes}

* 接口PlaybackEventListener有一个名为onReplaceMediaPlayerItem的新方法，您可以使用它来侦听新事件ITEM_REPLACED。 每当在MediaPlayer上替换MediaPlayeritem实例时，都会调度此事件。 实现此PlaybackEventListener的客户端应用程序必须实现或覆盖此新方法。

* AdClientFactory在类中添加了一个新函数，用于注册多个机会检测器：

```
public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem item);
```

例如，对于提前广告退出功能，您需要两个Opportunity检测器 — 一个用于广告插入，另一个用于提前退出广告。

要覆盖此新功能，请创建一个Opportunity Detector ，然后将其放入阵列并返回：

```
@Override

public List`<PlacementOpportunityDetector>` createOpportunityDetectors(MediaPlayerItem mediaPlayerItem) {

List`<PlacementOpportunityDetector>` opportunityDetectors = new ArrayList`<PlacementOpportunityDetector>`();

opportunityDetectors.add(createOpportunityDetector(mediaPlayerItem));

return opportunityDetectors;

}

}
```

## 1.4中的设备认证和支持 {#device-certification-and-support-in}

>[!NOTE]
>
>以下功能为 **非** TVSDK中支持：
>
>* 慢动作，在任何平台或版本上。
>* 玩现场戏法。

**版本1.4.43**

TVSDK 1.4.43已在具有Android 6.0.1/7.0和8.1 (Oreo)的Android设备上获得认证。

* **版本1.4.23：**

   * TVSDK 1.4.23已经过针对带有Android N的Android设备的认证。

* **版本1.4.18：**

   * Primetime已获得Amazon Fire TV认证。
   * VPAID 2.0仅在Android 4.0及更高版本的设备上受支持。

## 1.4中已解决的问题 {#resolved-issues-in}

>[!NOTE]
>
>强烈建议所有使用CRS的TVSDK客户升级到TVSDK 1.4.39或关于iOS和Android的最新版本。 此升级是现有应用程序实施的下拉式替代。 升级后，在代理工具（例如，Charles）中检查CRS创意URL请求，以验证路径中的版本是否反映了3.1版。例如：
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**版本1.4.43**

* 票证#27143 — 无法在FireTV设备上播放5.1音轨

   * TVSDK现在可以在FireTV设备上播放AC3音频。 播放始终采用立体声。

* 票证#33902 — 通过HTTPS的安全广告投放

   * Adobe Primetime提供了一个选项，用于请求通过https首次调用primetime广告服务器和CRS。

* 票证#34493 — 蓝牙音频延迟

   * 已添加 `alwaysUseAudioOutputLatency` 在MediaPlayer类中，如果设置，将导致在音频时间戳计算中使用音频输出滞后。

* 票证#34949 — 集成了新版本的视频心率库(VHL)。

**版本1.4.42 (1791)**

* Zendesk #33719：FireTV 4k自适应比特率缩放缓慢。 为FireTV 4K设备添加了对ABR的支持。
* Zendesk #33338： resetDRM清除应用程序的所有数据。  处理了非TVSDK线程中的异常导致TVSDK操作队列填充的额外情况。

**版本1.4.41 (1776)**

* Zendesk #33002 - Fire TV上TVSDK的伴随资产数据。 实施了一个新类AdBannerAsset，它将以列表形式返回伴随数据 &lt;adbannerasset> 和AdAsset：：id现在是一个字符串而不是长字符串。
* Zendesk #32821 - Android Primetime播放器在遇到WWE的演示时间戳(PTS)时冻结。 此问题已在此版本中修复。
* Zendesk #33572 - VideoAnalyticsProvider广告开始崩溃。 使用VideoHeartbeat.jar的VHL+Nielsen联合SDK版本的正确组合修复了此问题。
* Zendesk #33355 - Fire TV：按15秒后退。 没有来自TVSDK端的任何修复，客户正在其端和第三方验证此设置。

**版本1.4.40 (1764)**

* Zendesk #33068 — 新设备上的Amazon唇同步问题。 此版本中修复了唇同步问题。
* Zendesk #32215 - Android TVSDK 1.4.38安全问题 `[Hotlist]`. 已更新到最新的OpenSSL-1.1.0和curl-7.55.1。
* Zendesk #32920 — 广告时间为空白屏幕，无广告时间完成。 修复了VPAID容器可能进入挂起状态的问题，并处理了Facebook VPAID广告通常在单一\&amp;lt；AdParameters\&amp;gt；VAST节点中返回多个CDATA块的问题。

**版本1.4.39 (1744)**

* Zendesk #28976 — 许可请求需要超过一秒钟的时间。 在执行使用POST的DRM许可证请求调用时，Curl会添加额外的“Expect： 100-continue”标头。 删除了TVSDK中的“Expect：”标头。
* Zendesk #27707 - CSAI环境不接受CUE IN标记以提前返回或返回内容。 为多个机会生成器提供支持。

**版本1.4.38 (1722)**

* Zendesk #21590 — 最新源内部版本中的视频性能和跟踪

在TVSDK中集成并验证VHL 2.0，以通过降低API的复杂性来降低VideoHeartbeatsLibrary实施中的障碍。

* Zendesk #29688 — 支持Android O测试版客户。

新Android测试版支持TVSDK。

**版本1.4.36 (1713)**

* Zendesk #27392 - Android上的内容跳过

为了适应解密，Android TVSDK错误地将非iframe内容的字节范围扩大了16字节。 Iframe流的流量扩大是必需的，而非iframe流的流量则不是。

**版本1.4.34 (1702)**

* Zendesk #27638 - cURL INet对象中泄漏

在保留共享管理器和cURL连接中使用的DNS缓存时，Posix cURL INet对象泄漏。

通过从INet解构函数中删除Posix cURL INet对象，该问题得以解决。

**版本1.4.33 (1694)**

* **OpenSSL库**

OpenSSL库已更新为OpenSSL版本1.0.2j。

* Zendesk #21701 — 发送1401 CRS请求的原始创意URL，而不是规范化URL。
此问题可通过发送原始创意URL来解决。

* Zendesk #25023 — 长时间视频播放：视频冻结、屏幕闪烁通过设置CenturyLink机顶盒设备的最大视频格式尺寸，解决了此问题。

* Zendesk #27460 — 新的Akamai帐户无法处理POSTcdn请求。
更新了代码，以使 `cdn.auditude.com` 广告请求成为GET而非POST。

* Zendesk #28245 — 当应用程序从后台转到前台时，播放状态未正确通知。通过正确恢复播放状态，以便在应用程序返回前台时播放或暂停，解决了此问题。

**版本1.4.32 (1682)**

* Zendesk #25779 — 在WebView中启用JavaScript时，Android 4.2及更低版本的TVSDK中发现的安全漏洞将具有安全漏洞。 对于运行OS 4.2或更低版本的设备，已禁止通过TVSDK使用WebView。 这将禁止在这些设备上使用TVSDK中的VPAID广告。

* Zendesk #26890 — 屏幕状态（打开/关闭）中的问题处理参考 播放器当Adobe视频引擎(AVE)从“已挂起”状态恢复时，DefaultMediaPlayer不会更新其状态。 因此，即使AVE处于“正在播放”状态，DefaultMediaPlayer仍保持处于“已挂起”状态。 通过将DefaultMediaPlayer状态设置为PLAYING，解决了在从AVE收到PLAY状态时的问题，即使DefaultMediaPlayer的当前状态为SUSPENDED。

**版本1.4.31 (1675)**

* Zendesk #21974 — 由于null对象导致的异常
   * AdIndex很少在为null时增加。 这可能是由于为前置广告时间接收到的API调用不正确所致。 修复了数据类型以避免此类异常

* Zendesk #24714 — 关闭无关日志记录
   * 更新了TVSDK以关闭无关日志记录

* Zendesk #24488 - Fire TV中的AV同步问题
   * 通过改进对AV解码器线程的处理来修复。 具体地，每当修改输入或输出帧队列时，运行特定于帧内容类型的解码器线程。

* Zendesk #26551 — 修复CRS故障
   * 当请求HEAD(http head)时，我们不需要读取内容，因为它是空的。 虽然可以尝试读取它，但是在调用read()时旧的Android (4.0.x)挂起，而调用read()时较新的Android返回正确的值(-1)。 基于此，将代码更改为不读取“head”的内容

* 访问TrickPlayManager时，Zendesk#26696空指针异常
   * 在使用前通过检查TrickPlayManager对象是否不为空进行修复。

**版本1.4.30 (1659)**

* 没有为实时/线性流更新Zendesk #22675资产持续时间。通过在PTVideoAnalyticsTrackingMetadata中提供新的API assetDuration（为实时和线性流提供资产持续时间），解决了此问题。

* Zendesk #25853切换渠道时TVSDK中的内存泄漏解决了在下载文件时，重置或释放MediaPlayer时文件读取缓冲区泄漏的问题。

**版本1.4.29 (1653)**

* Zendesk #21200 — 当应用程序处于后台时，播放器不会从挂起状态恢复当发出流切换信号后播放器被挂起时，此解决方法允许播放器在播放器从挂起状态恢复时执行流切换，而不是恢复到以前的位置。

* Zendesk #23412 — 如果您在广告时间的最后3秒内点击任何广告，播放器会卡在黑盒中。此问题与Zendesk #21200的问题相同。

* Zendesk #23616 — 跳过的广告时间在将来搜寻得太远根据广告插入类型（插入/替换），TVSDK会确定计算中是否使用广告持续时间来确定广告时间终结点。

* Zendesk #25078 - Android TV STB上的TVSDK DRM内存泄漏已定位并修复了DRM适配器对象的内存泄漏。

* Zendesk #25067 - VideoEngineTimeline中的崩溃发生这种情况是因为对象未正确清理，并且在对象被销毁后调用了事件。 通过添加检查以防止null异常，解决了此问题。

* Zendesk #25352 — 设置自定义HTTP标头。已通过在TVSDK上向允许列表添加新的自定义标头来解决此问题。

* Zendesk #25617 - Live stream PTS变换导致播放器中断和内存崩溃当在区段中间发生变换时，通过在FragmentedHTTPStreamer中添加PTS变换处理来解决此问题。

**版本1.4.28 (1637)**

* Zendesk #23618 — 在咨询广告策略之前触发广告时间事件此问题可通过在因adForgiveness而跳过广告时不触发AD_BREAK_START和AD_START事件来解决。 而是发送AD_BREAK_SKIPPED事件。

**版本1.4.27 (1631)**

* Zendesk #23174 — 调整视频大小时的性能问题通过提供一个新的API MediaPlayerView.setSurfaceFixedSize来解决此问题，该API允许TVSDK从MediaPlayerView访问SurfaceHolder.setFixedSize()。

* Zendesk #24450 - TVSDK发出重复的广告请求。当经过的时间转换为长而不是双倍时，会发生此问题，并且此问题已得到修复。

**版本1.4.26 (1627)**

* Zendesk #21436 - OpenSSL库更新至1.0.2h版已将OpenSSL库更新至1.0.2h版
* Zendesk #23825 — 回调中不包含Cookie。通过支持Android Cookie修复了此问题。

**版本1.4.25 (1620)**

* Zendesk #22900 - Android参考播放器上未播放Live Adobe Primetime DRM流内存分配问题已修复。
* Zendesk #23176 — 应用程序在尝试播放VPAID广告时崩溃发生崩溃的原因是应用程序未创建自定义广告视图来呈现VPAID广告。 当没有自定义广告视图时，通过在广告服务器响应中忽略VPAID广告解决了此问题。

* Zendesk #23153 - SampleAES DRM流 — TVSDK参考播放器中的播放停滞此问题与Zendesk #22900相同。

**版本1.4.24 (1612)**

* Zendesk #20784 - Analytics：触发实时视频过渡的内容完成通过添加API (trackVideoComplete)在实时/线性视频跟踪会话期间手动触发内容完成，解决了此问题。

* Zendesk #21977 VideoEngineTimeline在placeAdBreak/acceptAd操作期间崩溃
   * 在本期中，更新了以下库：
      * AdobeMobile库到版本4.10.0
      * VHL库到版本1.5.6
      * VHL-Nielsen库到版本1.6.7

在将广告添加到接受的广告列表之前，通过添加空检查解决了此问题。

* Zendesk #22313使用Amilogic芯片组的STB的比特率不会超过120万通过预加载媒体编解码器功能并禁用Amilogic芯片组设备的无缝切换来解决此问题。

* Zendesk #19520示例AES HLS资产未在TVSDK播放器中播放通过为AES加密HLS示例流处理多个PMT描述符，该问题已得到解决。

**版本1.4.23 (1602)**

* Zendesk #18852 — 更新基于CRS规则的创意选择逻辑通过添加JSON配置文件以指定创意选择优先级来解决此问题。

* Zendesk #20861 - Android N此版本提供了对Android N的支持，方法是删除直接使用Android平台本机库的功能，而运行Android N的应用程序无法再访问这些库。

* Zendesk #21018 - Android N崩溃的解决方法与ZD# 20861相同。

* Zendesk #21266 - VideoEngineAdapter因Invalid_Key错误而崩溃Invalid_Key错误不包含来自AVE的说明，因此解析文本会导致NPE。 通过在解析onError期间对描述添加空值检查来解决此问题。

* Zendesk #22286 — 本机库正在分配内存读取密钥/片段，从而导致崩溃。修复了尝试同时加载具有多个密钥的清单时，Android上发生的此崩溃。

**版本1.4.22 (1581)**

* Zendesk #17236 — 使用DRM的HLS视频的播放头时间不可靠LBA流的时间跳转已得到修复，在这种情况下，音频区段开始时间与视频区段开始时间不匹配。

* Zendesk #17680 — 视频播放在Selevision Andredo盒上冻结此设备上的视频解码器有时在从输出缓冲器将视频帧出队时返回明显的输出时间跳转，并且此输出时间戳保持高水平。 通过返回 *不支持视频配置文件* 此错误不会强制播放器重试同一配置文件或选择其他配置文件。

* Zendesk #19074 - FFWD和REW特技播放期间视频冻结通过添加新的警告TRICKPLAY_ENDED_DUE_TO_ERROR来通知应用程序trickplay已退出并且视频由于不可恢复的错误而暂停，已解决此问题。

* Zendesk #19574 - TVSDK不返回DRM或非DRM内容的M3U8响应数据此问题已通过以下方式解决：

* Zendesk #19986 — 某些设备（如Android TV）的操作行为已损坏
* 向条件添加FILE_NOT_FOUND错误。
* 当错误来自 *未找到文件* 错误，如果响应可用，则将URL和响应与错误描述分开。
修复了NVidia shield OP支持引入的逻辑错误。 在非NVidia shield设备上，即使显示类型未知，也信任显示安全标志。

* Zendesk #20549 — 处理陈旧的播放列表。 如果以前的获取未接收新区段，则通过将Live Manifest更新之间的间隔减小到预期区段持续时间的一半，可以解决此问题。

* Zendesk #20742 — 在FireTV上播放实时内容时，内存使用率似乎继续增加。崩溃是由已达到限制的JNI对象引用表导致的。 通过删除在解码器重新启动期间创建的MediaFormat对象的引用，解决了此问题。

* Zendesk #21125 — 提前从实时/线性广告时间返回(CSAI)。 添加了一项功能，如果播放器使用机会检测器中的接合在广告提示中注册了接合，则该功能允许播放器在广告时间返回主内容。

* Zendesk #21334 — 第三方广告请求的TVSDK广告请求超时值。 向AdvertisingMetadata添加了adRequestTimeout设置，该设置允许为广告调用启用全局超时。

**版本1.4.21 (1566)**

* Zendesk #17781 - ADB屏幕捕获不再工作通过添加允许屏幕捕获的DefaultMediaPlayer.create(Context context， boolean secureSurface) API，解决了此问题。
要允许屏幕捕获，请为secureSurface传递false。
重要信息：我们强烈建议您不要在生产设置中启用此屏幕捕获功能。

* Zendesk #19074 — 在FFWD和REW特技播放期间视频冻结已解决当trickPlay在播放中冻结时出现的以下问题：

* Zendesk #19532 — 隐藏式字幕显示混乱
   * FHS开始了小技巧，但第一个iframe区段中没有框架。
   * 下载iframe区段时，如果FHS点击错误条件，则会退出点击播放并暂停播放。
   * Andorid MediaCodec实施在被要求刷新所有输入/输出缓冲区时永远等待输入队列的可用性。
通过颠倒WebVTT提示的顺序，使多个重叠提示显示为“向上滚动”，解决了此问题。

* Zendesk #19574 - TVSDK不返回DRM或非DRM内容的M3U8响应数据在PTMediaPlayerItem.prepareToPlay中的清单文件的初始加载中，如果加载失败，则TVSDK不会向应用程序报告失败响应的正文。
通过允许TVSDK将失败响应报告为应用程序错误，此问题得以解决。

* Zendesk #19701 — 播放因SAP/中断而冻结解决了音频和视频在中断时解除对齐时播放器冻结的问题。

* 错误#PTPLAY-11162 — 已解决将OpenSSL库更新到版本1.0.2f的问题。

**版本1.4.20 (1546)**

* Zendesk #17384 — 功能请求：从1.4.20版本开始，TVSDK已在Android中为AAC媒体中的ID3标记提供AAC播放支持和ID3元数据支持。

* Zendesk #18358 — 播放器因比特率开关不同步的不连续性而冻结。通过正确处理ABR拼接边缘案例，解决了此问题。

* Zendesk #19232 — 使用TVSDK 1.4.18的应用程序在旧版Amazon OS版本4上行为异常。通过删除在TVSDK播放器初始化过程中创建的隐藏Web视图来避免与不支持Android Webview的设备冲突，解决了此问题。

* Zendesk #19585 — 发生自适应比特率转换时的慢动作播放。
在ABR切换期间，如果新配置文件的音频采样速率与当前配置文件的音频采样速率不同，则播放变得快或慢。 这是因为视频演示者未收到音频格式已更改的通知。
通过确保在正确位置设置通知标志，此问题已得到解决。

* Zendesk #19683 - SAP DAI播放 — 几秒钟内无音频。
在TVSDK逻辑的若干情况下，当比较两个演绎版区段的时间戳时，会使用RENDITION_TIMEOUT_THRESHOLD作为可接受的值范围，因为时间戳不能始终与0毫秒的差异相匹配。 如果间隙在RENDITION_TIMEOUT_THRESHOLD的范围内，则假定它是匹配项。

RENDITION_TIMEOUT_THRESHOLD设置为100毫秒，但发现它对于某些流不足。 通过将RENDITION_TIMEOUT_THRESHOLD增加到200毫秒，解决了此问题。

* Zendesk #19699 - TVSDK无法在VTT字幕跟踪之间切换此问题已得到解决，具体方法是：在跟踪更改时进行播放器转储并重新加载清单；更正影响双字节WebVTT描述跟踪名称的UTF8字符串转换问题。

* Zendesk #19717 - CC选项显示问题通过正确处理Unicode字符串，该问题已得到解决。

* Zendesk #19910 — 未检测到TIT2 ID3标记通过为ID3 v2.4字符串编码和ID3 v2.3支持提供更全面的支持，此问题已得到解决。

* Zendesk #20135 - TVSDK正在为VOD内容触发多个onComplete。
通过在正确位置添加post_roll_complete事件侦听器，而不是在状态更改事件的完整情况下添加，解决了此问题。

**版本1.4.19 (1521)**

* Zendesk #4180 - TVSDK未强制实施HDCP。
   * 这是此票证的部分修复，仅解决NVidia防护设备的问题。
您必须在Nvidia Shield中使用正确实施的HDCP检测API来动态跟踪HDCP状态。

* Zendesk #18358 - TVSDK会在比特率交换机上冻结，并出现非同步不连续性。
   * 通过添加新的警告来检测PTS不连续性，并强制PTS检查为每个ABR交换机重新搜索正确的段，解决了此问题。
要修复冻结，对mediaPlayer.setCustomConfiguration方法的调用应包含forcePTSCheckForABR作为参数。

* Zendesk #19038 — 华硕Zenpad 10上无直播。

  通过预加载媒体编解码器信息，解决了此问题，这样您就不会在运行时查询函数。

* 以下问题与Zendesk #19038相同：
   * Zendesk #19483 - TVSDK在英特尔平台上崩溃。
   * Zendesk #19171 — 使用Android 5.0在Asus Memo Pad 7上崩溃。

**版本1.4.18 (1503)**

* Zendesk #3324 — 当VMAP中没有广告媒体时，Primetime广告报告不会跟踪广告时间。
当广告时间为空时，将不会触发广告时间开始和完成跟踪事件。 通过在空的广告时间（例如VMAP AdBreak）上发送广告时间开始Ping，并使用有效的AdSource节点来解决此问题。

* Zendesk #18229 - SetCCVisiblity(VISIBLE)在MediaPlayer.reset()调用后被忽略。通过将setCCVisiblity（Visibility.不可见）添加到MedIAPlAYER类中的RESET()函数，解决了此问题。

* Zendesk #18328 - Amazon Fire TV第2代设备上具有60FPS内容的丢帧问题通过应用编码的FPS进行睡眠时间决策并使用更好的编码FPS预测逻辑解决了此问题。

**版本1.4.17 (1472)**

* Zendesk #2231 — 获取在MediaPlayerNotification中不可用的清单时返回的错误。通过包含清单的响应正文，解决了此问题，但存在分析错误。

* Zendesk #17703 - VideoEngineView不会阻止视频播放过程中的屏幕截图setSecure方法自API 17起便已推出，但由于API 17涵盖4.2、4.2.1和4.2.2，因此并不知道哪一个会引发异常或者是否特定于设备。 通过将VideoEngineView.setSecure封装到try catch子句中，解决了此问题。

* Zendesk #17919 — 内容搜寻导致心跳错误。在前置广告后开始搜寻时生成的心跳调用导致出现无效的输入数据位置错误。 此问题已得到解决。

**1.4.16安** (1454a)

* Zendesk #18215 — 某些AES流无法加载。
通过先检查配置文件DRM元数据大小，然后再加载AES密钥，此问题得以解决。

**版本1.4.16 (1454)**

* Zendesk #3875 — 播放期间选项卡S崩溃恢复OKHTTP对CRSAuditude的依赖性，因为TVSDK现在直接使用httpurlconnection而不是curl。 通过先清除例外，然后再执行任何其他JNI调用，该问题得以解决。

* Zendesk #4487 — 跟踪线性内容渠道通过允许在线性流播放会话期间重新初始化视频心率跟踪器，该问题已得到解决。

* Zendesk #17919 - Android — 内容搜寻导致心跳错误当章节中存在搜寻时，心跳处于错误状态的问题已得到解决。

* Zendesk #18053 - Adobe Primetime在棉花糖上崩溃TVSDK在Android M操作系统上崩溃时，TVSDK库使用的霓虹灯代码进行YUV ->RGB颜色转换。 通过使用非霓虹灯版本的代码更新导致此问题的函数，解决了此问题。

* Zendesk #18072 - Android M — 应用程序崩溃在检查是否支持配置文件和级别时，调用MediaCodecList和MediaCodecInfo API时会发生崩溃。 通过提供临时解决方法，提前加载所有编解码器信息以避免仅在需要编解码器信息时调用这些API，解决了此问题。

* Zendesk #18074 — 使用Android 6.0的Nexus上无法使用的阿拉伯字幕。通过为Android提供CTS字体映射支持，解决了此问题。

**版本1.4.15更新(1438)**

* Zendesk #17437 — 使用某些AES流启动VOD内容时出现长时间延迟。
要解决此问题，如果清单中列出了多个键，请并行下载所有AES键。

**版本1.4.15 (1435)**

* Zendesk #4278 — 自适应比特率更改(ABR)时Android机顶盒上出现问题。
修复了使用最新的Android媒体编解码器添加对无缝ABR切换的支持。

* Zendesk #17063 — 调用mediaPlayer.reset()会导致视频引擎重置错误。
修复是在调度ErrorEvents时包括来自VideoEngineExceptions的原始MediaErrorCode。

* Zendesk #17130 — 在FireTV上看到更改比特率时短暂但明显的暂停。
(与上#4278相同)修复了问题，即使用最新的Android媒体编解码器添加对无缝ABR切换的支持。

* Zendesk #17666 — 其他广告标记，恢复内容时会出现意外或无广告。
修复了对video-on-demand (VOD)内容执行prepareToPlay时的问题，即初始搜寻是在本地时间而不是虚拟时间执行的。

* Zendesk #17437 — 使用某些AES流启动VOD内容时出现长时间延迟。
修复了清单中列出了多个键时并行下载所有AES键的问题。

* Zendesk #17851 - Android TV - ABR期间的黑帧修复方法是指定KEY_MAX_WIDTH和KEY_MAX_HEIGHT以启用自适应播放。

**版本1.4.14 (1415)**

* Zendesk #3875 — 在播放期间Tab S崩溃。
需要进行额外的修复以防止崩溃。

* Zendesk #17245 - Android TV上的回退无法正常工作。
修复了在启用回退时，播放挂起，并且VMAP响应具有空广告时间的附加问题。

**版本1.4.14 (1412)**

* Zendesk #17245 - Android TV上的回退无法正常工作。
移除了在后备广告上禁用创意重新打包的限制。

**版本1.4.13 (1388)**

* Zendesk #3502 — 在广告时间期间提供基于HLS客户端的故障转移支持允许在广告时间期间发生更新实时配置文件错误时故障转移到主清单。

* Zendesk #3875 — 播放期间选项卡S崩溃要解决HttpUrlConnection和cURLm之间的冲突，请使用第三方库。

* Zendesk #4450 — 在内容解析器中为单个投放设置自定义元数据时出现问题将设置器添加到Opportunity设置。

**版本1.4.12 (1388)**

* Zendesk #2751 - CSAI和CRS |增强：处理某些媒体文件URL中的动态元素。
更新了Creative重新打包服务，以正确处理具有动态创意URL的广告。

* Zendesk #3965 — 从Trickplay切换回正常播放会导致在开始播放之前向前跳转一点。
   * 此修复包括返回在速率更改之前的时间的TVSDK，直到更新所有变量为止，而不是尝试计算GetStreamTime。
   * 修复了在流结尾附近更改特技播放速度时的崩溃。
   * 纠正了特技播放期间的当前时间计算。

* Zendesk #3978 - 8倍和16倍的Trickplay经常冻结。
   * 应始终选择具有最低比特率的特技播放配置文件，以避免持续缓冲。
   * 增加跳过帧间隔以获得高特技播放率。
   * 修复了在特技播放期间达到目标长度后缓冲区继续增长的问题。

* Zendesk #3992 — 额外的Trickplay速度
TrickPlay已更新为接受高于16x的速率；+/- 32、+/-64和+/-128现在也是允许的。

* Zendesk #4007 — 将GEOB对象解释为时间轴元数据（Android和Web）的一部分。
添加了setByteArray和getByteArray API。

* PTPLAY-7301 — 从随机接入点开始即时。
即时打开已更新为允许非零起点。

**版本1.4.11 (1363)**

* Zendesk #2076 — 在使用Android 4.0.3的Motorola Xoom上播放视频时经常出现结巴。为允许列表添加了设备，以防止他们尝试播放高姿态内容。

* Zendesk #2197 - `[Ads]` 跟踪和错误调度带有警告通知的OperationFailedEvent。

* Zendesk #3304 - VAST 3.0 `[ERRORCODE]` 未填充宏
   * 如果内联广告的创意效果不佳，则会显示错误代码400。
   * `[ERRORCODE]` 宏将进行URL编码

**版本1.4.10 (1354)**

* Zendesk #2941 — 实时资产在可搜索范围内没有“0”以前在搜索实时流的开头时有3个区段缓冲区，现在可以搜索实时流的开头（即第一个区段的开头）。

* Zendesk #3169 — 使用Adobe Analytics集成更新引用播放器已使用Adobe Analytics库作为示例注入对引用播放器进行更新。
* Zendesk #3299 — 无法解释的戏法游戏行为
   * 修复了在停止特技播放后返回到播放状态可能需要几秒钟（有时需要25秒以上）的错误。
   * 修复了在同一媒体上再次调用特技播放可能导致流在当前时间冻结的错误。
* Zendesk #3433 - Android和Flash — 字幕问题

GetLine for WebVTT未遵守 &lt;cr>&lt;lf> 调整了包的长度；最后一个字幕可能包含以前字幕中的字符。

* PTPLAY-6243 — 增强引用播放器以捕获调试信息

Android示例引用播放器已得到增强，现在可以选择打开调试日志并通过电子邮件发送结果。 可在参考播放器的“日志”菜单下找到此选项。

**版本1.4.9 (1332)**

* Zendesk #2649 — 在初始缓冲已满之前发生缓冲完成

搜寻之后，视频引擎在视频演示者准备播放之前将状态设置为“正在播放”的可能情况。 在搜寻前缓冲状态为高时发生。 通过通知视频引擎低缓冲状态进行修复。 由于视频引擎的缓冲状态较低，调用Play会导致状态更改为BUFFERING而不是PLAYING。 当状态更改为“正在播放”时，将继续播放。

* Zendesk #2846 — 增强请求：提供为Auditude库发出的调用设置其他用户代理字符串的功能

添加了一个新的API，以便为与广告相关的调用auditudeSettings.setUserAgent(&quot;user/agent&quot;)设置用户代理。 如果未设置用户代理，则将使用默认值。 这仅影响广告相关调用的用户代理，媒体调用的用户代理保持不变，即“Adobe Primetime”+&lt;default useragent=&quot;&quot;>.

**版本1.4.8 (1324)**

* Zendesk #1218 - 106000.33本地错误……如果在FragmedHTTPStreamer：：ThreadParseManifest()中加载清单失败，请检查URL域是否为localhost，如果是，则将域更改为127.0.0.1，并调用ThreadParseManifest。
* Zendesk #3072 — 自动切换到更低的比特率。 更改了缓冲区长度计算以跳过零PTS有效负载。
* Zendesk #3168 — 仅在前10秒显示WebVTT字幕。
* Zendesk #3193 — 在TVSDK中添加了配置文件更改API请求，PlaybackEventListener.onProfileChanged()。

**版本1.4.7 (1311)**

* Zendesk #2197 — 跟踪广告错误。 为无法加载清单的资源添加了通知
* Zendesk #2575 - PSDK在视频之前忽略MARK自定义流中广告
* Zendesk #2719 — 使用auditude广告赢得死亡，在重定向到auditude插件中的相对url时固定信标跟踪
* Zendesk #2760 — 在TrickPlay模式中忽略DISCONTINUITY标记
* Zendesk #2805 — 播放开始时播放器崩溃，修复方法与Zendesk #2719相同
* Zendesk #2817 - Android播放器 — 播放器有时会挂起或停止播放，可通过将解码缓冲区从2.0秒扩展到3.0秒来修复此问题
* Zendesk #2839 - Adobe Primetime PSDK是否支持ARMv8芯片组？，添加了对Galaxy S6上存在的崩溃的修复。
* Zendesk #2885 -Auditude崩溃播放，修复方法与Zendesk #2719相同
* Zendesk #2895 — 播放10分钟后始终出现实时HLS故障
* Zendesk #2925 — 有关Android开发构建(1.4.5)的反馈，当我们将包排队到输入队列时，如果PTS为负值，则解码器将进入一种奇怪的状态，即我们总是会获得未来包的负值输出PTS。 如果输入的PTS为负数，则修复程序将设置为零，以避免出现此问题。
* PTPLAY-4645 — 在openssl中关闭RC4密码支持。 存在已知的RC4漏洞。 这意味着，如果尝试连接仅支持RC4的服务器，它将失败。

**版本1.4.6 (1282)**

* Zendesk #2192 — 在较差的网络条件下，比特率并不总是较低，可通过删除快速交换机实现来修复此问题。
* Zendesk #2631 - Android上的阿拉伯字幕：多行文本似乎被切断，通过调整阿拉伯字体的字体大小来修复。
* Zendesk #2844 — 注释4上的缓冲和片段下载时间不准确。

通过将视频区段下载之间的延迟添加到带宽计算中，并让下载时间计算逻辑使用完整的请求周期时间，解决了此问题。

* Zendesk #2908 — 在Nexust 5、6和7上无法使用的阿拉伯字幕，通过为阿拉伯脚本再添加2种后备字体来修复。
* PTPLAY-4627 — 将Nielson appsdk更新到版本1.2.3.7
* PTPLAY-5084 - Live主清单更新故障转移支持

**版本1.4.5 (1248)**

* Zendesk #1757 — 某些视频比特率配置文件仅播放音频或播放器崩溃，Nexus 4和Nexus 7崩溃已修复
* Zendesk #2072 - AdEvent的TimedMetadata不包含仅“http”的完整URL
* Zendesk #2192 — 在网络状况较差时，比特率并不总是较低
* Zendesk #2256 — 访问主播放列表，更新了PSDK以便为主播放列表上的订阅标记调度timedMetadata事件。
* Zendesk #2269 — 使用WebVTT时，屏幕上同时显示两种不同的字幕语言
* Zendesk #2417 — 播放器尝试在播放开始之前下载字幕，WebVTT使用错误的区段编号变量进行区段编号匹配。 只有区段索引从零开始的媒体才会显示错误。
* Zendesk #2470 — 在暂停后发生比特率更改时，PSDK不会从SUSPENDED状态返回。 在特殊情况下，当RestoreGPUResource调用智能搜寻（从挂起状态恢复播放器）并在此之前检测到流切换时，智能搜寻无法完成，并导致持续缓冲。
* Zendesk #2451 — 隐藏式字幕“bottom inset”，在字幕代码中添加了“bottomInset”参数
* Zendesk #2480 — 禁用HTTP 302重定向优化，添加了对设置useRedirectedUrl属性的支持
* Zendesk #2486 — 第三方信标
* Zendesk #2547 — 阿拉伯字幕：文本应右对齐

**版本1.4.4 (1195)**

* Zendesk #1158 — 在Huawei Valiant上播放失败(Y301A1)
* Zendesk #1709 — 不正确的媒体大小和延长视频
* Zendesk #1757 — 仅在具有相同spa/pps数据的流之间切换配置文件后播放音频
* Zendesk #2095 - HTTP 307状态（重定向）导致Adobe播放器停止播放
* Zendesk #2126 — 缺少上次ADEVENT的TimedMetaData事件，上次区段后存在的订阅标记未从AVE报告给PSDK
* Zendesk #2227 - VideoEngine nativeReset和nativePause中的锁定
* 错误#3921755 - OpenSSL库更新至1.0.1L版

**版本1.4.3 (1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 — 隐藏式字幕打开和关闭
* PTPLAY-1818 — 倒带特技播放在广告处停止，而不是倒带越过广告
* PTPLAY-2736 — 当包含WebVTT字幕的流完成播放时，屏幕上会显示之前显示的WebVTT字幕
* PTPLAY-3773 — 在广告位置后开始流播放时，不播放中置广告

**版本1.4.2**

* Zendesk #1561 - primetime中基于HLS客户端的故障转移支持。 将使用程序日期时间解决故障转移问题
* Zendesk #1590 - LoadInfo.MediaDuration始终为0（对于纯音频未修复）
* Zendesk #1626 — 播放器中潜在的内存泄漏。 不是实际的内存泄漏，NotificationHistory保存最后1000个通知时出现问题，现已减少到100个。
* Zendesk #2192 — 在网络状况较差时，比特率并不总是较低

**版本1.4.1 (1121)**

* Zendesk #1951 - 4.0.x设备上的VideoEngine.nativeReset()锁定
* Zendesk #2064 — 特定基于英特尔的Android设备上的本机崩溃SIGSEGV
* Zendesk #2075 - 4.0.x设备上的VideoEngine.nativeReleaseGPUResource中的锁定注意：此内部版本为 &#42;&#42;&#42;必填&#42;&#42;&#42; 支持Android 5.0 (Lollipop)
* Zendesk #1513 - Android Lollipop支持
* Zendesk #1709 — 不正确的媒体大小和延长视频
* Zendesk #1871 — 在使用WebVTT字幕查看实时流时，WebVTT字幕偶尔会消失并重新出现
* Zendesk #1996 - PSDK 1.4.0中看不到时间轴标记
* Zendesk #2046 — 使用PSDK 1.4.1.1113崩溃，修复了从审核未返回任何广告时的实时流崩溃
* 错误#3769657 — 将curl的版本更新为7.38.0
* PTPLAY-1575 — 当ABR播放以纯音频流开始，然后切换到音频/视频流时，视频在音频继续播放时从不渲染
* PTPLAY-2499 — 将更新到OpenSSL版本1.0.1j，以解决最近的漏洞
* PTPLAY-2632 — 在Android Lollipop上完成中置广告后，视频无法恢复
* PTPLAY-2678 — 在Android Lollipop上实时长寿测试期间视频停滞

**版本1.4.0**

* Zendesk #1024 — 通过清单从流中删除广告的功能
* Zendesk #1293 — 隐藏式字幕跟踪选择问题。
* Zendesk #1590 - LoadInfo.MediaDuration始终为0，mediaDuration现在显示正确的值。
* Zendesk #1629 - Galaxy S4上的广告播放结束时播放器/应用程序崩溃
* Zendesk #1674 — 未显示ClosedCaption，缺少0x03 ETX代码时显示正确的708字幕。
* PTPLAY-2157 - getter会返回默认隐藏式字幕样式，即使已在流中设置并可视化验证其他样式也是如此。 “隐藏式字幕”样式属性现在将显示已设置的值。

## 1.4中的已知问题 {#known-issues-in}

**版本1.4.31**

* PTPLAY-16803 — 由于字幕系统需要视频才能工作，因此隐藏字幕不适用于纯音频内容。 没有视频，就没有视区尺寸；如果没有视区尺寸，我们将无法显示任何用于字幕的图形。
* PTPLAY-1634 — 同一订阅标记在不同的Live Windows中具有不同的时间戳。 当实时窗口移动时，其中的同一标记应具有相同的时间戳。 但有时，即使相同的标记也会具有不同的时间戳。
* PTPLAY-3197 — 连续播放~1小时后，宏基Iconia设备出现信号11 SIGSEGV错误崩溃
* PTPLAY-3310 — 由于一些比特率较低的音频，Acer Iconia上的音频变得断断续续
* PTPLAY-3355 — 摩托罗拉Xoom在连续播放1 h后发生4.0.x的WIN DEAD车祸。
* PTPLAY-3557 — 广告时间倒带导致流完成
* PTPLAY-7079 - Android客户端上的播放窗口不适用于安全停止/硬停止
* 错误#3760144 — 当在Kindle Fire 7和Samsung Galaxy Nexus等设备上暂停流时，分辨率可能会移动或显示为脉动。 只有在仔细观察下才能观察到
* 错误#3761170 — 具有广告的实时中的seekToLocal无法重新搜索到广告内容，最适合将currentTime API用于实时流
* 错误#3763370 — 包含广告的直播流有时会同时显示两个广告标记，但实际上应该只显示一个。 这些广告标记表示相同的广告，并且只播放一个广告
* 错误#3763373 — 在VOD流中搜寻过去的广告时，广告标记可能会短暂消失。 广告标记将恢复，并且不会对时间轴产生其他不利影响
* 某些设备存在已知的播放问题。 请参阅 [1.4中的已知设备问题](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* 参考实施 — 在示例应用程序中未实施Trick Play
* 在某些Android TV设备上，由于在以下过渡点重置了解码器，因此可以看到黑色帧：
   * 进入和退出点击模式
   * 在后期捆绑音频轨道之间切换
   * 从广告到主内容。

**版本1.4.23**

* 隐藏式字幕不适用于纯音频内容，因为字幕系统需要视频才能工作。 没有视频，就没有视区尺寸；如果没有视区尺寸，您将无法显示任何用于字幕的图形。
* 从版本1.4.23开始，TVSDK不支持Gingerbread OS 2.3。这是因为TVSDK使用以下专用Android库来收集有关使用Gingerbread操作系统的设备的硬件信息：

   * `libstagefright.so`
   * `libcutils.so`

在Android N版本中，Google已删除对这些专用库的访问权限。 目前，Gingerbread操作系统在全球市场占有率不足1%，因此，在1.4.23版之后，TVSDK将不再支持Gingerbread操作系统。
当您使用版本1.4.23（包括对Android N的支持）或更高版本时：
* 更新您的应用程序以使用minSdkVersion 11。
* 如果最终用户运行的是OS 2.3，则SDK版本低于应用程序的minSdkVersion。 系统将中止应用程序的安装或升级。
* 如果最终用户运行的版本高于OS 2.3，则会正确安装应用程序。

如果更新minSdkVersion：

* 如果最终用户运行的是OS 2.3，则已安装应用程序，但无法正常播放。
这适用于更新和全新安装。
* 如果最终用户运行的系统高于OS 2.3，则表明应用程序已正确安装，并且内容可正确播放。

**版本1.4.22**

* 当接合输出和接合输入标记彼此太接近时，早期退出广告不适用于某些中置广告。

**版本1.4.2**

* 在广告时间倒带会导致流完成。

媒体播放器错误地发送了MediaPlayer PlayerState.Complete当它到达广告边界时，会在特技播放倒带操作期间完成。 当处于特技播放模式时，播放器应忽略此事件，否则SDK将正确处理状态。

**版本1.4.0 (1086)**

* PTPLAY-1634 — 同一订阅标记在不同的Live Windows中具有不同的时间戳。 当Live Windows移动时，每个窗口中的相同标记应具有相同的时间戳。 但有时，即使相同的标记也有不同的时间戳。
* PTPLAY-2541 — 有时，在断电中将多个备用流切换到/从该备用流切换后，会看到COMPONENT_CREATION_FAILURE
* 错误#3726865 — 如果MultiBitrate LBA流从纯音频流开始，则在切换到音频/视频流时，将不显示视频。 从音频/视频流开始播放将不会显示此问题，并且可以成功地在音频流和音频/视频流之间切换
* 错误#3760144 — 当流在Kindle Fire 7和Samsung Galaxy Nexus等设备上暂停时，分辨率可能会移动或显示为脉动。 只有在仔细观察下才能观察到
* 错误#3761170 — 包含广告的实时中的seekToLocal无法搜索回广告内容；最好将currentTime API用于实时流
* 错误#3763370 — 包含广告的直播流有时会同时显示两个广告标记，但实际上应该只显示一个。 这些广告标记表示相同的广告，并且只播放一个广告
* 错误#3763373 — 在VOD流中搜寻过去的广告时，广告标记可能会短暂消失。 广告标记将恢复，并且不会对时间轴产生其他不利影响
* 某些设备存在已知的播放问题。 有关更多信息，请参阅 [1.4中的已知设备问题](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14).
* 参考实施 — 未在示例应用程序中实施特技播放。

## 1.4中的已知设备问题 {#known-device-issues-in}

| 设备 | 芯片组 | 问题 | 原因 | 解决方法 |
|--- |--- |--- |--- |--- |
| Droid X | TI OMAP3 | ABR延迟是预期会出现的，因为它正在重新启动解码器。 |  |  |
| HTC Desire（与HTC Desire HD不同） | QSD8250 | 无法播放视频。 返回VIDEO_PROFILE_NOT_SUPPORTED错误。 | Design不能提供适当的硬件解码器。 它给了Stagefright的SW解码器。 | 重新启动设备。 |
| HTC EVO 4G | QSD8650 | 没有硬件解码器。 | 高通没有硬件解码器。 | 升级到Android 4.x。 |
| Kindle FireSystem版本6.0 | TI OMAP4 | 不播放HLS流。 AIR上的视频不起作用。 |  | 升级到系统版本6.3。 |
| Kindle Fire HD | TI OMAP4 | 可能会进入无法播放视频的状态。 返回VIDEO_PROFILE_NOT_SUPPORTED和UNRECOVERABLE_ERROR错误。 | 当应用程序未完全关闭硬件解码器（例如，在遇到崩溃之后）时，硬件解码器进入不可恢复状态。 也会在设备上的本机应用程序上发生。 | 重新启动设备。 |
| Kindle Fire HD 8.9 | Snapdragon 800 | AVE在多个ABR交换机后崩溃。 |  |  |
| 摩托罗拉·阿特里克斯 | Tegra2 | 与AIR相比，AVE存在总体性能问题。 音频/视频不同步，视频播放在9到15分钟之间停止播放。 崩溃。 | 可能与我们在AIR上启用的openGLES有关。 正在接受调查。 |  |
| Nexus 7（第2代） | S4Pro APQ8064 （高通） | 当电影暂停超过30分钟时，设备将挂起。 | 已报告给Google的设备问题。 | 应用程序应超时，以免出现长时间暂停状态。 |
| Nexus S (GB) | 嗡嗡的鸟 | 无法使用硬件解码器播放任何视频。 | Nexus S中没有基于Stagefright的硬件解码器，因此对于Android 2.3，我们使用SW解码器。 | 升级到ICS。 |
| Nexus S (ICS) | 嗡嗡的鸟 | 视频偶尔闪烁。 | 错误数据会导致解码器进入错误状态。 | 重新启动设备。 |
| Nook tabletAndroid操作系统：2.3 | TI OMAP 4 | 视频无法播放，应用程序挂起。 | Stagefright在运行应用程序几次后进入不稳定状态。 对mediaplayer：：QueryCodecs的调用挂起。 | 重新启动设备以重置状态。 |
| Samsung Galaxy ACE | 高通MSM7227 | 无法安装SampleMediaPlayer应用程序。 | 使用ARM v6而不是更常用的ARM v7芯片组。 FP/AIR不支持此设备。 |  |
| Samsung Galaxy ACE2Android操作系统：2.3.6 | 新托尔U8500 | 无法播放视频。 | 此芯片组是AVE中适用于Android预编译的未知解码器。 |  |
| Samsung Galaxy S2 (GT-I9100) | 埃克西诺斯 | 此设备的视频性能不达标。 | HW解码器返回带有错误PTS的解码帧。 解码器似乎正在使用解码时间而不是呈现时间。 |  |
| Samsung Galaxy S2 GAndroid OS：2.3.6 | TI OMAP4 | 启动视频时崩溃。 |  | 升级到Android 2.3.7或4.x。 |
| Samsung Galaxy S3 (I747) | 高通MSM8960 | 视频间歇性冻结，仅播放音频，然后变得无响应。 |  |  |
| Samsung Galaxy S3 I747M | SAMSUNG_M2ATT | 视频冻结。 | 正在调查。 |  |
| Samsung Galaxy Tab 1 v10.1 | 泰格拉2 | MBR转换最多可能需要三秒钟。 | 作为对MBR崩溃的修复，我们为每个流开关重新启动解码器，这最多可能需要三秒钟。 |  |
| Samsung Galaxy Y |  | 无法安装SampleMediaPlayer应用程序。 | 使用ARM v6而不是更常用的ARM v7芯片组。 FP/AIR不支持此设备。 |  |
| Xoom | 泰格拉 | 为了进行切换，将丢弃一些帧。 解码器未重新启动。 | OMXAL限制。 |  |

## 有用资源 {#helpful-resources}

* 请参阅完整的帮助文档，网址为 [Adobe Primetime学习与支持](https://helpx.adobe.com/support/primetime.html) 页面。
