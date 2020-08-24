---
title: TVSDK转换——对于JavaScript,1.3到2.0
seo-title: TVSDK转换——对于JavaScript,1.3到2.0
description: 2.0的许多方法签名和API元素名称已更改。请查看这些表以查看所有API更改详细信息。
seo-description: 2.0的许多方法签名和API元素名称已更改。请查看这些表以查看所有API更改详细信息。
uuid: d2d1742d-c90c-43f5-94fc-8c4a57cb8ed4
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
discoiquuid: c732f54d-116c-43f3-bec4-5e71af208426
translation-type: tm+mt
source-git-commit: cfd6da49e85e13e29e8458ee98231a8b476867db
workflow-type: tm+mt
source-wordcount: '5058'
ht-degree: 0%

---


# TVSDK转换——对于JavaScript,1.3到2.0 {#tvsdk-conversion-to-for-javascript}

2.0的许多方法签名和API元素名称已更改。请查看这些表以查看所有API更改详细信息。

## 在JavaScript中实现回调函数 {#implement-callback-functions-in-javascript}

方法文档中的注释建议您需要实现的回调的签名。

对于JavaScript,API语法基于Web ID。 对于TVSDK接口，方法名称称为 *methodName*()。 对于应用程序要实现的方法，将向接口添加一个名为 ** methodNameCallbackFunc的读／写属性，并且应用程序应将其设置为指向实现该方法的函数。 例如：

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

## 2.0的广告工作流程API元素更改 {#advertising-workflow-api-element-changes-for}

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
* 时间轴／时间轴项／时间轴标记
* AdBreak
* 广告/ AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset
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
   <td><p> <strong>TimedMetadata</strong>:接口TimedMetadata<br /> {const unsigned short METADATA_TYPE_TAG = 0; <br /> const unsigned short metadata_TYPE_ID3 = 1 ; <br /> 只读属性未签名短类型； <br /> 只读属性长时间；<br /> 只读属性DomString id;<br /> 只读属性DomString名称；<br /> 只读属性DomString内容； <br /> 只读属性对象元数据；<br /> }; </p> </td> 
   <td><p>接口TimedMetadata<br /> {const unsigned short METADATA_TYPE_TAG = 0;<br /> const unsigned short metadata_TYPE_ID3 = 1 ;<br /> 只读属性unsigned short metadataType;<br /> 只读属性长时间；<br /> 只读属性long id;<br /> 只读属性DomString名称；<br /><br /> 只读属性对象元数据；<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>:（2.0没有更改）</td> 
   <td><p>接口TimedMetadataList {readonly<br /> 属性未签名长度；<br /> getter TimedMetadata(unsigned long index);<br /> };</p> </td> 
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
   <td><p>接口AdSignlingMode { <br /> const unsigned short MODE_DEFAULT, <br /> const unsigned short MODE_MANIFEST_CASS, <br /> const unsigned short MODE_SERVER_MAP, <br /> const unsigned short MODE_CUSTOM_RANGES <br /> };</p> </td> 
   <td>这将替换MetadataKeys::MANIFEST_CAIS密钥。</td> 
  </tr> 
 </tbody> 
</table>

### 广告元数据 {#advertisingmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口AdvertisingMetadata { <br /> 属性AdSigningMode模式； <br /> 属性AdBreakWatchedPolicy adBreakAsWatched; <br /> 属性boolean livePreroll; <br /> 属性boolean delayAdLoading ; <br /> };</p> </td> 
   <td>此功能由<p>元数据密钥：:ADVERTISING_METADATA</p> key.</td> 
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
   <td><p>接口CustomRangeMetadata <br /> {包含未签名的短TYPE_MARK_RANGE; <br /> const unsigned short TYPE_DELETE_RANGE; <br /> const unsigned short TYPE_REPLACE_RANGE; <br /> 属性无符号短类型； <br /> 属性boolean adjustSeekPosition; <br /> 属性TimeRangeList timeRangeList; <br /> };</p> </td> 
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
   <td><p>interface ReplaceTimeRange {属 <br /> 性未签名长开始； <br /> 只读属性unsigned long end; <br /> 属性无符号长持续时间； <br /> 属性unsigned long replaceDuration; <br /> };</p> </td> 
   <td>（2.0新增）</td> 
  </tr> 
 </tbody> 
</table>

### 放置 {#placement}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口放置{ <br /> const unsigned short TYPE_MID_ROLL; <br /> const unsigned short TYPE_PRE_ROLL; <br /> const unsigned short TYPE_POST_ROLL; <br /> const unsigned short TYPE_SERVER_MAP; <br /> const unsigned short TYPE_CUSTOM_RANGE;<br /> 只读属性未签名短类型； <br /> 只读属性长时间； <br /> 只读属性长持续时间； <br /> const unsigned short MODE_DEFAULT; <br /> const unsigned short MODE_INSERT; <br /> const unsigned short MODE_REPLACE; <br /> const unsigned short MODE_DELETE; <br /> const unsigned short MODE_MARK; <br /> const unsigned short MODE_FREE_REPLACE; <br /> 只读属性无符号短模式； <br /> 只读属性TimeRange范围； <br /> };</p> </td> 
   <td>（2.0新增）</td> 
  </tr> 
 </tbody> 
</table>

### 机会 {#opportunity}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface Opportunity { <br /> readonly属性DomString id; <br /> 只读属性放置； <br /> 只读属性对象设置； <br /> readonly属性Object customParameters; <br /> }; </p> </td> 
   <td>（2.0新增）</td> 
  </tr> 
 </tbody> 
</table>

### 保留 {#reservation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口保留{ <br /> readonly属性TimeRange范围； <br /> 只读属性长保留； <br /> }; </p> </td> 
   <td> （2.0新增）</td> 
  </tr> 
 </tbody> 
</table>

### 时间轴／时间轴项／时间轴标记 {#timeline-timelineitem-timelinemarker}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p><strong>时间轴</strong>:接口时 <br /> 间线{ readeronly属性TimelineMarkerList timelineMarkers; <br /> 只读属性TimelineItemList timelineItems; <br /> 多次convertToLocalTime(多次时间); <br /> 多次convertToVirtualTime(多次时间); <br /> };</p> </td> 
   <td><p>接口时间线<br /> {readonly属性TimelineMarkerList timelineMarkers;<br /><br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>时间轴项</strong>:接口时间轴项：<br /> TimelineMarker {<br /> readonly属性long id; <br /> 只读属性TimeRange virtualRange; <br /> 只读属性TimeRange localRange; <br /> 只读属性boolean watched; <br /> 只读属性布尔临时值； <br /> }; </p> </td> 
   <td>（2.0新增）</td> 
  </tr> 
  <tr> 
   <td><strong>时间轴标记</strong>:（2.0没有更改）</td> 
   <td><p>接口TimelineMarker {<br /> readonly属性多次时间；<br /> 只读属性多次持续时间；<br /> };</p> </td> 
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
   <td><p>接口AdBreak {<br /> Readonly <br /> 属 <br /> 性 <br /> 多次持续时间；<br /> 只读属性AdList广告；<br /><br /> <br /> 只读属性AdInsertionType insertionType;<br /> }; </p> </td> 
   <td><p>接口AdBreak {<br /> readonly属性多次时间；<br /> 只读属性多次replaceDuration;<br /><br /> 只读属性多次持续时间；<br /> 只读属性AdList adList;<br /><br /> 只读属性DomString数据；<br /><br /> }; </p> </td> 
  </tr> 
 </tbody> 
</table>

### 广告/ AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset {#ad-adasset-adclick-adlist-adassetlist-adbannerasset}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>广告</strong>:接口Ad {<br /> readonly属性AdAsset primaryAsset;<br /> 只读属性AdAssetList companionAssets;<br /><br /> 只读属性多次持续时间；<br /> 只读属性DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINER = 1 ;<br /><br /> 只读属性unsigned short adType;<br /> 只读属性AdInsertionType adInsertionType; <br /> <br /> 只读属性布尔可单击； <br /> 只读属性boolean isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>接口Ad {<br /> readonly属性AdAsset primaryAsset;<br /> 只读属性AdAssetList companionAssets;<br /><br /> 只读属性多次持续时间；<br /> 只读属性DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINER = 1 ;<br /><br /> 只读属性未签名短类型；<br /> 只读属性AdInsertionType insertionType; <br /> 只读属性对象跟踪器；<br /><br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>:（2.0没有更改）</td> 
   <td><p>接口AdAsset {<br /> readonly属性DomString id;<br /> 只读属性多次持续时间；<br /> 只读属性MediaResource资源；<br /> 只读属性AdClick adClick;<br /> 只读属性对象元数据；<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>:（2.0没有更改）</td> 
   <td><p>接口AdClick {<br /> readonly属性DomString id;<br /> 只读属性DomString标题；<br /> 只读属性DomString url;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>:（2.0没有更改）</td> 
   <td><p>接口AdList {<br /> readonly属性未签名长；<br /> getter Ad（无符号长索引）;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>:（2.0没有更改）</td> 
   <td><p>接口AdAssetList {readonly<br /> 属性未签名长度；<br /> getter AdAsset（未签名长索引）;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>:接口AdBannerAsset:AdAsset<br /> {<br /> readonly attribute int width;<br /> readonly属性int height;<br /> 只读属性DomString staticUrl;<br /> 只读属性DomString height;<br /> 只读属性DomString width;<br /> };</p> </td> 
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
   <td><p> <strong>AdBreakTimelineItem</strong>:接口AdBreakTimelineItem:TimelineItem { <br /> readonly属性AdBreak adBreak; <br /> 只读属性AdTimelineItemList项； <br /> }; </p> </td> 
   <td> （2.0新增）</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>:接口AdTimelineItem:TimelineItem { <br /> readonly属性AdBreak adBreak; <br /> 只读属性广告； <br /> }; </p> </td> 
   <td> （2.0新增）</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>:interface AdBreakTimelineItemList { <br /> readonly属性未签名长； <br /> getterAdBreakTimelineItem（未签名日志索引）; <br /> };</p> </td> 
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
   <td><p>接口AdBreakPolicy<br /> {readonly属性短AD_BREAK_POLICY_SKIP;<br /> 只读属性short AD_BREAK_POLICY_PLAY;<br /> 只读属性short AD_BREAK_POLICY_REMOVE;<br /> 只读属性short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> 接口AdPolicyConstants<br /> {readonly属性短AD_BREAK_POLICY_SKIP;<br /> 只读属性short AD_BREAK_POLICY_PLAY;<br /> 只读属性short AD_BREAK_POLICY_REMOVE;<br /> 只读属性short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> 接口AdBreakWatchedPolicy<br /> {readonly属性short AD_BREAK_AS_WATCH_ON_BEGIN;<br /> 只读属性short AD_BREAK_AS_WATCH_ON_END;<br /> 只读属性short AD_BREAK_AS_WATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> .只读属性short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> 只读属性short AD_BREAK_AS_WATCH_ON_END;<br /> 只读属性short AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>接口AdPolicy<br /> {readonly属性short AD_POLICY_PLAY;<br /> 只读属性short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> 只读属性short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;只读属性short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /><br /> 只读属性short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> .... <br /> 只读属性short AD_POLICY_PLAY;<br /> 只读属性short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> 只读属性short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> 只读属性short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> 只读属性short AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>接口AdPolicyMode<br /> {readonly属性short AD_POLICY_MODE_PLAY;<br /> 只读属性short AD_POLICY_MODE_SEEK;<br /> 只读属性short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {readonly属性short AD_POLICY_MODE_PLAY;<br /> 只读属性short AD_POLICY_MODE_SEEK;<br /> 只读属性short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>接口AdPolicyInfo {readonly<br /> 属性AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> 只读属性AdTimelineItem adTimelineItem;<br /> 只读属性多次currentTime;<br /> 只读属性多次seekToTime;<br /> 只读属性多次率；<br /> 只读属性短模式；//AdPolicyMode<br /> };</p> </td> 
   <td><p>接口AdPolicyInfo {readonly<br /> 属性AdBreakPlacementList <br /> adBreakAptienations;<br /> 只读属性广告；<br /> 只读属性多次currentTime;<br /> 只读属性多次seekToTime;<br /> 只读属性多次率；<br /> 只读属性短模式；//AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>接口AdPolicySelector<br /> { /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute object selectPolicyForAdBreakCallbackFunc;<br /> /**<br /> * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */属<br /> 性对象selectAdBreaksToPlayCallbackFunc;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute object selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute object selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>接口AdPolicySelector<br /> { /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute object selectPolicyForAdBreakFuncCallback;<br /> /**<br /> * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */属<br /> 性对象selectAdBreaksToPlayCallback;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute object selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br /> attribute object selectWatchedPolicyForAdBreakCallback;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 时间轴操作 {#timelineoperation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口TimelineOperation { <br /> readonly属性放置； <br /> };</p> </td> 
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
   <td><p>接口AdBreakPlacement:TimelineOperation {<br /> readonly属性AdBreak adBreak;<br /> 只读属性放置；//从TimelineOperation只读<br /> 属性多次时间；<br /> 只读属性多次持续时间；<br /> };</p> </td> 
   <td><p>接口AdBreakPlacement {readonly<br /> 属性AdBreak adBreak;<br /> 只读属性放置；<br /> 只读属性多次时间；<br /> 只读属性多次持续时间；<br /> };</p> </td> 
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
   <td><p>接口AuditudeSettings:AdvertisingMetadata { <br /> 属性DomString zoneId; <br /> 属性DomString mediaId; <br /> 属性DomString defaultMediaId ; <br /> 属性DomString域； <br /> 属性对象targettingInfo ; <br /> 属性对象customParameters; <br /> 属性Boolean creativePackaingEnabled ;<br /> 属性boolean showStaticBanners ;<br /> };</p> </td> 
   <td>功能由MetadataKeys::AUDITUDE_METADATA_KEY提供。</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的自定义API元素更改 {#customization-api-element-changes-for}

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
   <td><p>接口MediaPlayerItemConfig {attribute<br /> ContentFactory adFactory;<br /> 属性StringList subscribeTags;<br /><br /> 属性StringList adTags;<br /><br /> <br /> 属性AdSigningMode adSigningMode;<br /> 属性CustomRangeMetadata customRangeMetadata;<br /> 属性NetworkConfiguration networkConfiguration;<br /> 属性AdvertisingMetadata advertisingMetadata;<br /> 属性Boolean useHardwareDecoder;<br /> };</p> </td> 
   <td><p>接口MediaPlayerConfig {属性<br /><br /> StringList <br /><br /> adTags;<br /> 属性StringList subscriptedTags;<br /> 属性MediaPlayerClientFactory clientFactory;<br /><br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>接口ContentFactory<br /> { /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem项);<br /> */<br /> attribute object retrieveAdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>接口MediaPlayerClientFactory<br /> { /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem项);<br /> */<br /> attribute object retrieveAdPolicySelectorFunc;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 网络配置 {#networkconfiguration}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface NetworkConfiguration<br /> {<br /> attribute boolean forceNativeNetworking;<br /> 属性boolean useRedirectedUrl;<br /> 属性对象cookieHeader;<br /> 属性boolean readSetCookieHeader;<br /> attribute int masterUpdateInterval; <br /> 属性boolean useCookieHeaderForAllRequests;<br /> 属性int readLimit;<br /> };</p> </td> 
   <td>在1.3中，其中一些功能是由MetadataKeys提供的</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的DRM API元素更改 {#drm-api-element-changes-for}

这些表比较了版本1.3和2.0之间JavaScript TVSDK的DRM API元素。

本主题中的表：

* DRM工作流初始化
* DRMAcquireLicenseSettings / DRMAuthenticationMethod
* DRMMetadata
* DRMPlaybackTimeWindow
* DRMLicense
* DRMLicenseDomain
* DRMPolicy
* DRMManager

### DRM工作流初始化 {#drm-workflow-initialization}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>应用程序需要调用AdobePSDK.initiateDRMWorkflow以启动DRM工作流。 没有此呼叫，DRM视频将无法播放。<p>接口AdobePSDK<br /> {<br /> void initiateDRMWorkFlow(<br /> DomString appStoratePath, <br /> DomString publisherId, <br /> DomString appId, <br /> DomString appVersion, <br /> boolean privacyModeOn);<br /> };</p> </td> 
   <td>初始化是在内部完成的，无需显式调用。</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| 2.0 API | 1.3 API |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| 2.0没有更改。 | 枚举DRMAcquireLicenseSettings <br>{<br> const unsigned int FORCE_REFRESH = 0;<br> const unsigned int LOCAL_ONLY = 1;<br> const unsigned int ALLOW_SERVER = 2;<br> }; |
| **DRMAuthenticationMethod** |  |
| 2.0没有更改。 | 枚举DRMAuthenticationMethod <br>{<br> const unsigned int UNKNOWN = 0;<br> const unsigned int ANONYMOUS = 1;<br> const unsigned int USERNAME_AND_PASSWORD = 2;<br> } |

### DRMMetadata {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0没有更改。</td> 
   <td><p>接口DRMMetadata<br /> {<br /> readonly属性DomString serverUrl;<br /> 只读属性DomString licenseId;<br /> readonly属性DRMPolicyArray策略； <br /> };</p> </td> 
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
   <td><p>interface DRMPlaybackTimeWindow {readonly<br /> attribute int playbackPeriodInSeconds;<br /> readonly属性long playbackStartDate;<br /> readonly属性long playbackEndDate;<br /> };</p> </td> 
   <td><p>interface DRMPlaybackTimeWindow {readonly<br /> attribute int periodInSeconds;<br /> readonly属性int startDate;<br /> int endDate的只读属性；<br /> };</p> </td> 
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
   <td><p>接口DRMLicense {readonly<br /> 属性Uint8Array字节；<br /> 只读属性Date licenseStartDate;<br /> 只读属性Date licenseEndDate;<br /> 只读属性Date offlineStorageStartDate;<br /> 只读属性Date offlineStorageEndDate; <br /> 只读属性DomString serverUrl;<br /> 只读属性DomString licenseID;<br /> 只读属性DomString policyID;<br /> readonly属性DRMPlaybackTimeWindow playbackTimeWindow;<br /> 只读属性Object customProperties;<br /> }; </p> </td> 
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
   <td><p>接口DRMLicenseDomain {readonly<br /> 属性DomString authenticationDomain;<br /> readonly属性DRMAuthenticationMethod authenticationMethod; <br /> 只读属性DomString serverUrl;<br /> };</p> </td> 
   <td><p>接口DRMLicenseDomain {readonly<br /> 属性DomString authDomain;<br /> 只读属性DRMAuthenticationMethod authMethod; <br /> 只读属性DomString serverURL;<br /> };</p> </td> 
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
   <td><p>接口DRMPolicy<br /> {readonly<br /> 属性DomString authenticationDomain;<br /> readonly属性DRMAuthenticationMethod authenticationMethod;<br /><br /> 只读属性DomString displayName;<br /> 只读属性DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
   <td><p>接口DRMPolicy<br /> {readonly<br /> 属性DomString authDomain;<br /> 只读属性DRMAuthenticationMethod authMethod;<br /> 只读属性DomString dispName;<br /> 只读属性DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
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
   <td><p>接口DRMManager:EventTarget {<br /> void acquireLicense(DRMMetadata元数据， <br /> DRMAcquireLicenseSettings设置， <br /> DRMAquireLicenseListener);<br /> void acquirePreviewLicense(DRMMetadata元数据， <br /> DRMAquireLicenseListener);<br /> void authenticate(DRMMetadata元数据 <br /> , DomString url<br /> , DomString &amp;authenticationDomain, <br /> DomString用户， <br /> DomString口令， <br /> DRMAuthenticateListener);<br /><br /> DRMMetadata createMetadataFromBytes<br /> (Uint8Array, DRMErrorListener);<br /> void initialize(DRMOperationCompleteListener);<br /> 属性long maxOperationTime;<br /><br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> DRMOperationCompleteListener);<br /> void leaveLicenseDomain<br /> (DRMLicenseDomain licenseDomain, <br /> DRMOperationCompleteListener);<br /><br /> void resetDRM(DRMOperationCompleteListener);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID, <br /> DomString policyID, boolean <br /> commitImtedialed,<br /> DRMReturnLicenseListener);<br /> void setAuthenticationToken(<br /> DRMMetadata元数据 <br /> , DomString authenticationDomain, <br /> Uint8Array令牌， <br /> DRMOperationCompleteListener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> DRMOperationCompleteListener);<br /> };</p> </td> 
   <td><p>接口DRMManager:EventTarget {<br /> void acquireLicense(DRMMetadata元数据， <br /> DRMAcquireLicenseSettings设置， <br /> EventContext eventContext);<br /> void acquirePreviewLicense(DRMMetadata元数据， <br /> EventContext eventContext);<br /> void authenticate(DRMMetadata元数据 <br /> 、DomString url<br /> 、DomString &amp;authenticationDomain、 <br /> DomString用户、 <br /> DomString口令、 <br /> EventContext eventContext);<br /><br /> DRMMetadata createMetadataFromBytes<br /> (Uint8Array, EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> 属性long maxOperationTime;<br /><br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> EventContext eventContext);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> EventContext eventContext);<br /><br /> void resetDRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID,<br /> DomString policyID, <br /> boolean commitImted,<br /> EventContext eventContext);<br /> void setAuthenticationToken(<br /> DRMMetadata元数据 <br /> , DomString authenticationDomain, <br /> Uint8Array令牌， <br /> EventContext eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext eventContext);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMErrorListener : <br /> public psdkutils::PSDKInterfaceWithUserData {public<br /> :<br /> virtual void onDRMError(uint32_t major, <br /> uint32_t minor, <br /> const psdkutils:PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl)= 0;<br /><br /> 受保护：<br /> virtual ~DRMErrorListener(){}<br /> }</p> </td> 
   <td>事件/接口／说明 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>在DRMManger的一种异步方法期间发生错误时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMOperationCompleteListener : <br /> public DRMErrorListener {<br /> public:<br /> virtual void onDRMOperationComplete()= 0;<br /><br /> 受保护：<br /> virtual ~DRMOperationCompleteListener(){}<br /> };</p> </td> 
   <td>事件/接口／说明 
    <ul> 
     <li>kEventDRMInitializationComplete<p>/ PSDKEvent</p> <p>DRM初始化完成时。</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>joinLicenseDomain()操作成功完成时。</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>leaveLicenseDomain()操作成功完成时。</p> </li> 
     <li>kEventDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>当resetDRM()操作成功完成时。</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEvent</p> <p>setAuthenticationTokenSet()操作成功完成时。</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEvent</p> <p>当storeLicenseBytes()操作成功完成时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMAuthenticateListener: <br /> public DRMErrorListener {<br /> public:<br /> virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* authenticationToken) <br /> = 0;<br /><br /> 受保护：<br /> virtual ~DRMAuthenticateListener(){}<br /> }</p> </td> 
   <td>事件/接口／说明 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/DRMAuthenticationCompleteEvent</p> <p>当DRMManager::authenticate方法调用成功时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMAquireLicenseListener: <br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseAppired(const DRMLicense*)= 0;<br /><br /> 受保护：<br /> virtual ~DRMAquireLicenseListener(){}<br /> };</p> </td> 
   <td>事件/接口／说明 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquired<p>/DRMLicenseAppiredEvent</p> <p>当DRMManager::acquirePreviewLicense方法调用成功时。</p> </li> 
     <li>kEventDRMLicenseAppired<p>/DRMLicenseAppiredEvent</p> <p>当DRMManager::acquireLicense方法调用成功时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMReturnLicenseListener: <br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseReturnComplete(uint32_t numReturned)= 0;<br /><br /> 受保护：<br /> virtual ~DRMReturnLicenseListener(){}<br /> };</p> </td> 
   <td>事件/接口／说明 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/DRMLicenseReturnCompleteEvent</p> <p>当DRMManager::returnLicense方法调用成功时。</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 2.0的通用播放API元素更改 {#generic-playback-api-element-changes-for}

这些表比较了JavaScript TVSDK 1.3和2.0之间的通用播放API元素。

本主题中的表：

* 媒体资源
* MediaPlayer
* ABRControlParameters
* BufferControlParameters
* TextFormat
* MediaPlayerItemLoader

### 媒体资源 {#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口MediaResource {<br /> attribute DomString url; <br /> 属性无符号短类型；<br /> 属性对象元数据；<br /> const unsigned short TYPE_HLS;<br /> const unsigned short TYPE_HDS;<br /> const unsigned short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> const unsigned short TYPE_UNKNOWN;<br /> };</p> </td> 
   <td><p>接口MediaResource {<br /> attribute DomString url;<br /> 属性DomString类型；<br /> 属性对象元数据；<br /><br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>接口MediaPlayer:EventTarget<br /> {<br /> void prepareToPlay(多次位置);<br /> void play();<br /> void pause();<br /> void seek(多次位置);<br /> void seekToLocal(多次位置);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem（MediaPlayerItem项）;<br /> void replaceCurrentResource(MediaResource rsource, <br /> MediaPlayerItemConfig); <br /> void suspend();<br /> void restore();<br /> void notifyClick();<br /><br /> 只读属性TimeRange playbackRange;<br /> 只读属性TimeRange seekableRange;<br /> 只读属性多次currentTime;<br /> 只读属性多次localTime;<br /> 只读属性TimeRange bufferedRange;<br /> 只读属性DRMManager drmManager;<br /> 只读属性MediaPlayerItem currentItem;<br /><br /> // PlayerStatus控制<br /><br /><br /> 未签名短PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /><br /> 只读属性未签名短状态；<br /><br /> 无符号短卷属性；<br /> 属性ABRControlParameters abrControlParameters;<br /> 属性BufferControlParameters bufferControlParameters;<br /><br /> const unsigned short VISIBLE;//对于CC可见性<br /> ，无符号短不可见；//对于CC可见性属性<br /> unsigned short cc可见性；<br /> 属性TextFormat ccStyle;<br /> 只读属性PlaybackMetrics playbackMetrics;<br /><br /> 属性多次率；<br /> 属性MediaPlayerView视图;<br /> 只读属性时间线时间线；<br /> 属性多次currentTimeUpdateInterval; <br /> //设置2.0 }不支持<br /> ;</p> </td> 
   <td><p>接口MediaPlayer:EventTarget<br /> {<br /> void prepareToPlay（int位置）;<br /> void play();<br /> void pause();<br /> void seek(int position);<br /> void seekToLocalTime(int position);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem（MediaResource源）;<br /><br /> <br /> <br /> <br /> <br /> <br /> 只读属性TimeRange playbackRange;<br /> 只读属性TimeRange seekableRange;<br /> 只读属性多次currentTime;<br /> 只读属性多次localTime;<br /> 只读属性TimeRange bufferedRange;<br /> 只读属性DRMManager drmManager;<br /> 只读属性MediaPlayerItem currentItem;<br /><br /> // PlayerState<br /> const unsigned short PLAYER_STATE_IDLE;<br /> const unsigned short PLAYER_STATE_INITIALIZING;<br /> const unsigned short PLAYER_STATE_INITIALIZED;<br /> const unsigned short PLAYER_STATE_PREPARING;<br /> const unsigned short PLAYER_STATE_PREPARED;<br /> const unsigned short PLAYER_STATE_PLAYING;<br /> const unsigned short PLAYER_STATE_PAUSED;<br /> const unsigned short PLAYER_STATE_SEEKING;<br /> const unsigned short PLAYER_STATE_COMPLETE;<br /> const unsigned short PLAYER_STATE_ERROR;<br /> const unsigned short PLAYER_STATE_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> 只读属性无符号短状态；<br /><br /> 无符号短卷属性；<br /> 属性ABRControlParameters abrControlParameters;<br /> 属性BufferControlParameters bufferControlParameters;<br /><br /> 只读未签名的短VISIBLE;//对于CC可见性<br /> ，只读未签名短INVISIBLE;//对于CC可见性属性<br /> unsigned short cc可见性；<br /> 属性TextFormat ccStyle;<br /> 只读属性PlaybackMetrics playbackMetrics;<br /> 属性MediaPlayerConfig mediaPlayerConfig;<br /> 属性多次率；<br /> 属性MediaPlayerView视图;<br /> 只读属性时间线时间线；<br /><br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>接口MediaPlayerStatus<br /> {<br /> // PlayerStatus包含未签名的<br /> SHORT PLAYER_STATUS_IDLE;<br /> const unsigned short PLAYER_STATUS_INITIALIZING;<br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> };</p> </td> 
   <td>（2.0新增）</td> 
  </tr> 
 </tbody> 
</table>

#### 事件受MediaPlayer支持 {#events-supported-by-mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>2.0事件名</th> 
   <th>2.0接口</th> 
   <th> </th> 
   <th>1.3事件名</th> 
   <th>1.3接口</th> 
  </tr> 
  <tr> 
   <td><p>（2.0已删除）</p> </td> 
   <td> </td> 
   <td> </td> 
   <td>制备</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td><p>itemUpdated</p> <p>媒体播放器项目更新时。</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>已更新</p> <p>媒体播放器成功更新媒体时。</p> </td> 
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
   <td>状态事件</td> 
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
   <td>进度</td> 
   <td>ProgressEvent</td> 
  </tr> 
  <tr> 
   <td>bufferingBegin</td> 
   <td>事件</td> 
   <td> </td> 
   <td>缓冲</td> 
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
   <td>通知事件</td> 
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
   <td>保留事件</td> 
   <td> </td> 
   <td>timelineHolderReached</td> 
   <td>TimelineHolderEvent</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>比特率已更改</td> 
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
   <td>adBreakBricked</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakBricked</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>广告点击<br /> “用户单击广告时”。</td> 
   <td>AdClickedEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>profileChanged<br /> 当播放用户档案更改时。</td> 
   <td>ProfileEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>seekPositionAdjusted<br /> 当搜索位置因内部或外部规则而调整时。</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>audioUpdated<br /> 当媒体播放器项目更新时。 对于包含仅在播放时可检测的音轨的特定流，当有新的音轨可用时，将触发此事件。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>字幕更 <br /> 新媒体播放器项目更新时。 对于实时／线性流，客户端必须定期刷新媒体资源以检测新的可用内容。 发生这种情况时，某些媒体特性可能会发生变化。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>主更 <br /> 新媒体播放器项更新时。 对于实时／线性流，客户端必须定期刷新媒体资源以检测新的可用内容。 发生这种情况时，某些媒体特性可能会发生变化。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRange更新<br /> ：媒体播放器项目更新时。 对于实时／线性流，客户端必须定期刷新媒体资源以检测新的可用内容。 发生这种情况时，某些媒体特性可能会发生变化。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>TimedEvent<br /> 生成定时事件时发送。</td> 
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
   <td><p>接口ABRControlParameters<br /> {const<br /> unsigned short ABR_POLICY_CONSERVAL = 0;<br /> const unsigned short ABR_POLICY_MEADE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESSIVE = 2 ;<br /><br /> attribute unsigned short abrPolicy;<br /> attribute unsigned int initialBitRate;<br /> 属性unsigned int minBitRate;<br /> 属性unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE;<br /> const unsigned short DEFAULT_ABR_MIN_BITRATE;<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>接口ABRControlParameters<br /> {const<br /> unsigned short ABR_POLICY_CONSERVAL = 0;<br /> const unsigned short ABR_POLICY_MEADE = 1 ;<br /> const unsigned short ABR_POLICY_AGGRESSIVE = 2 ;<br /><br /> attribute unsigned short abrPolicy;<br /> attribute unsigned int initialBitRate;<br /> 属性unsigned int minBitRate;<br /> 属性unsigned int maxBitRate;<br /><br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>接口BufferControlParameters<br /> {属<br /> 性多次initialBufferTime;<br /> 属性多次playBufferTime;<br /> 多次DEFAULT_INITIAL_BUFFER_TIME;<br /> 多次DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>接口BufferControlParameters<br /> {属<br /> 性多次initialBufferTime;<br /> 属性多次playBufferTime;<br /><br /> <br /> };</p> </td> 
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
   <td><p>接口TextFormat<br /> {<br /> // Color Const<br /> unsigned short COLOR_DEFAULT = 0 ;<br /> const unsigned short COLOR_BLACK = 1 ;<br /> const unsigned short COLOR_GRAY = 2 ;<br /> const unsigned short COLOR_WHITE = 3 ;<br /> const unsigned short COLOR_BRIGHT_WHITE = 4 ;<br /> const unsigned short COLOR_DARK_RED = 5 ;<br /> const unsigned short COLOR_RED = 6;<br /> const unsigned short COLOR_BRIGHT_RED = 7;<br /> const unsigned short COLOR_DARK_GREEN = 8 ;<br /> const unsigned short COLOR_GREEN = 9 ;<br /> const unsigned short COLOR_BRIGHT_GREEN = 10 ;<br /> const unsigned short COLOR_DARK_BLUE = 11 ;<br /> const unsigned short COLOR_BLUE = 12 ;<br /> const unsigned short COLOR_BRIGHT_BLUE = 13 ;<br /> const unsigned short COLOR_DARK_YELLOW = 14 ;<br /> const unsigned short COLOR_YELLOW = 15 ;<br /> const unsigned short COLOR_BRIGHT_YELLOW = 16 ;<br /> const unsigned short COLOR_DARK_MAGENTA = 17 ;<br /> const unsigned short COLOR_MAGENTA = 18 ;<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 19;<br /> const unsigned short COLOR_DARK_CYAN = 20;<br /> const unsigned short COLOR_CYAN = 21 ;<br /> const unsigned short COLOR_BRIGHT_CYAN = 22;<br /><br /> 只读属性unsigned short fontColor;<br /> 只读属性unsigned short backgroundColor;<br /> 只读属性unsigned short fillColor;<br /> 只读属性unsigned short edgeColor;<br /><br /> // Size const<br /> unsigned short SIZE_DEFAULT = 0;<br /> const unsigned short SIZE_SMALL = 1 ;<br /> const unsigned short SIZE_MEDIUM = 2 ;<br /> const unsigned short SIZE_LARGE = 3 ;<br /><br /> 只读属性无符号短大小；<br /><br /> // FontEdge<br /> const unsigned short FONT_EDGE_DEFAULT = 0;<br /> const unsigned short FONT_EDGE_NONE = 1 ;<br /> const unsigned short FONT_EDGE_ROURDED = 2 ;<br /> const unsigned short FONT_EDGE_DISCEPTED = 3 ;<br /> const unsigned short FONT_EDGE_UNIFORM = 4 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_RIGHT = 6 ;<br /> 只读属性unsigned short fontEdge;<br /><br /> // Font const<br /> unsigned short FONT_DEFAULT = 0;<br /> const unsigned short FONT_MONOSPACED_WITH_SERIFS = 1 ;<br /> const unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2 ;<br /> const unsigned short FONT_MONSPACED_WITHOUT_SERIFS = 3 ;<br /> const unsigned short FONT_CAUSAL = 4 ;<br /> const unsigned short FONT_CURSIVE = 5 ;<br /> const unsigned short FONT_SMALL_CAPITALS = 6 ;<br /> 只读属性无符号短字体；<br /> 只读属性unsigned short fontOpacity;<br /> readonly属性unsigned short backgroundOpacity;<br /> 只读属性unsigned short fillOpacity;<br /> 只读属性unsigned short DEFAULT_OPACITY;<br /> };</p> </td> 
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
   <td><p>接口MediaPlayerItemLoader:<br /> {<br /> void load(MediaResource资源，长资源Id<br /> , ItemLoaderListener, <br /> MediaPlayerItemConfig);<br /> void cancel();<br /> 只读属性MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
  <tr> 
   <td><p>interfaceItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)var onLoadCompleteCallbackFunc<br /> ;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc;<br /> }</p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的媒体特性API元素更改 {#media-characteristics-api-element-changes-for}

这些表比较了C++ TVSDK的媒体特性API元素（版本1.3和2.0）。

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
   <td><p>接口MediaPlayerItem {readonly<br /> 属性MediaResource资源；<br /> readonly属性long resourceId;<br /> 只读属性布尔live;<br /><br /> readonly属性boolean hasAlternateAudio;<br /> 只读属性AudioTrackList audioTracks;<br /> readonly属性AudioTrack selectedAudioTrack;<br /> void selectAudioTrack(AudioTrack); <br /> <br /> readonly属性boolean hasClosedCaptions;<br /> readonly属性ClosedCaptionsTrackList closedCaptionsTracks;<br /> readonly属性ClosedCaptionsTrack selectedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(<br /> ClosedCaptionsTrack); <br /> <br /> readonly属性boolean hasTimedMetadata;<br /> 只读属性TimedMetadataList timedMetadata;<br /> 只读属性布尔动态；<br /><br /> readonly属性boolean isProtected;<br /> 只读属性DRMMetadataInfoList drmMetadataInfos;<br /> 只读属性ProfileList用户档案;<br /> 只读属性用户档案selectedProfile;<br /><br /> 只读属性boolean trickPlaySupported;<br /> 只读属性floatArray availablePlaybackRates;<br /> readonly属性float selectedPlaybackRate;<br /><br /> <br /> 只读属性MediaPlayer mediaPlayer;<br /> 只读属性MediaPlayerItemConfig;<br /> };</p> </td> 
   <td><p>接口MediaPlayerItem {readonly<br /> 属性MediaResource资源；<br /> readonly属性long resourceId;<br /> 只读属性布尔live;<br /><br /> readonly属性boolean hasAlternateAudio;<br /> 只读属性AudioTrackList audioTracks;<br /> 属性AudioTrack selectedAudioTrack;<br /><br /> <br /> readonly属性boolean hasClosedCaptions;<br /> 只读属性ClosedCaptionsTrackList ccTracks;<br /> 属性ClosedCaptionsTrack selectedCCTrack;<br /><br /> <br /> <br /> readonly属性boolean hasTimedMetadata;<br /> 只读属性TimedMetadataList timedMetadata;<br /> 只读属性布尔动态；<br /><br /> readonly属性boolean isProtected;<br /> 只读属性DRMMetadataInfoList drmMetadataInfos;<br /> 只读属性ProfileList用户档案;<br /><br /> <br /> 只读属性boolean trickPlaySupported;<br /> 只读属性Int32Array availablePlaybackRates;<br /><br /> 只读属性StringList adTags;<br /><br /> 只读属性MediaPlayer mediaPlayer;<br /><br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 音轨／音轨／隐藏字幕轨 {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口Track<br /> {<br /> readonly属性DomString名称；<br /> 只读属性DomString语言；<br /> 只读属性布尔型默认值；<br /> 只读属性boolean autoSelect;<br /> }; </p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
  <tr> 
   <td><p>接口AudioTrack:跟踪<br /> {<br /> readonly属性DomString名称；//FromTrack<br /> readonly属性DomString语言；//FromTrack<br /> readonly属性布尔默认值；// From Track<br /> readonly attribute boolean autoSelect;//FromTrack<br /> readonly属性 <br /> unsigned int pid;<br /> };</p> </td> 
   <td><p>接口AudioTrack<br /> {<br /> readonly属性DomString名称；<br /> 只读属性DomString语言； <br /> 只读属性布尔型默认值；<br /> 只读属性boolean autoSelect;<br /> 只读属性布尔型强制；<br /><br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0没有更改</td> 
   <td><p>接口AudioTrackList<br /> {readonly<br /> attribute unsigned longgh;<br /> getter AudioTrack（无符号长索引）;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>接口ClosedCaptionsTrack:跟踪<br /> {<br /> readonly属性DomString名称；//FromTrack<br /> readonly属性DomString语言；//FromTrack<br /> readonly属性布尔默认值；// FromTrack<br /> readonly属性boolean autoSelect<br /> ;// FromTrack <br /> <br /> const unsigned short SERVICE_608_CAPTIONS = 0;<br /> const unsigned short SERVICE_708_CAPTIONS = 1;<br /> const unsigned short SERVICE_WEB_VTT_CAPTIONS = 2;<br /> 只读属性unsigned short serviceType;<br /> 只读属性布尔型强制；<br /> };</p> </td> 
   <td><p>接口ClosedCaptionsTrack<br /> {<br /> readonly属性DomString名称；<br /> 只读属性DomString语言；<br /> 只读属性布尔型默认值；<br /><br /> <br /> 只读属性布尔值活动；<br /><br /> <br /> <br /> <br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0没有更改</td> 
   <td><p>接口ClosedCaptionsTrackList<br /> {readonly<br /> attribute unsigned longgh;<br /> getterClosedCaptionsTrack(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 用户档案 {#profile}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>用户档案:2.0没有更改</td> 
   <td><p>接口用户档案<br /> {<br /> readonly属性unsigned int width;<br /> 只读属性unsigned int height;<br /> 只读属性unsigned int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList:2.0没有更改</td> 
   <td><p>interface ProfileList<br /> {readonly<br /> attribute unsigned longlength;<br /> getter用户档案（无符号长索引）;<br /> };</p> </td> 
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
   <td><p>interface DRMMetadataInfo<br /> { <br /> readonly属性DRMMetadata元数据；<br /> 只读属性long prefetchTimestamp;<br /> 只读属性TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>:2.0没有更改</td> 
   <td><p>接口DRMMetadataInfoList<br /> {readonly<br /> attribute unsigned longgh;<br /> getterDRMMetadataInfo(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 将C++错误映射到不同语言的异常 {#mapping-c-errors-to-exceptions-in-different-languages}

您可以将C++错误代码映射到不同语言的异常。

C++ PSDK的API有一个“不抛出”策略。 大多数API方法都返回一个PSDKErrorCode值，以指示该方法是否成功执行。 异步错误通过错误事件通知。

ActionScript和JAVA PSDK有不同的策略。 大多数错误将引发ArgumentError或IllegalStateException，以指示无法执行方法的同步部分。 不会捕获这些例外，应用程序代码负责处理例外。 它们通常包含方法调用失败原因的有用信息。 例如，如果在无效状态中调用prepareToPlay命令，则会引发以下异常：

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

ActionScript/JAVA还会引发构造函数的异常，以指示某些内部对象创建不正确。 这些例外是内部处理的，不会传播到应用程序。 这些例外将包含在发送给应用程序的警告通知中

例如，如果未为接收的广告响应找到有效的媒体文件，则无法创建有效的广告资产对象或广告。 因此，时间轴上不放置任何广告，并调度NotificationEvent.OperationFailed通知。

从Adobe视频引擎(AVE)异步接收的错误或警告代码作为普通事件调度给应用程序。 通知事件包含所有接收到的错误代码和任何其他元数据，如URL、资源标识符、句柄等。 如果错误严重且无法继续播放当前媒体，则MediaPlayer将过渡为ERROR状态，并调度onStatusChanged回调或MediaPlayerStatusChanged.STATUS_CHANGED事件。 如果播放可以继续，将调度普通通知事件。

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
   <td>参数错误</td> 
   <td>代码= 1的异常，描述= "INVALID_ARGUMENT"和additionalInfo= &lt;as pass by方法传递的异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>参数错误</td> 
   <td>代码为2的异常，描述= "GENERIC_ERROR"和additionalInfo= &lt;as pass by方法传递的异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>代码为3的异常，描述= "ILLEGAL_STATE"和additionalInfo= &lt;as pass by方法传递的异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为4的异常，描述= "GENERIC_ERROR"和additionalInfo= &lt;as pass by方法传递的异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为5的异常，描述= "CREATION_FAILED"和additionalInfo= &lt;as pass by方法传递的异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为5的异常，描述= "CREATION_FAILED"和additionalInfo= &lt;as pass by方法传递的异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为7的异常，描述= "DATA_NOT_AVAILABLE"和additionalInfo= &lt;as通过引发此异常的方法传递的&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为8的异常，描述= "SEEK_ERROR"和additionalInfo= &lt;按引发此异常的方法传递的&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupported功能</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为9的异常，描述= "UNSUPPORTED_FEATURE"和additionalInfo= &lt;as pass by方法传递的异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为10的异常，说明= "RANGE_ERROR"和其他Info= &lt;按引发此异常的方法传递的</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为11的异常，描述= "CODEC_NOT_SUPPORTED"和additionalInfo= &lt;as通过引发此异常的方法传递的&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为12的异常，描述= "MEDIA_ERROR"和additionalInfo= &lt;按引发此异常的方法传递的&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为13的异常，说明= "NETWORK_ERROR"和additionalInfo= &lt;按引发此异常的方法传递的&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error或MediaPlayerNotification.Warning</td> 
   <td>MediaError或NotificationEvent</td> 
   <td>代码为14的异常，description = "GENERIC_ERROR"和additionalInfo= &lt;as pass by方法传递的异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为15的异常，描述= "INVALID_SEEK_TIME"和additionalInfo= &lt;as通过引发此异常的方法传递的&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为16的异常，描述= "AUDIO_TRACK_ERROR"和additionalInfo= &lt;as通过引发此异常的方法传递的&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferent<p>线程错误</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为17的异常，description = "GENERIC_ERROR"和additionalInfo= &lt;as pass by方法传递的异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为18的异常，description = "GENERIC_ERROR", additionalInfo= &lt;as pass by方法传递，该方法引发此异常</td> 
  </tr> 
  <tr> 
   <td>kECNotImplemented</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为19的异常，description = "GENERIC_ERROR" and additionalInfo= &lt;as pass by方法传递的异常&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为200的异常，说明= "PLAYBACK_OPERATION_FAILED"和additionalInfo= &lt;as通过引发此异常的方法传递的&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>通知事件</td> 
   <td>代码为201的异常，description = "NATIVE_WARNING"和additionalInfo= &lt;as通过引发此异常的方法传递</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>代码为202的异常，说明= "AD_RESOLVER_FAILED"和additionalInfo= &lt;as通过引发此异常的方法传递的&gt;</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的实用程序和帮助程序API元素更改 {#utility-and-helper-api-element-changes-for}

这些表比较了JavaScript TVSDK的实用程序和帮助程序API元素在版本1.3和2.0之间。

本主题中的表：

* 版本
* 时间范围
* QOSProvider
* 设备信息
* LoadInfo
* 视图
* 播放信息

### 版本 {#version}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口版本<br /> {<br /> readonly属性DomString版本；<br /> 只读属性DomString描述；<br /> 只读属性长主题；<br /> 只读属性长小调；<br /> 只读属性长修订；<br /> 只读属性long apiVersion;<br /> };</p> </td> 
   <td><p>接口版本<br /> {<br /> readonly属性DomString版本；<br /> 只读属性DomString描述；<br /> 只读属性DomString major;<br /> 只读属性DomString次要；<br /> 只读属性DomString修订版；<br /> 只读属性DomString apiVersion;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 时间范围 {#timerange}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0没有更改</td> 
   <td><p>接口TimeRange<br /> {readonly<br /> attribute unsigned long begin;<br /> 只读属性unsigned long end;<br /> 只读属性无符号长持续时间；<br /> };</p> </td> 
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
   <td><p>接口QOSProvider<br /> {<br /> void attachMediaPlayer（MediaPlayer播放器）;<br /> void detachMediaPlayer();<br /><br /> 只读属性deviceInformation deviceInformation;<br /> readonly属性playbackInformation playbackInformation;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 设备信息 {#deviceinformation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口DeviceInformation<br /> {<br /> readonly属性DomString os;<br /><br /> <br /> <br /> 只读属性DomString id;<br /> 只读属性int densityDPI;<br /> readonly属性int heightPixels;<br /> 只读属性int widthPixels;<br /> 只读属性boolean seekToKeyFrame;<br /> };</p> </td> 
   <td><p>接口DeviceInformation<br /> {<br /> readonly属性DomString os;<br /> readonly属性int sdk;<br /> 只读属性DomString模型；<br /> 只读属性DomString制造商；<br /> 只读属性DomString id;<br /> 只读属性int densityDPI;<br /> readonly属性int heightPixels;<br /> 只读属性int widthPixels;<br /><br /> };</p> </td> 
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
   <td><p>接口LoadInfo<br /> {<br /> readonly属性DomString url;<br /> 只读属性int size;<br /> 只读属性多次downloadDuration;<br /> readonly属性int periodIndex;<br /> 只读属性多次mediaDuration;<br /> 只读属性short TRACK_TYPE_FRAGMENT;<br /> 只读属性short TRACK_TYPE_TRACK;<br /> 只读属性short TRACK_TYPE_MANIFEST;<br /> 只读属性短类型；<br /> 只读属性DomString trackName;<br /> 只读属性DomString trackType;<br /> readonly属性int trackIndex;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 视图 {#view}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0没有更改</td> 
   <td><p>接口视图<br /><br /> { readonly属性unsigned short x;<br /> 只读属性unsigned shorg y;<br /> 只读属性无符号短宽度；<br /> 只读属性无符号短高度；<br /><br /> void setSize(unsigned short width, unsigned short height);<br /> void setPos(unsigned short x, unsigned short y);<br /> }</p> </td> 
  </tr> 
 </tbody> 
</table>

### 播放信息 {#playbackinformation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口PlaybackInformation<br /> {<br /> readonly属性多次timeToFirstByte;<br /> 只读属性多次timeToLoad;<br /> 只读属性多次timeToStart;<br /> 只读属性多次timeToFail;<br /> readonly属性int totalSecondsPlayed;<br /> readonly属性int totalSecondsSpent;<br /> 只读属性多次frameRate;<br /> 只读属性int droppedFrameCount;<br /> readonly属性int envericedBandwidth;<br /> 只读属性int比特率；<br /> 只读属性多次bufferTime;<br /> readonly属性int bufferLength;<br /> readonly属性int emptyBufferCount;<br /> 只读属性多次bufferingTime;<br /> };</p> </td> 
   <td><p>接口PlaybackInformation<br /> {<br /> readonly属性多次timeToFirstByte;<br /> 只读属性多次timeToLoad;<br /> 只读属性多次timeToStart;<br /> 只读属性多次timeToFail;<br /> readonly属性int totalSecondsPlayed;<br /> readonly属性int totalSecondsSpent;<br /> 只读属性多次frameRate;<br /> 只读属性int droppedFrameCount;<br /><br /> 只读属性int比特率；<br /> 只读属性多次bufferTime;<br /> readonly属性int bufferLength;<br /> readonly属性int emptyBufferCount;<br /> 只读属性多次bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 实用资源 {#helpful-resources}

* 请参阅Adobe Primetime学习和支 [持页面上的完整帮助](https://helpx.adobe.com/support/primetime.html) 文档。
