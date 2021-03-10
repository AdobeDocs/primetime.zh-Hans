---
title: TVSDK转换 — 对于JavaScript，为1.3到2.0
description: 2.0的许多方法签名和API元素名称已更改。请查看这些表以查看所有API更改详细信息。
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
translation-type: tm+mt
source-git-commit: b33240bf1b42b80389cd95a7ae4d3f85185a2d32
workflow-type: tm+mt
source-wordcount: '5034'
ht-degree: 0%

---


# TVSDK转换 — 对于JavaScript {#tvsdk-conversion-to-for-javascript}，为1.3到2.0

2.0的许多方法签名和API元素名称已更改。请查看这些表以查看所有API更改详细信息。

## 在JavaScript {#implement-callback-functions-in-javascript}中实现回调函数

方法文档中的注释建议您需要实施的回呼的签名。

对于JavaScript，API语法基于Web ID。 对于TVSDK接口，方法名称称为&#x200B;*methodName*()。 对于应用程序要实现的方法，将向接口添加一个名为&#x200B;*methodName* CallbackFunc的读/写属性，并且应用程序应将其设置为指向实现该方法的函数。 例如：

```shell
// An app implementable interface
interface ContentFactory
{
    /*
     * AdPolicySelector retrieveAdPolicySelector(MediaPlayerItem item);
     */
    attribute Object retrieveAdPolicySelectorCallbackFunc;
 
    /*
     * ContentResolverList retrieveResolvers(MediaPlayerItem item);
     */
    attribute Object retrieveResolversCallbackFunc;
 
    /*
     * OpportunityGeneratorList retrieveGenerators(MediaPlayerItem item);
     */
    attribute Object retrieveGeneratorsCallbackFunc;
};

// this is how to implement it
var factory = new AdobePSDK.ContentFactory();
factory.retrieveAdPolicySelectorCallbackFunc = function(item)
{
    // return your adPolicySelector according to the item
    return adPolicySelector;
}
 
mediaPlayerItemConfig = new AdobePSDK.MediaPlayerItemConfig ();
playerConfig.adFactory = factory;
// Use this config to load new MediaResource
```

## 2.0 {#advertising-workflow-api-element-changes-for}的广告工作流API元素更改

这些表比较了版本1.3和2.0之间JavaScript TVSDK的广告工作流API元素。

本主题中的表：

* TimedMetadata
* AdSigningMode
* 广告元数据
* CustomRangeMetadata
* ReplaceTimeRange
* 放置
* 机会
* 保留
* 时间轴/时间轴项/时间轴标记
* AdBreak
* Ad / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset
* AdBreakTimelineItem / AdTimelineItem
* AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector
* 时间轴操作
* AdBreakPlacement
* AuditudeSettings

### TimedMetadata {#timedmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>TimedMetadata</strong>:接口TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ; <br /> const unsigned short metadata_TYPE_ID3 = 1 ; <br /> 只读属性unsigned short type; <br /> readonly属性long time;readonly<br /> 属性DomString id;readonly<br /> 属性DomString名称；<br /> readonly属性DomString内容； <br /> 只读属性对象元数据；<br /> }; </p> </td> 
   <td><p>interfaceTimedMetadata {<br />包含未签名的短METADATA_TYPE_TAG = 0 ;<br />包含未签名的短METADATA_TYPE_ID3 = 1 ;<br />只读属性unsigned short metadataType;<br />只读属性长时间；<br />只读属性长id;<br />只读属性domString name;<br /> <br />只读属性对象元数据；<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>:（2.0没有变化）</td> 
   <td><p>接口TimedMetadataList {<br />只读属性unsigned long length;<br /> getter TimedMetadata(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdSigningMode {#adsignalingmode}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口AdSigningMode { <br />控制未签名短MODE_DEFAULT， <br />控制未签名短MODE_MANIFEST_CEASS， <br />控制未签名短MODE_SERVER_MAP， <br />控制未签名短MODE_CUSTOM_RANGES <br /> };</p> </td> 
   <td>这将替换MetadataKeys::MANIFEST_CAIS键。</td> 
  </tr> 
 </tbody> 
</table>

### AdvertisingMetadata {#advertisingmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口AdvertisingMetadata { <br />属性AdSigningMode模式；<br />属性AdBreakWatchedPolicy adBreakAsWatched;<br />属性boolean livePreroll;<br />属性boolean delayAdLoading ;<br /> };</p> </td> 
   <td>此功能由<p>MetadataKeys::ADVERTISING_METADATA</p> key.</td> 
  </tr> 
 </tbody> 
</table>

### CustomRangeMetadata {#customrangemetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口CustomRangeMetadata { <br />控制未签名的短TYPE_MARK_RANGE;<br /> const unsigned short TYPE_DELETE_RANGE;<br /> const unsigned short TYPE_REPLACE_RANGE;<br />属性未签名短类型；<br />属性boolean adjustSeekPosition;<br />属性TimeRangeList timeRangeList;<br /> };</p> </td> 
   <td>（2.0新增）</td> 
  </tr> 
 </tbody> 
</table>

### ReplaceTimeRange {#replacetimerange}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaceReplaceTimeRange { <br />属性unsigned long begin;<br /> readonly属性unsigned long end;<br />属性未签名的长持续时间；<br />属性unsigned long replaceDuration;<br /> };</p> </td> 
   <td>（2.0新增）</td> 
  </tr> 
 </tbody> 
</table>

### 位置{#placement}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口位置{ <br />包含未签名的短TYPE_MID_ROLL;<br /> const unsigned short TYPE_PRE_ROLL;<br /> const unsigned short TYPE_POST_ROLL;<br /> const unsigned short TYPE_SERVER_MAP;<br /> const unsigned short TYPE_CUSTOM_RANGE;<br /> readonly attribute unsigned short type;<br />只读属性时间较长；<br />只读属性长持续时间；<br /> const unsigned short MODE_DEFAULT;<br /> const unsigned short MODE_INSERT;<br />控制未签名的短MODE_REPLACE;<br /> const unsigned short MODE_DELETE;<br /> const unsigned short MODE_MARK;<br />控制未签名的短MODE_FREE_REPLACE;<br />只读属性未签名短模式；<br />只读属性TimeRange范围；<br /> };</p> </td> 
   <td>（2.0新增）</td> 
  </tr> 
 </tbody> 
</table>

### 机会{#opportunity}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口机会{ <br />只读属性DomString id;<br />只读属性放置；<br />只读属性对象设置；<br /> readonly属性Object customParameters;<br /> }; </p> </td> 
   <td>（2.0新增）</td> 
  </tr> 
 </tbody> 
</table>

### 保留{#reservation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口保留{ <br />只读属性TimeRange范围；<br /> readonly属性long hold;<br /> }; </p> </td> 
   <td> （2.0新增）</td> 
  </tr> 
 </tbody> 
</table>

### 时间轴/时间轴项/时间轴标记{#timeline-timelineitem-timelinemarker}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p><strong>时间轴</strong>:接口时 <br /> 间线{只读属性TimelineMarkerList timelineMarkers; <br /> 只读属性TimelineItemList timelineItems; <br /> 多次convertToLocalTime(多次时间); <br /> 多次convertToVirtualTime(多次时间); <br /> };</p> </td> 
   <td><p>接口时间线{<br />只读属性TimelineMarkerList timelineMarkers;<br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>TimelineItem</strong>:interfaceTimelineItem:<br /> TimelineMarker {<br /> readonly属性long id; <br /> 只读属性TimeRange virtualRange; <br /> 只读属性TimeRange localRange; <br /> 只读属性boolean watched; <br /> 只读属性布尔临时； <br /> }; </p> </td> 
   <td>（2.0新增）</td> 
  </tr> 
  <tr> 
   <td><strong>时间轴标记</strong>:（2.0没有变化）</td> 
   <td><p>interfaceTimelineMarker {<br />只读属性多次时间；<br />只读属性多次持续时间；<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdBreak {#adbreak}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口AdBreak {<br /> <br /> <br /> <br />只读属性多次持续时间；<br />只读属性AdList广告；<br /> <br /> <br />只读属性AdInsertionType插入类型；<br /> }; </p> </td> 
   <td><p>接口AdBreak {<br />只读属性多次时间；<br />只读属性多次replaceDuration;<br /> <br />只读属性多次持续时间；<br />只读属性AdList adList;<br /> <br />只读属性DomString数据；<br /> <br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### Ad / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset {#ad-adasset-adclick-adlist-adassetlist-adbannerasset}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>广告</strong>:interface Ad {readonly<br /> 属性AdAsset primaryAsset;readonly<br /> 属性AdAssetList companionAssets;readonly属性多次持续时间；readonly<br /> <br /> 属性DomString id;const short ADTYPE_LINEAR = 0 <br /> <br /> <br /> <br /> <br /> <br /> const unsigned short AD类型；只读AdInSERTIONType ADInSERTIONType; <br /> <br /> 只读属性布尔可单击； <br /> 只读属性boolean isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>接口Ad {<br />只读属性AdAsset primaryAsset;<br />只读属性AdAssetList companionAssets;<br /> <br />只读属性多次持续时间；<br />只读属性DomString id;<br />连续未签名的短ADTYPE_LINEAR = 0;<br />const unsigned short ADTYPE_NONLINERAL = 1;<br /> <br /> readonly属性unsigned short type;<br /> readonly属性AdInsertionType insertionType;<br />只读属性对象跟踪器；<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>:（2.0没有变化）</td> 
   <td><p>接口AdAsset {<br />只读属性DomString id;<br />只读属性多次持续时间；<br />只读属性MediaResource资源；<br />只读属性AdClick adClick;<br />只读属性Object元数据；<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>:（2.0没有变化）</td> 
   <td><p>接口AdClick {<br />只读属性DomString id;<br />只读属性DomString title;<br />只读属性DomString url;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>:（2.0没有变化）</td> 
   <td><p>接口AdList {<br />只读属性unsigned long length;<br /> getter Ad(unsigned long index);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>:（2.0没有变化）</td> 
   <td><p>接口AdAssetList {<br />只读属性unsigned long length;<br /> getter AdAsset(unsigned long index);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>:接口AdBannerAsset:AdAsset<br /> {<br /> readonly attribute int width;readonly<br />  attribute int height;readonly <br /> attribute DomString staticUrl;readonly <br /> attribute DomString height;<br /> readonly attribute DomString width<br /> ;};</p> </td> 
   <td> 2.0中的新增功能</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakTimelineItem / AdTimelineItem {#adbreaktimelineitem-adtimelineitem}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>AdBreakTimelineItem</strong>:接口AdBreakTimelineItem:TimelineItem {  <br /> readonly属性AdBreak adBreak; <br /> 只读属性AdTimelineItemList项； <br /> }; </p> </td> 
   <td> （2.0新增）</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>:接口AdTimelineItem:TimelineItem {  <br /> readonly属性AdBreak adBreak; <br /> 只读属性广告； <br /> }; </p> </td> 
   <td> （2.0新增）</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>:interfaceAdBreakTimelineItemList {  <br /> readonly attribute unsigned longgh; <br /> getterAdBreakTimelineItem（未签名的lo ng索引）； <br /> };</p> </td> 
   <td> （2.0新增）</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector {#adbreakpolicy-adbreakwatchedpolicy-adpolicy-adpolicymode-adpolicyinfo-adpolicyselector}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口AdBreakPolicy {<br />只读属性short AD_BREAK_POLICY_SKIP;<br />只读属性short AD_BREAK_POLICY_PLAY;<br />只读属性short AD_BREAK_POLICY_REMOVE;<br />只读属性short AD_AD_AD_BREK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> 接口AdPolicyConstants {<br />只读属性short AD_BREAK_POLICY_SKIP;<br />只读属性short AD_BREAK_POLICY_PLAY;<br />只读属性short AD_BREAK_POLICY_REMOVE;<br />只读属性shortAD_POLICY_REMOVE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interfaceAdBreakWatchPolicy {<br />只读属性short AD_BREAK_AS_WATCHED_ON_BEGIN;<br />只读属性shortAD_BREAK_AS_WATCHED_ON_END;<br />只读属性shortAD_BREAD_BREK_BREK_BREK_AS_AS_AS_AS_ASWATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br />只读属性short AD_BREAK_AS_WATCHED_ON_BEGIN;<br />只读属性short AD_BREAK_AS_WATCHED_ON_END;<br />只读属性short AD_BREAK_AS_WAS_WATCH_NEVER;&lt;at;<br />...</p> </td> 
  </tr> 
  <tr> 
   <td><p>接口AdPolicy {<br />只读属性short AD_POLICY_PLAY;<br />只读属性short AD_POLICY_PLAY_FROM_AD_BEGIN;<br />只读属性short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;只读属性short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br /> readonly属性short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br />只读属性short AD_POLICY_PLAY;<br />只读属性short AD_POLICY_PLAY_FROM_AD_BEGIN;<br />只读属性shortAD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br />仅属性short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br />只读属性short AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>接口AdPolicyMode {<br />只读属性short AD_POLICY_MODE_PLAY;<br />只读属性short AD_POLICY_MODE_SEEK;<br />只读属性short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {readonly attribute short AD_POLICY_MODE_PLAY;<br /> readonly attribute short AD_POLICY_MODE_SEEK;<br /> readonly attribute short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaceAdPolicyInfo {<br />只读属性AdBreakTimelineItemList <br /> adBreakTimelineItems;<br />只读属性AdTimelineItem adTimelineItem;<br />只读属性多次currentTime;<br />只读属性多次搜索toTime;<br />只读属性多次率；<br />只读属性短模式；//AdPolicyMode<br /> };</p> </td> 
   <td><p>interfaceAdPolicyInfo {<br />只读属性AdBreakPlacementList <br /> adBreakAptiens;<br />只读属性Ad;<br />只读属性多次currentTime;<br />只读属性多次seekToTime;<br />只读属性多次速率；a6/&gt;只读属性短模式；//AdPolicyMode<br /> };<br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>接口AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br />属性Object selectPolicyForAdBreakCallbackInfofunc;<br /> /**<br /> * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br />属性Object selectAdBreaksToPlayCallbackInfofunc;<br /> /**<br /> * AdPolicy selectForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br />属性Object selectPolicyForSeekIntoAdAdcallbackFunc;<br /> /**<br /> * AdBreakWatchPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br />属性对象selectWatkedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>接口AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectForAdBreak(<br /> * AdPolicyInfo adPolicyPolicyInfo);<br /> */<br />属性Object selectPolicyForAdBreakFuncFunc回调；<br /> /**<br /> * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br />属性Object selectAdBreaksToPlayCallback;&lt;allback;<br /> /**<br /> * AdPolicy selectForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br />属性Object selectPolicyForSeekIntoAdCallback;<br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br />属性对象selectWatedPolicyForAdBreakCallback;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TimelineOperation {#timelineoperation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口TimelineOperation { <br />只读属性放置；<br /> };</p> </td> 
   <td> （2.0新增）</td> 
  </tr> 
 </tbody> 
</table>

### AdBreakPlacement {#adbreakplacement}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口AdBreakPlacement:TimelineOperation {<br />只读属性AdBreak adBreak;<br />只读属性放置；//从TimelineOperation<br />只读属性多次时间；<br />只读属性多次持续时间；<br /> };</p> </td> 
   <td><p>interfaceAdBreakPlacement {<br />只读属性AdBreak adBreak;<br />只读属性Placement;<br />只读属性多次时间；<br />只读属性多次持续时间；<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AuditudeSettings {#auditudesettings}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口AuditudeSettings:AdvertisingMetadata { <br />属性DomString zoneId;<br />属性DomString mediaId;<br />属性DomString defaultMediaId ;<br />属性DomString域；<br />属性Object targettingInfo ;<br />属性Object customParameters;<br />属性Boolean creativePackaingEnabled ;<br />属性Boolean showStaticBanners ;<br /> };</p> </td> 
   <td>功能由MetadataKeys::AUDITUDE_METADATA_KEY提供。</td> 
  </tr> 
 </tbody> 
</table>

## 2.0 {#customization-api-element-changes-for}的自定义API元素更改

这些表比较了版本1.3和2.0之间JavaScript TVSDK的自定义API元素。

本主题中的表：

* MediaPlayerItemConfig
* ContentFactory
* 网络配置

### MediaPlayerItemConfig {#mediaplayeritemconfig}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaceMediaPlayerItemConfig {<br />属性ContentFactory adFactory;<br />属性StringList subscribeTags;<br /> <br />属性StringList adTags;<br /> <br /> <br />属性AdSigningMode;<br />属性CustomRangeMetadata customRangeMetadata;<br />属性NetworkConfiguration networkConfiguration;<br />属性AdvertisingMetadata advertisingMetadata;<br />属性Boolean useHardwareDecoder;<br /> };</p> </td> 
   <td><p>interfaceMediaPlayerConfig {<br /> <br /> <br /> <br />属性StringList adTags;<br />属性StringList subscriedTags;<br />属性MediaPlayerClientFactoryFactory;<br /> <br /> <br /> <br /> &lt;a&gt; <br />a10/&gt; <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### ContentFactory {#contentfactory}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaceContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector（<br /> * MediaPlayerItem项）；<br /> */<br />属性Object retrieveAdPolicySelectorCallbackFunc;<br />;</p> </td> 
   <td><p>interfaceMediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector（<br /> * MediaPlayerItem项）；<br /> */<br />属性Object retrieveAdPolicySelectorFunc;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### NetworkConfiguration {#networkconfiguration}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaceNetworkConfiguration<br /> {<br />属性boolean forceNativeNetworking;<br />属性boolean useRedirectedUrl;<br />属性Object cookieHeader;<br />属性boolean readSetCookieHeader;<br />属性int masterUpdateInterIntervateInterIntervateInterva;<br />属性boolean useCookieHeaderForAllRequests;<br />属性int readLimit;<br /> };</p> </td> 
   <td>在1.3中，部分此功能是由MetadataKeys提供的</td> 
  </tr> 
 </tbody> 
</table>

## 2.0 {#drm-api-element-changes-for}的DRM API元素更改

这些表比较了版本1.3和2.0之间的JavaScript TVSDK的DRM API元素。

本主题中的表：

* DRM工作流初始化
* DRMAcquireLicenseSettings/DRMAuthenticationMethod
* DRMMetadata
* DRMPlaybackTimeWindow
* DRMLicense
* DRMLicenseDomain
* DRMPolicy
* DRMManager

### DRM工作流初始化{#drm-workflow-initialization}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>应用程序需要调用AdobePSDK.initiateDRMWorkflow以启动DRM工作流。 没有此呼叫，DRM视频将无法播放。<p>接口AdobePSDK<br /> {<br /> void initiateDRMWorkFlow(<br /> DomString appStoratePath， <br /> DomString publisherId， <br /> DomString appId， <br /> AppVersion， <br /> boolean privacyModeOn);<br /> };</p> </td> 
   <td>初始化是在内部完成的，不需要显式调用。</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| 2.0 API | 1.3 API |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| 2.0没有更改。 | enum DRMAcquireLicenseSettings <br>{<br> const unsigned int FORCE_REFRESH = 0;<br> const unsigned int LOCAL_ONLY = 1;<br> const unsigned int ALLOW_SERVER = 2;<br> }; |
| **DRMAuthenticationMethod** |  |
| 2.0没有更改。 | enum DRMAuthenticationMethod <br>{<br> const unsigned int UNKNOWN = 0;<br> const unsigned int ANNOMYS = 1;<br> const unsigned int USERNAME_AND_PASSWORD = 2;<br> } |

### DRMMetadata {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0没有更改。</td> 
   <td><p>interfaceDRMMetadata<br /> {<br />只读属性DomString serverUrl;<br />只读属性DomString licenseId;<br />只读属性DRMPolicyArray策略；<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPlaybackTimeWindow {#drmplaybacktimewindow}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaceDRMPlaybackTimeWindow {<br /> readonly attribute int playbackPeriodInSeconds;<br /> readonly attribute long playbackStartDate;<br /> readonly attribute long playbackEndDate;<br /> };</p> </td> 
   <td><p>interface DRMPlaybackTimeWindow {<br /> readonly attribute int periodInSeconds;<br /> readonly attribute int startDate;<br /> readonly attribute intentDate;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicense {#drmlicense}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0没有更改。</td> 
   <td><p>interfaceDRMLicense {<br />只读属性Uint8Array bytes;<br />只读属性Date licenseStartDate;<br />只读属性Date licenseEndDate;<br />只读属性Date offflineStorageStartDate;<br />只读属性Date offlineStorageEndStoreStorageEnd日期；<br />只读属性DomString serverUrl;<br />只读属性DomString licenseID;<br />只读属性DomString policyID;<br />只读属性DRMPlaybackTimeWindow playbackTimeWindow;<br />只读属性Object customPropertiter;<br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMLicenseDomain {#drmlicensedomain}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaceDRMLicenseDomain {<br />只读属性DomString authenticationDomain;<br />只读属性DRMAuthenticationMethod authenticationMethod;<br />只读属性DomString serverUrl;<br /> };</p> </td> 
   <td><p>interfaceDRMLicenseDomain {<br />只读属性DomString authDomain;<br />只读属性DRMAuthenticationMethod authMethod;<br />只读属性DomString serverURL;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPolicy {#drmpolicy}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaceDRMPolicy<br /> {<br />只读属性DomString authenticationDomain;<br />只读属性DRMAuthenticationMethod authenticationMethod;<br /> <br />只读属性DomString displayName;<br />只读属性DRMLicenseDomain lice域；<br /> }</p> </td> 
   <td><p>interfaceDRMPolicy<br /> {<br />只读属性DomString authDomain;<br />只读属性DRMAuthenticationMethod authMethod;<br />只读属性DomString dispName;<br />只读属性DRMLicenseDomain licenseDomainDomain;5/&gt; };<br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMManager {#drmmanager}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口DRMManager:EventTarget {<br /> void acquireLicense（DRMMetadata元数据， <br /> DRMAcquireLicenseSettings， <br /> DRMAquireLicenseListener）；<br /> void acquirePreviewLicense(DRMMetadata， <br /> DRMAQuireLicenseListener);<br /> void authenticate（DRMMetadata， <br /> DomString url，<br /> DomString &amp;authenticationDomain， <br /> DomString用户， <br /> DomString密码， <br /> DRMAuthenticatelistener）；<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array， DRMErrorListener);<br /> void initialize(DRMOperationCompleteListener);<br />属性long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain， <br /> boolean forceRefresh， <br /> DRMOperationCompleteListener);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain， <br /> DRMOperationCompleteListener);<br /> <br /> void resetDRM(DRMOperationCompleteListener);&lt;a)26/&gt; void returnLicense(DomString serverURL， <br /> DomString licenseID， <br /> DomString policyID， <br /> boolean commitImtedially，<br /> DRMReturLicenseListener);<br /> void setAuthenticationToken（<br /> DRMMetadata元数据， <br /> DomString authenticationDomain， <br /> Uint8Array令牌， <br /> DRMOperationCompleteListener）；<br /> void storeLicenseBytes(Uint8Array licenseBytes， <br /> DRMOperationCompleteListener);<br /> };<br /></p> </td> 
   <td><p>接口DRMManager:EventTarget {<br /> void acquireLicense（DRMMetadata元数据， <br /> DRMAcquireLicenseSettings， <br /> EventContext eventContext）；<br /> void acquirePreviewLicense(DRMMetatadata， <br /> EventContextContextContext);<br /> void authenticate（DRMMetadata元数据，<br /> DomString url，<br /> DomString &amp;authenticationDomain， <br /> DomString用户， <br /> DomString密码， <br /> EventContext）；<br />12/&gt; DRMMetadata createMetadataFromBytes(<br /> Uint8Array， EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> attribute longOperationTime;<br />a17/&gt; void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain， <br /> boolean forceRefresh， <br /> EventContext);<br /> void leaveLicenseDomain(<br /> DRMLICENSEDomain licenseDomain， <br /> EventContext eventContext);<br /> <br /> void resetDRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL， <br /> DomString licenseID，<br /> DomString policyID， <br /> boolean commitImmetially，<br /> EventContext);<br /> void setAuthenticationToken（<br /> DRMMetadata元数据，<br /> DomString authenticationDomain、<br /> Uint8Array令牌、<br /> EventContext事件Context）；<br /> void storeLicenseBytes（Uint8Array licenseBytes， <br /> EventContext事件Context）；<br /> };<br /><br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMErrorListener :<br /> public psdkutils::PSDKInterfaceWithUserData {<br /> public:<br /> virtual void onDRMError(uint32_t major， <br /> uint32_t minor， <br /> const psdkutils:PSDKString&amp;errorString， <br /> const psdkutils::PSDKString&amp; errorServerUrl)= 0;<br /> <br />受保护：<br />虚拟~DRMErrorListener(){} <br /> }</p> </td> 
   <td>事件/界面/说明 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>在DRMManger的异步方法之一期间发生错误时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMOperationCompleteListener :<br /> public DRMErrorListener {<br /> public:<br /> virtual void onDRMOperationComplete()= 0;<br /> <br />受保护：<br />虚拟~DRMOperationCompleteListener(){} <br /> };</p> </td> 
   <td>事件/界面/说明 
    <ul> 
     <li>kEventDRMInitializationComplete<p>/ PSDKEvent</p> <p>完成DRM初始化时。</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>joinLicenseDomain()操作成功完成时。</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>leaveLicenseDomain()操作成功完成。</p> </li> 
     <li>kEventDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>resetDRM()操作成功完成时。</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEvent</p> <p>setAuthenticationTokenSet()操作成功完成时。</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEvent</p> <p>当storeLicenseBytes()操作成功完成时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMAuthenticateListener:<br />公用DRMErrorListener {<br />公用：<br /> virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken)= 0;<br /> <br />受保护：<br /> ~drmauthenticateListener(){}<br /> }</p> </td> 
   <td>事件/界面/说明 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>当DRMManager::authenticate方法调用成功时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMAquireLicenseListener:<br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseAppired(const DRMLicense*)= 0;<br /> <br /> protected:<br /> virtual ~DRMAquireLicensenseListener(){} {}<br /> };</p> </td> 
   <td>事件/界面/说明 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquired<p>/ DRMLicenseAppiredEvent</p> <p>当DRMManager::acquirePreviewLicense方法调用成功时。</p> </li> 
     <li>kEventDRMLicenseAppired<p>/ DRMLicenseAppiredEvent</p> <p>当DRMManager::acquireLicense方法调用成功时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMReturnLicenseListener:<br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseReturnComplete(uint32_t numReturned)= 0;<br /> <br /> protected:<br /> ~ virtual DRMReturnLicenseListener(){} {} <br />;</p> </td> 
   <td>事件/界面/说明 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>当DRMManager::returnLicense方法调用成功时。</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 2.0 {#generic-playback-api-element-changes-for}的通用回放API元素更改

这些表比较JavaScript TVSDK 1.3和2.0之间的通用播放API元素。

本主题中的表：

* 媒体资源
* MediaPlayer
* ABRControlParameters
* BufferControlParameters
* TextFormat
* MediaPlayerItemLoader

### MediaResource {#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface MediaResource {<br />属性DomString url;<br />属性未签名短类型；<br />属性对象元数据；<br />控制未签名短类型TYPE_HLS;<br />控制未签名短类型TYPE_DASH;<br />控制未签名短类型TYPE_CUSTOM;<br />控制未签名短类型TYPE;<br />_UNKNOWN;<br /> };</p> </td> 
   <td><p>interfaceMediaResource {<br />属性DomString url;<br />属性DomString类型；<br />属性对象元数据；<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayer {#mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口MediaPlayer:EventTarget<br /> {<br /> void prepareToPlay(多次位置);<br /> void play();<br /> void pause();<br /> void seek(多次位置);<br /> void seekToLocal(多次位置);<br /> void reset();<br /> void release);<br /> void replaceCurrentItem（MediaPlayerItem项）；<br /> void replaceCurrentResource（MediaResource资源， <br /> MediaPlayerItemConfig）；<br /> void suspend();<br /> void restore();<br /> void notifyClick();<br /> <br />只读属性TimeRange playbackRange;<br />只读属性TimeRange seekableRange;&lt;ableRange&gt;只读属性多次currentTime;<br />只读属性多次localTime;<br />只读属性TimeRange bufferedRange;<br />只读属性DRMManager drmManager;<br />只读属性MediaPlayerItem currentItem;<br /> <br /> // PlayerStatus<br /> <br /> <br /> <br />控制未签名的短PLAYER_STATUS_INITIALIZED;<br />控制未签名的短PLAYER_STATUS_PREPARING;<br />控制未签名的短PLAYER_PLAYER_status_PREPARED;<br />包含未签名短播放器_状态_播放；<br />包含未签名短播放器_状态_暂停；<br />包含未签名短播放器_状态_搜索；<br />包含未签名短播放器_状态_SEEKINGcomplete;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> <br /> readonly attribute short status;<br /> <br /> attribute sunignsigned volumededed9/&gt; attribute ABRControlParameters abrControlParameters;<br /> attribute BufferControlParameters bufferControlParameters;<br /> <br />包含无符号短VISIBLE;//对于CC可见性<br />，无符号短不可见；//对于CC可见性<br />属性unsigned short ccVisibility;<br />属性TextFormat ccStyle;<br />只读属性PlaybackMetricsMetrics;<br /> <br />属性多次率；<br />属性MediaPlayer查看视图;<br />只读属性时间轴；<br />属性多次currentTimeUpdateInterval;<br /> //设置2.0<br /> }不支持此设置；<br /></p> </td> 
   <td><p>接口MediaPlayer:EventTarget<br /> {<br /> void prepareToPlay(int position);<br /> void play();<br /> void pause();<br /> void seekToLocalTime(int position);<br /> void reset();<br /> void release);<br /> void replaceCurrentItem（MediaResource源）；<br /> <br /> <br /> <br /> <br /> <br /> <br />只读属性TimeRange playbackRange;<br />属性TimeRange seekableRange;<br />只读属性多次 currentTime;<br />只读属性多次localTime;<br />只读属性TimeRange bufferedRange;<br />只读属性DRMManager drmManager;<br />仅属性MediaPlayerItem currentItem;<br /> <br /> // PlayerState<br />包含未签名的短PLAYER_STATE_IDLE;<br />包含未签名的短PLAYER_STATE_INITIALIZING;<br />包含未签名的短PLAYERSTATE_INITIALIZED;<br />控制未签名短PLAYER_STATE_PREPARING;<br />控制未签名短PLAYER_STATE_PREPARED;<br />控制未签名短PLAYER_STATE_PLAYING;<br />控制未签名短PLAYER_STATEPAUSED;<br />继续未签名的短PLAYER_STATE_SEEKING;<br />继续未签名的短PLAYER_STATE_COMPLETE;<br />继续未签名的短PLAYER_STATE_ERROR;<br />继续未签名的短PLAYER_STATE_RELEASE;<br />const unsigned short PLAYER_STATUS_SUSPENDED;<br /> readonly attribute unsigned short state;<br /> <br /> attribute unsigned short volume;<br /> attribute ABRControlParameters abreters;&lt;aters;<br />属性BControlParameters bufferControlParameters;<br /> <br />只读未签名的短VISIBLE;//对于CC可见性<br />只读未签名短INVISIBLE;//对于CC可见性<br />属性unsigned short ccVisibility;<br />属性TextFormat ccStyle;<br />只读属性PlaybackMetrics playbackMetrics;<br />属性MediaPlayerConfig;<br />属性多次rate;<br />属性MediaPlayerView视图;<br />只读属性时间轴；<br /> <br /> <br /> };<br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>interfaceMediaPlayerStatus<br /> {<br /> // PlayerStatus<br />控制未签名短PLAYER_STATUS_IDLE;<br />控制未签名短PLAYER_STATUS_INITIALIZED;<br />控制未签名短PLAYER_STATUS_INITIALIZED;<br />player_STATUS_PREPARING;<br />包含未签名的短PLAYER_STATUS_PREPARED;<br />包含未签名的短PLAYER_STATUS_PLAYING;<br />包含未签名的短PLAYER_STATUS_SEEKING;<br />连接未签名的短PLAYER_STATUS_COMPLETE;<br />连接未签名的短PLAYER_STATUS_ERROR;<br />连接未签名的短PLAYER_STATUS_RELEASED;<br />连接未签名的短PLAYER_STATUS_SUSPENDED;<br />;<br /></p> </td> 
   <td>（2.0新增）</td> 
  </tr> 
 </tbody> 
</table>

#### 事件受MediaPlayer {#events-supported-by-mediaplayer}支持

<table> 
 <tbody> 
  <tr> 
   <th>2.0事件名称</th> 
   <th>2.0接口</th> 
   <th> </th> 
   <th>1.3事件名称</th> 
   <th>1.3接口</th> 
  </tr> 
  <tr> 
   <td><p>（2.0版已删除）</p> </td> 
   <td> </td> 
   <td> </td> 
   <td>准备</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td><p>itemUpdated</p> <p>媒体播放器项目更新时。</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>更新</p> <p>媒体播放器成功更新媒体时。</p> </td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>timedMetadataAvailable</td> 
   <td>TimedMetadataEvent</td> 
   <td> </td> 
   <td>TtmedMetadata</td> 
   <td>TimedMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>timelineUpdated</td> 
   <td>事件</td> 
   <td> </td> 
   <td>TetmelineUpdated</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>已在2.0中删除</td> 
   <td> </td> 
   <td> </td> 
   <td>playStart</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>已删除2.0</td> 
   <td> </td> 
   <td> </td> 
   <td>playComplete</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>statusChanged</td> 
   <td>StatusEvent</td> 
   <td> </td> 
   <td>stateChanged</td> 
   <td>StateEvent</td> 
  </tr> 
  <tr> 
   <td>sizeAvailable</td> 
   <td>SizeEvent</td> 
   <td> </td> 
   <td>大小</td> 
   <td>SizeEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakStarted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakStart</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adStarted</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>adStart</td> 
   <td>AdEvent</td> 
  </tr> 
  <tr> 
   <td>adProgress</td> 
   <td>AdProgressEvent</td> 
   <td> </td> 
   <td>adProgress</td> 
   <td>AdProgressEvent</td> 
  </tr> 
  <tr> 
   <td>adCompleted</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>adComplete</td> 
   <td>AdEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakCompleted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakComplete</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>timeChanged</td> 
   <td>TimeEvent</td> 
   <td> </td> 
   <td>进展</td> 
   <td>ProgressEvent</td> 
  </tr> 
  <tr> 
   <td>bufferingBegin</td> 
   <td>事件</td> 
   <td> </td> 
   <td>缓冲区</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>bufferingEnd</td> 
   <td>事件</td> 
   <td> </td> 
   <td>bufferComplete</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>seekBegin</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>seekStart</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>seekEnd</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>seekComplete</td> 
   <td>TimeEvent</td> 
  </tr> 
  <tr> 
   <td>loadInformationAvailable</td> 
   <td>LoadInformationEvent</td> 
   <td> </td> 
   <td>loadInfo</td> 
   <td>LoadInfoEvent</td> 
  </tr> 
  <tr> 
   <td>operationFailed</td> 
   <td>NotificationEvent</td> 
   <td> </td> 
   <td>operationFailed</td> 
   <td>ErrorEvent</td> 
  </tr> 
  <tr> 
   <td>drmMetadataInfoAvailable</td> 
   <td>DRMMetadataEvent</td> 
   <td> </td> 
   <td>drmMetadata</td> 
   <td>DRMMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>reservationReached</td> 
   <td>ReservationEvent</td> 
   <td> </td> 
   <td>timelineHolderReached</td> 
   <td>TimelineHolderEvent</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>bitrateChanged</td> 
   <td>BitrateChangedEvent</td> 
  </tr> 
  <tr> 
   <td>rateSelected</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>rateSelected</td> 
   <td>PlaybackRateEvent</td> 
  </tr> 
  <tr> 
   <td>ratePlaying</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>ratePlaying</td> 
   <td>PlaybackRateEvent</td> 
  </tr> 
  <tr> 
   <td>adBreakBripted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakBripted</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adClicked<br />当用户单击广告时。</td> 
   <td>AdClickedEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>profileChanged<br />当播放用户档案更改时。</td> 
   <td>ProfileEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>seekPositionAdjusted<br />当搜索位置因内部或外部规则而调整时。</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>audioUpdated<br />当媒体播放器项目更新时。 对于包含仅在播放时可检测的音轨的特定流，当有新的音轨可用时，将触发此事件。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>字幕更新<br />当媒体播放器项目更新时。 对于实时/线性流，客户端必须定期刷新媒体资源以检测新的可用内容。 发生这种情况时，某些媒体特性可能会发生变化。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>master更新<br />媒体播放器项目更新时。 对于实时/线性流，客户端必须定期刷新媒体资源以检测新的可用内容。 发生这种情况时，某些媒体特性可能会发生变化。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRangeUpdated<br />当媒体播放器项目更新时。 对于实时/线性流，客户端必须定期刷新媒体资源以检测新的可用内容。 发生这种情况时，某些媒体特性可能会发生变化。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>timedEvent<br />在生成定时事件时发送。</td> 
   <td>TimedEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
  </tr> 
 </tbody> 
</table>

### ABRControlParameters {#abrcontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaceABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVAL = 0 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 1 ;<br /> <br />attribute unsigned short abrPolicy;<br /> attribute unsigned int initialBitRate;<br /> attribute unsigned int minBitRate;<br /> attribute unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ ABR_ABR_MIN_BITRATE;<br />包含未签名的短DEFAULT_ABR_MAX_BITRATE;<br />包含ABRPolicy DEFAULT_ABR_POLICY;<br /> };<br /><br /></p> </td> 
   <td><p>interfaceABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVAL = 0 ;<br /> const unsigned short ABR_POLICY_AGGRESIVE = 1 ;<br /> <br />attribute unsigned short abrPolicy;<br /> attribute unsigned int initialBitRate;<br /> attribute unsigned int minBitRate;<br /> attribute unsigned int maxBitRate;<br /> <br /> <br /> <br /> };<br /><br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### BufferControlParameters {#buffercontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaceBufferControlParameters<br /> {<br />属性多次initialBufferTime;<br />属性多次playBufferTime;<br />控制多次DEFAULT_INITIAL_BUFFER_TIME;<br />控制多次DEFAULT_PLAY_BUFFER_TIME;&lt;a/&gt; };<br /></p> </td> 
   <td><p>interfaceBufferControlParameters<br /> {<br />属性多次initialBufferTime;<br />属性多次playBufferTime;<br /> <br /> <br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TextFormat {#textformat}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0没有更改</td> 
   <td><p>interfaceTextFormat<br /> {<br /> // Color<br />包含无符号短COLOR_DEFAULT = 0;<br />包含无符号短COLOR_BLACK = 1;<br />包含无符号短COLOR_GRAY = 2;<br />包含无符号短COLOR_WHITE = 3; a6/&gt;连接未签名短COLOR_BRIGHT_WHITE = 4;<br />连接未签名短COLOR_DARK_RED = 5;<br />连接未签名短COLOR_BRIGHT_RED = 6;<br />连接未签名短COLOR = 7;<br />_DARK_GREEN = 8 ;<br />未签名短COLOR_GREEN = 9 ;<br />未签名短COLOR_BRIGHT_GREEN = 10 ;<br />未签名短COLOR_DARK_BLUE = 11 ;<br /> constshort COLOR_BLUE = 12;<br />无符号短COLOR_BRIGHT_BLUE = 13;<br />无符号短COLOR_DARK_YELLOW = 14;<br />无符号短COLOR_YELLOW = 15;<br />连续未签名短色COLOR_BRIGHT_YELLOW = 16 ;<br />连续未签名短色COLOR_DARK_MAGENTA = 17 ;<br />连续未签名短色COLOR_BRIGHT_MAGENA = 19;<br />包含无符号短COLOR_DARK_CYAN = 20;<br />包含无符号短COLOR_CYAN = 21;<br />包含无符号短COLOR_BRIGHT_CYAN = 22;<br /><br />仅读属性unsigned short fontColor;<br />只读属性unsigned short backgroundColor;<br />只读属性unsigned short fillColor;<br />只读属性unsigned short edgeColor;<br /> <br /> // Size<br /> const unsigned SIZE SIZE_ DEFAULT= 0;<br /> const unsigned short SIZE_SMALL = 1;<br /> const unsigned short SIZE_MEDIUM = 2;<br /> const unsigned short SIZE_LARGE = 3;<br /> <br /> readonly attribute short size;<br /><br /> // FontEdge<br />控制未签名短FONT_EDGE_DEFAULT = 0 ;<br />控制未签名短FONT_EDGE_NONE = 1 ;<br />控制未签名短FONT_EDGE_ROUSED = 2 ;<br /> CONST UNSIGNEDSHORT FONT_EDGE_CONSECTED = 3;<br /> const unsigned short FONT_EDGE_UNIFORM = 4;<br /> const unsigned short FONT_EDGE_SHADOW_LEFT = 5;<br />const const shortFONT_EDGE_EDGE_EDGE_EDGE_EDGE_EDGE_UNSIGNED_UNSIGNEDdrop_SHADOW_RIGHT = 6 ;<br />只读属性unsigned short fontEdge;<br /> <br /> // Font<br /> const unsigned short FONT_DEFAULT = 0 ;<br /> const unsigned short FONT_MONOSPACED_WITH_WIFS = 1 ;<br />包含无符号短FONT_PROPORTION_WITH_SERIFS = 2 ;<br />包含无符号短FONT_MONSPACED_WITHOUT_SERIFS = 3 ;<br />包含无符号短FONT_CASIAL = 4 ;<br />unsigned short FONT_CURSIVE = 5;<br /> const unsigned short FONT_SMALL_CAPPALITES = 6;<br />只读未签名的short fontOpacity;<br />只读属性unsigned short backgroundOpacity;&lt;acyatattribute unsigned short fillOpacity;<br /> readonly attribute unsigned short DEFAULT_OPACITY;<br /> };<br /><br /><br /><br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### MediaPlayerItemLoader {#mediaplayeritemloader}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaceMediaPlayerItemLoader:<br /> {<br /> void load(MediaResource， long resourceId，<br /> ItemLoaderListener， <br /> MediaPlayerItemConfig);<br /> void();<br />只读属性MediaPlayerItemItemcurrentItem;<br /> };</p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
  <tr> 
   <td><p>interfaceItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br />var onErrorCallbackFunc;<br /> }</p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
 </tbody> 
</table>

## 2.0 {#media-characteristics-api-element-changes-for}的媒体特性API元素更改

这些表比较了版本1.3和2.0之间C++ TVSDK的媒体特性API元素。

本主题中的表：

* MediaPlayerItem
* Track、AudioTrack、ClosedCaptionsTrack
* 用户档案
* DRMMetadataInfo

### MediaPlayerItem {#mediaplayeritem}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaceMediaPlayerItem {<br />只读属性MediaResource;<br />只读属性long resourceId;<br />只读属性boolean live;<br /> <br />只读属性boolean hasAlternateAudio;<br />只读属性AudioTrackList audioTrackstrichoTracks;&lt;adoTroadioTradoTro属性AudioTrack selectedAudioTrack;<br /> void selectAudioTrack(AudioTrack);<br /> <br />只读属性boolean hasClosedCaptions;<br />只读属性ClosedCaptionsTrackClosedCaptionsTracks;<br />只读属性ClosedCaptionsTrack;<br /> void selectClodesCloidClodCoidCedCaptionsCaptionsCaptionsCaptionsCaptionsCaptionstrack（<br /> ClosedCaptionsTrack轨道）；<br /> <br />只读属性boolean hasTimedMetadata;<br />只读属性TimedMetadataList timedMetadata;<br />只读属性boolean dynamic;<br /> <br />只读属性boolean isProtected;<br />仅属性DRMMetadataInfoList drmMetadataInfos;<br />只读属性ProfileList用户档案;<br />只读属性用户档案selectedProfile;<br /> <br />只读属性boolean trickPlaySupported;<br />FloatArray availablePlaybackRates;<br />只读属性float selectedPlaybackRate;<br /> <br /> <br />只读属性MediaPlayer mediaPlayer;<br />只读属性MediaPlayerItemConfig;<br /> };<br /></p> </td> 
   <td><p>interfaceMediaPlayerItem {<br />只读属性MediaResource;<br />只读属性long resourceId;<br />只读属性boolean live;<br /> <br />只读属性boolean hasAlternateAudio;<br />只读属性AudioTrackList audioTracksadioTracks;&lt;adioTrachoTrachoTrachoTreaudioTrack selectedAudioTrack;<br /> <br /> <br />只读属性boolean hasClosedCaptions;<br />只读属性ClosedCaptionsTrackList ccTracks;<br />属性ClosedCtedCCTrack;&lt;acta13/&gt; <br /> <br />只读属性boolean hasTimedMetadata;<br />只读属性TimedMetadataList timedMetadata;<br />只读属性boolean dynamic;<br /> <br />只读属性boolean isProtected;<br />只读属性DRMMetadataInfoList drmMetadataInfos;<br />只读属性ProfileList用户档案;<br /> <br /> <br />只读属性boolean trickPlaySupported;<br />只读属性Int32Array availablePlaybackRates;<br /> <br />只读属性StringList adTags;<br /> <br />只读属性MediaPlayer mediaPlayer;<br /> <br /> };<br /><br /><br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### 音轨/音轨/隐藏字幕轨道{#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface Track<br /> {<br />只读属性DomString name;<br />只读属性DomString语言；<br />只读属性布尔默认值；<br />只读属性布尔值autoSelect;<br /> }; </p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
  <tr> 
   <td><p>接口AudioTrack:Track<br /> {<br />只读属性DomString名称；//FromTrack<br />只读属性DomString语言；//FromTrack<br />只读属性布尔默认值；// From Track<br /> readonly attribute autoSelect;//FromTrack<br /> <br /> readonly attribute unsigned int pid;<br /> };</p> </td> 
   <td><p>interfaceAudioTrack<br /> {<br />只读属性DomString名称；<br />只读属性DomString语言；<br />只读属性布尔默认值；<br />只读属性boolean autoSelect;<br />只读属性布尔值强制；<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0没有更改</td> 
   <td><p>interfaceAudioTrackList<br /> {<br />只读属性unsigned long length;<br /> getter AudioTrack(unsigned long index);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>接口ClosedCaptionsTrack:Track<br /> {<br />只读属性DomString名称；//FromTrack<br />只读属性DomString语言；//FromTrack<br />只读属性布尔默认值；// FromTrack<br />只读属性boolean autoSelect;// FromTrack<br /> <br /> <br />  const unsigned short SERVICE_608_CAPTIONS = 0;<br /> const unsigned short SERVICE = 1;<br />_WEB_VTT_CAPTIONS = 2;<br />只读属性unsigned short serviceType;<br />只读属性boolean forced;<br /> };</p> </td> 
   <td><p>interfaceClosedCaptionsTrack<br /> {<br />只读属性DomString name;<br />只读属性DomString语言；<br />只读属性布尔默认值；<br /> <br /> <br />只读属性布尔活动；<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0没有更改</td> 
   <td><p>interfaceClosedCaptionsTrackList<br /> {<br />只读属性unsigned long length;<br /> getter ClosedCaptionsTrack(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 用户档案{#profile}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>用户档案:2.0没有更改</td> 
   <td><p>接口用户档案<br /> {<br /> readonly attribute unsigned int width;<br /> readonly attribute unsigned int height;<br /> readonly attribute unsigned intRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList:2.0没有更改</td> 
   <td><p>interfaceProfileList<br /> {<br />只读属性unsigned long length;<br /> getter 用户档案(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMMetadataInfo {#drmmetadatainfo}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfo</strong>:2.0没有更改</td> 
   <td><p>interfaceDRMMetadataInfo<br /> { <br />只读属性DRMMetadata;<br />只读属性long prefetchTimestamp;<br />只读属性TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>:2.0没有更改</td> 
   <td><p>interfaceDRMMetadataInfoList<br /> {<br />只读属性unsigned longlength;<br /> getter DRMMetadataInfo(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 将C++错误映射到不同语言的异常{#mapping-c-errors-to-exceptions-in-different-languages}

您可以将C++错误代码映射到不同语言的异常。

C++ PSDK的API有“不抛送”策略。 大多数API方法返回PSDKErrorCode值以指示方法是否成功执行。 异步错误通过错误事件通知。

ActionScript和JAVA PSDK有不同的策略。 大多数错误将引发ArgumentError或IllegalStateException，以指示无法执行方法的同步部分。 不会捕获这些例外，应用程序代码负责处理例外。 它们通常提供方法调用失败的原因的有用信息。 例如，如果在无效状态中调用prepareToPlay命令，将引发以下异常：

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

ActionScript/JAVA还会引发构造函数的异常，以指示某些内部对象创建不正确。 这些例外是内部处理的，不会传播到应用程序。 这些例外将包含在发送到应用程序的警告通知中

例如，如果未为接收的广告响应找到有效的媒体文件，则无法创建有效的广告资产对象或广告。 因此，不会在时间轴上放置任何广告，并调度NotificationEvent.OperationFailed通知。

从Adobe视频引擎(AVE)异步接收的错误或警告代码作为普通事件调度给应用程序。 通知事件包含所有接收的错误代码和任何其他元数据，如URL、资源标识符、句柄等。 如果错误严重且无法继续播放当前媒体，则调度MediaPlayer过渡为ERROR状态和onStatusChanged回调或MediaPlayerStatusChanged.STATUS_CHANGED事件。 如果播放可以继续，则调度普通通知事件。

<table> 
 <tbody> 
  <tr> 
   <th>C++错误（PSDKError代码）</th> 
   <th> </th> 
   <th>Java</th> 
   <th>ActionScript</th> 
   <th>JavaScript</th> 
  </tr> 
  <tr> 
   <td>kECInvalidArgument</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>代码为1的异常，description = "INVALID_ARGUMENT", additionalInfo= &lt;as pass by方法引发此异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>代码为2的异常，description = "GENERIC_ERROR" and additionalInfo= &lt;as pass by方法引发此异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>代码为3的异常，description = "ILLEGAL_STATE", additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为4的异常，description = "GENERIC_ERROR" and additionalInfo= &lt;as pass by方法引发此异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为5的异常，description = "CREATION_FAILED", additionalInfo= &lt;as pass by方法引发此异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为5的异常，description = "CREATION_FAILED", additionalInfo= &lt;as pass by方法引发此异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为7的异常，description = "DATA_NOT_AVAILABLE"和additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为8的异常，description = "SEEK_ERROR" and additionalInfo= &lt;as pass by方法引发此异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupported功能</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为9的异常，description = "UNSUPPORTED_FEATURE" and additionalInfo= &lt;as pass by方法引发此异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为10的异常，description = "RANGE_ERROR", additionalInfo= &lt;as pass by方法引发此异常</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为11的异常，description = "CODEC_NOT_SUPPORTED"和additionalInfo= &lt;as pass by方法引发此异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为12的异常，description = "MEDIA_ERROR" and additionalInfo= &lt;as pass by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为13的异常，description = "NETWORK_ERROR" and additionalInfo= &lt;as pass by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error或MediaPlayerNotification.Warning</td> 
   <td>MediaError或NotificationEvent</td> 
   <td>代码为14的异常，description = "GENERIC_ERROR" and additionalInfo= &lt;as pass by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为15的异常，description = "INVALID_SEEK_TIME"和additionalInfo= &lt;as pass by方法引发此异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为16的异常，description = "AUDIO_TRACK_ERROR"和additionalInfo= &lt;as pass by方法引发此异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferent<p>线程错误</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为17的异常，description = "GENERIC_ERROR" and additionalInfo= &lt;as pass by方法引发此异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为18的异常，description = "GENERIC_ERROR", additionalInfo= &lt;as pass by方法引发此异常</td> 
  </tr> 
  <tr> 
   <td>kECNotImplemented</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为19的异常，description = "GENERIC_ERROR" and additionalInfo= &lt;as pass by方法引发此异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为200的异常，description = "PLAYBACK_OPERATION_FAILED" and additionalInfo= &lt;as pass by方法引发此异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>NotificationEvent</td> 
   <td>代码为201的异常，description = "NATIVE_WARNING", additionalInfo= &lt;as pass by方法引发此异常</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>代码为202的异常，description = "AD_RESOLVER_FAILED"和additionalInfo= &lt;as pass by方法传递的异常&gt;</td> 
  </tr> 
 </tbody> 
</table>

## 2.0 {#utility-and-helper-api-element-changes-for}的实用程序和帮助程序API元素更改

这些表比较了版本1.3和2.0之间JavaScript TVSDK的实用程序和帮助程序API元素。

本主题中的表：

* 版本
* 时间范围
* QOSProvider
* 设备信息
* LoadInfo
* 视图
* 播放信息

### 版本{#version}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口版本<br /> {<br />只读属性DomString版本；<br />只读属性DomString描述；<br />只读属性long major;<br />只读属性long minor;<br />只读属性long revision;<br />只读属性long apiVersion;<br /> };</p> </td> 
   <td><p>接口版本<br /> {<br />只读属性DomString版本；<br />只读属性DomString描述；<br />只读属性DomString主要；<br />只读属性DomString次要；<br />只读属性DomString修订版；<br />只读属性DomString apiversion;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### TimeRange {#timerange}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0没有更改</td> 
   <td><p>interfaceTimeRange<br /> {<br />只读属性unsigned long begin;<br />只读属性unsigned long end;<br />只读属性unsigned long duration;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### QOSProvider {#qosprovider}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0没有更改</td> 
   <td><p>接口QOSProvider<br /> {<br /> void attachMediaPlayer(MediaPlayer);<br /> void detachMediaPlayer();<br /> <br />只读属性DeviceInformation;<br />只读属性PlaybackInformation;<br />};</p> </td> 
  </tr> 
 </tbody> 
</table>

### 设备信息{#deviceinformation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaceDeviceInformation<br /> {<br />只读属性DomString os;<br /> <br /> <br /> <br />只读属性DomString id;<br />只读属性int intDPI;<br />只读属性int heightPixels;<br />只读属性int widthPix;<br />只读属性boolean seekToKeyFrame;<br /> };</p> </td> 
   <td><p>interfaceDeviceInformation<br /> {<br />只读属性DomString os;<br />只读属性int sdk;<br />只读属性DomString模型；<br />只读属性DomString制造商；<br />只读属性DomString id;<br />只读属性intDPI7/&gt;只读属性int heightPixels;<br />只读属性int widthPixels;<br /> <br /> };<br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### LoadInfo {#loadinfo}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0没有更改</td> 
   <td><p>interfaceLoadInfo<br /> {<br />只读属性DomString url;<br />只读属性int size;<br />只读属性多次downloadDuration;<br />只读属性int periodIndex;<br />只读属性多次 mediaDuration;<br />只读属性短TRACK_TYPE_TYPE_TYPE_TYPE_fragment;<br />只读属性short TRACK_TYPE_TRACK;<br />只读属性short TRACK_TYPE_MANIFEST;<br />只读属性short type;<br />只读属性DomString trackName;<br />只读属性DomString trackType;&lt;ackType;&lt;a;12/&gt; readonly attribute int trackIndex;<br /> };<br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### 视图{#view}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0没有更改</td> 
   <td><p>接口视图<br /> {<br />只读属性unsigned short x;<br />只读属性unsigned short y;<br />只读属性unsigned short width;<br />只读属性unsigned short height;<br /> <br /> void setSize(unsigned short x， short y);<br /> }<br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### PlaybackInformation {#playbackinformation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfacePlaybackInformation<br /> {<br />只读属性多次timeToFirstByte;<br />只读属性多次timeToLoad;<br />只读属性多次timeToStart;<br />只读属性多次timeToFail;<br />只读属性intTotal已播放；<br />只读属性int totalSecondsSpent;<br />只读属性多次frameRate;<br />只读属性int droppedFrameCount;<br />只读属性intencedBandwidth;<br />只读属性intbitrate;<br />只读属性多次bittime;<br />只读属性int bufferLength;<br />只读属性int emptyBufferCount;<br />只读属性多次bufferingTime;<br /> };</p> </td> 
   <td><p>interfacePlaybackInformation<br /> {<br />只读属性多次timeToFirstByte;<br />只读属性多次timeToLoad;<br />只读属性多次timeToStart;<br />只读属性多次timeToFail;<br />只读属性intTotal已播放；<br />只读属性int totalSecondsSpent;<br />只读属性多次frameRate;<br />只读属性int droppedFrameCount;<br /> <br />只读属性intbitrate;<br />只读属性多次缓冲区Time;<br />仅属性int bufferLength;<br /> readonly属性int emptyBufferCount;<br /> readonly属性多次bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 有用资源{#helpful-resources}

* 请参阅[Adobe Primetime学习和支持](https://helpx.adobe.com/support/primetime.html)页面上的完整帮助文档。
