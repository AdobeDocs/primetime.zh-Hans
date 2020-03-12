---
title: 适用于Android的TVSDK 1.4至2.5(Java)
seo-title: 适用于Android的TVSDK 1.4至2.5(Java)
description: TVSDK 2.5在性能、安全性、更好的集成等方面比版本1.4提供多种优势。
seo-description: TVSDK 2.5在性能、安全性、更好的集成等方面比版本1.4提供多种优势。
uuid: aaab7aec-cb5b-4840-82e8-7112a8d98a8a
contentOwner: vishgupt
products: SG_PRIMETIME
topic-tags: migration
discoiquuid: 8d9136bf-b3ae-450c-bd8a-0bb246527886
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# 适用于Android的TVSDK 1.4至2.5(Java) {#tvsdk-to-for-android-java}

TVSDK 2.5在性能、安全性、更好的集成等方面比版本1.4提供多种优势。

TVSDK解决了最重要的设备上的最大挑战。 Android继续占据着全球主导地位，占据了86%的市场份额。 在Android上迁移到TVSDK将优化播放性能，从而提高用户参与度并加快上市速度，同时支持新的内容格式。

## 迁移到TVSDK v2.5的优势 {#benefits-of-migrating-to-tvsdk-v}

TVSDK 2.5在性能、安全性、更好的集成等方面比版本1.4提供多种优势。 继续阅读，快速了解迁移到此新版本的好处。

根据第三方基准测试研究，v2.5的启动时间缩短了5倍，丢帧减少了3.8倍。

| 性能功能 | 说明 |
|--- |--- |
| VOD和实时的即时启动 | 预加载初始段，以便在频道切换时立即播放VOD和实时线性流，以获得类似电视的体验。 |
| 延迟广告加载 | 在并行线程中解析中间卷广告时，在预卷或内容可用时立即开始播放。 |
| 永久网络连接 | 提高效率并缩短网络代码的等待时间，以提高回放性能。 |
| 改进的ABR逻辑 | 新的ABR逻辑基于缓冲器长度、缓冲器长度的变化速率和测量带宽。 这确保了ABR在带宽波动时选择正确的比特率，并且还通过监视缓冲长度变化的速率来优化比特率切换的实际发生的次数。 |
| 部分区段下载 | 只要有足够多的段帧可用于在客户端可靠地渲染视频，就立即开始播放。 |
| 并行下载 | TVSDK并行下载音频和视频段以取消混音内容以优化回放性能。 |

回放功能通过提供数字上的线性广播体验来提高消费者参与度。 此外，它还有助于您利用本机DRM（如Widevine）进行HD回放。

| 播放功能 | 说明 |
|--- |--- |
| MP4播放 | MP4短片无需重新转码为在TVSDK中播放。 |
| 虚线VOD内容播放 | 支持基本的DASH VOD播放用例。 |
| 使用ABR顺畅地播放 | 支持在HLS中使用低速率关键帧和更快速度的I-Frames快进和快退。 支持所有支持的帧的ABR。 |

这些功能对于满足工作室限制（如通过本机DRM回放HD）很重要。

| 功能 | 说明 |
|--- |--- |
| 基于分辨率的输出保护 | 播放只能限制为DRM要求允许的特定分辨率。 仅通过Primetime DRM提供。 |
| Widevine支持 | 支持DASH VOD流，以启用本机DRM用例。 |

直接计费增强功能无需每月创建手动计费报表。 VHL 2.0具有预建集成和更准确的跟踪功能，可缩短上市时间。

| 功能 | 说明 |
|--- |--- |
| Moat集成 | 支持从Moat中测量广告可见性。 |
| VHL 2.0 | 最新优化的视频心率库集成，可自动收集Adobe Analytics的使用数据。 |
| 故障转移支持 | 尽管主机服务器、播放列表文件和段出现故障，但还是实施了继续不间断播放的其他策略。 |
| 直接计费集成 | 将计费指标发送到Adobe Analytics后端，后端经Adobe Primetime认证，可用于客户使用的流。 |

>[!NOTE]
>
>v2.5中支持TVSDK v1.4的所有功能，但多CDN支持除外。

## 迁移过程概述 {#overview-of-the-migration-process}

从TVSDK 1.4顺利迁移到2.5需要更改到版本2.5库，重新编译，然后使用本文档帮助调试出现的任何问题。

TVSDK v1.4库不能与v2.5库一起使用并共存。 您必须将v2.5库与TVSDK 2.5一起使用，并迁移您的应用程序和集成以升级到TVSDK 2.5。本文档介绍如何更改应用程序代码以及如何解决重新编译过程中的错误。

psdk.jar文件使用第三方库支持不同的功能。 要防止删除库，请在文件中包括以下内 `proguard.cfg` 容：

```java
# Adobe TVSDK keep classes
-keep class com.adobe.** { *; }
-keep class com.google.android.exoplayer.**
{ *; }
```

在文 `build.gradle` 件中，您需要包含编译指令以包含基于TVSDK的JAR文件。 如果您的应用程序包含Adobe Video Analytics，则您需要在应用程序中包含编译指令，以获取Adobe Video Analytics集成所需的其他jar文件

```java
# Compile Adobe TVSDK jars compile files('libs/psdk-va.jar')
compile files('libs/VideoHeartbeat.jar')
```

本文档未涵盖多项细微更改。 有关API的细微更改，请 [参阅TVSDK 2.5 for Android Java API](https://help.adobe.com/en_US/primetime/api/psdk/javadoc_2.5/index.html)。 相应的C++ API参考有详细的说明。 有关类似的C++ API文档，请参 [阅适用于Android C++ API的TVSDK 2.5](https://help.adobe.com/en_US/primetime/api/psdk/cpp_2.5/index.html)。

随TVSDK一起分发的参考实现中介绍了API使用的多个示例。

## TVSDK v2.5中的API更改 {#api-changes-in-tvsdk-v}

新的、过时的和修改的API在下面进行了说明。

| TVSDK v1.4 | TVSDK v2.5 | 说明 |
|--- |--- |--- |
| 导入com.adobe.ave.drm .DRMAcquireLicenseSettings | 导入com.adobe.mediacore.drm .DRMAcquireLicenseSettings; | TVSDK 2.5 API中的所有类名以com.adobe.mediacore前缀开头。 这只是一个例子。 |
| MediaPlayerException、IllegalStateException或IllegalArgumentException | MediaPlayerException | 在2.5中，API仅生成MediaPlayerException。 |
| MediaPlayer.PlayerState(MediaPlayer.Event.PLAYBACK) | MediaPlayerStatus(MediaPlayerEvent.STATUS_CHANGED) | 在v2.5中，MediaPlayer.PlayerState已更名为单独的enum MediaPlayerStatus。 |
| DefaultMediaPlayer.create(getActivity()。getApplicationContext()) | MediaPlayer mediaPlayer = new MediaPlayer(getActivity()。 getApplicationContext()); | 用于创建对象的静态方法由公共构造函数替换。 |
| MediaPlayer.seekToLocalTime() | MediaPlayer.seekToLocal() | MediaPlayer.seekToLocalTime()方法现在称为MediaPlayer.seekToLocal()。 |
| closedCaptionsTrack.isActive() |  | 不可用 |
| 元数据节点 | 元数据 | 在v2.5中，Metadata类替换了v1.4 MetadataNode类的使用。 |
| DefaultMetadataKeys | 元数据键 | v1.4中的DefaultMetadataKeys在v2.5 enum MetadataKeys中。 |
| AdvertisingFactory | ContentFactory | v1.4中的AdvertisingFactory在v2.5中更名为ContentFactory |
| PlacementOpportunityDetector | OpportunityGenerator | 探测器被替换为发电机。 |
| mediaPlayer.getView()。notifyClick(); | mediaPlayer.notifyClick(); | MediaPlayerView的notifyClick()方法已移至MediaPlayer类。 |
| public ABRControlParameters(ABRPolicy abrPolicy, int nInitialBitRate, int nMinBitRate, int nMaxBitRate) | public ABRControlParameters(int nInitialBitRate, int nMinBitRate, int nMaxBitRate, ABRPolicy abrPolicy, int nMinTrickPlayBitRate, intMaxTPlayBitRate, intmaxTrickPlayBandwidthUsage, double dMaxPlayoutRate) |  |
| playbackInformation.getTimeToFirstFrame() |  | 不可用 |
|  | playbackInformation.get ExperiencedBandwidth() | TVSDK v2.5 QOSProvider具有新属性，用于确定流会话期间的可感知带宽。 |

### 删除的类 {#removed-classes}

将删除以下类，且没有对等类。

* `TimeRangeCollection`
* `PSDKConfig`
* `BaseLogger`
* `DefaultLogger`
* `Log`
* `Logger`
* `LogFactory`
* `NullLogger`

在参考实现中，最后六个类作为实用程序类可用。

## 命名空间更改 {#namespace-changes}

TVSDK 2.5 API整合了命名空间。

TVSDK 2.5 API中的所有类名以com.adobe.mediacore前缀开头。 TVSDK 1.4 API中的某些类名以com.adobe.ave开头。 相应的2.5类将com.adobe.ave更改为com.adobe.mediacore。 例如，请注意以下代码行中对1.4和2.5的更改：

```java
// TVSDK 1.4
import com.adobe.ave.drm.DRMAcquireLicenseSettings; import com.adobe.ave.drm.DRMLicense;
import com.adobe.ave.drm.DRMManager; import com.adobe.ave.drm.DRMMetadata
```

```java
// TVSDK 2.5
import com.adobe.mediacore.drm.DRMAcquireLicenseSettings; import com.adobe.mediacore.drm.DRMLicense;
import com.adobe.mediacore.drm.DRMManager; import com.adobe.mediacore.drm.DRMMetadata;
```

## 事件处理中的更改 {#changes-in-event-handling}

要在此版本中注册事件，请将处理函数传递给 `addEventListener`。 活动列表已从版本1.4大幅修改为版本2.5。\
例如，下面是如何为 `MediaPlayerEvent.STATUS_CHANGED:`

```java
mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED,
new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent event) {
//Handle status change event
}
});
```

这是1.4中活动的注册方式：

```java
mPlayer.addEventListener(MediaPlayer.Event.PLAYBACK, new MediaPlayer.PlaybackEventListener() {
@Override
public void onStateChanged(MediaPlayer.PlayerState state,
MediaPlayerNotification notification) {
//Handle status change event
}
// Additional handlers
...
});
```

MediaPlayerEvent枚举包含所有事件代码。 2.5中不再存在以下1.4中的事件代码：

* `ADBREAK_PLACEMENT_COMPLETED`
* `ADBREAK_PLACEMENT_FAILED`
* `ADBREAK_REMOVAL_COMPLETED`
* `AD_BREAK_MANIFEST_LOAD_COMPLETE`
* `AD_MANIFEST_LOAD_COMPLETE`
* `AD_MANIFEST_LOAD_FAILED`
* `AUDIO_TRACK_FAILED`
* `BACKGROUND_MANIFEST_FAILED`
* `BUFFERING_FULL, CUSTOM_AD_EVENT`
* `CONTENT_MARKER`
* `CONTENT_PLACEMENT_COMPLETE`
* `CONTENT_CHANGED`
* `ITEM_REPLACED`
* `ITEM_READY`
* `VIEW_CLICKED`
* `PREPARED`
* `UPDATED`
* `OPPORTUNITY_COMPLETED`
* `OPPORTUNITY_CREATED`
* `OPPORTUNITY_FAILED`
* `PAUSE_AT_PERIOD_END`
* `PLAYBACK_STARTED`
* `PLAYBACK_PAUSED`
* `PLAYBACK_COMPLETED`
* `PLAY_COMPLETE`
* `POST_ROLL_COMPLETE`
* `RESOURCE_LOADED`
* `TIMED_METADATA_SKIPPED`
* `VIDEO_ERROR`
* `VIDEO_STATE_CHANGED`

以下事件代码是2.5中新增的：

* `AD_RESOLUTION_COMPLETE`
* `BUFFER_PREPARED`
* `CAPTIONS_UPDATED`
* `MANIFEST_UPDATED`
* `PLAYBACK_RANGE_UPDATED`
* `RESERVATION_REACHED`
* `TIME_CHANGED`
* `TIMED_EVENT`
* `TIMED_METADATA_ADDED_IN_BACKGROUND`

### 重命名的事件 {#renamed-events}

| 新名称 | 旧名 |
|--- |--- |
| SEEK_BEGIN | SEEK_STARTED |
| SEEK_END | SEEK_COMPLETED |
| SEEK_POSITION_ADJUSTED | SEEK_ADJUST_COMPLETED |
| BUFFERING_BEGIN | BUFFERING_STARTED |
| BUFFERING_END | BUFFERING_COMPLETED |
| AUDIO_TRACK_UPDATED | AUDIO_TRACK_CHANGED |
| STATUS_CHANGED | STATE_CHANGED |
| TIMED_METADATA_AVAILABLE | TIMED_METADATA_ADDED |
| SIZE_AVAILABLE | SIZE_CHANGED |
| LOAD_INFO | LOAD_INFORMATION_AVAILABLE |

## MediaPlayer更改 {#mediaplayer-changes}

对一些方法的 `MediaPlayer` 构造和改进提出了新的思路。

**对MediaPlayer类的更改**

以下是对类的更 `MediaPlayer` 改：

* 此枚 `MediaPlayerStatus` 举将替换 `MediaPlayer.PlayerState`。 例如：

```java
//TVSDK v1.4
mPlayer. addEventListener(MediaPlayer.Event.PLAYBACK, new MediaPlayer.PlaybackEventListener() {

@Override
public void onStateChanged(MediaPlayer.PlayerState state,MediaPlayerNotification notification) {
//Handle status change event
}
// Additional handlers
...
});

//TVSDK v2.5
mPlayer.addEventListener(MediaPlayerEvent.STATUS_CHANGED, new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent event) {
//Handle status change event
}
//Additional handlers.
...
});
```

* 现 `MediaPlayer.seekToLocalTime()` 在调用该方法 `MediaPlayer.seekToLocal`。 例如：

```java
//TVSDK v1.4
public void seekToLocal(long localPosition) { mediaPlayer.seekToLocalTime(localPosition);
}

//TVSDK v2.5
public void seekToLocal(long localPosition) { mediaPlayer.seekToLocal(localPosition);
}
```

* 现 `MediaPlayerView.notifyClick()` 在有了方法 `MediaPlayer.notifyClick()`。 例如：

```java
//TVSDK v1.4
public void adClick() { mediaPlayer.getView().notifyClick();
}

//TVSDK v2.5
public void adClick() { mediaPlayer.notifyClick();
}
```

* 前一种方 `MediaPlayer.MediaPlayer.getNotificationHistory()` 法现在已不复存在，而且没有被取代。
* 前者分 `MediaPlayer.replaceCurrentItem()` 为两种方法： `replaceCurrentResource()`它以实例为 `MediaResource`例， `replaceCurrentItem()`它以实例为例 `MediaPlayerItem`。 例如：

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, getAdvertisingMetadata());

mediaPlayer.replaceCurrentItem(playerResource);

//TVSDK v2.5 - replacing a resource
MediaResource playerResource = new MediaResource(url,
MediaResource.Type.HLS, getAdvertisingMetadata());
...
try {
mMediaPlayer.replaceCurrentResource(playerResource, _mediaPlayerItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
// handle exception.
}
// TVSDK 2.5 - replacing an Item
MediaPlayerItemLoader itemLoader = new MediaPlayerItemLoader(context, new MediaPlayerItemLoader.LoaderListener() {

@Override
public void onError(PSDKErrorCode psdkErrorCode, String s) {
...
}
@Override
public void onLoadComplete(MediaPlayerItem mediaPlayerItem) {
...
}
@Override
public void onBufferingBegin() {
...
}
@Override
public void onBufferPrepared() {
...
}
});
MediaResource playerResource = new MediaResource(url,
MediaResource.Type.HLS, getAdvertisingMetadata());

itemLoader.load(playerResource); itemLoader.prepareBuffer();
mediaPlayer.replaceCurrentItem(itemLoader.getItem());
```

您可以使用它在预先初始化的MediaPlayer实例之间切换，如果出现封锁期。

**构造函数替换静态create()方法**

可以使用TVSDK v2.5中的构造函数，而不 `create()` 是使用TVSDK v1.4的方法。名称以“默认”开头的所有类( `DefaultMediaPlayer`如 `DefaultNetworkConfig`、 `DefaultContentFactory`、)在v2.5中不可用。

在某些情况下，TVSDK v1.4 API使用以下模式创建类：

1. 定义一个界面(例如， `MediaPlayer`)。
1. 提供默认类(例如， `DefaultMediaPlayer`)。
1. 在默认 `create()` 类上提供一个方法，以提供实现接口的类。

在TVSDK v2.5中，此类接口是具体的类，您可以使用相应的构造函数创建这些类的实例。 以下代码片段说明了这一区别：

```java
//TVSDK v1.4
// Create a media player
// MediaPlayer is an interface
private MediaPlayer createMediaPlayer() { MediaPlayer mediaPlayer =
DefaultMediaPlayer.create(getActivity().getApplicationContext()); return mediaPlayer;

//TVSDK v2.5
// Create a media player
// MediaPlayer is a class that you instantiate private MediaPlayer createMediaPlayer() {
MediaPlayer mediaPlayer =
new MediaPlayer(getActivity().getApplicationContext()); return mediaPlayer;
}
```

不遵循此模式但在1.4中使用方法 `create()` 的其他类包括：

* MediaResource\
   这以前使用过 `MediaResource.createFromUrl()`。 现在使用构造函数，它采用URL、资源类型和元数据。 例如：

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, getAdvertisingMetadata());
mediaPlayer.replaceCurrentItem(playerResource);

//TVSDK v2.5
MediaResource playerResource =
new MediaResource(url, MediaResource.Type.HLS, getAdvertisingMetadata());

try { mediaPlayer.replaceCurrentResource(playerResource,_mediaPlayerItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
// handle exception.
}
```

* 广告
* AdAsset
* AdBreak

某些类(例如， `ContentFactory`)是没有公开可用的默认实现的抽象类(例如， `DefaultContentFactory`)。 在这些情况下，您可以通过方便功能提供默认实现，例如： `mediaPlayerItemConfig.getDefaultContentFactory()`

**隐藏式字幕中的更改**

以下更改影响与隐藏式字幕相关的类：

* 检索隐藏字幕轨道时，仅 `MediaPlayerItem.getClosedCaptionTracks()` 返回活动轨道。
* `ClosedCaptionTrack` 不再有方 `isActive()` 法。

```java
//TVSDK v1.4
public List<String> getClosedCaptionTracks(String label) {
List<String> closedCaptionsTracksAsStrings = new ArrayList<String>(); MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); List<ClosedCaptionsTrack> closedCaptionsTracks =
currentItem.getClosedCaptionsTracks(); Iterator<ClosedCaptionsTrack> iterator =
closedCaptionsTracks.iterator();
if (currentItem != null) {
while (iterator.hasNext()) {
ClosedCaptionsTrack closedCaptionsTrack = iterator.next(); String isActive = closedCaptionsTrack.isActive() ? " (" + label
+ ")" : "";
closedCaptionsTracksAsStrings.add(closedCaptionsTrack.getName()
+ " : " + closedCaptionsTrack.getLanguage() + isActive);
}
}
return closedCaptionsTracksAsStrings;
}

//TVSDK v2.5
public List<String> getClosedCaptionTracks(String label) {

MediaPlayerItem currentItem = mediaPlayer.getCurrentItem(); List<ClosedCaptionsTrack> closedCaptionsTracks =
currentItem.getClosedCaptionsTracks();
Iterator<ClosedCaptionsTrack> iterator = closedCaptionsTracks.iterator();

List<String> closedCaptionsTracksAsStrings = new ArrayList<String>(); if (currentItem != null) {
while (iterator.hasNext()) {
ClosedCaptionsTrack closedCaptionsTrack = iterator.next(); closedCaptionsTracksAsStrings.
add(closedCaptionsTrack.getName() + " : ");
}
}
return closedCaptionsTracksAsStrings;
}
// Add snippet and desc for CaptionsUpdatedEventListener mediaPlayer.addEventListener(MediaPlayerEvent.CAPTIONS_UPDATED,
captionsUpdatedEventListener);

private final CaptionsUpdatedEventListener captionsUpdatedEventListener = new CaptionsUpdatedEventListener() {

@Override
public void onCaptionsUpdated(MediaPlayerItemEvent mediaPlayerItemEvent) { getActivity().findViewById(R.id.sbPlayerControlCC).setVisibility(
View.VISIBLE/*Visible*/);
}
};
```

## 广告变化 {#advertising-changes}

版本2.5中有若干与广告相关的更改。

**广告行为的变化**

在v2.5中，当用户执行超越广告窗格的搜索时，广告播放的默认行为会稍有更改。如果未观看广告中断，则在向前搜索后将播放广告。 当应用程序使用默认广告策略时，在播放完成后，广告中断即被删除。 使用TVSDK v2.5，如果用户在时间线上的广告窗格后面搜索并且广告中断未被观看，则不会回放任何广告。

但是，在TVSDK v1.4中，默认情况下，在向后搜索时将回放广告。 例如，如果在第三个和第四个广告中断之间向后搜索，TVSDK v1.4的默认行为是播放第三个广告中断。

**广告规则更改**

广告规则是使用JSON文件指定的。 TVSDK的两个版本中的JSON文件格式保持不变。 但是，在TVSDK v2.5中，广告规则JSON文件必须托管在可通过HTTP URL访问的位置。 应用程序可以使用AuditudeSettings的实例。

```java
//TVSDK v2.5
AuditudeSettings result = new AuditudeSettings(); result.setCRSRulesJsonURL(<http url of AdobeTVSDKConfig.json>);
```

在TVSDK版本1.4中，此文件位于应用程序中assets文件夹的下方，TVSDK将加载该文件。

**广告工厂重命名**

`AdvertisingFactory` 现在已命名 `ContentFactory`。 您可 `ContentFactory` 以通过覆盖其某些方法来创建自定义的广告工作流程。 使用返回null保留默认行为，如下所示：

```java
//TVSDK v2.5
new ContentFactory() {
@Override
public AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem item) { return new CustomAdPolicySelector();
}
@Override
public List<OpportunityGenerator> retrieveGenerators(MediaPlayerItem item) { return null;
}
@Override
public List<ContentResolver> retrieveResolvers(MediaPlayerItem item) { return null;
}
@Override
public List<CustomAdHandler> retrieveCustomAdPlaybackHandlers(MediaPlayerItem item) { return null;
}
};
```

**零长广告分段**

当广告服务器不返回任何广告时，TVSDK 2.5将零长广告分段作为占位符插入。

零长度广告中断可通过使用onAdBreakStarted事件检测广告中断中的广告计数为零来确定，应用程序必须相应地处理这些广告中断。

**元数据更改**

Metadata类为以前的MetadataNode类提供了更有力的替换。

* Metadata类可以存储字符串、字节数组和其他元数据对象：

```java
TVSDK v1.4
public AuditudeSettings createAdvertisementSettings() { Metadata advertisingParams = new MetadataNode();
advertisingParams.setValue("platform", Build.VERSION.RELEASE); advertisingParams.setValue("model", Build.MODEL);
AuditudeSettings adSettings = new AuditudeSettings();
// Set ad domain, zone id and media_id
...

// Set the target paramaters adSettings.setTargetingParameters(advertisingParams);

return adSettings;
}
//TVSDK v2.5
public AuditudeSettings createAdvertisementSettings() { Metadata advertisingParams = new Metadata();
advertisingParams.setValue("platform", Build.VERSION.RELEASE); advertisingParams.setValue("model", Build.MODEL);
AuditudeSettings adSettings = new AuditudeSettings();
// Set ad domain, zone id and media_id
...

// Set the target paramaters adSettings.setTargetingInfo(advertisingParams);

return adSettings;
}
```

* 此枚 `MetadataKeys` 举将替换 `DefaultMetadataKeys`。 新版本中并 `DefaultMetadataKeys` 非包含所有键。

```java
//TVSDK v1.4
if (this.mediaPlayer != null && this.mediaPlayer.getCurrentItem() != null) { MetadataNode resourceMetadata =
(MetadataNode) this.mediaPlayer.getCurrentItem().getResource().getMetadata();
VideoAnalyticsMetadata vaMetadata = (VideoAnalyticsMetadata)
resourceMetadata.getNode(DefaultMetadataKeys.
VIDEO_ANALYTICS_METADATA_KEY.getValue());
}

//TVSDK v2.5
if (resourceMetadata.containsKey(VideoAnalyticsMetadata.
VIDEO_ANALYTICS_METADATA_KEY)) {
JSONObject vaMetadataObj =
new JSONObject(resourceMetadata.
getValue(VideoAnalyticsMetadata. VIDEO_ANALYTICS_METADATA_KEY));
vaMetadata = parseVideoAnalyticsMetadata(vaMetadataObj);
}

} catch (JSONException e) { e.printStackTrace();
}
```

* 广告元数据现在由类(元数 `AdvertisingMetadata` 据的子类)表示，现在存储在而不是 `MediaPlayerItemConfig` 存储中 `MediaResource`。

```java
//TVSDK v1.4
MetadataNode mediaMetadata = new MetadataNode();

if (stream.live) { mediaMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue(),
getAdSettingsForLive());
} else {
mediaMetadata.setNode(DefaultMetadataKeys.AUDITUDE_METADATA_KEY.getValue(), getAdSettingsForVod());
}
MediaResource playerResource = MediaResource.createFromUrl(url, mediaMetadata);

//TVSDK v2.5
MediaPlayerItemConfig mediaItemConfig = new MediaPlayerItemConfig(context);

if (stream.live) {
AuditudeSettings adSettings = getAdSettingsForLive(); adSettings.setLivePreroll(true); mediaItemConfig.setAdvertisingMetadata(adSettings);
} else {
// Set the advertising parameters for VOD. mediaItemConfig.setAdvertisingMetadata(getAuditudeSettingsForVod());
}

// Create advertising metadata node Metadata mediaMetadata = new Metadata();

// Asset Url
MediaResource playerResource =
new MediaResource(url, MediaResource.Type.HLS, mediaMetadata);
try {
mediaPlayer.replaceCurrentResource(playerResource, mItemConfig);
} catch (MediaPlayerException mediaPlayerException) {
//handle exception.
}
```

网络配置元数据(以前是类的成 `MediaResource` 员)现在由类表示， `NetworkConfiguration` 并且现在存储在而不是 `MediaPlayerItemConfig` 类中 `MediaResource`。

```java
//TVSDK v1.4
MediaResource playerResource = MediaResource.createFromUrl(url, mediaMetadata);
...

//TVSDK v2.5
MediaPlayerItemConfig mediaItemConfig = new MediaPlayerItemConfig(context);

NetworkConfiguration mediaNetworkConfiguration = mediaItemConfig.getNetworkConfiguration();
```

**对TimedMetadata解析的更改**

在2.5中， `TimedMetadata` 对于用于解析ID3标签的数据类型，解析已更改。

```java
//TVSDK v1.4
public void onTimedMetadata(TimedMetadata timedMetadata) { TimedMetadata.Type type = timedMetadata.getType();
if (type.equals(TimedMetadata.Type.ID3)){ PMPDemoApp.logger.i(LOG_TAG + "#onTimedMetadata",
"New ID3 tag detected at time = " + timedMetadata.getTime());
Metadata metadata = timedMetadata.getMetadata(); Set<String> keys = metadata.keySet();
for (String key : keys) {
String value = metadata.getValue(key); PMPDemoApp.logger.i(LOG_TAG + "#onTimedMetadata",
"Key = " + key + " Value = " + value);
}
} else if (_mediaPlayer.getPlaybackRange() != null &&
_mediaPlayer.getPlaybackRange().getDuration() > 0) { displayRanges();
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New timed metadata. Name " + timedMetadata.getName() +
", time " + timedMetadata.getTime() + ", id " + timedMetadata.getId() + ", metadata " +
timedMetadata.getMetadata() + ".");
/*if (!_timedMetadataList.contains(timedMetadata)) {
_timedMetadataList.add(timedMetadata);
}*/
/* scte35 */
if (timedMetadata.getName().equalsIgnoreCase("#EXT-OATCLS-SCTE35")) { parseSCTE35Tag(timedMetadata);
}
}
}

//TVSDK v2.5
public void onTimedMetadata(TimedMetadataEvent timedMetadataEvent) { PMPDemoApp.logger.i(LOG_TAG + " inside"," ontimedmetadata"); TimedMetadata timedMetadata = timedMetadataEvent.getTimedMetadata();

TimedMetadata.Type type = timedMetadata.getType(); if (type.equals(TimedMetadata.Type.ID3)) {
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New ID3 tag detected at time = " + timedMetadata.getTime());
Metadata metadata = timedMetadata.getMetadata();
if (metadata != null) { PMPDemoApp.logger.i(LOG_TAG +
"::expandID3Metadata", "isEmpty " + metadata.isEmpty());
Set<String> keys = metadata.keySet(); PMPDemoApp.logger.i(LOG_TAG + "::expandID3Metadata",
"No of keys=" + keys.size());
String s;
for (String key : keys) {
byte[] value = metadata.getByteArray(key); s = new String(value);
if (key.equalsIgnoreCase("APIC"))
s = "SUPPRESSING BINARY DATA FOR ATTACHED PICTURE.";
PMPDemoApp.logger.i(LOG_TAG + "::expandID3Metadata",
"Key=" + key + ", Length=" + value.length + ", Value=" + s.trim());
}
}
} else if (_mediaPlayer.getPlaybackRange() != null &&
_mediaPlayer.getPlaybackRange().getDuration() > 0) { displayRanges();
PMPDemoApp.logger.i(LOG_TAG +
"#onTimedMetadata",
"New timed metadata. Name " + timedMetadata.getName() +
", time " + timedMetadata.getTime() + ", id " + timedMetadata.getId() + ", metadata " +
timedMetadata.getMetadata() + ".");
/*if (!_timedMetadataList.contains(timedMetadata)) {
_timedMetadataList.add(timedMetadata);
}*/
/* scte35 */
if (timedMetadata.getName().equalsIgnoreCase("#EXT-OATCLS-SCTE35")) { PMPDemoApp.logger.i(LOG_TAG +
" inside ontimedmetadata"," ext"); parseSCTE35Tag(timedMetadata);
}
}
}
```

**其他更改**

版本2.5中提供了以下其他更改：

* 方 `notifyClick()` 法已从变 `MediaPlayerView` 为 `MediaPlayer`。

* `AdPolicySelector` 是接口，而不是类。 实施其所有方法。
* `AdPolicyInfo` 现在包含列表， `AdBreakTimelineItem`而非列 `AdBreakPlacement`表。

* 抽象类的 `ContentResolver` API名称已更改。
* `PlacementOpportunityDetector` 不再可用。 而是扩展 `OpportunityGenerator` 抽象类。 引用实现提供了一个示例。

* 构造函数的 `AdBreakPlacement` 参数相同，但顺序不同。 有关示例实施，请参阅与产品绑定的Reference Player实施。

## DRM中的更改 {#changes-in-drm}

此版本中的大部分更改位于DRM层。 下表显示了版本1.4和2.5之间的其他更改：

| DRMManager方法 | 1.4中的成功回调 | 1.4中的错误回调 | 2.5中的监听器 |
|--- |--- |--- |--- |
| acquireLicense | DRMLicenseApperiedCallback | DRMOperationErrorCallback | DRMAcquireLicenseListener |
| acquirePreviewLicense | DRMLicenseApperiedCallback | DRMOperationErrorCallback | DRMAcquireLicenseListener |
| 身份验证 | DRMAuthenticationCompleteCallback | DRMOperationErrorCallback | DRMAuthenticateListener |
| createMetadataFromBytes | NA | DRMOperationErrorCallback | DRMErrorListener |
| 初始化 | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| joinLicenseDomain | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| leaveLicenseDomain | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| resetDRM | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| returnLicense | DRMLicenseReturnCompleteCallback | DRMOperationErrorCallback | DRMReturnLicenseListener |
| setAuthenticationToken | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |
| storeLicenseBytes | DRMOperationCompleteCallback | DRMOperationErrorCallback | DRMOperationCompleteListener |

```java
//TVSDK 1.4
private final MediaPlayer.DRMEventListener _drmEventListener = new MediaPlayer.DRMEventListener() {

@Override
public void onDRMMetadata(final DRMMetadataInfo drmMetadataInfo) { PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.DRMEventListener#onDRMMetadata",
"DRM metadata available: " + drmMetadataInfo + ".");
if (getSuppressAutoPlayPreference() && drmMetadataInfo != null) {
// if suppress play setting, then the user is a tester who
// wishes to manually intervene between the metadata available
// event and the play event, so launch the metadata interface
// and give it the loaded metadata bytes, but only once
_drmMetadata = drmMetadataInfo.getDRMMetadata();
}
if (drmMetadataInfo == null ||
!DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { PMPDemoApp.logger.i(LOG_TAG + "#onDRMMetadata", "DRM auth is not needed."); return;
}
// Perform DRM auth.
// Possible logic might take into consideration a threshold
// between the current player time and the DRM metadata start
// time. For the time being, we resolve it as soon as we receive
// the DRM metadata.

DRMManager drmManager = _mediaPlayer.getDRMManager(); if (drmManager == null) {
PMPDemoApp.logger.e(LOG_TAG + "#onDRMMetadata", "DRMManager is null."); return;
}
SharedPreferences sharedPreferences =
PreferenceManager.getDefaultSharedPreferences(getActivity()); String authUser =
sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_USERNAME,
getResources().getString(R.string.drmUsername));
String authPass = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_PASSWORD,
getResources().getString(R.string.drmPassword));
DRMHelper.performDrmAuthentication(drmManager,
drmMetadataInfo.getDRMMetadata(), authUser,
authPass,
new DRMAuthenticationListener() {
@Override
public void onAuthenticationStart() { PMPDemoApp.logger.i(LOG_TAG + "#onAuthenticationStart",
"DRM authentication started for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
@Override
public void onAuthenticationError(long majorCode,
long minorCode, Exception e) {
if (getActivity() == null) { return;
}
PMPDemoApp.logger.e(LOG_TAG +
"#onAuthenticationError",
"DRM authentication failed. " + majorCode + " 0x" + Long.toHexString(minorCode));
_handler.post(new Runnable() {
@Override
public void run() { showToast(getString(R.string.drmAuthenticationError)); getActivity().finish();
}
});
}
@Override
public void onAuthenticationComplete(byte[] authenticationToken) { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationComplete",
"Auth successful for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
});
}
};

//TVSDK 2.5
private final DRMMetadataInfoEventListener drmMetadataInfoEventListener = new DRMMetadataInfoEventListener() {
@Override
public void onDRMMetadataInfo(DRMMetadataInfoEvent drmMetadataInfoEvent) { final DRMMetadataInfo drmMetadataInfo =
drmMetadataInfoEvent.getDRMMetadataInfo();
PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.DRMEventListener#onDRMMetadata",
"DRM metadata available: " + drmMetadataInfo + ".");
if (getSuppressAutoPlayPreference() && drmMetadataInfo != null) {
// if suppress play setting, then the user is a tester who
// wishes to manually intervene between the metadata
// available event and the play event, so launch the
// metadata interface and give it the loaded metadata
// bytes, but only once
drmMetadata = drmMetadataInfo.getDRMMetadata();
}
if (drmMetadataInfo ==
null || !DRMHelper.isAuthNeeded(drmMetadataInfo.getDRMMetadata())) { PMPDemoApp.logger.i(LOG_TAG +
"#onDRMMetadata",
"DRM auth is not needed.");
return;
}
// Perform DRM auth.
// Possible logic might take into consideration a threshold between
// the current player time and the DRM metadata start time. For the
// time being, we resolve it as soon as we receive the DRM metadata.

DRMManager drmManager = _mediaPlayer.getDRMManager(); if (drmManager == null) {
PMPDemoApp.logger.e(LOG_TAG +
"#onDRMMetadata", "DRMManager is null.");
return;
}

SharedPreferences sharedPreferences = PreferenceManager.getDefaultSharedPreferences(getActivity());
String authUser = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_USERNAME,
getResources().getString(R.string.drmUsername));
String authPass = sharedPreferences.getString(PMPDemoApp.SETTINGS_DRM_PASSWORD,
getResources().getString(R.string.drmPassword));
DRMHelper.performDrmAuthentication(drmManager,
drmMetadataInfo.getDRMMetadata(), authUser,
authPass,
new DRMAuthenticationListener() {
@Override
public void onAuthenticationStart() { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationStart",
"DRM authentication started for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
@Override
public void onAuthenticationError(int major,
int minor,
String erroString, String serverErrorURL) {
if (getActivity() == null) { return;
}
PMPDemoApp.logger.e(LOG_TAG +
"#onAuthenticationError",
"DRM authentication failed. " + major +
" 0x" +
Long.toHexString(minor));
_handler.post(new Runnable() {
@Override
public void run() { showToast(getString(R.string.drmAuthenticationError)); getActivity().finish();
}
});
}
@Override
public void onAuthenticationComplete(byte[] authenticationToken) { PMPDemoApp.logger.i(LOG_TAG +
"#onAuthenticationComplete",
"Auth successful for DRM metadata at [" + drmMetadataInfo.getPrefetchTimestamp() + "].");
}
});
}
};
```

现在， `DRMManager` 在触发事件监听器后，可以使用在创建mediaplayer后1.4中可用 `onDRMMetadataInfo` 的静态实例。

## 自适应比特率(ABR)相关更改 {#adaptive-bitrate-abr-related-changes}

**常量的更改**

许多常量的类型已从 `String` 更改为 `int`。 例如： `MediaResourceType`、 `ABRControlParameters`和 `MediaPlayerStatusChangeEvent`。

```java
//TVSDK v1.4
ABRControlParameters
private void setAbrControlParams() { SharedPreferences sharedPreferences =
PreferenceManager.getDefaultSharedPreferences(getActivity());
if (sharedPreferences.getBoolean(PMPDemoApp.SETTINGS_ABR_CTRL_ENABLED,
PMPDemoApp.DEFAULT_ABR_ENABLED)) {
int initialBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_INITIAL_BITRATE, 0);
int minBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_BITRATE, 0);
int maxBitRate = getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_BITRATE, PMPDemoApp.DEFAULT_MAX_BIT_RATE);
int mbrPolicyAsInt =
getIntPreference(sharedPreferences, PMPDemoApp.SETTINGS_ABR_POLICY, 0); ABRControlParameters.ABRPolicy abrPolicy = policyFromInt(mbrPolicyAsInt); abrPolicy = abrPolicy != null ?
abrPolicy : ABRControlParameters.ABRPolicy.ABR_MODERATE;
_mediaPlayer.setABRControlParameters(new ABRControlParameters(initialBitRate,
minBitRate, maxBitRate, abrPolicy));
}
}

//TVSDK v2.5
ABRControlParameters
private void setAbrControlParams() { ABRControlParametersBuilder abrBuilder =
new ABRControlParametersBuilder();

if (sharedPreferences.getBoolean(PMPDemoApp.SETTINGS_ABR_CTRL_ENABLED, PMPDemoApp.DEFAULT_ABR_ENABLED)) {

abrBuilder.setInitialBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_INITIAL_BITRATE,
ABRControlParameters.DEFAULT_ABR_INITIAL_BITRATE)); abrBuilder.setMinBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_BITRATE,
ABRControlParameters.DEFAULT_ABR_MIN_BITRATE)); abrBuilder.setMaxBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_BITRATE,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE)); abrBuilder.setMaxPlayoutRate(getDoublePreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_PLAYOUT_RATE,
ABRControlParameters.DEFAULT_MAX_PLAYOUT_RATE)); abrBuilder.setMinTrickPlayBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MIN_TRICKPLAY_BITRATE,
ABRControlParameters.DEFAULT_ABR_MIN_BITRATE)); abrBuilder.setMaxTrickPlayBitRate(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_TRICKPLAY_BITRATE,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE)); abrBuilder.setMaxTrickPlayBandwidthUsage(getIntPreference(sharedPreferences,
PMPDemoApp.SETTINGS_ABR_MAX_TRICKPLAY_BANDWIDTH,
ABRControlParameters.DEFAULT_ABR_MAX_BITRATE));

switch (getIntPreference(sharedPreferences, PMPDemoApp.SETTINGS_ABR_POLICY, -1)) {
case 0: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_CONSERVATIVE); break;
case 1: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_MODERATE); break;
case 2: abrBuilder.setPolicy(ABRControlParameters.ABRPolicy.ABR_AGGRESSIVE); break;
default: abrBuilder.setPolicy(ABRControlParameters.DEFAULT_ABR_POLICY);
}
}
_mediaPlayer.setABRControlParameters(abrBuilder.toABRControlParameters());
}
```

**对ABRControlParameters构造函数的更改**

某些参数已添加、某些已重命名，有些已移动。 以下是v1.4中的构造函数签名和2.5中的新签名：

```java
//TVSDK v1.4
public ABRControlParameters(ABRPolicy abrPolicy,
int nInitialBitRate, int nMinBitRate,
int nMaxBitRate)

//TVSDK v2.5
public ABRControlParameters(int nInitialBitRate,
int nMinBitRate, int nMaxBitRate,
ABRPolicy abrPolicy,
int nMinTrickPlayBitRate, int nMaxTrickPlayBitRate,
int nMaxTrickPlayBandwidthUsage, double dMaxPlayoutRate)
```

## 错误事件和处理 {#error-events-and-handling}

**错误处理中的更改**

该 `MediaError` 类已替换为该 `Notification` 类。 类和类之间的唯一 `MediaError` 区别 `Notification` 是后者不包含description属性。 TVSDK 2.5中不存在值为101xxx、102xxx、104xxx、106xxx、107xxx、109xxx的TVSDK 1.4错误代码。有关TVSDK 2.5中的播放代码，请参阅 [本机错误——视频播放值](assets/psdk_android_2.5.pdf)。

以下是TVSDK 1.4和2.5中的错误处理示例：

```java
//TVSDK v1.4
@Override
public void onStateChanged(MediaPlayer.PlayerState state, MediaPlayerNotification notification) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Player state changed to [" + state
+ "].");

switch (state) {
// Non recoverable state - either reset player and reinitialize
// or release the player and create a new one.
case ERROR: PMPDemoApp.logger.e(LOG_TAG +
"::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Error: " + notification + "."); getActivity().finish();
break;
default:
// do nothing
}
}

//TVSDK v2.5
private final StatusChangeEventListener statusChangeEventListener = new StatusChangeEventListener() {
@Override
public void onStatusChanged(MediaPlayerStatusChangeEvent mediaPlayerStatusChangeEvent)
{
MediaPlayerStatus state = mediaPlayerStatusChangeEvent.getStatus(); PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Player state changed to [" + state
+ "].");
switch (state) {
// Non recoverable state - either reset player and reinitialize
// or release the player and create a new one.
case ERROR:
PMPDemoApp.logger.e(LOG_TAG + "::MediaPlayer.PlayerStateEventListener#onStateChanged()", "Error: ");
printErrorMetadata(mediaPlayerStatusChangeEvent.getMetadata()); showToast("MediaPlayer status ERROR: Look at the logs for details"); getActivity().finish();
break;
default:
// do nothing
}
}
};
```

所有可恢复的错误均视为警告，并使用TVSDK 2.5 `NotificationEventListener` 中的“”进行处理。警告与TVSDK 1.4中的 `onOperationFailed` QOS处理程序中的监听器一起显示为通知，与TVSDK 2.5中的通知是单独的事件一样。 1.4和2.5中处理的警告如下：

```java
//TVSDK v1.4
private final MediaPlayer.QOSEventListener _qosEventListener = new MediaPlayer.QOSEventListener()
{
@Override
public void onBufferStart() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
}
@Override
public void onBufferComplete() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onBufferComplete()", "Buffering complete.");
}
@Override
public void onSeekStart() {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
}
@Override
public void onSeekComplete(long adjustedTime) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " + adjustedTime + ".");
}
@Override
public void onLoadInfo(LoadInfo loadInfo) {
PMPDemoApp.logger.i(LOG_TAG + "::MediaPlayer.QOSEventListener#onLoadInfo()", "Url: " + loadInfo.getUrl() + ", size: "
+ loadInfo.getSize() + " bytes, media duration: " + loadInfo.getMediaDuration() + "ms, download duration: " + loadInfo.getDownloadDuration() + "ms");
}
@Override
public void onOperationFailed(MediaPlayerNotification.Warning warning) {

StringBuffer sb = new StringBuffer("Player operation failed: "); sb.append(warning.getCode()).append(" - ").append(warning.getDescription()); if (warning.getMetadata() != null) {
sb.append("Warning metadata: ").append(warning.getMetadata().toString());
}

MediaPlayerNotification innerNotification = warning.getInnerNotification(); registerFailedAudioTrackIndex(innerNotification); handleFailedSeekEvent(innerNotification);

while (innerNotification != null) { sb.append("Inner notification: ");
sb.append(innerNotification.getCode()).append(" - ").append(innerNotification.getDescription());
Metadata metadata = innerNotification.getMetadata(); if (metadata != null) {
for (String key : metadata.keySet()) { sb.append(" - ").append

//TVSDK v2.5
private final NotificationEventListener notificationEventListener = new NotificationEventListener() {
/**
* An example of dumping the information within a Notification. Here, we don't handle the event in
* any way except to print a log message.
* @param event The NotificationEvent
*/
@Override
public void onNotification(NotificationEvent event) { Notification notification = event.getNotification(); Notification.Type type = notification.getType(); StringBuilder sb = new StringBuilder(); sb.append("[").append(type).append("]");
sb.append(" Player operation failed (").append(notification.getCode()).append(")"); Metadata metadata = notification.getMetadata();
if (metadata != null)
{
for (String key : metadata.keySet())
{
sb.append(", ").append(key).append(" = ").append(metadata.getValue(key));
}
}
Notification inner = notification.getInnerNotification(); if (inner != null) {
sb.append(" :: Inner Notification [").append(inner.getType()).append("](").append(inner.getCode()).append(")");
Metadata innerMetadata = inner.getMetadata(); if (innerMetadata != null) {
for (String iKey : innerMetadata.keySet()) { sb.append(", ").append(iKey).append(" =
").append(innerMetadata.getValue(iKey));
}
}
}
switch(type)
{
case ERROR:
PMPDemoApp.logger.e(LOG_TAG, sb.toString()); break;
case WARNING:
PMPDemoApp.logger.w(LOG_TAG, sb.toString()); break;
default:
PMPDemoApp.logger.i(LOG_TAG, sb.toString()); break;
}
showToast(sb.toString()); PMPDemoApp.logger.d(LOG_TAG, sb.toString());
}
};
```

**新例外**

TVSDK v1.4将空值、错误返回和各种异常( `MediaPlayerException`、 `IllegalStateException`和 `IllegalArgumentException`)组合使用，而TVSDK v2.5则用于所 `generatesMediaPlayerException` 有错误。

>[!NOTE]
>
>要获取MediaPlayerException的详细信息，您可以使用 `getErrorCode()`。

更改的示例如下：

```java
//TVSDK v1.4
public void setBufferControlParams() { try {
mediaPlayer.setBufferControlParameters(getBufferParamsFromSettings());
} catch (IllegalArgumentException e) { PrimetimeReference.logger.w(LOG_TAG +
"#setBufferControlParams",
"Unable to apply buffering params: " + e.getMessage() + ".");
}
}

//TVSDK v2.5
public void setBufferControlParams() { try {
mediaPlayer.setBufferControlParameters(getBufferParamsFromSettings());
} catch (MediaPlayerException e) { PrimetimeReference.logger.w(LOG_TAG + "#setBufferControlParams", "Unable to apply buffering params: " + e.getMessage() + ".");
}
}
```

## 对QOS参数的更改 {#changes-to-qos-parameters}

对QOSProvider对象属性做了细微更改：

* TVSDK `TimeToFirstFrame` 2.5中不提供。
* TVSDK 2.5 QOSProvider具有新属性，用于确定流会话期间的可感知带宽。

```java
//TVSDK v1.4
public void updateQosInformation(PlaybackInformation playbackInformation) { if (playbackInformation == null) {
return;
}
setQosItem("Frame rate", (int) playbackInformation.getFrameRate() +
" (" + (int) playbackInformation.getDroppedFrameCount() + " dropped)"); setQosItem("Bitrate", (int) playbackInformation.getBitrate()); setQosItem("Buffering time", (long) playbackInformation.getBufferingTime()); setQosItem("Buffer length", (long) playbackInformation.getBufferLength()); setQosItem("Buffer time", (long) playbackInformation.getBufferTime()); setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount()); setQosItem("Time to load", (int) playbackInformation.getTimeToLoad()); setQosItem("Time to start", (int) playbackInformation.getTimeToStart()); setQosItem("Time to first frame", (int) playbackInformation.getTimeToFirstFrame()); setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare()); setQosItem("Last seek time", (int) playbackInformation.getLastSeekTime());
}

//TVSDK v2.5
public void updateQosInformation(PlaybackInformation playbackInformation) { if (playbackInformation == null) {
return;
}
setQosItem("Frame rate", (int) playbackInformation.getFrameRate() +
" (" + (int) playbackInformation.getDroppedFrameCount() + " dropped)"); setQosItem("Bitrate", (int) playbackInformation.getBitRate()); setQosItem("Buffering time", (long) playbackInformation.getBufferingTime()); setQosItem("Buffer length", (long) playbackInformation.getBufferLength()); setQosItem("Buffer time", (long) playbackInformation.getBufferTime()); setQosItem("Empty buffer count", (int) playbackInformation.getEmptyBufferCount()); setQosItem("Time to load", (int) playbackInformation.getTimeToLoad()); setQosItem("Time to start", (int) playbackInformation.getTimeToStart());
setQosItem("Time to prepare", (int) playbackInformation.getTimeToPrepare());
setQosItem("Perceived Bandwidth", (int) playbackInformation.getPerceivedBandwidth());
```

* TVSDK `QOSEventListener::onOperationFailed()` 2.5中不再存在。此事件监听器中过去显示的警告现在将显示在事件监听 `NotificationEventListener::onNotification()` 器中。

* 、、 `QOSProvider event listeners onBufferStart()`、 `onBufferComplete()`和是与mediaPlayer实例 `onSeekStart()``onSeekComplete()``onLoadInfo()` 绑定的单个事件监听器。

```java
//TVSDK v1.4
private final MediaPlayer.QOSEventListener _qosEventListener = new MediaPlayer.QOSEventListener() {

@Override
public void onBufferStart() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
showBufferingSpinner();
}
@Override
public void onBufferComplete() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferComplete()", "Buffering complete.");
hideBufferingSpinner();
}
@Override
public void onSeekStart() { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
inTrickPlayMode = false;
}
@Override
public void onSeekComplete(long adjustedTime) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " +
adjustedTime + ".");
_controlBar.setPosition(adjustedTime);
if (adjustedTime == _mediaPlayer.getPlaybackRange().getEnd() &&
_mediaPlayer.getStatus() == MediaPlayer.PlayerState.COMPLETE) {
// Show the replay button. showReplayButton();
}
if (_mediaPlayer.getStatus() == MediaPlayer.PlayerState.PAUSED) {
// Show the pause icon.
_controlBar.pause();
}
}
@Override
public void onLoadInfo(LoadInfo loadInfo) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onLoadInfo()", "Url: " +
loadInfo.getUrl() + ", size: " + loadInfo.getSize() +
" bytes, media duration: " +
loadInfo.getMediaDuration() + "ms, download duration: " +
loadInfo.getDownloadDuration() + "ms");
 
public void onOperationFailed(MediaPlayerNotification.Warning warning) {

StringBuffer sb = new StringBuffer("Player operation failed: "); sb.append(warning.getCode()).append(" - ").append(warning.getDescription()); if (warning.getMetadata() != null) {
sb.append("Warning metadata: ").append(warning.getMetadata().toString());
}

MediaPlayerNotification innerNotification = warning.getInnerNotification(); registerFailedAudioTrackIndex(innerNotification); handleFailedSeekEvent(innerNotification);

while (innerNotification != null) { sb.append("Inner notification: ");
sb.append(innerNotification.getCode()).append(" - "). append(innerNotification.getDescription());
Metadata metadata = innerNotification.getMetadata(); if (metadata != null) {
for (String key : metadata.keySet()) { sb.append(" - ").append(key).append(": ").
append(metadata.getValue(key));
}
}
innerNotification = innerNotification.getInnerNotification();
}
String errMsg = sb.toString(); PMPDemoApp.logger.w(LOG_TAG +
"::MediaPlayer.QOSEventListener#onOperationFailed()", errMsg);
showToast(errMsg);
}
};

//TVSDK v2.5
mediaPlayer.addEventListener(MediaPlayerEvent.LOAD_INFORMATION_AVAILABLE,
loadInfoEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.BUFFERING_BEGIN,
bufferingBeginEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.BUFFERING_END,
bufferingEndEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.SEEK_BEGIN,
seekBeginEventListener); mediaPlayer.addEventListener(MediaPlayerEvent.SEEK_END,
seekEndEventListener);
// Buffering events.
BufferingBeginEventListener bufferingBeginEventListener = new BufferingBeginEventListener() {
@Override
public void onBufferingBegin(BufferEvent bufferEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferStart()", "Buffering started.");
showBufferingSpinner();
}
};

BufferingEndEventListener bufferingEndEventListener = new BufferingEndEventListener() {
@Override
public void onBufferingEnd(BufferEvent bufferEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onBufferComplete()",
"Buffering complete."); hideBufferingSpinner();
}
};

BufferPreparedEventListener bufferPreparedEventListener = new BufferPreparedEventListener() {
@Override
public void onBufferPrepared() {
}
};
// seek events.
SeekBeginEventListener seekBeginEventListener = new SeekBeginEventListener() {

@Override
public void onSeekBegin(SeekEvent seekEvent) { PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekStart()", "Seek starting.");
inTrickPlayMode = false;
}
};
SeekEndEventListener seekEndEventListener = new SeekEndEventListener() {
@Override
public void onSeekEnd(SeekEvent seekEvent) {
double adjustedTime = seekEvent.getActualPosition();
PMPDemoApp.logger.i(LOG_TAG +
"::MediaPlayer.QOSEventListener#onSeekComplete()", "Seek complete at position: " + adjustedTime + ".");
_controlBar.setPosition((long) adjustedTime);
if (adjustedTime == _mediaPlayer.getPlaybackRange().getEnd() &&
_mediaPlayer.getStatus() == MediaPlayerStatus.COMPLETE) {
// Show the replay button. showReplayButton();
}
if (_mediaPlayer.getStatus() == MediaPlayerStatus.PAUSED) {
// Show the pause icon.
_controlBar.pause();
}
}
};
/**
* LoadInformationEventListener that intercepts PSDK load info events
*/
private final LoadInformationEventListener loadInfoEventListener = new LoadInformationEventListener() {

@Override
public void onLoadInformation(LoadInformationEvent event) { LoadInformation loadInfo = event.getLoadInfomation(); PMPDemoApp.logger.i(
LOG_TAG + "::LoadInformationEventListener#onLoadInfomation()", "Url: " + loadInfo.getUrl() + ", size: "
+ loadInfo.getSize()
+ " bytes, download duration: "
+ loadInfo.getDownloadDuration() + "ms");
}
};
```

## 实用资源 {#helpful-resources}

* 请参阅 [Adobe Primetime学习和支持页面上的完整帮助文档](https://helpx.adobe.com/support/primetime.html) 。