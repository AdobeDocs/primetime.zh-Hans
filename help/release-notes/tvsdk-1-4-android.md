---
title: TVSDK 1.4 for Android发行说明
seo-title: TVSDK 1.4 for Android发行说明
description: TVSDK 1.4 for Android发行说明描述了TVSDK Android 1.4中的新增功能或更改功能、已解决和已知问题以及设备问题。
seo-description: TVSDK 1.4 for Android发行说明描述了TVSDK Android 1.4中的新增功能或更改功能、已解决和已知问题以及设备问题。
uuid: 8bd8ee42-7a1b-4c14-aad9-22804743e505
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: release-notes
discoiquuid: f1ebc1a8-185a-493a-9c00-a6102dffb128
translation-type: tm+mt
source-git-commit: ed910a60440ae7c0d19d9be56c80c8bdbc62bcf1

---


# TVSDK 1.4 for Android发行说明 {#tvsdk-for-android-release-notes}

TVSDK 1.4 for Android发行说明描述了TVSDK Android 1.4中的新增功能或更改功能、已解决和已知问题以及设备问题。

## 新增功能 {#new-features}

**版本1.4.43**

**通过HTTPS安全加载广告**

Adobe Primetime提供了通过HTTPS请求对primetime广告服务器和CRS的首次调用的选项。

**alwaysUseAudioOutputLatency(boolean val)在MediaPlayer类中**

设置此参数后，在音频时间戳计算中使用音频输出延迟。

它接受一个布尔参数值。 如果其值为，则客 `True`户端在音频时间戳计算中使用音频输出延迟。

**版本1.4.42**

**部分广告中断插入：**加入广告中间而不触发部分观看广告的跟踪的电视体验。
示例：用户在包含3个30秒广告的90秒广告分时段中间（40秒）加入。 这是片段内第二个广告的10秒。
* 第二个广告在剩余持续时间（20秒）内播放，然后是第三个广告。
* 不触发已播放部分广告（第二个广告）的广告跟踪器。 仅触发第三个广告的跟踪器。

**版本1.4.41**

无新增功能。

**版本1.4.40**

无新增功能。

>[!NOTE]
>
>如果您使用的版本低于1.4.39，则不需要API更改。

**版本1.4.39**

* TVSDK通过VHL 2.0.1和VHL 2.0.1认证，Nielsen通过。
* 更新Android TVSDK以从新的Akamai主机发出CRS请求 `primetime-a.akamaihd.net`。
* 新的主机名配置通过HTTP和HTTPS(SSL)提供更大规模的CRS资产交付。
* TVSDK支持Android Oreo版本。
* 向类中添加了一个新函数， `AdClientFactory` 以支持注册多个Opportunity Detectars:

   ```
   public List<PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem item);
   ```

   这应返回一组PlacementOpportunityDetector。 现在，您可以注册多个机会检测器。 例如，对于早期广告退出功能，需要两个机会检测器——一个用于广告插入，另一个用于早期广告退出。 只有在您实施了自己的AdvertisingFactory（而不是使用DefaultAdvertisingFactory）时，才需要实施此新功能。 要获取现有行为——您需要创建一个Opportunity Detector，如createOpportunityDetector()函数，并放入数组中并返回：

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
>如果您使用的版本低于1.4.39，则不需要API更改。

**版本1.4.36**

Android上内容跳过的错误修复。

**版本1.4.35**

* **网络广告信息**

   TVSDK API现在提供有关第三方VAST响应的其他信息。 广告ID、广告系统和VAST广告扩展在可通过广告资产上的networkAdInfo属性访问的NetworkAdInfo类中提供。 此信息可用于与其他Ad Analytics平台(如 **Moat Analytics)集成**。

**版本1.4.31**

**CRS广告的多CDN支持**
* 默认情况下，所有转码的资源将托管在Akamai上的Adobe拥有的CDN上。 在最新版本中，Adobe Creative Repackaging Service(CRS)提供了将转码创意内容上传到客户指定的多个CDN的功能。
* 将新API添加到TVSDK以启用在未使用默认URL时指定最终的CRS创作URL。 请参阅文档，了解如何使用这些新API。

**版本1.4.18** Primetime Android TVSDK现在支持VPAID 2.0 Javascript创意，以实现丰富的交互式流内广告体验。 有关VPAID 2.0的详细信息，请参阅 [VPAID广告支持](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/vpaid-ads/android-3x-vpaid-ads.md)。

**版本1.4.17**

AC-3 5.1仅在Amazon FireTV上受支持。

**版本1.4.11**

* **广告回退，广告选择逻辑中的菊花链(Zendesk #3103** For VAST ads(creatives)，对于启用回退规则的广告，TVSDK将MIME类型无效的广告视为空广告并尝试在其位置使用回退广告。 您可以配置回退行为的某些方面。

有关详细信息，请参 [阅VAST和VMAP广告的广告回退](../programming/tvsdk-3x-android-prog/android-3x-advertising/ad-insertion/ad-fallback/android-3x-ad-fallback.md)。

* **更新到版本1.5的视频心率库(VHL)**
   * 能够将视频开始和／或视频／广告／章节开始作为上下文数据发送元数据
   * 网络流量更少——心率平均更小且更小

**版本1.4.7**

* **内部部署个性化**&#x200B;支持支持对Adobe Indelication Server的内部部署安装的支持，以自定义客户端的个性化请求以转到其他端点。

**版本1.4.6**

* **示例AES加密（需要Flash Player版本17.0.0.134）**现在支持基于示例的AES加密。

**版本1.4.2**

* **视频心率库(VHL)更新至版本1.4.0.1**

   * 添加了将其他SDK或播放器中的不同分析用例与Adobe Analytics Video Essentials捆绑在一起的功能。
   * 通过删除trackAdBreakStart和trackAdBreakComplete方法，广告跟踪已得到优化。 广告中断从trackAdStart和trackAdComplete方法调用推断出来。
   * 跟踪广告时不再需要播放头属性。

* **Nielsen SDK集**&#x200B;成TVSDK现在支持将用户跟踪信息发送到Nielsen SDK，而无需任何自定义集成。

**版本1.4.0**

* **使用替代内容替换的封锁信号** TVSDK作为1.4 TVSDK更新的一部分，现在还支持针对线性内容的区域封锁进入和返回。 TVSDK现在可以并行处理两个清单文件（主文件和备用文件），以监视断电信号，即使当替代原始编程显示备用程序时也是如此。

* **删除／替换C3广告** “立即”，无需额外的准备工作即可将新广告动态插入从C3窗口发出的视频点播(VOD)资产中。 TVSDK现在提供了一个API，用于删除自定义内容范围和动态插入新广告。 当直播／线性内容在广播期间出现并且立即被拉下来作为点播内容使用时，这一强大的新功能在没有适当时间“清理”资产的情况下也很有用。

* 接口PlaybackEventListener有一个名为onReplaceMediaPlayerItem的新方法，可用于侦听新事件 `ITEM_REPLACED`。 每当在MediaPlayer上替换MediaPlayer项实例时，都会调度此事件。 实现此PlaybackEventListener的客户端应用程序必须实现或覆盖此新方法。
* AdClientFactory为类添加了一个新功能以注册多个Opportunity Detectars:

   public List&lt;PlacementOpportunityDetector> createOpportunityDetectors（MediaPlayerItem项）;

   例如，对于早期广告退出功能，您需要两个“机会检测器”-一个用于广告插入，另一个用于早期退出 `ad`。

   要覆盖此新函数，请创建单个Opportunity Detector，并放入数组中并返回：

   @覆盖

   public List&lt;PlacementOpportunityDetector> createOpportunityDetectors(MediaPlayerItem mediaPlayerItem){

   List&lt;PlacementOpportunityDetector> opportunityDetectors = new ArrayList&lt;PlacementOpportunityDetector>();

   opportunityDetecters.add(createOpportunityDetector(mediaPlayerItem));

   返回机会检测器；}

   }

## 1.4的TVSDK更改 {#tvsdk-changes}

* 接口PlaybackEventListener有一个名为onReplaceMediaPlayerItem的新方法，可用于侦听新事件ITEM_REPLACED。 每当在MediaPlayer上替换MediaPlayer项实例时，都会调度此事件。 实现此PlaybackEventListener的客户端应用程序必须实现或覆盖此新方法。

* AdClientFactory为类添加了一个新功能以注册多个Opportunity Detectars:

public List`<PlacementOpportunityDetector>` createOpportunityDetectars（MediaPlayerItem项）;

例如，对于早期广告退出功能，您需要两个“机会检测器”-一个用于广告插入，另一个用于早期广告退出。

要覆盖此新函数，请创建单个Opportunity Detector，并放入数组中并返回：

@覆盖

public List`<PlacementOpportunityDetector>` createOpportunityDetecters(MediaPlayerItem mediaPlayerItem){

List`<PlacementOpportunityDetector>` opportunityDetectors = new ArrayList`<PlacementOpportunityDetector>`();

opportunityDetecters.add(createOpportunityDetector(mediaPlayerItem));

返回机会检测器；

}

}

## 1.4中的设备认证和支持 {#device-certification-and-support-in}

>[!NOTE]
>
>TVSDK中不 **支持** 以下功能：
>
>* 在任何平台或版本上慢动作。
>* 实时戏法播放。


**版本1.4.43**

TVSDK 1.4.43已通过Android设备的认证，这些设备具有Android 6.0.1/7.0和8.1(Oreo)。

* **版本1.4.23:**

   * TVSDK 1.4.23已通过Android N设备的认证。

* **版本1.4.18:**

   * Primetime已通过Amazon Fire TV认证。
   * VPAID 2.0仅在Android 4.0及更高版本的设备上受支持。

## 解决了1.4中的问题 {#resolved-issues-in}

>[!NOTE]
>
>强烈建议所有使用CRS的TVSDK客户升级到iOS和Android上的TVSDK 1.4.39或最新版本。 此升级是对现有应用程序实施的直接替换。 升级后，在代理工具（例如，Charles）中检查CRS创意URL请求，以验证路径中的版本是否反映版本3.1。例如：
>
>`https://primetime-a.akamaihd.net/assets/3p/v3.1/222000/167/d77/ 167d775d00cbf7fd224b112sf5a4bc7d_0e34cd3ca5177fbc74d66d784bf3586d.m3u8`

**版本1.4.43**

* 票证#27143 —— 无法在FireTV设备上播放5.1音轨

   * TVSDK现在可以在FireTV设备上播放AC3音频。 回放始终采用立体声。

* 票证#33902 —— 通过HTTPS安全广告交付

   * Adobe Primetime提供了通过https请求对primetime广告服务器和CRS的第一次调用的选项。

* 票证#34493 —— 蓝牙音频延迟

   * 在MediaPlayer `alwaysUseAudioOutputLatency` 类中添加了该类，当设置时，将导致在音频时间戳计算中使用音频输出延迟。

* 票证#34949 —— 集成了新版视频心率库(VHL)。

**版本1.4.42(1791)**

* Zendesk #33719:FireTV 4k自适应比特率缩放缓慢。 增加了对FireTV 4K设备的ABR支持。
* Zendesk #33338: resetDRM将清除应用程序的所有数据。  处理了非TVSDK线程中的异常导致TVSDK操作队列填满的额外情况。

**版本1.4.41(1776)**

* Zendesk #33002 - Fire TV上TVSDK的配套资源数据。 实施了一个新类AdBannerAsset，它将Companion数据返回为List &lt;AdBannerAsset>,AdAsset::id现在是一个字符串，而不是长的。
* Zendesk #32821 - Android Primetime播放器在遇到WWE的演示时间戳(PTS)时会冻结。 此版本中修复了此问题。
* Zendesk #33572 - VideoAnalyticsProvider广告开始崩溃。 使用VHL+Nielsen联合SDK版本的VideoHeartbeat.jar的正确组合修复了此问题。
* Zendesk #33355 - Fire TV:删除15秒问题。 TVSDK方的任何修复均不在其终端和第三方验证。

**版本1.4.40(1764)**

* Zendesk #33068 - Amazon lip sync issue on new device. 此版本中修复了口型同步问题。
* Zendesk #32215 - Android TVSDK 1.4.38安全问题 `[Hotlist]`。 更新至最新的OpenSSL-1.1.0和curl-7.55.1。
* Zendesk #32920 —— 广告中断内的白屏，无广告中断完成。 修复了VPAID容器可能处于挂起状态并处理Facebook VPAID广告通常在一个\&amp;lt;AdParameters\&amp;gt中返回多个CDATA块的问题；VAST节点。

**版本1.4.39(1744)**

* Zendesk #28976 —— 授权许可请求需要超过一秒钟。 当使用POST的DRM许可证请求调用正在执行时，Curl会添加额外的“期望：100-continue”标题。 删除了TVSDK中的“Expest:”标题。
* Zendesk #27707 - CSAI环境不支持CUE IN标记以及早返回或返回内容。 为多个机会生成器提供支持。

**版本1.4.38(1722)**

* Zendesk #21590 —— 最新源构建中的视频性能和跟踪

在TVSDK中集成和认证VHL 2.0，通过降低API的复杂性来降低VideoHeartbeatsLibrary实现中的障碍。

* Zendesk #29688 —— 支持Android O Beta客户。

对新Android测试版的TVSDK支持。

**版本1.4.36(1713)**

* Zendesk #27392 - Android上的内容跳过

为了容许解密，Android TVSDK错误地将非iframe内容的字节范围扩大了16字节。 Iframe流需要扩展，但非iframe流不需要扩展。

**版本1.4.34(1702)**

* Zendesk #27638 - Leak in cURL INet object

当保持在cURL连接中使用的共享管理器和DNS缓存时，Posix cURL INet对象正在泄漏。

通过从INet解构程序中删除Posix cURL INet对象，解决了此问题。

**版本1.4.33(1694)**

* **OpenSSL库**

OpenSSL库已使用OpenSSL版本1.0.2j进行更新。

* Zendesk #21701 —— 发送1401 CRS请求的原始创意URL，而不是标准化的URL。
通过发送原始创意URL可解决此问题。

* Zendesk #25023 —— 长持续时间视频回放：视频冻结、屏幕闪烁通过为CenturyLink机顶盒设备设置最大视频格式尺寸，解决了此问题。

* Zendesk #27460 —— 新的Akamai帐户无法处理POST cdn请求。
更新了代码，将广 `cdn.auditude.com` 告请求设为GET而非POST。

* Zendesk #28245 —— 当应用程序从后台进入前台时，播放状态未正确通知通过正确恢复播放状态以在应用程序返回到前台时播放或暂停，此问题得以解决。

**版本1.4.32(1682)**

* Zendesk #25779 —— 当在WebView中启用JavaScript时，使用TVSDKAndroid 4.2及更低版本发现的安全漏洞存在安全漏洞。 对于运行OS 4.2或更低版本的设备，已禁用WebView by TVSDK。 这将禁用这些设备上TVSDK中的VPAID广告。

* Zendesk #26890 —— 处理参考的“屏幕”状态（开／关）的问题 播放器当Adobe视频引擎(AVE)从SUSPENDED状态恢复时，DefaultMediaPlayer不更新其状态。 因此，即使AVE处于“播放”状态，DefaultMediaPlayer仍保持为SUSPENDED状态。 通过在从AVE接收PLAY状态时将DefaultMediaPlayer状态设置为PLAYING，即使DefaultMediaPlayer的当前状态为SUSPENDED，此问题已得到解决。

**版本1.4.31(1675)**

* Zendesk #21974 —— 空对象导致的例外
   * AdIndex在null时很少递增。 这可能是由于为前置adBreak收到的API调用不正确所致。 修复了数据类型以避免此类例外

* Zendesk #24714 —— 关闭无关的日志记录
   * 更新了TVSDK以关闭无关的日志记录

* Zendesk #24488 - Fire TV上的AV同步问题
   * 通过改进AV解码器线程的处理来修复。 具体而言，每当修改输入或输出帧队列时，就运行特定于帧的内容类型的解码器线程。

* Zendesk #26551 —— 修复CRS故障
   * 当请求为HEAD(http head)时，我们无需读取内容，因为它为空。 尽管可以尝试读取它，但旧版Android(4.0.x)在我们调用read()时挂起，而较新的Android在调用read()时返回正确值(-1)。 基于此，将代码更改为不读取“head”的内容

* Zendesk #26696访问TrickPlayManager时空指针异常
   * 通过在使用TrickPlayManager对象之前检查该对象是否不是null来修复。

**版本1.4.30(1659)**

* Zendesk #22675资产持续时间未针对实时／线性流进行更新通过在PTVideoAnalyticsTrackingMetadata中提供新的APIassetDuration来解决此问题，该API提供了实时和线性流的资产持续时间。

* Zendesk #25853切换频道时TVSDK中的内存泄漏问题解决了在下载文件时重置或释放MediaPlayer时文件读取缓冲区泄漏的问题。

**版本1.4.29(1653)**

* Zendesk #21200 —— 当应用程序处于后台时，播放器不会从挂起状态恢复当播放器在发出流切换信号后被挂起时，该分辨率允许播放器在从挂起状态恢复播放器时执行流切换，而不是恢复到先前的位置。

* Zendesk #23412 —— 如果您在广告中断的最后3秒内点击任何广告，播放器会被卡在黑框内。此问题与Zendesk #21200相同。

* Zendesk #23616 —— 跳过广告中断搜索在将来太长取决于广告插入类型（插入／替换）,TVSDK确定在计算中是否使用广告持续时间来确定广告中断端点。

* Zendesk #25078 - TVSDK DRM Android TV上的内存泄漏已找到并修复DRM适配器对象的内存泄漏。

* Zendesk #25067 - VideoEngineTimeline中的崩溃发生这种情况是因为对象没有正确清除，并且在对象被破坏后调用了事件。 通过添加检查以防止空异常，解决了该问题。

* Zendesk #25352 —— 设置自定义HTTP头通过向TVSDK的白名单中添加新的自定义头解决了此问题。

* Zendesk #25617 —— 实时流PTS翻转导致播放器中断和内存崩溃通过在段中间发生翻转时在DiferatedHTTPStreamer中添加PTS翻转处理，解决了此问题。

**版本1.4.28(1637)**

* Zendesk #23618 —— 咨询广告策略前广告中断事件触发解决此问题的方法是：在由于adInterprisation而跳过广告时不触发AD_BREAK_START和AD_START事件。 而是发送AD_BREAK_BRIPPED事件。

**版本1.4.27(1631)**

* Zendesk #23174 —— 调整视频大小时的性能问题通过证明新的API MediaPlayerView.setSurfaceFixedSize解决了此问题，它允许TVSDK从MediaPlayerView访问SurfaceHolder.setFixedSize()。

* Zendesk #24450 - TVSDK发出重复的广告请求当已用时间转换为长时间而非双倍时，出现此问题，此问题已得到修复。

**版本1.4.26(1627)**

* Zendesk #21436 - OpenSSL库更新至版本1.0.2h将OpenSSL库更新至OpenSSL版本1.0.2h
* Zendesk #23825 - Cookies未包含在回呼中。通过提供对android cookies的支持，修复了回呼。

**版本1.4.25(1620)**

* Zendesk #22900 - Live Adobe Primetime DRM流未在Android参考播放器上播放内存分配问题已得到修复。
* Zendesk #23176 —— 应用程序在尝试播放VPAID广告时崩溃由于应用程序不创建用于呈现VPAID广告的自定义广告视图，导致崩溃。 当没有自定义广告视图时，将忽略广告服务器响应中的VPAID广告，从而解决了此问题。

* Zendesk #23153 - SampleAES DRM Stream —— 在TVSDK参考播放器中播放停滞此问题与Zendesk #22900相同。

**版本1.4.24(1612)**

* Zendesk #20784 - Analytics:实时视频过渡的触发内容完成通过添加API(trackVideoComplete)来在实时／线性视频跟踪会话期间手动触发内容完成，解决了此问题。

* Zendesk #21977 VideoEngineplaceAdBreak/accept广告操作期间时间线崩溃
   * 在此期间，更新了以下库：
      * Adobe Mobile库到版本4.10.0
      * 版本1.5.6的VHL库
      * VHL-Nielsen库到版本1.6.7

通过在将广告添加到已接受的广告列表之前添加空选项，解决了此问题。

* Zendesk #22313使用Amilogic芯片组的STB的比特率不会超过1.2MT。通过预加载媒体编解码器功能和禁用Amilogic芯片组设备的无缝切换，解决了该问题。

* Zendesk #19520示例AES HLS资源未在TVSDK播放器中播放通过为示例AES加密的HLS流处理多个PMT描述符，解决了此问题。

**版本1.4.23(1602)**

* Zendesk #18852 —— 根据CRS规则更新创意选择逻辑通过添加JSON配置文件来指定创意选择优先级，解决了此问题。

* Zendesk #20861 - Android NT此版本通过删除直接使用Android平台本机库的功能提供对Android N的支持，这些库不再对运行于Android N上的应用程序可访问。

* Zendesk #21018 - Android N崩溃与ZD# 20861相同的分辨率。

* Zendesk #21266 - VideoEngineAdapter在Invalid_Key错误时崩溃Invalid_Key错误不包括来自AVE的描述，因此解析文本会导致NPE。 通过在onError期间为说明添加空检查，解决了此问题，然后解析说明。

* Zendesk #22286 —— 本机库正在分配内存读取键／片段，导致崩溃尝试同时加载具有多个键的清单时在Android上发生的崩溃已得到修复。

**版本1.4.22(1581)**

* Zendesk #17236 —— 带DRMT的HLS视频的不可靠播放头时间已修复LBA流的时间跳转，其中音频段开始时间与视频段开始时间不匹配。

* Zendesk #17680 - Selevision Andredo框上的视频播放冻结此设备上的视频解码器有时会在从输出缓冲区将视频帧出队时返回显着的输出时间跳变，并且此输出时间戳保持较高。 通过返回不支持的视频配 *置文件* ，解决了此问题，该错误不会迫使播放器重试同一配置文件或选择其他配置文件。

* Zendesk #19074 - FWD和REW特技播放期间的视频冻结通过添加新警告TRICKPLAY_ENDED_DUE_TO_ERROR来解决此问题，以通知应用程序trickplay已退出，且视频因不可恢复的错误而暂停。

* Zendesk #19574 - TVSDK不会为DRM或非DRM内容返回M3U8响应数据通过以下方式解决了此问题：

* Zendesk #19986 —— 某些设备（如Android TV）的操作行为已中断
* 将FILE_NOT_FOUND错误添加到条件。
* 当错误来自未找 *到的文件时* ，如果响应可用，则将URL和响应与错误描述分开。
由NVidia屏蔽OP支持引入的逻辑错误已修复。 在非NVidia屏蔽设备上，即使显示类型未知，也可以信任显示安全标记。

* Zendesk #20549 —— 处理陈旧的播放列表。 如果以前的提取没有收到新的区段，则通过将实时清单更新之间的间隔缩短为预期区段持续时间的一半，解决了此问题。

* Zendesk #20742 —— 在FireTV上回放实时内容时，内存使用情况似乎继续增加。崩溃是由已达到限制的JNI对象参考表引起的。 通过删除对在解码器重新启动期间创建的MediaFormat对象的引用，解决了此问题。

* Zendesk #21125 —— 提早从实时／线性广告中断(CSAI)返回。 添加了一个功能，该功能允许玩家在广告中断期间返回到主内容，如果玩家通过使用拼接机会检测器在广告提示中注册拼接。

* Zendesk #21334 - TVSDK ad request timeout value for third-party ad request. adRequestTimeout设置已添加到AdvertisingMetadata中，用于为广告调用启用全局超时。

**版本1.4.21(1566)**

* Zendesk #17781 - ADB屏幕捕捉不再工作通过添加DefaultMediaPlayer.create(Context, boolean secureSurface)API解决了此问题，该API允许屏幕捕捉。
要允许屏幕捕获，请为secureSurface传递false。
重要说明：我们强烈建议您不要在生产设置中启用此屏幕捕捉功能。

* Zendesk #19074 - FWD和REW特技播放期间的视频冻结问题解决了trickPlay可能在播放中冻结时发生的以下问题：

* Zendesk #19532 —— 隐藏式字幕显示不顺序
   * FHS会开始变戏法，但第一个iframe段中没有帧。
   * 在下载iframe段时，如果FHS达到错误条件，则它会退出trickplay并暂停播放。
   * Andorid MediaCodec实现会在要求刷新所有输入／输出缓冲区时，等待输入队列可用性的持续时间。
通过颠倒WebVTT提示的顺序，使多个重叠提示显示为“向上滚动”，解决了此问题。

* Zendesk #19574 - TVSDK不返回DRM或非DRM内容的M3U8响应数据在PTMediaPlayerItem.prepareToPlay中清单文件的初始加载中，如果加载失败，TVSDK不会向应用程序报告失败响应的正文。
通过允许TVSDK将失败响应作为错误报告给应用程序，解决了此问题。

* Zendesk #19701 —— 使用SAP/Dinstruction播放冻结已解决音频和视频在不连续处未对齐时播放器冻结的问题。

* 错误#PTPLAY-11162 —— 已解决对版本1.0.2f的OpenSSL库更新。

**版本1.4.20(1546)**

* Zendesk #17384 —— 功能请求：对AAC播放的ID3元数据支持从版本1.4.20开始，AAC媒体中的ID3标记已在Android的TVSDK中提供。

* Zendesk #18358 —— 播放器在位速率开关上冻结而出现不同步不连续的问题通过适当处理ABR拼接边缘情况解决了此问题。

* Zendesk #19232 —— 使用TVSDK 1.4.18的应用程序在旧版Amazon OS上行为异常4通过删除TVSDK播放器初始化过程中的隐藏Web视图创建，避免与不支持Android Web视图的设备发生冲突，解决了此问题。

* Zendesk #19585 —— 当发生自适应比特率转换时慢动作播放。
在ABR切换期间，如果新配置文件的音频采样率与当前配置文件的音频采样率不同，则播放会变得快速或慢速。 这是因为视频演示者没有收到音频格式已更改的通知。
通过确保在正确的位置设置通知标志，解决了此问题。

* Zendesk #19683 - SAP DAI回放——几秒钟内无音频。
对于TVSDK逻辑中的几种情况，当比较两个再现段的时间戳时，RENDITION_TIMEOUT_THRESHOLD将用作可接受的值范围，因为时间戳不能始终与0毫秒差值相匹配。 如果间隙在RENDITION_TIMEOUT_THRESHOLD的范围内，则假定该间隙为匹配。

RENDITION_TIMEOUT_THRESHOLD设置为100ms，但发现它对于某些流不足。 通过将RENDITION_TIMEOUT_THRESHOLD增加到200ms，解决了此问题。

* Zendesk #19699 - TVSDK无法在VTT子标题轨道之间切换通过在轨道发生变化时进行播放器转储并重新加载清单以及校正影响双字节WebVTT字幕轨道名称的UTF8字符串转换问题，解决了此问题。

* Zendesk #19717 - CC选项显示问题通过正确处理Unicode字符串解决了此问题。

* Zendesk #19910 —— 未检测到TIT2 ID3标记通过提供对ID3 v2.4字符串编码的更全面支持和对ID3 v2.3的支持，解决了此问题。

* Zendesk #20135 - TVSDK正在为VOD内容触发多个onComplete。
通过在正确的位置而不是状态更改事件的完整情况添加post_roll_complete事件监听器，解决了此问题。

**版本1.4.19(1521)**

* Zendesk #4180 - TVSDK不强制使用HDCP。
   * 这是对此票证的部分修复，仅解决NVidia屏蔽设备的问题。
您必须使用Nvidia Shield中正确实现的HDCP检测API来动态跟踪HDCP状态。

* Zendesk #18358 - TVSDK在不同步不连续的情况下冻结在比特率开关上。
   * 通过添加新警告来检测PTS不连续性，并强制PTS检查重做搜索每个ABR交换机的正确段，解决了此问题。
要修复冻结问题，对mediaPlayer.setCustomConfiguration方法的调用应包含forcePTSCheckForABR作为参数。

* Zendesk #19038 - Asus Zenpad 10上没有实时流。

   通过预加载媒体编解码器信息来解决此问题，因此您不会在运行时查询该函数。

* 以下问题与Zendesk #19038相同：
   * Zendesk #19483 - TVSDK在英特尔平台上崩溃。
   * Zendesk #19171 - Asus Memo Pad 7上的Android 5.0崩溃

**版本1.4.18(1503)**

* Zendesk #3324 - Primetime广告报告不跟踪VMAP中没有广告媒体的广告中断。
当广告中断为空时，广告中断开始和完整跟踪事件不会被ping。 通过在空广告中断（如VMAP AdBreak）上发送广告中断开始ping以有效的AdSource点，解决了此问题。

* Zendesk #18229 - SetCCVisibility(VISIBLE)在MediaPlayer.reset()调用后被忽略通过添加setCCVisibility(Visibility.INVISIBLE)解决了此问题；到MediaPlayer类中的reset()函数。

* Zendesk #18328 - Amazon Fire TV第2代设备上60FPST内容的丢帧问题通过将编码的FPS应用于睡眠时间决策并使用更好的编码的FPS预测逻辑来解决此问题。

**版本1.4.17(1472)**

* Zendesk #2231 —— 从获取MediaPlayerNotification中不可用的清单返回的错误通过在出现解析错误时包含清单的响应正文解决了此问题。

* Zendesk #17703 - VideoEngineView在视频播放期间不会阻止屏幕截图setSecure方法自API 17起就可用，但由于API 17涵盖4.2、4.2.1和4.2.2，因此不知道哪个会引发异常，或是否特定于设备。 通过将VideoEngineView.setSecure打包到try catch子句中，解决了此问题。

* Zendesk #17919 —— 内容搜索导致心跳错误输入数据无效位置错误是由于在预置启动搜索后开始搜索时生成的心跳调用而导致的。 此问题已解决。

**1.4.16a** (1454a)

* Zendesk #18215 —— 某些AES流无法加载。
通过在加载AES密钥之前检查配置文件DRM元数据大小，解决了此问题。

**版本1.4.16(1454)**

* Zendesk #3875 - Tab S在播放期间崩溃由于TVSDK现在直接使用httpurconnection而不是curl，因此还原OKHTTP对CRS Auditude的依赖关系。 通过在进行任何其他JNI调用之前清除例外，解决了该问题。

* Zendesk #4487 —— 跟踪内容的线性通道通过允许在线性流播放会话期间重新初始化视频心跳跟踪器，解决了该问题。

* Zendesk #17919 - Android —— 内容搜索导致心跳错误已解决心跳处于错误状态时在章节中存在搜索的问题。

* Zendesk #18053 - Adobe Primetime在Marshmallow上崩溃当TVSDK库使用执行YUV -> RGB颜色转换的neon代码时，TVSDK在Android M OS上崩溃。 通过使用非Neon版本的代码更新导致此问题的函数解决了该问题。

* Zendesk #18072 - Android M —— 应用程序崩溃在检查配置文件和级别是否受支持时，在调用MediaCodecList和MediaCodecInfo API时会发生崩溃。 通过提前加载所有编解码器信息来提供临时工作，以避免仅在需要编解码器信息时调用这些API，解决了该问题。

* Zendesk #18074 - Nexus上Android 6.0的阿拉伯字幕不工作通过为Android提供CTS字体映射支持，问题得以解决。

**版本1.4.15更新(1438)**

* Zendesk #17437 —— 使用某些AES流启动VOD内容的长延迟。
要解决此问题，如果清单中列出多个键，请并行下载所有AES键。

**版本1.4.15(1435)**

* Zendesk #4278 - Android机顶盒上的故障（当自适应比特率发生变化时）。
修复是添加对无缝ABR交换机的支持，该交换机具有最新的Android媒体编解码器。

* Zendesk #17063 —— 调用mediaPlayer.reset()会导致视频引擎重置错误。
修复是在调度ErrorEvents时包括VideoEngineExceptions中的原始MediaErrorCode。

* Zendesk #17130 —— 在FireTV上看到的比特率发生变化时，短暂但引人注目的暂停。
（与上面的#4278相同）修复是添加对无缝ABR交换机的支持以及最新的Android媒体编解码器。

* Zendesk #17666 —— 恢复内容时的其他广告标记、意外或无广告。
修复了对视频点播(VOD)内容执行prepareToPlay时，初始搜索在本地时间而不是虚拟时间执行的问题。

* Zendesk #17437 —— 使用某些AES流启动VOD内容的长延迟。
修复是当清单中列出多个密钥时，并行下载所有AES密钥。

* Zendesk #17851 - Android TV - Black Frame在ABRT中修复是指定KEY_MAX_WIDTH和KEY_MAX_HEIGHT以启用自适应播放。

**版本1.4.14(1415)**

* Zendesk #3875 - Tab S在播放期间崩溃。
需要额外的修复以防止崩溃。

* Zendesk #17245 - Fallback on Android TV is not function（Zendesk #17245 - Fallback on Android TV无法正常使用）。
修复了在启用回退时播放挂起，且VMAP响应有空广告中断的其他问题。

**版本1.4.14(1412)**

* Zendesk #17245 - Fallback on Android TV is not function.
删除了在回退广告上禁用创意重新打包的限制。

**版本1.4.13(1388)**

* Zendesk #3502 —— 广告中断期间基于HLS客户端的故障转移支持在广告中断期间发生更新实时配置文件错误时允许故障转移到主清单。

* Zendesk #3875 - Tab S在播放期间崩溃要解决HttpUrlConnection与cURLm之间的冲突，请使用第三方库。

* Zendesk #4450 —— 问题设置内容解析器中单个位置的自定义元数据向“业务机会”设置添加setter。

**版本1.4.12(1388)**

* Zendesk #2751 - CSAI和CRS|增强：处理某些媒体文件URL中的动态元素。
更新了Creative Repackaging Service以正确处理带有动态创意URL的广告。

* Zendesk #3965 —— 从滴播切换回正常播放会在开始播放之前向前跳转一点。
   * Fix包含TVSDK，它返回在速率更改前的时间，直到所有变量都更新，而不是尝试计算GetStreamTime。
   * 修复了在流末尾附近更改特技播放速度时的崩溃问题。
   * 修正了特技播放期间的当前时间计算。

* Zendesk #3978 - Trickplay at 8x and 16x frequences.
   * 始终以最低的位速率选择特技播放配置文件以避免持续缓冲。
   * 增加跳帧间隔以实现高特技播放率。
   * 修复了在特技播放期间达到目标长度后缓冲区继续增大的问题。

* Zendesk #3992 —— 更多Trickplay速度。
TrickPlay已更新为接受16倍以上的速率；+/- 32、+/-64和+/-128现在也允许。

* Zendesk #4007 —— 将GEOB对象解释为时间轴元数据（Android和Web）的一部分。
添加了setByteArray和getByteArray API。

* PTPLAY-7301 —— 在随机访问点即时启动。
“即时启动”已更新，以允许非零起始点。

**版本1.4.11(1363)**

* Zendesk #2076 —— 在Motorola Xoom上使用Android 4.0.3播放视频时，经常断断续续地向白名单中添加设备，以防止它们尝试播放高调内容。

* Zendesk #2197 —— 跟踪广告错 `[Ads]` 误调度OperationFailedEvent并带有警告通知。 

* Zendesk #3304 —— 未填充VAST 3.0 `[ERRORCODE]` 宏
   * 如果内联广告的创意不佳，则会显示错误代码400。
   * `[ERRORCODE]` 宏将采用URL编码

**版本1.4.10(1354)**

* Zendesk #2941 —— 实时资产在可搜索范围中没有“0”以前，当搜索到实时流的开头时有3个段缓冲区，现在可以搜索到实时流的最开始（即第一个段的开始）。

* Zendesk #3169 —— 借助Adobe Analytics集成更新参考播放器参考播放器已使用Adobe Analytics库进行更新，作为示例植入。 
* Zendesk #3299 —— 无法解释的技巧播放行为
   * 修复了在停止特技播放后返回播放状态可能需要数秒（有时为25秒以上）的错误。
   * 修复了在同一媒体上再次调用特技播放可能导致流在当前时间冻结的错误。
* Zendesk #3433 - Android和Flash —— 字幕问题

GetLine for WebVTT不遵守数据包的&lt;CR>&lt;LF>调整长度；最后一个题注可能包含以前题注中的字符。

* PTPLAY-6243 —— 增强参考播放器以捕获调试信息

Android示例参考播放器已得到增强，并提供了打开调试日志和通过电子邮件发送结果的选项。 此选项位于引用播放器的“日志”菜单下。

**版本1.4.9(1332)**

* Zendesk #2649 —— 在初始缓冲区已满之前，发生缓冲区完成

搜索后，视频引擎在视频演示者准备好播放之前将状态设置为“播放”的可能情况。 在搜索前缓冲区状态为高时发生。 通过通知视频引擎缓冲区状态低来修复。 由于视频引擎缓冲区状态较低，调用“播放”将导致状态更改为BUFFERING而不是PLAYING。 当状态变为“播放”时，回放将恢复。

* Zendesk #2846 —— 增强请求：提供为Auditude库发出的调用设置不同用户代理字符串的功能

已添加一个新API，用于为与广告相关的调用设置用户代理auditudeSettings.setUserAgent(&quot;user/agent&quot;)。 如果未设置用户代理，则将使用默认代理。 这仅影响广告相关呼叫的用户代理，媒体呼叫的用户代理保持不变，即“Adobe Primetime”+&lt;default useragent>。

**版本1.4.8(1324)**

* Zendesk #1218 - 106000.33本地错误……如果在DiferatedHTTPStreamer::ThreadParseManifest()中加载清单失败，请检查URL域是否为localhost，如果是，则将域更改为127.0.0.1并重新调用ThreadParseManifest。
* Zendesk #3072 —— 自动切换到较低比特率。 更改了缓冲区长度计算以跳过零PTS有效负荷。
* Zendesk #3168 —— 仅为前10秒显示WebVTT字幕。
* Zendesk #3193 —— 在TVSDK中请求配置文件更改API，已添加PlaybackEventListener.onProfileChanged()。

**版本1.4.7(1311)**

* Zendesk #2197 —— 跟踪广告错误。 为资产添加的通知加载清单失败
* Zendesk #2575 - PSDK在视频之前忽略MARK自定义流内广告
* Zendesk #2719 - Win Death with auditude ads，修复了重定向到auditude插件中的相对url时的信标跟踪
* Zendesk #2760 —— 在TrickPlay模式中忽略的DINSTRUCTION标签
* Zendesk #2805 —— 播放开始时播放器崩溃，与Zendesk #2719相同的修复
* Zendesk #2817 - Android播放器——播放器有时挂起并停止播放，通过将解码缓冲区从2.0秒扩展到3.0秒来修复
* Zendesk #2839 - Adobe Primetime PSDK是否支持ARMv8芯片组？新增了Galaxy S6上的崩溃修复。
* Zendesk #2885 - Auditude崩溃播放，与Zendesk #2719相同的修复
* Zendesk #2895 —— 回放10分钟后，HLS实时故障始终如一
* Zendesk #2925 —— 当我们将数据包排到输入队列时，在某些设备上对Android开发版本(1.4.5)的反馈，如果PTS为负，则解码器会进入一个奇怪的状态，而我们将来的数据包总是得到一个负输出PTS。 如果输入PTS为负值，则该修复会将其设置为零以避免此问题。
* PTPLAY-4645 —— 关闭openssl中的RC4密码支持。 已知有RC4漏洞。 这意味着，如果尝试连接仅支持RC4的服务器，则该连接将失败。

**版本1.4.6(1282)**

* Zendesk #2192 —— 在糟糕的网络条件下，比特率并不总是会降低，通过删除快速交换机实施来修复。
* Zendesk #2631 - Android上的阿拉伯语字幕：通过调整阿拉伯字体的字体大小，可以修复多行文本出现截断的问题。
* Zendesk #2844 - Buffering on Note 4 and Fragment download time is not caracte.

通过在带宽计算中增加视频段下载之间的延迟并使下载时间计算逻辑使用完全请求周期时间来修复此问题。

* Zendesk #2908 —— 阿拉伯字幕在Nexust 5、6和7上不工作，通过为阿拉伯文脚本添加2种备用字体来修复。
* PTPLAY-4627 —— 将Nielson appsdk更新至版本1.2.3.7
* PTPLAY-5084 - Live Master Manifest更新故障转移支持

**版本1.4.5(1248)**

* Zendesk #1757 —— 修复了某些视频比特率配置文件中仅播放音频或播放器崩溃、Nexus 4和Nexus 7崩溃的问题
* Zendesk #2072 - AdEvent的TimedMetadata不包含仅“http”的完整URL
* Zendesk #2192 —— 在糟糕的网络条件下，比特率并不总是较低
* Zendesk #2256 —— 访问主播放列表，更新了PSDK以为主播放列表上订阅的标记调度timedMetadata事件。
* Zendesk #2269 —— 借助WebVTT，两种不同的子标题语言同时出现在屏幕上
* Zendesk #2417 —— 播放器尝试在播放开始前下载字幕，WebVTT使用错误的段号变量进行段号匹配。 只有区段索引从零开始的媒体才会显示错误。
* Zendesk #2470 —— 当挂起后发生比特率更改时，PSDK不会从SUSPED状态返回。 在由RestoreGPUResource调用智能搜索（从挂起状态恢复播放器）和之前检测到的流切换的特殊情况下，智能搜索无法完成并导致持续缓冲。
* Zendesk #2451 —— 隐藏式字幕“底部插入”，向字幕代码添加了“bottomInset”参数
* Zendesk #2480 —— 禁用HTTP 302重定向优化，增加了对设置useRedirectedUrl属性的支持
* Zendesk #2486 —— 第三方信标
* Zendesk #2547 —— 阿拉伯语字幕：文本应右对齐

**版本1.4.4(1195)**

* Zendesk #1158 - Playback fails on Wawei Valiant(Y301A1)
* Zendesk #1709 —— 媒体大小不正确，视频已拉伸
* Zendesk #1757 —— 仅在具有相同spa/pps数据的流之间进行配置文件切换后播放的音频
* Zendesk #2095 - HTTP 307状态（重定向）导致Adobe播放器停止播放
* Zendesk #2126 —— 最后一个ADEVENT缺少TimedMetaData事件，在最后一个段之后存在的预订标记未从AVE报告给PSDK
* Zendesk #2227 - VideoEngine nativeReset和nativePause中的锁定
* 错误#3921755 - OpenSSL库更新至版本1.0.1L

**版本1.4.3(1173)**

* Zendesk #1591 - RENDITION_M3U8_ERROR
* Zendesk #1870 —— 隐藏式字幕打开和关闭
* PTPLAY-1818 —— 倒回特技剧在广告停止，而不是翻过它
* PTPLAY-2736 —— 当具有WebVTT字幕的流完成播放时，屏幕上会显示以前显示的WebVTT字幕
* PTPLAY-3773 —— 当在广告位置之后启动流播放时，不播放中间广告

**版本1.4.2**

* Zendesk #1561 —— 黄金时段基于HLS客户端的故障转移支持。 将使用程序日期时间解决故障转移问题
* Zendesk #1590 - LoadInfo.MediaDuration始终为0（未修复仅音频）
* Zendesk #1626 —— 播放器中的潜在内存泄漏。 不是实际的内存泄漏，NotificationHistory保存最近1000个通知的问题，已减少到100个。
* Zendesk #2192 —— 在糟糕的网络条件下，比特率并不总是较低

**版本1.4.1(1121)**

* Zendesk #1951 - VideoEngine.nativeReset()中在4.0.x设备上锁定
* Zendesk #2064 —— 基于Intel的特定Android设备上的本机崩溃SIGSEGV
* Zendesk #2075 - VideoEngine.nativeReleaseGPUResource on 4.0.x devices注：此版本是***必需****，用于支持Android 5.0(Lollipop)
* Zendesk #1513 - Android Lollipop支持
* Zendesk #1709 —— 媒体大小不正确，视频已拉伸
* Zendesk #1871 —— 查看包含WebVTT字幕的实时流时，WebVTT字幕偶尔会消失，然后重新显示
* Zendesk #1996 - PSDK 1.4.0中不显示时间轴标记
* Zendesk #2046 - Crassur with PSDK 1.4.1.1113，修复了从auditude中不返回广告时实时流的崩溃问题
* 错误#3769657 —— 将curl的版本更新至7.38.0
* PTPLAY-1575 —— 当ABR播放以仅音频流开始，然后切换到音频／视频流时，在音频继续时，视频从不呈现
* PTPLAY-2499 —— 更新至OpenSSL至版本1.0.1j以解决最近的漏洞
* PTPLAY-2632 —— 在Android Lollipop上完成中间广告后，视频无法恢复
* PTPLAY-2678 —— 在Android Lollipop上进行实时寿命测试期间视频停止

**版本1.4.0**

* Zendesk #1024 —— 通过清单从流中删除广告的功能
* Zendesk #1293 —— 隐藏式字幕轨道选择问题。
* Zendesk #1590 - LoadInfo.MediaDuration始终为0,mediaDuration现在显示正确的值。
* Zendesk #1629 —— 播放器／应用程序在Galaxy S4上的广告播放结束时崩溃
* Zendesk #1674 - ClosedCaption未显示，当0x03 ETX代码缺失时，708字幕显示正确。
* PTPLAY-2157 - Getter返回默认的隐藏字幕样式，即使在流上设置不同样式并以可视方式进行验证后也是如此。 “隐藏式字幕”样式属性现在将显示已设置的值。

## 1.4中的已知问题 {#known-issues-in}

**版本1.4.31**

* PTPLAY-16803 —— 由于字幕系统需要视频才能工作，隐藏式字幕将不能处理仅音频内容。 没有视频，就没有视口尺寸，没有视口尺寸，就无法显示任何字幕图形。
* PTPLAY-1634 - Same Subscribed标签在不同实时窗口中具有不同的时间戳。 移动实时窗口时，其中的同一标签应具有相同的时间戳。 但是，有时，即使同一标签也具有不同的时间戳。
* PTPLAY-3197 —— 在连续播放约1小时后，Acer Iconia设备上出现信号11 SIGSEGV错误，导致崩溃
* PTPLAY-3310 —— 使用一些较低比特率的音频，Acer Iconia上的音频变得生硬／断断续续
* PTPLAY-3355 —— 在持续播放约1小时后，Motorola Xoom上的4.0.x发生死亡事件。
* PTPLAY-3557 —— 在广告中断时倒回导致流完成
* PTPLAY-7079 - Android客户端上的播放窗口不能与安全停止／硬停止一起使用
* 错误#3760144 —— 在Kindle Fire 7和Samsung Galaxy Nexus等某些设备上暂停流时，分辨率可能会移动或显示为脉冲。 仅可观察
* 错误#3761170 - seekToLocal in Live with Ads无法返回到广告内容中，它最好使用实时流的currentTime API
* 错误#3763370 —— 带有广告的实时流偶尔会在应该只有一个广告时一起显示两个广告标记。 这些广告标记表示同一广告，并且只有一个
* 错误#3763373 —— 在VOD流中通过广告搜索时，广告标记可能会短暂消失。 广告标记会恢复，并且时间线上没有其他不利影响
* 某些设备有已知的播放问题。 请参 [阅1.4中的已知设备问题](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14)。
* 引用实现——特技播放未在范例应用程序中实现
* 在某些Android TV设备上，由于以下过渡点处的解码器重置，可以看到黑帧：
   * 进入和退出戏剧模式
   * 在较晚绑定音轨之间切换
   * 从广告到主内容。

**版本1.4.23**

* “隐藏式字幕”不能用于仅音频内容，因为字幕系统需要视频才能使用。 没有视频，就没有视口尺寸，没有视口尺寸，就无法显示任何字幕图形。
* 从版本1.4.23开始，TVSDK将不支持Gingerbread OS 2.3。这是因为TVSDK使用以下专用Android库收集有关Gingerbread OS设备的硬件信息：

   * `libstagefright.so`
   * `libcutils.so`

在Android N版本中，Google已删除了对这些专用库的访问权。 Gingerbread OS目前在全球Android操作系统市场中的份额不到1%，因此，在版本1.4.23之后，Gingerbread OS将不再受TVSDK支持。
使用版本1.4.23（包括对Android N的支持）或更高版本时：
* 更新您的应用程序以使用minSdk版本11。
* 如果您的最终用户运行的是OS 2.3，则SDK版本低于应用程序的minSdkVersion。 系统中止应用程序的安装或升级。
* 如果最终用户运行的版本高于OS 2.3，则应用程序将正确安装。

如果更新minSdk版本：

* 如果最终用户运行的是OS 2.3，则安装了应用程序，但播放将无法进行。
这适用于更新和新安装。
* 如果最终用户运行的系统高于OS 2.3，则应用程序安装正确，内容可正确播放。

**版本1.4.22**

* 当剪接标签和剪接标签彼此过于接近时，早期退出广告不适用于某些中间广告。

**版本1.4.2**

* 在广告中断时倒回导致流完成。

Media Player在“特技播放”倒回操作过程中，当其到达广告边界时，会错误地发送MediaPlayer PlayerState。完成。 播放器在特技播放模式下应忽略此事件，否则SDK将正确处理状态。

**版本1.4.0(1086)**

* PTPLAY-1634 —— 同一“订阅”标签在不同实时窗口中具有不同的时间戳。 移动实时窗口时，每个窗口中的同一标签应具有相同的时间戳。 但是，有时，即使同一标签也具有不同的时间戳。
* PTPLAY-2541 - COMPONENT_CREATION_FAILURE有时在多次切换到／从封锁期中的备用流时显示
* 错误#3726865 —— 如果多比特率LBA流从仅音频流开始，则切换到音频／视频流时，视频不会显示。 从音频／视频流开始将不显示此问题，并且可以在音频流和音频／视频流之间成功切换
* 错误#3760144 —— 当某些设备（如Kindle Fire 7和Samsung Galaxy Nexus）上的流暂停时，分辨率可能会移动或显示为脉冲。 仅可观察
* 错误#3761170 - seekToLocal in Live with Ads无法重新搜索广告内容；最好将currentTime API用于实时流
* 错误#3763370 —— 带有广告的实时流偶尔会在应该只有一个广告时一起显示两个广告标记。 这些广告标记表示同一广告，并且只有一个
* 错误#3763373 —— 在VOD流中通过广告搜索时，广告标记可能会短暂消失。 广告标记会恢复，并且时间线上没有其他不利影响
* 某些设备有已知的播放问题。 有关详细信息，请参 [阅1.4中的已知设备问题](https://helpx.adobe.com/primetime/release-notes/tvsdk-1-4-android.html#Knownissuesin14)。
* 引用实现——特技播放未在范例应用程序中实现。

## 1.4中的已知设备问题 {#known-device-issues-in}

| 设备 | 芯片组 | 问题 | 原因 | 解决方法 |
|--- |--- |--- |--- |--- |
| Droid X | TI OMAP3 | ABR延迟是预期的，因为它正在重新启动解码器。 |  |  |
| HTC Desire（与HTC Desire HD不同） | QSD8250 | 无法播放视频。 返回VIDEO_PROFILE_NOT_SUPPORTED错误。 | Desire不提供正确的硬件解码器。 它提供了Stagefright的SW解码器。 | 重新启动设备。 |
| HTC EVO 4G | QSD8650 | 无硬件解码器。 | Qualcomm没有硬件解码器。 | 升级到Android 4.x。 |
| Kindle FireSystem版本6.0 | TI OMAP4 | 不播放HLS流。 AIR上的视频不起作用。 |  | 升级到系统版本6.3。 |
| Kindle Fire HD | TI OMAP4 | 可以进入无法播放视频的状态。 返回VIDEO_PROFILE_NOT_SUPPORTED和UNRECOVABLE_ERROR错误。 | 当应用程序未完全关闭硬件解码器时（例如，在遇到崩溃后），硬件解码器会进入不可恢复状态。 在设备上的本机应用程序上也会发生这种情况。 | 重新启动设备。 |
| Kindle Fire HD 8.9 | Snapdragon 800 | AVE在多个ABR交换机后崩溃。 |  |  |
| Motorola Atrix | Tegra2 | 与AIR相比，AVE的整体性能问题。 音频／视频不同步，在播放9到15分钟后，视频回放将冻结。 崩溃。 | 可能与我们在AIR上启用的openGLES相关。 正在接受调查。 |  |
| Nexus 7（第2代） | S4Pro APQ8064(Qualcomm) | 暂停电影超过30分钟时，设备挂起。 | 已报告给Google的设备问题。 | 应用程序应超时，以便不允许长暂停状态。 |
| Nexus S(GB) | 蜂鸟 | 无法使用硬件解码器播放任何视频。 | Nexus S中没有基于Stagefright的硬件解码器，因此，对于Android 2.3，我们使用SW解码器。 | 升级到ICS。 |
| Nexus S(ICS) | 蜂鸟 | 视频偶尔闪烁。 | 坏数据可能导致解码器进入坏状态。 | 重新启动设备。 |
| Nook tabletAndroid OS:2.3 | TI OMAP 4 | 视频不播放，应用程序挂起。 | Stagefright在运行应用程序几次后进入不稳定状态。 对mediaplayer::QueryCodec的调用挂起。 | 重新启动设备以重置状态。 |
| Samsung Galaxy ACE | Qualcomm MSM7227 | 无法安装SampleMediaPlayer应用程序。 | 使用ARM v6而不是更常见的ARM v7芯片组。 FP/AIR不支持此设备。 |  |
| Samsung Galaxy ACE2Android OS:2.3.6 | NovaThor U8500 | 无法播放视频。 | 此芯片组是AVE中Android预ICS的未知解码器。 |  |
| Samsung Galaxy S2(GT-I9100) | Exynos | 此设备的视频性能不能达到标准。 | HW解码器返回具有错误PTS的解码帧。 看起来解码器使用的是解码时间而不是呈现时间。 |  |
| Samsung Galaxy S2 GAndroid OS:2.3.6 | TI OMAP4 | 启动视频时崩溃。 |  | 升级到Android 2.3.7或4.x。 |
| Samsung Galaxy S3(I747) | Qualcomm MSM8960 | 视频会间歇性地冻结并仅播放音频，然后变得无响应。 |  |  |
| Samsung Galaxy S3 I747M | SAMSUNG_M2ATT | 视频冻结。 | 调查。 |  |
| Samsung Galaxy Tab 1 v10.1 | 特格拉2 | MBR过渡最多可能需要三秒。 | 作为MBR崩溃的修复，我们为每个流交换机重新启动解码器，这可能需要三秒钟。 |  |
| Samsung Galaxy Y |  | 无法安装SampleMediaPlayer应用程序。 | 使用ARM v6而不是更常见的ARM v7芯片组。 FP/AIR不支持此设备。 |  |
| Xoom | 特格拉 | 为进行切换而丢弃了几帧。 解码器未重新启动。 | OMXAL限制。 |  |

## 实用资源 {#helpful-resources}

* 请参阅 [Adobe Primetime学习和支持页面上的完整帮助文档](https://helpx.adobe.com/support/primetime.html) 。
