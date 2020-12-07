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


# TVSDK转换——对于JavaScript {#tvsdk-conversion-to-for-javascript},1.3到2.0

2.0的许多方法签名和API元素名称已更改。请查看这些表以查看所有API更改详细信息。

## 在JavaScript {#implement-callback-functions-in-javascript}中实现回调函数

方法文档中的注释建议您需要实现的回调的签名。

对于JavaScript,API语法基于Web ID。 对于TVSDK接口，方法名称称为&#x200B;*methodName*()。 对于应用程序要实现的方法，将向接口添加一个名为&#x200B;*methodName* CallbackFunc的读／写属性，并且应用程序应将其设置为指向实现该方法的函数。 例如：

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
   <td><p> <strong>TimedMetadata</strong>:接口TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0; <br /> const unsigned short metadata_TYPE_ID3 = 1 ; <br /> 只读属性未签名短类型； <br /> 只读属性长时间；只<br /> 读属性DomString id；只<br /> 读属性DomString名称；只<br /> 读属性DomString内容； <br /> 只读属性对象元数据；<br /> }; </p> </td> 
   <td><p>interface TimedMetadata {<br />将无符号短METADATA_TYPE_TAG = 0 ;<br />将无符号短METADATA_TYPE_ID3 = 1 ;<br />只读属性短元数据类型；<br />只读属性长时间；<br />只读属性长id;<br />只读属性domString name;<br /> <br />只读属性对象元数据；<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>:（2.0没有更改）</td> 
   <td><p>接口TimedMetadataList {<br />只读属性未签名长度；<br /> getter TimedMetadata（未签名长索引）;<br /> };</p> </td> 
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
   <td><p>接口AdSignlingMode { <br />控制未签名短MODE_DEFAULT, <br />控制未签名短MODE_MANIFEST_CEASS, <br />控制未签名短MODE_SERVER_MAP, <br />控制未签名短MODE_CUSTOM_RANGES &lt;A4/&gt; };<br /></p> </td> 
   <td>这将替换MetadataKeys::MANIFEST_CAIS密钥。</td> 
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
   <td><p>接口CustomRangeMetadata { <br />控制未签名的短TYPE_MARK_RANGE;<br />控制未签名的短TYPE_DELETE_RANGE;<br />控制未签名的短TYPE_REPLACE_RANGE;<br />属性未签名短类型；<br />属性boolean adjustSeekPosition;<br />属性TimeRangeList timeRangeList;<br /> };</p> </td> 
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
   <td><p>interface ReplaceTimeRange { <br />属性未签名的长开始；<br /> readonly属性unsigned long end;<br />属性未签名的长持续时间；<br />属性unsigned long replaceDuration;<br /> };</p> </td> 
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
   <td><p>接口位置{ <br />控制未签名的短TYPE_MID_ROLL;<br />控制未签名的短类型PRE_ROLL;<br /> const unsigned short TYPE_POST_ROLL;<br />控制未签名的短类型SERVER_MAP;<br /> const unsigned short TYPE_CUSTOM_RANGE;<br /> readonly属性unsigned short type;<br />只读属性长时间；<br />只读属性长持续时间；<br /> const unsigned short MODE_DEFAULT;<br />控制无符号短MODE_INSERT;<br />控制未签名的短MODE_REPLACE;<br />控制未签名的短MODE_DELETE;<br />控制无符号短MODE_MARK;<br />控制未签名的短MODE_FREE_REPLACE;<br />只读属性未签名短模式；<br />只读属性TimeRange范围；<br /> };</p> </td> 
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
   <td><p>interface Opportunity { <br />只读属性DomString id;<br />只读属性放置；<br />只读属性对象设置；<br /> readonly属性Object customParameters;<br /> }; </p> </td> 
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
   <td><p>接口保留{ <br />只读属性TimeRange范围；<br />只读属性long hold;<br /> }; </p> </td> 
   <td> （2.0新增）</td> 
  </tr> 
 </tbody> 
</table>

### 时间轴／时间轴项／时间轴标记{#timeline-timelineitem-timelinemarker}

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
   <td><p> <strong>时间轴项</strong>:接口TimelineItem:<br /> TimelineMarker <br /> {readonly属性长id; <br /> 只读属性TimeRange virtualRange; <br /> 只读属性TimeRange localRange; <br /> 只读属性boolean watched; <br /> 只读属性布尔临时值； <br /> }; </p> </td> 
   <td>（2.0新增）</td> 
  </tr> 
  <tr> 
   <td><strong>时间轴标记</strong>:（2.0没有更改）</td> 
   <td><p>接口TimelineMarker {<br />只读属性多次时间；<br />只读属性多次持续时间；<br /> };</p> </td> 
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
   <td><p> <strong>广告</strong>:接口Ad {<br /> readonly属性AdAsset <br /> primaryAsset;readonly<br /> <br /> 属性AdAssetList companionAssets;readonly属性多次持续时间；readonly属性<br /> DomString id;const short ADTYPE_LINEAR = 0 <br /> const unsigned short ADTYPE_NONLINEAR = 1;readonarals <br /> <br /> <br /> <br /> 无符号属性类型；只读属性AdInsertionType adInsertionType; <br /> <br /> 只读属性布尔可单击； <br /> 只读属性boolean isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>接口Ad {<br />只读属性AdAsset primaryAsset;<br />只读属性AdAssetList companionAssets;<br /> <br />只读属性多次持续时间；<br />只读属性DomString id;<br />无符号短ADTYPE_LINEAR = 0;<br />const unsigned short ADTYPE_NONLINERAL = 1;<br /> <br /> readonly属性unsigned short type;<br /> readonly属性AdInsertionType insertionType;<br />只读属性对象跟踪器；<br /> <br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>:（2.0没有更改）</td> 
   <td><p>接口AdAsset {<br />只读属性DomString id;<br />只读属性多次持续时间；<br />只读属性MediaResource资源；<br />只读属性AdClick adClick;<br />只读属性对象元数据；<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>:（2.0没有更改）</td> 
   <td><p>接口AdClick {<br />只读属性DomString id;<br />只读属性DomString title;<br />只读属性DomString url;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>:（2.0没有更改）</td> 
   <td><p>接口AdList {<br />只读属性未签名长度；<br /> getter Ad（未签名长索引）;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>:（2.0没有更改）</td> 
   <td><p>接口AdAssetList {<br />只读属性未签名长度；<br /> getter AdAsset（未签名长索引）;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>:接口AdBannerAsset:AdAsset<br /> {<br /> readonly属性int width;readonly<br /> 属性int height;readonly<br /> 属性DomString staticUrl;readonly属性<br /> DomString height;readonly<br /> 属性DomString width;<br /> };</p> </td> 
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
   <td><p><strong>AdBreakTimelineItemList</strong>:interface AdBreakTimelineItemList {  <br /> readonly属性未签名长； <br /> getterAdBreakTimelineItem（未签名日志索引）; <br /> };</p> </td> 
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
   <td><p>接口AdBreakPolicy {<br />只读属性短AD_BREAK_POLICY_SKIP;<br />只读属性短AD_BREAK_POLICY_PLAY;<br />只读属性短AD_BREAK_POLICY_REMOVE;<br />只读属性短AD_AD_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> 接口AdPolicyConstants {<br />只读属性短AD_BREAK_POLICY_SKIP;<br />只读属性短AD_BREAK_POLICY_PLAY;<br />只读属性短AD_BREAK_POLICY_REMOVE;<br />只读属性短ADONLYAD_POLICY_REMOVE_AFTER_PLAY;}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interface AdBreakWatchedPolicy {<br />只读属性short AD_BREAK_AS_WATCH_ON_BEGIN;<br />只读属性short AD_BREAK_AS_WATCHED_ON_END;<br />只读属性short AD_BREK_BREAK_BREAK_BREAKWATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br />只读属性short AD_BREAK_AS_WATCHED_ON_BEGIN;<br />只读属性short AD_BREAK_AS_WATCHED_ON_END;<br />只读属性short AD_BREAK_AS_WATEVEREVER;&lt;AT/<br />&lt;a/&gt;...</p> </td> 
  </tr> 
  <tr> 
   <td><p>接口AdPolicy {<br />只读属性short AD_POLICY_PLAY;<br />只读属性short AD_POLICY_PLAY_FROM_AD_BEGIN;<br />只读属性short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;只读属性short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> <br />只读属性short AD_POLICY_SKIP_AD_BREAK;<br /> };</p> </td> 
   <td><p> ... <br />只读属性short AD_POLICY_PLAY;<br />只读属性short AD_POLICY_PLAY_FROM_AD_BEGIN;<br />只读属性short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br />仅属性short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br />只读属性short AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>接口AdPolicyMode {<br />只读属性short AD_POLICY_MODE_PLAY;<br />只读属性short AD_POLICY_MODE_SEEK;<br />只读属性shortAD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> {readonly attribute short AD_POLICY_MODE_PLAY;<br /> readonly attribute short AD_POLICY_MODE_SEEK;<br /> readonly attribute short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>接口AdPolicyInfo {<br />只读属性AdBreakTimelineItemList <br /> adBreakTimelineItems;<br />只读属性AdTimelineItem;<br />只读属性多次currentTime;<br />只读属性多次搜索toTime;<br />只读属性多次率；<br />只读属性短模式；//AdPolicyMode<br /> };</p> </td> 
   <td><p>接口AdPolicyInfo {<br />只读属性AdBreakPlacementList <br /> adBreakAptions;<br />只读属性Ad;<br />只读属性多次currentTime;<br />只读属性多次seekToTime;<br />只读属性多次率；a6/&gt;只读属性短模式；//AdPolicyMode<br /> };<br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>接口AdPolicySelector {<br /> /*<br /> * AdbreakPolicy selectForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br />属性Object selectPolicyForAdBreakCallbackInfofunc;<br /> /**<br /> * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br />属性对象选择AdBreaksToPlayCallbackInfofunc;<br /> /**<br /> * AdPolicy selectForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br />属性Object selectPolicyForSeekIntoAdcallbackFunc;<br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br />属性对象selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>接口AdPolicySelector {<br /> /*<br /> * AdbreakPolicy selectForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br />属性Object selectPolicyForAdFuncBreakInfo回调；<br /> /**<br /> * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br />属性Object selectAdBreaksToPlayCallback;&lt;allback;&lt;alalack0/&gt; /**<br /> * AdPolicy selectForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */<br />属性Object selectPolicyForSeekIntoAdCallback;<br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */<br />属性对象selectWatckedPolicyForAdBreakCallback;<br /> };<br /></p> </td> 
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
   <td><p>接口AdBreakPlacement:TimelineOperation {<br />只读属性AdBreak adBreak;<br />只读属性位置；//从TimelineOperation<br />只读属性多次时间；<br />只读属性多次持续时间；<br /> };</p> </td> 
   <td><p>接口AdBreakPlacement {<br />只读属性AdBreak adBreak;<br />只读属性位置；<br />只读属性多次时间；<br />只读属性多次持续时间；<br /> };</p> </td> 
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
   <td><p>接口AuditudeSettings:AdvertisingMetadata { <br />属性DomString zoneId;<br />属性DomString mediaId;<br />属性DomString defaultMediaId ;<br />属性DomString域；<br />属性对象targettingInfo ;<br />属性Object customParameters;<br />属性Boolean creativePackaingEnabled ;<br />属性Boolean showStaticBanners ;<br /> };</p> </td> 
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
   <td><p>接口MediaPlayerItemConfig {<br />属性ContentFactory adFactory;<br />属性StringList subscribeTags;<br /> <br />属性StringList adTags;<br /> <br />属性AdSigningMode adSigningMode;&lt;ag7/&gt;属性CustomRangeMetadata customRangeMetadata;<br />属性NetworkConfiguration networkConfiguration;<br />属性AdvertisingMetadatisMetadata;<br />属性Boolean useHardwareDecoder;<br /> };<br /><br /></p> </td> 
   <td><p>接口MediaPlayerConfig {<br /> <br /> <br /> <br />属性StringList adTags;<br />属性StringList subscribedTags;<br />属性MediaPlayerClientFactoryFactory;<br /> <br /> <br /> <br />a10/&gt; <br /> };<br /></p> </td> 
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
   <td><p>interfaceContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector（<br /> * MediaPlayerItem项）;<br /> */<br />属性对象retrieveAdPolicySelectorCallbackFunc;<br />;</p> </td> 
   <td><p>接口MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieAdPolicySelector（<br /> * MediaPlayerItem项）;<br /> */<br />属性对象检索AdPolicySelectorFunc;<br />;</p> </td> 
  </tr> 
 </tbody> 
</table>

### 网络配置{#networkconfiguration}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interfaceNetworkConfiguration<br /> {<br />属性boolean forceNativeNetworking;<br />属性boolean useRedirectedUrl;<br />属性Object cookieHeader;<br />属性boolean readSetCookieHeader;<br />属性int masterUpdateInterateInterval;<br />属性boolean useCookieHeaderForAllRequests;<br />属性int readLimit;<br /> };</p> </td> 
   <td>在1.3中，其中一些功能是由MetadataKeys提供的</td> 
  </tr> 
 </tbody> 
</table>

## 2.0 {#drm-api-element-changes-for}的DRM API元素更改

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

### DRM工作流初始化{#drm-workflow-initialization}

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
   <td><p>interface DRMMetadata<br /> {<br />只读属性DomString serverUrl;<br />只读属性DomString licenseId;<br />只读属性DRMPolicyArray策略；<br /> };</p> </td> 
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
   <td><p>interface DRMPlaybackTimeWindow {<br /> readonly属性int playbackPeriodInSeconds;<br /> readonly属性long playbackStartDate;<br /> readonly属性long playbackEndDate;<br /> };</p> </td> 
   <td><p>interface DRMPlaybackTimeWindow {<br /> readonly attribute int periodInSeconds;<br /> readonly attribute int startDate;<br /> readonly attribute int entDate;<br /> };</p> </td> 
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
   <td><p>interface DRMLicense {<br />只读属性Uint8Array字节；<br />只读属性Date licenseStartDate;<br />只读属性Date licenseEndDate;<br />只读属性Date offlineStorageStartDate;<br />只读属性Date offlineStorageEnd日期；<br />只读属性DomString serverUrl;<br />只读属性DomString licenseID;<br />只读属性DomString policyID;<br />只读属性DRMPlaybackTimeWindow playbackTimeWindow;<br />只读属性Object customPropertiestopropertites;<br /> }; </p> </td> 
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
   <td><p>interface DRMLicenseDomain {<br />只读属性DomString authenticationDomain;<br />只读属性DRMAuthenticationMethod authenticationMethod;<br />只读属性DomString serverUrl;<br /> };</p> </td> 
   <td><p>interface DRMLicenseDomain {<br />只读属性DomString authDomain;<br />只读属性DRMAuthenticationMethod authMethod;<br />只读属性DomString serverURL;<br /> };</p> </td> 
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
   <td><p>interface DRMPolicy<br /> {<br />只读属性DomString authenticationDomain;<br />只读属性DRMAuthenticationMethod authenticationMethod;<br /> <br />只读属性DomString displayName;<br />只读属性DRMLicenseDomain licensenecese域；<br /> };</p> </td> 
   <td><p>interface DRMPolicy<br /> {<br />只读属性DomString authDomain;<br />只读属性DRMAuthenticationMethod authMethod;<br />只读属性DomString dispName;<br />只读属性DRMLicenseDomain licenseDomain;5/&gt; };<br /></p> </td> 
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
   <td><p>接口DRMManager:EventTarget {<br /> void acquireLicense（DRMMetadata元数据， <br /> DRMAcquireLicenseSettings设置， <br /> DRMAquireLicenseListener）;<br /> void acquirePreviewLicense(DRMMetadata, <br /> DRAQuIRELicenseLISTENER);&lt;A5/&gt; VOID AUTHENTICATE（DRMMetadata元数据， <br /> DomString url,<br /> DomString &amp;authenticationDomain, <br /> DomString用户， <br /> DomString口令， <br /> DRMAuthenticate监听器）;<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array, DRMErrorListener);<br /> void initialize(DRMOperationCompleteListener);<br />属性long maxOperationTime;<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> DRMOperationCompleteListener);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> DRMOperationCompleteListener);<br /> <br /> void resetDRM(DRMOperationCompleteListener);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID, <br /> DomString policyID, <br /> booleanImtedially,<br /> DRMReturnLicenseer);&lt;atener31/&gt; void setAuthenticationToken（<br /> DRMMetadata元数据， <br /> DomString authenticationDomain, <br /> Uint8Array令牌， <br /> DRMOperationCompleteListener）;<br /> store voidLicenseBytes(Uint8Array licenseBytes, <br /> DRMOperationCompleteListener);<br /> };<br /><br /></p> </td> 
   <td><p>接口DRMManager:EventTarget {<br /> void acquireLicense（DRMMetadata元数据， <br /> DRMAcquireLicenseSettings, <br /> EventContext eventContext）;<br /> voidPreviewLicense(DRMMetadata, <br /> EventContextContext);<br /> void authenticate（DRMMetadata元数据， <br /> DomString url,<br /> DomString &amp;authenticationDomain, <br /> DomString用户， <br /> DomString口令， <br /> EventContext）;<br />12/&gt; DRMMetadata createMetadataFromBytes(<br /> Uint8Array, EventContexteventContext);<br /> void initialize(EventContexteventContext);<br />属性long maxOperationTime;<br />a17/&gt; void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> EventContext eventContext);<br /> void leaveLicenseDomain(<br /> DRMLICENSEDomain licenseDomain, <br /> EventContext eventContext);<br /> <br /> void resetDRM(EventContext eventContext);<br /> void returnLicense（DomString serverURL, <br />字符串licenseID,<br /> DomString策略ID, <br />布尔commitImmetially,<br /> EventContext事件Context）;<br /> void setAuthenticationToken（<br /> DRMMetadata, <br /> DomString authenticationDomain, <br /> Uint8Array令牌， <br /> EventContext事件Context）;<br /> void storeLicenseBytes（Uint8Array licenseBytes, <br /> EventContext事件Context）;&lt;atextext8/&gt; };<br /><br /><br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMErrorListener :<br /> public psdkutils::PSDKInterfaceWithUserData {<br /> public:<br /> virtual void onDRMError(uint32_t major, <br /> uint32_t minor, <br /> const psdkutils:PSDKString&amp; errorString, <br /> const psdkutils::PSDKString&amp; errorServerUrl)= 0;<br /> <br />受保护：<br />虚拟~DRMErrorListener(){}<br /> }</p> </td> 
   <td>事件/接口／说明 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>在DRMManger的一种异步方法期间发生错误时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMOperationCompleteListener :<br /> public DRMErrorListener {<br /> public:<br /> virtual void onDRMOperationComplete()= 0;<br /> <br />受保护：<br />虚拟~DRMOperationCompleteListener(){}<br /> };</p> </td> 
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
   <td><p>类DRMAuthenticateListener:<br />公用DRMErrorListener {<br />公用：<br /> virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken)= 0;<br /> <br />受保护：<br />虚拟drmaUTHENTICATElistener(){}<br /> }</p> </td> 
   <td>事件/接口／说明 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/DRMAuthenticationCompleteEvent</p> <p>当DRMManager::authenticate方法调用成功时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMAquireLicenseListener:<br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseAppired(const DRMLicense*)= 0;<br /> <br /> protected:<br /> virtual ~DRMAquireLicenseListener(){}<br /> };</p> </td> 
   <td>事件/接口／说明 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquired<p>/DRMLicenseAppiredEvent</p> <p>当DRMManager::acquirePreviewLicense方法调用成功时。</p> </li> 
     <li>kEventDRMLicenseAppired<p>/DRMLicenseAppiredEvent</p> <p>当DRMManager::acquireLicense方法调用成功时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMReturnLicenseListener:<br /> public DRMErrorListener {<br /> public:<br /> virtual void onLicenseReturnComplete(uint32_t numReturned)= 0;<br /> <br /> protected:<br /> virtual DRMReturnLicenseListener(){}&lt;a6/};<br /></p> </td> 
   <td>事件/接口／说明 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/DRMLicenseReturnCompleteEvent</p> <p>当DRMManager::returnLicense方法调用成功时。</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 2.0 {#generic-playback-api-element-changes-for}的通用播放API元素更改

这些表比较JavaScript TVSDK 1.3和2.0之间的通用播放API元素。

本主题中的表：

* 媒体资源
* MediaPlayer
* ABRControlParameters
* BufferControlParameters
* TextFormat
* MediaPlayerItemLoader

### 媒体资源{#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口MediaResource {<br />属性DomString url;<br />属性未签名短类型；<br />属性对象元数据；<br />控制未签名短类型TYPE_HLS;<br />控制未签名短类型TYPE_HDS;<br />控制未签名短类型TYPE_DASH;<br />控制未签名短类型TYPE_CUSTOM;<br />控制未签名短类型_UNKNOWN;<br /> };</p> </td> 
   <td><p>interface MediaResource {<br />属性DomString url;<br />属性DomString类型；<br />属性对象元数据；<br /> <br /> <br /> <br /> <br /> <br /> };</p> </td> 
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
   <td><p>接口MediaPlayer:EventTarget<br /> {<br /> void prepareToPlay(多次位置);<br /> void play();<br /> void pause();<br /> void seek(多次位置);<br /> void seekToLocal(多次位置);<br /> void reset();<br /> void release);<br /> void replaceCurrentItem（MediaPlayerItem项）;<br /> void replaceCurrentResource(MediaResource rsource, <br /> MediaPlayerItemConfig);<br /> void suspend();<br /> void restore();<br /> void notifyClick();<br /> <br />只读属性TimeRange playbackRange;<br />只读属性TimeRange seekableRange;<br /> 只读属性多次currentTime;<br />只读属性多次localTime;<br />只读属性TimeRange bufferedRange;<br />只读属性DRMManager drmManager;<br />只读属性MediaPlayerItem currentItem;<br /> <br /> // PlayerStatus<br /> <br /> <br />收藏未签名短播放器状态初始化；<br />收藏未签名短播放器状态准备；<br />收藏未签名短播放器状态准备；<br />收藏未签名短播放器状态播放；<br />控制未签名的短PLAYER_STATUS_PAUSED;<br />控制未签名的短PLAYER_STATUS_SEEKING;<br />控制未签名的短PLAYER_STATUS_COMPLETE;<br />控制未签名的短PLAYER_STATUS_ERROR;&lt;a1<br /> <br /> <br />只读属性unsigned short status;<br /> <br />属性unsigned short volume;<br />属性ABRControlParametersabrControlParameters;<br />属性BufferControlParameters bufferControlParameters;<br /> <br />控制未签名的short VISIBLE;//对于CC可见性<br />，无符号短INVISIBLE;//对于CC可见性<br />属性未签名的short ccVisibility;<br />属性TextFormat ccStyle;<br />只读属性PlaybackMetrics playbackMetrics;<br /> <br />属性多次率；<br />属性MediaPlayerView视图;<br />只读属性时间线；<br />属性多次currentTimeUpdateInterval;<br /> //设置2.0<br /> }不支持此设置；</p> </td> 
   <td><p>接口MediaPlayer:EventTarget<br /> {<br /> void prepareToPlay(int position);<br /> void play();<br /> void pause();<br /> void seek(int position);<br /> void reset();<br /> void release);<br /> void replaceCurrentItem（MediaResource源）;<br /> <br /> <br /> <br /> <br /> <br /> <br />只读属性TimeRange playbackRange;<br />属性TimeRange seekableRange;<br />只读属性多次currentTime;<br /> <br />只读属性多次localTime;<br />只读属性TimeRange bufferedRange;<br />只读属性DRMManager drmManager;<br />只读属性MediaPlayerItem currentItem;<br /> <br /> // PlayerState<br />控制未签名的短PLAYER_STATEIDLE;<br />控制未签名的短PLAYER_STATE_INITIALIZING;<br />控制未签名的短PLAYER_STATE_INITIALIZED;<br />控制未签名的短PLAYER_STATE_PREPARED;<br />unsigned short PLAYER_STATE_PLAYING;<br /> const unsigned short PLAYER_STATE_PAUSED;<br /> const unsigned short PLAYER_STATE_SEEKING;<br /> const unsigned short PLAYERSTATE_ERROR;<br />包含未签名的短PLAYER_STATE_RELEASED;<br /> <br /><br />const unsigned short PLAYER_STATUS_SUSPENDED;<br />只读属性unsigned short state;<br /> <br />属性unsigned short volume;<br />属性ABRControlParameters abrControlParameters;<br /> <br />仅无符号短可见；//对于CC可见性<br />只读未签名短INVISIBLE;//对于CC可见性<br />属性unsigned short ccVisibility;<br />属性TextFormat ccStyle;<br />只读属性PlaybackMetrics playbackMetrics;<br />属性MediaPlayerConfigMediaPlayerConfig;<br />属性多次率；<br />属性MediaPlayerView视图;<br />只读属性时间线；<br /> <br /> <br /> };<br /></p> </td> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerStatus<br /> {<br /> // PlayerStatus<br />控制未签名的短PLAYER_STATUS_IDLE;<br />控制未签名的短PLAYER_STATUS_INITIALIZED;<br />控制未签名的短PLAYER_STATUS_INITIALIZED;<br />player_STATUS_PREPARING;<br />包含未签名的短PLAYER_STATUS_PREPARED;<br />包含未签名的短PLAYER_STATUS_PLAYING;<br />包含未签名的短PLAYER_STATUS_PAUSED;<br />包含未签名的短PLAYER_STATUS_STATUS_SETHOTAPEARK0/&gt;包含未签名的短PLAYER_STATUS_COMPLETE;<br />包含未签名的短PLAYER_STATUS_ERROR;<br />包含未签名的短PLAYER_STATUS_RELEASED;<br />包含未签名的短PLAYER_STATUS_SUSPSENDED;<br />;<br /></p> </td> 
   <td>（2.0新增）</td> 
  </tr> 
 </tbody> 
</table>

#### 事件受MediaPlayer {#events-supported-by-mediaplayer}支持

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
   <td>广告已点击<br />用户单击广告时。</td> 
   <td>AdClickedEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>profileChanged<br />当播放用户档案发生更改时。</td> 
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
   <td>字幕更新<br />当媒体播放器项更新时。 对于实时／线性流，客户端必须定期刷新媒体资源以检测新的可用内容。 发生这种情况时，某些媒体特性可能会发生变化。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>masterUpdated <br />当媒体播放器项更新时。 对于实时／线性流，客户端必须定期刷新媒体资源以检测新的可用内容。 发生这种情况时，某些媒体特性可能会发生变化。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRangeUpdated<br />当媒体播放器项目更新时。 对于实时／线性流，客户端必须定期刷新媒体资源以检测新的可用内容。 发生这种情况时，某些媒体特性可能会发生变化。</td> 
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
   <td><p>interface ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONST = 0 ;<br /> const unsigned short ABR_POLICY_MEDEATE = 1 ;<br /> const sort unsigned ABR short ABR_ POLICY_ POLICY_ POLICY = 2 ;<br /> &lt;a4/&gt; &lt;a5attribute short abrPolicy;<br /> attribute unsigned int initialBitRate;<br /> attribute unsigned int minBitRate;<br /> attribute unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ABRE_BITRATE;<br />const short shortst DEFAULTABR_MIN_BITRATE;<br />控制未签名的短DEFAULT_ABR_MAX_BITRATE;<br />控制ABRPolicy DEFAULT_ABR_POLICY;<br /> };<br /></p> </td> 
   <td><p>interface ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONST = 0 ;<br /> const unsigned short ABR_POLICY_MEDEATE = 1 ;<br /> const sort unsigned ABR short ABR_ POLICY_ POLICY_ POLICY = 2 ;<br /> &lt;a4/&gt; &lt;a5attribute unsigned short abrPolicy;<br /> attribute unsigned int initialBitRate;<br /> attribute unsigned int minBitRate;<br /> attribute unsigned int maxBitRate;<br /> <br /> <br /> <br /> };<br /><br /></p> </td> 
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
   <td><p>interface BufferControlParameters<br /> {<br />属性多次initialBufferTime;<br />属性多次playBufferTime;<br />控制多次DEFAULT_INITIAL_BUFFER_TIME;<br />控制多次DEFAULT_PLAY_BUFFER_TIME;&lt;a5;/&gt; };<br /></p> </td> 
   <td><p>interface BufferControlParameters<br /> {<br />属性多次initialBufferTime;<br />属性多次playBufferTime;<br /> <br /> <br /> };</p> </td> 
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
   <td><p>接口TextFormat<br /> {<br /> // Color<br />控制未签名短COLOR_DEFAULT = 0 ;<br />控制未签名短COLOR_BLACK = 1 ;<br />控制未签名短COLOR_GRAY = 2 ;<br />控制未签名短COLOR_WHITE = 3 ; a6/&gt;连续无符号短COLOR_BRIGHT_WHITE = 4;<br />连续无符号短COLOR_DARK_RED = 5;<br />连续无符号短COLOR_RED = 6;<br />连续无符号短COLOR_BRIGHT_RED = 7;<br />无符号短COLOR_DARK_GREEN = 8;<br />无符号短COLOR_GREEN = 9;<br />无符号短COLOR_BRIGHT_GREEN = 10;<br />无符号短COLOR_DARK_BLUE = 11;<br />无符号short COLOR_BLUE = 12 ;<br />无符号短COLOR_BRIGHT_BLUE = 13 ;<br />无符号短COLOR_DARK_YELLOW = 14 ;<br />无符号短COLOR_YELLOW = 15 ;<br /> <br />const unsigned short COLOR_BRIGHT_YELLOW = 16 ;<br /> const unsigned short COLOR_DARK_MAGENTA = 17 ;<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 18 ;<br /> const unsigned short unsigned short short COLOR COLORshortsht SHORTst SHORT SHORT SHORT SHORTCOLOR_DARK_CYAN = 20;<br />无符号短COLOR_CYAN = 21;<br />无符号短COLOR_BRIGHT_CYAN = 22;<br /> <br />只读属性无符号短fontColor;<br />只读属性无符号短背景Color;<br />只读属性unsigned short fillColor;<br />只读属性unsigned short edgeColor;<br /> <br /> // Size<br /> const short SIZE_DEFAULT = 0 ;<br /> const unsigned short SIZE = 1 ;<br />连续未签名短SIZE_MEDIUM = 2 ;<br /><br /> const unsigned short SIZE_LARGE = 3;<br /> <br />只读属性未签名的短大小；<br /> <br /> // FontEdge<br />控制未签名的短FONT_EDGE_DEFAULT = 0;<br />控制未签名的短FONT_EDGE_NONE = 1;<br />st unsigned short FONT_EDGE_ROUNDED = 2 ;<br /> const unsigned short FONT_EDGE_CONSERED = 3 ;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5 ;<br />控制未签名的短字FONT_EDGE_DROP_SHADOW_RIGHT = 6;<br />只读属性未签名的短字Edge;<br /> <br /> // Font<br />控制未签名的短字FONT_DEFAULT = 0;<br />无签名FONT_MONOSPACED_WITH_SERIFS = 1 ;<br /><br /> const unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2;<br /> const unsigned short FONT_MONSPACED_WITH_SERIFS = 3;<br /> const unsigned short FONT_CURSIVE = 5;<br /> const shortFONT_SMALL_CAPITALS = 6;<br />只读属性未签名短字体；<br />只读属性未签名短字体Opacity;<br />只读属性未签名短背景Opacity;<br />只读属性未签名短DEFAULT_OPACITY;<br /> };<br /><br /></p> </td> 
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
   <td><p>接口MediaPlayerItemLoader:<br /> {<br /> void load(MediaResource, long resourceId,<br /> ItemLoaderListener, <br /> MediaPlayerItemConfig);<br /> void cancel();<br />只读属性MediaPlayerItemItemcurrentItem;<br /> };</p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
  <tr> 
   <td><p>接口ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br />var onErrorCallbackFunc;<br /> }</p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
 </tbody> 
</table>

## 2.0 {#media-characteristics-api-element-changes-for}的媒体特性API元素更改

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
   <td><p>接口MediaPlayerItem {<br />只读属性MediaResource;<br />只读属性long resourceId;<br />只读属性boolean live;<br /> <br />只读属性boolean hasAlternateAudio;<br />只读属性AudioTrackst audioReadTracks;&lt;adoreadoReadoReadoreadoReads;&lt;adattributeAudioTrack selectedAudioTrack;<br /> void selectAudioTrack(AudioTrack);<br /> <br />只读属性boolean hasClosedCaptions;<br />只读属性ClosedCaptionsTrackClosedCaptionsTracks;<br />只读属性ClosedCaptionsTrack;<br /> void selectColectedCelectedCaptCedCaptionsCaptionstrack(<br /> ClosedCaptionsTrack);<br /> <br /><br /> 只读属性boolean hasTimedMetadata;<br />只读属性TimedMetadataList timedMetadata;<br />只读属性boolean dynamic;<br /> <br />只读属性boolean isProtected;<br />只读属性DRMMetadataInfolistMetadataReadInfos;<br />属性ProfileList用户档案;<br />只读属性用户档案selectedProfile;<br /> <br />只读属性boolean trickPlaySupported;<br />只读属性FloatArray availablyPlaybackRates;<br />只读属性floatPlaybackRate;&lt;a111/&gt;2/&gt; <br />只读属性MediaPlayer mediaPlayer;<br />只读属性MediaPlayerItemConfig;<br /> };<br /><br /></p> </td> 
   <td><p>interface MediaPlayerItem {<br />只读属性MediaResource;<br />只读属性long resourceId;<br />只读属性boolean live;<br /> <br />只读属性boolean hasAlternateAudio;<br />只读属性AudioTrackst audioTracks;<br />属性audioTrack selectedAudioTrack;<br /> <br /> <br />只读属性boolean hasClosedCaptions;<br />只读属性ClosedCaptionsTrackList ccTracks;<br />属性ClosedCtRACK;<br />a13/&gt; <br /> <br /> <br />只读属性boolean hasTimedMetadata;<br />只读属性TimedMetadataList timedMetadata;<br />只读属性boolean dynamic;<br /> <br />只读属性boolean isProtected;<br />只读属性DRMMetadataInfolistMetadataReadInfos;<br />属性ProfileList用户档案符；<br /> <br /> <br />只读属性boolean trickPlaySupported;<br />只读属性Int32Array availablePlaybackRates;<br /> <br />只读属性StringList adTags;<br />13/&gt;只读属性MediaPlayer mediaPlayer;<br /> <br /> };<br /></p> </td> 
  </tr> 
 </tbody> 
</table>

### 音轨／音轨／隐藏字幕音轨{#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface Track<br /> {<br />只读属性DomString name;<br />只读属性DomString语言；<br />只读属性布尔默认值；<br />只读属性布尔自动选择；<br /> }; </p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
  <tr> 
   <td><p>接口AudioTrack:Track<br /> {<br />只读属性DomString名称；//FromTrack<br />只读属性DomString语言；//FromTrack<br />只读属性布尔默认值；//从Track<br />只读属性boolean autoSelect;//FromTrack<br /> <br />只读属性unsigned int pid;<br /> };</p> </td> 
   <td><p>interfaceAudioTrack<br /> {<br />只读属性DomString name;<br />只读属性DomString语言；<br />只读属性布尔默认值；<br />只读属性布尔自动选择；<br />只读属性布尔值强制；<br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0没有更改</td> 
   <td><p>interface AudioTrackList<br /> {<br />只读属性未签名长度；<br /> getter AudioTrack（未签名长索引）;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>接口ClosedCaptionsTrack:Track<br /> {<br />只读属性DomString名称；//FromTrack<br />只读属性DomString语言；//FromTrack<br />只读属性布尔默认值；// FromTrack<br />只读属性boolean autoSelect;// FromTrack<br /> <br /> <br /> &lt;a7/&gt;未签名的短服务= 0;<br />未签名的短服务SERVICE_708_CAPTIONS = 1;<br />未签名的短服务_WEB_VTT_CAPTIONS = 2;<br />只读属性unsigned short serviceType;<br />只读属性boolean forced;<br /> };</p> </td> 
   <td><p>接口ClosedCaptionsTrack<br /> {<br />只读属性DomString name;<br />只读属性DomString语言；<br />只读属性布尔默认值；<br /> <br /> <br />只读属性布尔值active;<br /> <br /> <br /><br /> <br /> };<br /></p> </td> 
  </tr> 
  <tr> 
   <td>2.0没有更改</td> 
   <td><p>接口ClosedCaptionsTrackList<br /> {<br />只读属性未签名长度；<br /> getter ClosedCaptionsTrack（未签名长索引）;<br /> };</p> </td> 
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
   <td><p>接口用户档案<br /> {<br /> readonly attribute unsigned int width;<br /> readonly attribute unsigned int height;<br /> readonly attribute unsigned int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList:2.0没有更改</td> 
   <td><p>接口ProfileList<br /> {<br />只读属性未签名长度；<br /> getter用户档案（未签名长索引）;<br /> };</p> </td> 
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
   <td><p>interface DRMMetadataInfo<br /> { <br />只读属性DRMMetadata;<br />只读属性long prefetchTimestamp;<br />只读属性TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>:2.0没有更改</td> 
   <td><p>接口DRMMetadataInfoList<br /> {<br />只读属性未签名长度；<br /> getter DRMMetadataInfo(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 将C++错误映射到不同语言的异常{#mapping-c-errors-to-exceptions-in-different-languages}

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

## 2.0 {#utility-and-helper-api-element-changes-for}的实用程序和帮助程序API元素更改

这些表比较了JavaScript TVSDK的实用程序和帮助程序API元素在版本1.3和2.0之间。

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
   <td><p>接口版本<br /> {<br />只读属性DomString版本；<br />只读属性DomString描述；<br />只读属性DomString主题；<br />只读属性DomString次要；<br />只读属性DomString修订版；<br />只读属性DomString apiversion;<br /> };</p> </td> 
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
   <td><p>interfaceTimeRange<br /> {<br />只读属性未签名的长开始；<br />只读属性未签名的长结尾；<br />只读属性未签名的长持续时间；<br /> };</p> </td> 
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
   <td><p>接口QOSProvider<br /> {<br /> void attachMediaPlayer(MediaPlayer);<br /> void detachMediaPlayer();<br /> <br />只读属性DeviceInformation deviceInformation;<br />只读属性PlaybackInformation;<br />};</p> </td> 
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
   <td><p>接口DeviceInformation<br /> {<br />只读属性DomString os;<br /> <br /> <br /> <br />只读属性DomString id;<br />只读属性int densityDPI;<br />只读属性int heightPixels;<br />只读属性widites widthWidPes;<br />只读属性boolean seekToKeyFrame;<br /> };</p> </td> 
   <td><p>interfaceDeviceInformation<br /> {<br />只读属性DomString os;<br />只读属性int sdk;<br />只读属性DomString模型；<br />只读属性DomString制造商；<br />只读属性DomString id;<br />只读属性intDPI;7/&gt;只读属性int heightPixels;<br />只读属性int widthPixels;<br /> <br /> };<br /></p> </td> 
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
   <td><p>接口LoadInfo<br /> {<br />只读属性DomString url;<br />只读属性int size;<br />只读属性多次downloadDuration;<br />只读属性int periodIndex;<br />只读属性多次mediaDuration;<br />只读属性短TRACK_TYPEfragment;<br />只读属性短TRACK_TYPE_TRACK;<br />只读属性短TRACK_TYPE_MANIFEST;<br />只读属性短类型；<br />只读属性DomString trackName;<br />只读属性DomString trackType;&lt;ackAckAckAtype;int trackIndex;<br /> }中的readonly属性；<br /></p> </td> 
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
   <td><p>接口视图<br /> {<br /> readonly attribute unsigned short x;<br /> readonly attribute unsigned short y;<br /> readonly attribute unsigned short width;<br /> <br /> void setSize(unsigned short x, short y);<br /> }<br /><br /></p> </td> 
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
   <td><p>interfacePlaybackInformation<br /> {<br />只读属性多次时间ToFirstByte;<br />只读属性多次时间ToLoad;<br />只读属性多次时间ToStart;<br />只读属性多次时间ToFail;<br />只读属性int totalSeconds已播放；<br />只读属性int totalSecondsSpent;<br />只读属性多次frameRate;<br />只读属性int droppedFrameCount;<br />只读属性int envericedBandwidth;<br />只读属性int bitrate;<br />只读属性多次bute bittime;<br /> readonly attribute int bufferLength;<br /> readonly attribute int emptyBufferCount;<br /> readonly attribute bufferingTime;<br /> };</p> </td> 
   <td><p>interfacePlaybackInformation<br /> {<br />只读属性多次时间ToFirstByte;<br />只读属性多次时间ToLoad;<br />只读属性多次时间ToStart;<br />只读属性多次时间ToFail;<br />只读属性int totalSeconds已播放；<br />只读属性int totalSecondsSpent;<br />只读属性多次frameRate;<br />只读属性int droppedFrameCount;<br /> <br />只读属性int bitrate;<br />只读属性多次readTime;<br />仅属性int bufferLength;<br /> readonly属性int emptyBufferCount;<br /> readonly属性bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 帮助资源{#helpful-resources}

* 请参阅[Adobe Primetime学习和支持](https://helpx.adobe.com/support/primetime.html)页面上的完整帮助文档。
