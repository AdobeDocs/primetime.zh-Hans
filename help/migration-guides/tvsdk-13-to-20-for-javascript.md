---
title: TVSDK转换——对于JavaScript,1.3到2.0
seo-title: TVSDK转换——对于JavaScript,1.3到2.0
description: 许多方法签名和API元素名称在2.0中已更改。查看这些表以查看所有API更改详细信息。
seo-description: 许多方法签名和API元素名称在2.0中已更改。查看这些表以查看所有API更改详细信息。
uuid: d2d1742d-c90c-43f5-94fc-8c4a57cb8ed4
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
discoiquuid: c732f54d-116c-43f3-bec4-5e71af208426
translation-type: tm+mt
source-git-commit: e644e8497e118e2d03e72bef727c4ce1455d68d6

---


# TVSDK转换——对于JavaScript,1.3到2.0 {#tvsdk-conversion-to-for-javascript}

许多方法签名和API元素名称在2.0中已更改。查看这些表以查看所有API更改详细信息。

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

## 针对2.0的广告工作流程API元素更改 {#advertising-workflow-api-element-changes-for}

这些表比较了JavaScript TVSDK的广告工作流程API元素（版本1.3和2.0）。

本主题中的表：

* TimedMetadata
* AdSignalingMode
* 广告元数据
* CustomRangeMetadata
* ReplaceTimeRange
* 位置
* 机会
* 保留
* 时间轴／时间轴项／时间轴标记
* AdBreak
* 广告/ AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset
* AdBreakTimelineItem / AdTimelineItem
* AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector
* TimelineOperation
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
   <td><p> <strong>TimedMetadata</strong>:interfaceTimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0;const <br /> unsigned short METADATA_TYPE_ID3 = 1 ; <br /> readonly属性unsigned short type; <br /> readonly属性长时间；<br /> readonly属性DomString id;<br /> readonly属性DomString名称；<br /> readonly属性DomString内容；只读 <br /> 属性对象元数据；<br /> }; </p> </td> 
   <td><p>interfaceTimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0;<br /> const unsigned short metadata_TYPE_ID3 = 1 ;<br /> readonly属性unsigned short metadataType;<br /> 只读属性时间较长；<br /> 只读属性long id;<br /> readonly属性DomString名称；<br /> 只读 <br /> 属性对象元数据；<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>:（2.0没有更改）</td> 
   <td><p>interface TimedMetadataList {<br /> readonly属性未签名长；<br /> getterTimedMetadata(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### AdSignalingMode {#adsignalingmode}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口AdSignalingMode { <br /> const unsigned short MODE_DEFAULT, <br /> const unsigned short MODE_MANIFEST_CASES, <br /> const unsigned short MODE_SERVER_MAP, <br /> const unsigned short MODE_CUSTOM_RANGES <br /> };</p> </td> 
   <td>这将替换MetadataKeys::MANIFEST_CEASS键。</td> 
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
   <td><p>接口AdvertisingMetadata {属 <br /> 性AdSigningMode模式；属 <br /> 性AdBreakWatchedPolicy adBreakAsWatched;属 <br /> 性boolean livePreroll;属性 <br /> boolean delayAdLoading; <br /> };</p> </td> 
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
   <td><p>接口CustomRangeMetadata { <br /> const unsigned short TYPE_MARK_RANGE;const <br /> unsigned short TYPE_DELETE_RANGE;const <br /> unsigned short TYPE_REPLACE_RANGE;无 <br /> 符号短类型属性；属 <br /> 性boolean adjustSeekPosition;属 <br /> 性TimeRangeList timeRangeList; <br /> };</p> </td> 
   <td>（2.0的新增功能）</td> 
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
   <td><p>interface ReplaceTimeRange { <br /> attribute unsigned long begin; <br /> readonly属性unsigned long end;无 <br /> 符号长持续时间；unsigned <br /> long replaceDuration属性； <br /> };</p> </td> 
   <td>（2.0的新增功能）</td> 
  </tr> 
 </tbody> 
</table>

### 位置 {#placement}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>界面放置{ <br /> const unsigned short TYPE_MID_ROLL;const <br /> unsigned short TYPE_PRE_ROLL;const <br /> unsigned short TYPE_POST_ROLL;const <br /> unsigned short TYPE_SERVER_MAP;const <br /> unsigned short TYPE_CUSTOM_RANGE;<br /> 只读属性未签名短类型； <br /> readonly属性长时间； <br /> readonly属性长持续时间；const unsigned <br /> short MODE_DEFAULT;const unsigned <br /> short MODE_INSERT;const unsigned <br /> short MODE_REPLACE;const unsigned <br /> short MODE_DELETE; <br /> const unsigned short MODE_MARK;const <br /> unsigned short MODE_FREE_REPLACE;只读 <br /> 属性未签名短模式；只 <br /> 读属性TimeRange范围； <br /> };</p> </td> 
   <td>（2.0的新增功能）</td> 
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
   <td><p>interface Opportunity { <br /> readonly属性DomString id;只读 <br /> 属性放置；只读 <br /> 属性对象设置；只 <br /> 读属性Object customParameters; <br /> }; </p> </td> 
   <td>（2.0的新增功能）</td> 
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
   <td><p>interface Reservation { <br /> readonly属性TimeRange范围； <br /> readonly属性长持久； <br /> }; </p> </td> 
   <td> （2.0的新增功能）</td> 
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
   <td><p><strong>时间轴</strong>:interface Timeline <br /> { readonly属性TimelineMarkerList timelineMarkers;只 <br /> 读属性TimelineItemList timelineItems; <br /> double convertToLocalTime(double time); <br /> double convertToVirtualTime(double time); <br /> };</p> </td> 
   <td><p>接口时间线<br /> {readonly属性TimelineMarkerList timelineMarkers;<br /><br /> <br /><br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>TimelineItem</strong>:interface TimelineItem:<br /> TimelineMarker {<br /> readonly属性long id;只读 <br /> 属性TimeRange virtualRange;只 <br /> 读属性TimeRange localRange; <br /> readonly属性boolean watched;只 <br /> 读属性布尔临时； <br /> }; </p> </td> 
   <td>（2.0的新增功能）</td> 
  </tr> 
  <tr> 
   <td><strong>TimelineMarker</strong>:（2.0没有更改）</td> 
   <td><p>interface TimelineMarker {<br /> readonly属性两次；<br /> 只读属性双持续时间；<br /> };</p> </td> 
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
   <td><p>interface AdBreak {<br /> <br /> readonly属 <br /><br /> 性重复持续时间；<br /> 只读属性AdList广告；<br /> 只 <br /> 读 <br /> 属性AdInsertionType insertionType;<br /> }; </p> </td> 
   <td><p>interface AdBreak {<br /> readonly属性两次；<br /> readonly属性double replaceDuration;<br /><br /> readonly属性双持续时间；<br /> 只读属性AdList adList;<br /> 只 <br /> 读属性DomString数据；<br /><br /> }; </p> </td> 
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
   <td><p> <strong>广告</strong>:interface Ad {readonly<br /> attribute AdAsset primaryAsset;<br /> readonly属性AdAssetList companionAssets;<br /><br /> readonly属性双持续时间；<br /> readonly属性DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINER = 1;<br /> 只 <br /> 读属性unsigned short adType;<br /> readonly属性AdInsertionType adInsertionType; <br /> 只 <br /> 读属性布尔可点击；只 <br /> 读属性boolean isCustomAdMarker;<br /> }; </p> </td> 
   <td><p>interface Ad {readonly<br /> attribute AdAsset primaryAsset;<br /> readonly属性AdAssetList companionAssets;<br /><br /> readonly属性双持续时间；<br /> readonly属性DomString id;<br /> const unsigned short ADTYPE_LINEAR = 0 ;<br /> const unsigned short ADTYPE_NONLINER = 1;<br /><br /> readonly属性unsigned short type;<br /> readonly属性AdInsertionType insertionType;只读 <br /> 属性对象跟踪器；<br /><br /> <br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>:（2.0没有更改）</td> 
   <td><p>interface AdAsset {<br /> readonly属性DomString id;<br /> 只读属性双持续时间；<br /> 只读属性MediaResource资源；<br /> 只读属性AdClick adClick;<br /> 只读属性对象元数据；<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>:（2.0没有更改）</td> 
   <td><p>interface AdClick {<br /> readonly属性DomString id;<br /> readonly属性DomString标题；<br /> readonly属性DomString url;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdList</strong>:（2.0没有更改）</td> 
   <td><p>interface AdList {<br /> readeronly属性未签名长；<br /> getter Ad（未签名长索引）;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>:（2.0没有更改）</td> 
   <td><p>interface AdAssetList {<br /> readonly属性未签名长；<br /> getter AdAsset（未签名长索引）;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>:接口AdBannerAsset:AdAsset<br /> {readonly<br /> attribute int width;<br /> readonly属性int height;<br /> readonly属性DomString staticUrl;<br /> readonly属性DomString height;<br /> readonly属性DomString width;<br /> };</p> </td> 
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
   <td><p> <strong>AdBreakTimelineItem</strong>:interface AdBreakTimelineItem:TimelineItem { <br /> readonly属性AdBreak adBreak;只 <br /> 读属性AdTimelineItemList项； <br /> }; </p> </td> 
   <td> （2.0的新增功能）</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>:接口AdTimelineItem:TimelineItem { <br /> readonly属性AdBreak adBreak;只 <br /> 读属性广告； <br /> }; </p> </td> 
   <td> （2.0的新增功能）</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>:interface AdBreakTimelineItemList { <br /> readonly属性未签名长；getterAdBreakTimelineItem(unsigned long index); <br /><br /> };</p> </td> 
   <td> （2.0的新增功能）</td> 
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
   <td><p>interface AdBreakPolicy {<br /> readonly属性short AD_BREAK_POLICY_SKIP;<br /> readonly属性short AD_BREAK_POLICY_PLAY;<br /> readonly属性short AD_BREAK_POLICY_REMOVE;<br /> readonly属性short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> };</p> </td> 
   <td><p> interface AdPolicyConstants {<br /> readonly属性short AD_BREAK_POLICY_SKIP;<br /> readonly属性short AD_BREAK_POLICY_PLAY;<br /> readonly属性short AD_BREAK_POLICY_REMOVE;<br /> readonly属性short AD_BREAK_POLICY_REMOVE_AFTER_PLAY;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> interface AdBreakWatchedPolicy<br /> {readonly属性short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> readonly属性short AD_BREAK_AS_WATCHED_ON_END;<br /> readonly属性short AD_BREAK_AS_WATCHED_NEVER;<br /> }; </p> </td> 
   <td><p> ...<br /> readonly属性short AD_BREAK_AS_WATCHED_ON_BEGIN;<br /> readonly属性short AD_BREAK_AS_WATCHED_ON_END;<br /> readonly属性short AD_BREAK_AS_WATCHED_NEVER;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicy {<br /> readonly属性short AD_POLICY_PLAY;<br /> 只读属性short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> 只读属性short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;readonly属性short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> AD_ <br /> POLICY_SKIP_AD_BREAK的只读属性；<br /> };</p> </td> 
   <td><p> ...AD_ <br /> POLICY_PLAY的只读属性；<br /> 只读属性short AD_POLICY_PLAY_FROM_AD_BEGIN;<br /> 只读属性short AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN;<br /> readonly属性short AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK;<br /> readonly属性short AD_POLICY_SKIP_AD_BREAK;<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyMode {<br /> readonly属性short AD_POLICY_MODE_PLAY;<br /> readonly属性short AD_POLICY_MODE_SEEK;<br /> readonly属性short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
   <td><p> ...<br /> 只读属性short AD_POLICY_MODE_PLAY;<br /> readonly属性short AD_POLICY_MODE_SEEK;<br /> readonly属性short AD_POLICY_MODE_TRICKPLAY;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicyInfo {readonly<br /> 属性AdBreakTimelineItemList <br /> adBreakTimelineItems;<br /> readonly属性AdTimelineItem adTimelineItem;<br /> readonly属性double currentTime;<br /> readonly属性double seekToTime;<br /> 只读属性双速率；<br /> 只读属性短模式；//AdPolicyMode<br /> };</p> </td> 
   <td><p>interface AdPolicyInfo {readonly<br /> 属性AdBreakPlacementList <br /> adBreakApplications;<br /> 只读属性广告；<br /> readonly属性double currentTime;<br /> readonly属性double seekToTime;<br /> 只读属性双速率；<br /> 只读属性短模式；//AdPolicyMode<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */属性<br /> 对象selectPolicyForAdBreakCallbackFunc;<br /> /**<br /> * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */属性<br /> 对象selectAdBreaksToPlayCallbackFunc;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */属性<br /> 对象selectPolicyForSeekIntoAdCallbackFunc; <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */属性<br /> 对象selectWatchedPolicyForAdBreakCallbackFunc;<br /> };</p> </td> 
   <td><p>interface AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */属性<br /> 对象selectPolicyForAdBreakFuncCallback;<br /> /**<br /> * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo);<br /> */属性<br /> 对象selectAdBreaksToPlayCallback;<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo);<br /> */属性<br /> 对象selectPolicyForSeekIntoAdCallback; <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo);<br /> */属性<br /> 对象selectWatchedPolicyForAdBreakCallback;<br /> };</p> </td> 
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
   <td><p>interface TimelineOperation { <br /> readonly属性位置； <br /> };</p> </td> 
   <td> （2.0的新增功能）</td> 
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
   <td><p>接口AdBreakPlacement:TimelineOperation {<br /> readonly属性AdBreak adBreak;<br /> 只读属性放置；//从TimelineOperation<br /> readonly属性两次；<br /> 只读属性双持续时间；<br /> };</p> </td> 
   <td><p>interface AdBreakPlacement {readonly<br /> 属性AdBreak adBreak;<br /> 只读属性放置；<br /> 只读属性重复时间；<br /> 只读属性双持续时间；<br /> };</p> </td> 
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
   <td><p>接口AuditudeSettings:AdvertisingMetadata { <br /> attribute DomString zoneId;属 <br /> 性DomString mediaId;属 <br /> 性DomString defaultMediaId ;属 <br /> 性DomString域；属 <br /> 性对象targettingInfo;属性 <br /> 对象customParameters;属 <br /> 性Boolean creativePackaingEnabled ;<br /> 属性Boolean showStaticBanners ;<br /> };</p> </td> 
   <td>功能由MetadataKeys::AUDITUDE_METADATA_KEY提供。</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的自定义API元素更改 {#customization-api-element-changes-for}

这些表比较了JavaScript TVSDK的自定义API元素（版本1.3和2.0）。

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
   <td><p>interface MediaPlayerItemConfig {<br /> attribute ContentFactory adFactory;<br /> 属性StringList subscribeTags;<br /> 属 <br /> 性StringList adTags;<br /> 属 <br /><br /> 性AdSigningMode adSigningMode;<br /> 属性CustomRangeMetadata customRangeMetadata;<br /> 属性NetworkConfiguration networkConfiguration;<br /> 属性Advertising元数据advertising元数据；<br /> 属性Boolean useHardwareDecoder;<br /> };</p> </td> 
   <td><p>interface MediaPlayerConfig {<br /> StringList <br /> adTags属 <br /><br /> 性；<br /> 属性StringList subscribedTags;<br /> 属性MediaPlayerClientFactory clientFactory;<br /><br /><br /> <br /><br /><br /> };</p> </td> 
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
   <td><p>interfaceContentFactory {<br /> /*<br /> * AdPolicySelector retreiveAdPolicySelector(<br /> * MediaPlayerItem项);<br /> */<br /> attribute object retrieveAdPolicySelectorCallbackFunc;<br /> };</p> </td> 
   <td><p>interface MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem项);<br /> */<br /> attribute object retrieveAdPolicySelectorFunc;<br /> };</p> </td> 
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
   <td><p>interface NetworkConfiguration<br /> {<br /> attribute boolean forceNativeNetworking;<br /> 属性boolean useRedirectedUrl;<br /> 属性对象cookieHeader;<br /> 属性boolean readSetCookieHeader;<br /> attribute int masterUpdateInterval;属性 <br /> boolean useCookieHeaderForAllRequests;<br /> 属性int readLimit;<br /> };</p> </td> 
   <td>在1.3中，其中一些功能是由MetadataKeys提供的</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的DRM API元素更改 {#drm-api-element-changes-for}

这些表比较了JavaScript TVSDK的DRM API元素在版本1.3和2.0之间。

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
   <td>应用程序需要调用AdobePSDK.initiateDRMWorkflow以启动DRM工作流。 没有此呼叫，DRM视频将无法播放。<p>interface AdobePSDK<br /> {<br /> void initiateDRMWorkFlow(<br /> DomString appStoratePath, <br /> DomString publisherId, <br /> DomString appId, <br /> DomString appVersion, <br /> boolean privacyModeOn);<br /> };</p> </td> 
   <td>初始化是在内部完成的，无需显式调用。</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| 2.0 API | 1.3 API |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| 2.0没有更改。 | enum DRMAcquireLicenseSettings <br><br> {const unsigned int FORCE_REFRESH = 0;<br> const unsigned int LOCAL_ONLY = 1;<br> const unsigned int ALLOW_SERVER = 2;<br> }; |
| **DRMAuthenticationMethod** |  |
| 2.0没有更改。 | enum DRMAuthenticationMethod <br><br> {const unsigned int UNKNOWN = 0;<br> const unsigned int ANONYMOUS = 1;<br> const unsigned int USERNAME_AND_PASSWORD = 2;<br> } |

### DRMMetadata {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0没有更改。</td> 
   <td><p>interface DRMMetadata<br /> {readonly<br /> 属性DomString serverUrl;<br /> readonly属性DomString licenseId;<br /> readonly属性DRMPolicyArray策略； <br /> };</p> </td> 
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
   <td><p>interface DRMPlaybackTimeWindow {<br /> readonly属性int periodInSeconds;<br /> readonly属性int startDate;<br /> endDate的只读属性；<br /> };</p> </td> 
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
   <td><p>interface DRMLicense {<br /> readonly属性Uint8Array字节；<br /> readonly属性Date licenseStartDate;<br /> readonly属性Date licenseEndDate;<br /> readonly属性Date offlineStorageStartDate;<br /> readonly属性Date offlineStorageEndDate;只 <br /> 读属性DomString serverUrl;<br /> readonly属性DomString licenseID;<br /> readonly属性DomString policyID;<br /> readonly属性DRMPlaybackTimeWindow playbackTimeWindow;<br /> readonly属性Object customProperties;<br /> }; </p> </td> 
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
   <td><p>interface DRMLicenseDomain {readonly<br /> 属性DomString authenticationDomain;<br /> readonly属性DRMAuthenticationMethod authenticationMethod;只 <br /> 读属性DomString serverUrl;<br /> };</p> </td> 
   <td><p>interface DRMLicenseDomain {readonly<br /> 属性DomString authDomain;<br /> readonly属性DRMAuthenticationMethod authMethod;只 <br /> 读属性DomString serverURL;<br /> };</p> </td> 
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
   <td><p>interface DRMPolicy<br /> {readonly<br /> 属性DomString authenticationDomain;<br /> readonly属性DRMAuthenticationMethod authenticationMethod;<br /> 只 <br /> 读属性DomString displayName;<br /> readonly属性DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
   <td><p>interface DRMPolicy<br /> {readonly<br /> 属性DomString authDomain;<br /> readonly属性DRMAuthenticationMethod authMethod;<br /> readonly属性DomString dispName;<br /> readonly属性DRMLicenseDomain licenseDomain;<br /> };</p> </td> 
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
   <td><p>接口DRMManager:EventTarget {<br /> void accuripeLicense(DRMMetadata元数据， <br /> DRMAcquireLicenseSettings设置， <br /> DRMAquireLicenseListener);<br /> void acquirePreviewLicense(DRMMetadata元数据， <br /> DRMAquireLicenserListener);<br /> void authenticate(DRMMetadata元数据， <br /> DomString url,<br /> DomString &amp;authenticationDomain, <br /> DomString用户， <br /> DomString密码， <br /> DRMAuthenticateListener);<br /><br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array数组， DRMErrorListener);<br /> void initialize(DRMOperationCompleteListener);<br /> 属性long maxOperationTime;<br /><br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> DRMOperationCompleteListener);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> DRMOperationCompleteListener);<br /> void <br /> resetDRM(DRMOperationCompleteListener);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID, <br /> DomString policyID, boolean commitImmediated, <br /><br /> DRMReturnLicenseListener);<br /> void setAuthenticationToken(<br /> DRMMetadata元数据， <br /> DomString authenticationDomain, <br /> Uint8Array令牌， <br /> DRMOperationCompleteListener);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> DRMOperationCompleteListener);<br /> };</p> </td> 
   <td><p>接口DRMManager:EventTarget {<br /> void acquireLicense(DRMMetadata元数据， <br /> DRMAcquireLicenseSettings设置， <br /> EventContext eventContext);<br /> void acquirePreviewLicense(DRMMetadata元数据， <br /> EventContext eventContext);<br /> void authenticate(DRMMetadata元数据， <br /> DomString url,<br /> DomString &amp;authenticationDomain, <br /> DomString用户， <br /> DomString密码， <br /> EventContext eventContext);<br /><br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array数组， EventContext eventContext);<br /> void initialize(EventContext eventContext);<br /> 属性long maxOperationTime;<br /><br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> boolean forceRefresh, <br /> EventContext eventContext);<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain, <br /> EventContext eventContext);<br /><br /> void resetDRM(EventContext eventContext);<br /> void returnLicense(DomString serverURL, <br /> DomString licenseID,<br /> DomString policyID, <br /> boolean commitImmetiled,<br /> EventContext eventContext);<br /> void setAuthenticationToken(<br /> DRMMetadata元数据， <br /> DomString authenticationDomain, <br /> Uint8Array令牌， <br /> EventContext eventContext);<br /> void storeLicenseBytes(Uint8Array licenseBytes, <br /> EventContext eventContext);<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMErrorListener:public <br /> psdkutils::PSDKInterfaceWithUserData {<br /> public:<br /> virtual void onDRMError(uint32_t major, <br /> uint32_t minor, <br /> const psdkutils:PSDKString&amp; errorString, const <br /> psdkutils::PSDKString&amp; errorServerUrl)= 0;<br /><br /> 受保护：<br /> virtual ~DRMErrorListener(){}<br /> }</p> </td> 
   <td>事件／界面／说明 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>在DRMManger的异步方法之一期间发生错误时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMOperationCompleteListener:公 <br /> 共DRMErrorListener {<br /> public:<br /> virtual void onDRMOperationComplete()= 0;<br /><br /> 受保护：<br /> virtual ~DRMOperationCompleteListener(){}<br /> };</p> </td> 
   <td>事件／界面／说明 
    <ul> 
     <li>kEventDRMInitializationComplete<p>/ PSDKEvent</p> <p>当DRM初始化完成时。</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>当joinLicenseDomain()操作成功完成时。</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>leaveLicenseDomain()操作成功完成时。</p> </li> 
     <li>kEventDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>当resetDRM()操作成功完成时。</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEvent</p> <p>当setAuthenticationTokenSet()操作成功完成时。</p> </li> 
     <li>kEventDRMLicenseStored<p>/ PSDKEvent</p> <p>当storeLicenseBytes()操作成功完成时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMAuthenticateListener:公 <br /> 共DRMErrorListener {<br /> public:<br /> virtual void onAuthenticationComplete(<br /> psdkutils::PSDKImmutableByteArray* <br /> authenticationToken)= 0;<br /><br /> 受保护：<br /> virtual ~DRMAuthenticateListener(){}<br /> }</p> </td> 
   <td>事件／界面／说明 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>当DRMManager::authenticate方法调用成功时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMAquireLicenseListener:公 <br /> 共DRMErrorListener {<br /> public:<br /> virtual void onLicenseAppired(const DRMLicense*)= 0;<br /><br /> 受保护：<br /> virtual ~DRMAquireLicenseListener(){}<br /> };</p> </td> 
   <td>事件／界面／说明 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>当DRMManager::acquirePreviewLicense方法调用成功时。</p> </li> 
     <li>kEventDRMLicenseApided<p>/ DRMLicenseAcquiredEvent</p> <p>当DRMManager::acquireLicense方法调用成功时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMReturnLicenseListener:公 <br /> 共DRMErrorListener {<br /> public:<br /> virtual void onLicenseReturnComplete(uint32_t numReturned)= 0;<br /><br /> 受保护：<br /> virtual ~DRMReturnLicenseListener(){}<br /> };</p> </td> 
   <td>事件／界面／说明 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>当DRMManager::returnLicense方法调用成功时。</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 2.0的通用回放API元素更改 {#generic-playback-api-element-changes-for}

这些表比较JavaScript TVSDK 1.3和2.0之间的通用播放API元素。

本主题中的表：

* MediaResource
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
   <td><p>interface MediaResource {<br /> attribute DomString url;无 <br /> 符号短类型属性；<br /> 属性对象元数据；<br /> const unsigned short TYPE_HLS;<br /> const unsigned short TYPE_HDS;<br /> const unsigned short TYPE_DASH;<br /> const unsigned short TYPE_CUSTOM;<br /> const unsigned short TYPE_UNKNOWN;<br /> };</p> </td> 
   <td><p>interface MediaResource {<br /> attribute DomString url;<br /> 属性DomString类型；<br /> 属性对象元数据；<br /><br /><br /> <br /><br /><br /> };</p> </td> 
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
   <td><p>接口MediaPlayer:EventTarget<br /> {<br /> void prepareToPlay（双位置）;<br /> void play();<br /> void pause();<br /> void seek(double position);<br /> void seekToLocal（双位置）;<br /> void reset();<br /> void release();<br /> void replaceCurrentItem（MediaPlayerItem项）;<br /> void replaceCurrentResource(MediaResource rsource, <br /> MediaPlayerItemConfig); <br /> void suspend();<br /> void restore();<br /> void notifyClick();<br /> 只读 <br /> 属性TimeRange playbackRange;<br /> readonly属性TimeRange seekableRange;<br /> readonly属性double currentTime;<br /> readonly属性double localTime;<br /> readonly属性TimeRange bufferedRange;<br /> readonly属性DRMManager drmManager;<br /> readonly属性MediaPlayerItem currentItem;<br /><br /> // PlayerStatus<br /><br /><br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /><br /> readonly属性未签名短状态；<br /><br /> 属性未签名短卷；<br /> 属性ABRControlParameters abrControlParameters;<br /> 属性BufferControlParameters bufferControlParameters;<br /> const unsigned <br /> short VISIBLE;//对于CC可见性<br /> ，无符号短不可见；//对于CC visibility<br /> attribute unsigned short ccVisibility;<br /> 属性TextFormat ccStyle;<br /> readonly属性PlaybackMetrics playbackMetrics;<br /><br /> 属性双倍率；<br /> 属性MediaPlayerView视图；<br /> 只读属性时间线时间线；<br /> 属性double currentTimeUpdateInterval; <br /> //设置2.0<br /> }不支持；</p> </td> 
   <td><p>接口MediaPlayer:EventTarget<br /> {<br /> void prepareToPlay(int position);<br /> void play();<br /> void pause();<br /> void seek(int position);<br /> void seekToLocalTime(int position);<br /> void reset();<br /> void release();<br /> void replaceCurrentItem（MediaResource源）;<br /><br /><br /><br /><br /><br /><br /> TimeRange playbackRange的只读属性；<br /> readonly属性TimeRange seekableRange;<br /> readonly属性double currentTime;<br /> readonly属性double localTime;<br /> readonly属性TimeRange bufferedRange;<br /> readonly属性DRMManager drmManager;<br /> readonly属性MediaPlayerItem currentItem;<br /><br /> // PlayerState<br /> const unsigned short PLAYER_STATE_IDLE;<br /> const unsigned short PLAYER_STATE_INITIALIZING;<br /> const unsigned short PLAYER_STATE_INITIALIZED;<br /> const unsigned short PLAYER_STATE_PREPARING;<br /> const unsigned short PLAYER_STATE_PREPARED;<br /> const unsigned short PLAYER_STATE_PLAYING;<br /> const unsigned short PLAYER_STATE_PAUSED;<br /> const unsigned short PLAYER_STATE_SEEKING;<br /> const unsigned short PLAYER_STATE_COMPLETE;<br /> const unsigned short PLAYER_STATE_ERROR;<br /> const unsigned short PLAYER_STATE_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> 只读属性未签名短状态；<br /><br /> 属性未签名短卷；<br /> 属性ABRControlParameters abrControlParameters;<br /> 属性BufferControlParameters bufferControlParameters;<br /> 只读 <br /> 未签名的短VISIBLE;//对于CC可见性<br /> ，只读未签名短不可见；//对于CC visibility<br /> attribute unsigned short ccVisibility;<br /> 属性TextFormat ccStyle;<br /> readonly属性PlaybackMetrics playbackMetrics;<br /> 属性MediaPlayerConfig mediaPlayerConfig;<br /> 属性双倍率；<br /> 属性MediaPlayerView视图；<br /> 只读属性时间线时间线；<br /><br /> <br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface MediaPlayerStatus<br /> {<br /><br /> // PlayerStatus控制未签名短PLAYER_STATUS_IDLE;<br /> const unsigned short PLAYER_STATUS_INITIALIZING;<br /> const unsigned short PLAYER_STATUS_INITIALIZED;<br /> const unsigned short PLAYER_STATUS_PREPARING;<br /> const unsigned short PLAYER_STATUS_PREPARED;<br /> const unsigned short PLAYER_STATUS_PLAYING;<br /> const unsigned short PLAYER_STATUS_PAUSED;<br /> const unsigned short PLAYER_STATUS_SEEKING;<br /> const unsigned short PLAYER_STATUS_COMPLETE;<br /> const unsigned short PLAYER_STATUS_ERROR;<br /> const unsigned short PLAYER_STATUS_RELEASED;<br /> const unsigned short PLAYER_STATUS_SUSPENDED;<br /> };</p> </td> 
   <td>（2.0的新增功能）</td> 
  </tr> 
 </tbody> 
</table>

#### MediaPlayer支持的事件 {#events-supported-by-mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>2.0活动名称</th> 
   <th>2.0界面</th> 
   <th> </th> 
   <th>1.3活动名称</th> 
   <th>1.3界面</th> 
  </tr> 
  <tr> 
   <td><p>（已为2.0删除）</p> </td> 
   <td> </td> 
   <td> </td> 
   <td>制备</td> 
   <td>活动</td> 
  </tr> 
  <tr> 
   <td><p>itemUpdated</p> <p>当媒体播放器项目更新时。</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>已更新</p> <p>媒体播放器成功更新媒体时。</p> </td> 
   <td>活动</td> 
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
   <td>活动</td> 
   <td> </td> 
   <td>TetmelineUpdated</td> 
   <td>活动</td> 
  </tr> 
  <tr> 
   <td>已在2.0中删除</td> 
   <td> </td> 
   <td> </td> 
   <td>playStart</td> 
   <td>活动</td> 
  </tr> 
  <tr> 
   <td>已删除2.0版本</td> 
   <td> </td> 
   <td> </td> 
   <td>playComplete</td> 
   <td>活动</td> 
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
   <td>进度</td> 
   <td>ProgressEvent</td> 
  </tr> 
  <tr> 
   <td>bufferingBegin</td> 
   <td>活动</td> 
   <td> </td> 
   <td>缓冲</td> 
   <td>活动</td> 
  </tr> 
  <tr> 
   <td>bufferingEnd</td> 
   <td>活动</td> 
   <td> </td> 
   <td>bufferComplete</td> 
   <td>活动</td> 
  </tr> 
  <tr> 
   <td>seekBegin</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td>seekStart</td> 
   <td>活动</td> 
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
   <td>reservationReceaded</td> 
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
   <td>adBreakKbipted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakKbipted</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adClicked<br /> When user clicks on an Ad.</td> 
   <td>AdClickedEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>配置文件更改<br /> 当播放配置文件发生更改时。</td> 
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
   <td>audioUpdated<br /> When a media player item is updated. 对于包含仅在播放时可检测的音轨的特定流，当有新的音轨可用时，将触发此事件。</td> 
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
   <td>master更新 <br /> 当媒体播放器项目更新时。 对于实时／线性流，客户端必须定期刷新媒体资源以检测新的可用内容。 发生这种情况时，某些媒体特性可能会发生变化。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRangeUpdated<br /> When a media player item is updated. 对于实时／线性流，客户端必须定期刷新媒体资源以检测新的可用内容。 发生这种情况时，某些媒体特性可能会发生变化。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>timedEvent<br /> Sent when timed events are generated.</td> 
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
   <td><p>interface ABRControlParameters<br /><br /> {const unsigned short ABR_POLICY_CONSERVAL = 0;<br /> const unsigned short ABR_POLICY_MEADE = 1;<br /> const unsigned short ABR_POLICY_AGGRESSIVE = 2;<br /> 属性unsigned <br /> short abrPolicy;<br /> attribute unsigned int initialBitRate;<br /> attribute unsigned int minBitRate;<br /> attribute unsigned int maxBitRate;<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE;<br /> const unsigned short DEFAULT_ABR_MIN_BITRATE;<br /> const unsigned short DEFAULT_ABR_MAX_BITRATE;<br /> const ABRPolicy DEFAULT_ABR_POLICY;<br /> };</p> </td> 
   <td><p>interface ABRControlParameters<br /><br /> {const unsigned short ABR_POLICY_CONSERVAL = 0;<br /> const unsigned short ABR_POLICY_MEADE = 1;<br /> const unsigned short ABR_POLICY_AGGRESSIVE = 2;<br /> 属性unsigned <br /> short abrPolicy;<br /> attribute unsigned int initialBitRate;<br /> attribute unsigned int minBitRate;<br /> attribute unsigned int maxBitRate;<br /><br /><br /> <br /><br /> };</p> </td> 
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
   <td><p>interface BufferControlParameters<br /> {<br /> attribute double initialBufferTime;<br /> 属性double playBufferTime;<br /> const double DEFAULT_INITIAL_BUFFER_TIME;<br /> const double DEFAULT_PLAY_BUFFER_TIME;<br /> };</p> </td> 
   <td><p>interface BufferControlParameters<br /> {<br /> attribute double initialBufferTime;<br /> 属性double playBufferTime;<br /><br /> <br /> };</p> </td> 
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
   <td><p>interfaceTextFormat<br /> {<br /><br /> // Color Const unsigned short COLOR_DEFAULT = 0 ;<br /> const unsigned short COLOR_BLACK = 1;<br /> const unsigned short COLOR_GRAY = 2;<br /> const unsigned short COLOR_WHITE = 3;<br /> const unsigned short COLOR_BRIGHT_WHITE = 4;<br /> const unsigned short COLOR_DARK_RED = 5;<br /> const unsigned short COLOR_RED = 6;<br /> const unsigned short COLOR_BRIGHT_RED = 7;<br /> const unsigned short COLOR_DARK_GREEN = 8;<br /> const unsigned short COLOR_GREEN = 9;<br /> const unsigned short COLOR_BRIGHT_GREEN = 10;<br /> const unsigned short COLOR_DARK_BLUE = 11;<br /> const unsigned short COLOR_BLUE = 12;<br /> const unsigned short COLOR_BRIGHT_BLUE = 13;<br /> const unsigned short COLOR_DARK_YELLOW = 14;<br /> const unsigned short COLOR_YELLOW = 15;<br /> const unsigned short COLOR_BRIGHT_YELLOW = 16;<br /> const unsigned short COLOR_DARK_MAGENTA = 17;<br /> const unsigned short COLOR_MAGENTA = 18;<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 19;<br /> const unsigned short COLOR_DARK_CYAN = 20;<br /> const unsigned short COLOR_CYAN = 21;<br /> const unsigned short COLOR_BRIGHT_CYAN = 22;<br /> 只读 <br /> 属性unsigned short fontColor;<br /> readonly属性unsigned short backgroundColor;<br /> readonly属性unsigned short fillColor;<br /> readonly属性unsigned short edgeColor;<br /><br /> // Size<br /> const unsigned short SIZE_DEFAULT = 0;<br /> const unsigned short SIZE_SMALL = 1;<br /> const unsigned short SIZE_MEDIUM = 2;<br /> const unsigned short SIZE_LARGE = 3;<br /> 只读 <br /> 属性未签名短大小；<br /><br /> // FontEdge<br /> const unsigned short FONT_EDGE_DEFAULT = 0 ;<br /> const unsigned short FONT_EDGE_NONE = 1;<br /> const unsigned short FONT_EDGE_ROURDED = 2 ;<br /> const unsigned short FONT_EDGE_DISCREPTED = 3;<br /> const unsigned short FONT_EDGE_UNIFORM = 4;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5;<br /> const unsigned short FONT_EDGE_DROP_SHADOW_RIGHT = 6;<br /> readonly属性unsigned short fontEdge;<br /><br /> // Font<br /> const unsigned short FONT_DEFAULT = 0;<br /> const unsigned short FONT_MONOSPACED_WITH_SERIFS = 1;<br /> const unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2;<br /> const unsigned short FONT_MONSPACED_WITHOUT_SERIFS = 3;<br /> const unsigned short FONT_CASUAL = 4;<br /> const unsigned short FONT_CURSIVE = 5;<br /> const unsigned short FONT_SMALL_CAPITALS = 6;<br /> 只读属性未签名短字体；<br /> readonly属性unsigned short fontOpacity;<br /> readonly属性unsigned short backgroundOpacity;<br /> readonly属性unsigned short fillOpacity;<br /> readonly属性unsigned short DEFAULT_OPACITY;<br /> };</p> </td> 
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
   <td><p>接口MediaPlayerItemLoader:<br /> {<br /> void load(MediaResource资源， long resourceId,<br /> ItemLoaderListener, <br /> MediaPlayerItemConfig);<br /> void cancel();<br /> readonly属性MediaPlayerItem currentItem;<br /> };</p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
  <tr> 
   <td><p>interfaceItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc;<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc;<br /> }</p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的媒体特性API元素更改 {#media-characteristics-api-element-changes-for}

这些表比较了C++ TVSDK的媒体特性API元素（版本1.3和2.0）。

本主题中的表：

* MediaPlayerItem
* Track、AudioTrack、ClosedCaptionsTrack
* 个人资料
* DRMMetadataInfo

### MediaPlayerItem {#mediaplayeritem}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口MediaPlayerItem {readonly<br /> 属性MediaResource资源；<br /> readonly属性long resourceId;<br /> 只读属性布尔live;<br /> 只 <br /> 读属性booleanhasAlternateAudio;<br /> readonly属性AudioTrackList audioTracks;<br /> readonly属性AudioTrack selectedAudioTrack;<br /> void selectAudioTrack(AudioTrack); <br /> readonly <br /> 属性boolean hasClosedCaptions;<br /> readonly属性ClosedCaptionsTrackList closedCaptionsTracks;<br /> readonly属性ClosedCaptionsTrack selectedClosedCaptionsTrack;<br /> void selectClosedCaptionsTrack(<br /> ClosedCaptionsTrack跟踪); <br /> 只 <br /> 读属性boolean hasTimedMetadata;<br /> readonly属性TimedMetadataList timedMetadata;<br /> 只读属性布尔动态；<br /> 只 <br /> 读属性boolean isProtected;<br /> 只读属性DRMMetadataInfoList drmMetadataInfos;<br /> 只读属性ProfileList配置文件；<br /> readonly属性selectedProfile;<br /> 只 <br /> 读属性boolean trickPlaySupported;<br /> readonly属性FloatArray availablePlaybackRates;<br /> readonly属性float selectedPlaybackRate;<br /> MediaPlayer <br /> MediaPlayer的只 <br /> 读属性；<br /> readonly属性MediaPlayerItemConfig;<br /> };</p> </td> 
   <td><p>接口MediaPlayerItem {readonly<br /> 属性MediaResource资源；<br /> readonly属性long resourceId;<br /> 只读属性布尔live;<br /> 只 <br /> 读属性booleanhasAlternateAudio;<br /> readonly属性AudioTrackList audioTracks;<br /> aduioTrack selectedAudioTrack属性；<br /><br /> readonly <br /> 属性boolean hasClosedCaptions;<br /> readonly属性ClosedCaptionsTrackList ccTracks;<br /> 属性ClosedCaptionsTrack selectedCCTrack;<br /><br /><br /> 只 <br /> 读属性boolean hasTimedMetadata;<br /> readonly属性TimedMetadataList timedMetadata;<br /> 只读属性布尔动态；<br /> 只 <br /> 读属性boolean isProtected;<br /> 只读属性DRMMetadataInfoList drmMetadataInfos;<br /> 只读属性ProfileList配置文件；<br /><br /> 只 <br /> 读属性boolean trickPlaySupported;<br /> readonly属性Int32Array availablePlaybackRates;<br /> 只 <br /> 读属性StringList adTags;<br /> 只 <br /> 读属性MediaPlayer mediaPlayer;<br /><br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 音轨／音频轨道／隐藏字幕轨道 {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface Track<br /> {<br /> readonly属性DomString名称；<br /> readonly属性DomString语言；<br /> 只读属性布尔值默认值；<br /> 只读属性boolean autoSelect;<br /> }; </p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
  <tr> 
   <td><p>接口AudioTrack:Track<br /> {readonly<br /> attribute DomString name;//FromTrack<br /> readonly属性DomString语言；//FromTrack<br /> readonly属性布尔默认值；// From Track<br /> readonly attribute boolean autoSelect;//FromTrack<br /><br /> readonly attribute unsigned int pid;<br /> };</p> </td> 
   <td><p>interface AudioTrack<br /> {readonly<br /> 属性DomString名称；<br /> readonly属性DomString语言； <br /> readonly属性布尔型默认值；<br /> 只读属性boolean autoSelect;<br /> 只读属性布尔值强制；<br /><br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0没有更改</td> 
   <td><p>interface AudioTrackList<br /> {<br /> readonly属性未签名长；<br /> getter AudioTrack（未签名长索引）;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><p>interface ClosedCaptionsTrack:Track<br /> {readonly<br /> attribute DomString name;//FromTrack<br /> readonly属性DomString语言；//FromTrack<br /> readonly属性布尔默认值；// FromTrack<br /> readonly属性boolean autoSelect;//FromTrack<br /> <br /><br /> const unsigned short SERVICE_608_CAPTIONS = 0;<br /> const unsigned short SERVICE_708_CAPTIONS = 1;<br /> const unsigned short SERVICE_WEB_VTT_CAPTIONS = 2;<br /> readonly属性unsigned short serviceType;<br /> 只读属性布尔值强制；<br /> };</p> </td> 
   <td><p>interface ClosedCaptionsTrack<br /> {<br /> readonly属性DomString名称；<br /> readonly属性DomString语言；<br /> 只读属性布尔值默认值；<br /><br /> 只 <br /> 读属性布尔活动；<br /><br /><br /> <br /><br /><br /> };</p> </td> 
  </tr> 
  <tr> 
   <td>2.0没有更改</td> 
   <td><p>interfaceClosedCaptionsTrackList<br /> {<br /> readonly属性未签名长；<br /> getter ClosedCaptionsTrack(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 个人资料 {#profile}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>简介：2.0没有更改</td> 
   <td><p>interface Profile<br /> {readonly<br /> attribute unsigned int width;<br /> readonly属性unsigned int height;<br /> readonly属性unsigned int bitRate;<br /> }; </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList:2.0没有更改</td> 
   <td><p>interface ProfileList<br /> {<br /> readonly属性未签名长；<br /> getter Profile(unsigned long index);<br /> };</p> </td> 
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
   <td><p>interface DRMMetadataInfo<br /> { <br /> readonly属性DRMMetadata元数据；<br /> readonly属性long prefetchTimestamp;<br /> 只读属性TimeRange timeRange;<br /> };</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>:2.0没有更改</td> 
   <td><p>interface DRMMetadataInfoList<br /> {<br /> readonly属性未签名长；<br /> getter DRMMetadataInfo(unsigned long index);<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 将C++错误映射到不同语言的例外 {#mapping-c-errors-to-exceptions-in-different-languages}

您可以将C++错误代码映射到不同语言的例外。

C++ PSDK的API有“不抛出”策略。 大多数API方法都会返回PSDKErrorCode值，以指示该方法是否成功执行。 异步错误通过错误事件通知。

ActionScript和JAVA PSDK有不同的策略。 大多数错误将引发ArgumentError或IllegalStateException，以指示无法执行方法的同步部分。 不会捕获这些例外，应用程序代码负责处理例外。 它们通常提供方法调用失败原因的有用信息。 例如，如果在无效状态中调用prepareToPlay命令，则会引发以下异常：

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

ActionScript/JAVA还会引发构造函数的异常，以指示某些内部对象创建错误。 这些例外是在内部处理的，不会传播到应用程序。 例外情况将包含在发送到应用程序的警告通知中

例如，如果未找到接收广告响应的有效媒体文件，则无法创建有效的广告资产对象或广告。 因此，不会在时间线上放置任何广告，并会调度NotificationEvent.OperationFailed通知。

从Adobe视频引擎(AVE)异步接收的错误或警告代码作为普通事件调度给应用程序。 通知事件包含所有接收到的错误代码和任何其他元数据，如URL、资源标识符、句柄等。 如果错误严重且无法继续播放当前媒体，则MediaPlayer将转换为ERROR状态，并调度onStatusChanged回调或MediaPlayerStatusChanged.STATUS_CHANGED事件。 如果播放可以继续，则调度常规通知事件。

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
   <td>代码为1的异常，description = "INVALID_ARGUMENT" and additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPointer</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>ArgumentError</td> 
   <td>代码为2的异常，description = "GENERIC_ERROR" and additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalStateException</td> 
   <td>IllegalStateException</td> 
   <td>代码为3的异常，description = "ILLEGAL_STATE" and additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为4的异常，description = "GENERIC_ERROR" and additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为5的异常，description = "CREATION_FAILED" and additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为5的异常，description = "CREATION_FAILED" and additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为7的异常，description = "DATA_NOT_AVAILABLE" and additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为8的异常，description = "SEEK_ERROR" and additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupported功能</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为9的异常，description = "UNSUPPORTED_FEATURE" and additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为10的异常，description = "RANGE_ERROR" and additionalInfo= &lt;as pass by method which this exception</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为11的异常，description = "CODEC_NOT_SUPPORTED" and additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为12的异常，description = "MEDIA_ERROR" and additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为13的异常，description = "NETWORK_ERROR", additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error或MediaPlayerNotification.Warning</td> 
   <td>MediaError或NotificationEvent</td> 
   <td>代码为14的异常，description = "GENERIC_ERROR" and additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为15的异常，description = "INVALID_SEEK_TIME" and additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为16的异常，description = "AUDIO_TRACK_ERROR" and additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferent<p>ThreadError</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为17的异常，description = "GENERIC_ERROR" and additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为18的异常，description = "GENERIC_ERROR", additionalInfo= &lt;as pass by method which this exception</td> 
  </tr> 
  <tr> 
   <td>kECNotImplemented</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为19的异常，description = "GENERIC_ERROR" and additionalInfo= &lt;as passed by method which this exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码为200的异常，description = "PLAYBACK_OPERATION_FAILED" and additionalInfo= &lt;as pass by method which this the exception&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>NotificationEvent</td> 
   <td>代码为201的异常，description = "NATIVE_WARNING", additionalInfo= &lt;as passed by method which this exception</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>代码为202的异常，description = "AD_RESOLVER_FAILED" and additionalInfo= &lt;as passed by method which this the exception&gt;</td> 
  </tr> 
 </tbody> 
</table>

## 2.0的实用程序和帮助程序API元素更改 {#utility-and-helper-api-element-changes-for}

这些表比较了JavaScript TVSDK的实用程序和帮助程序API元素（在版本1.3和2.0之间）。

本主题中的表：

* 版本
* TimeRange
* QOSProvider
* 设备信息
* LoadInfo
* 查看
* 播放信息

### 版本 {#version}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>interface Version<br /> {readonly<br /> attribute DomString version;<br /> readonly属性DomString描述；<br /> 只读属性长主题；<br /> 只读属性长小；<br /> 只读属性长修订；<br /> readonly属性long apiVersion;<br /> };</p> </td> 
   <td><p>interface Version<br /> {readonly<br /> attribute DomString version;<br /> readonly属性DomString描述；<br /> readonly属性DomString主题；<br /> readonly属性DomString次要；<br /> readonly属性DomString修订版；<br /> readonly属性DomString apiVersion;<br /> };</p> </td> 
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
   <td><p>interface TimeRange<br /> {<br /> readonly属性unsigned long begin;<br /> readonly属性unsigned long end;<br /> 只读属性未签名的长持续时间；<br /> };</p> </td> 
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
   <td><p>接口QOSProvider<br /> {<br /> void attachMediaPlayer（MediaPlayer播放器）;<br /> void detachMediaPlayer();<br /> 只 <br /> 读属性DeviceInformation deviceInformation;<br /> readonly属性PlaybackInformation playbackInformation;<br /> };</p> </td> 
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
   <td><p>interfaceDeviceInformation<br /> {<br /> readonly属性DomString os;<br /><br /><br /> 只 <br /> 读属性DomString id;<br /> 只读属性int densityDPI;<br /> readonly属性int heightPixels;<br /> idthPixels的只读属性；<br /> readonly属性boolean seekToKeyFrame;<br /> };</p> </td> 
   <td><p>interfaceDeviceInformation<br /> {<br /> readonly属性DomString os;<br /> int sdk;<br /> readonly属性DomString模型；<br /> readonly属性DomString制造商；<br /> readonly属性DomString id;<br /> 只读属性int densityDPI;<br /> readonly属性int heightPixels;<br /> idthPixels的只读属性；<br /><br /> };</p> </td> 
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
   <td><p>interface LoadInfo<br /> {<br /> readonly属性DomString url;<br /> 只读属性int大小；<br /> readonly属性double downloadDuration;<br /> readonly属性int periodIndex;<br /> readonly属性double mediaDuration;<br /> 只读属性短TRACK_TYPE_FRAGMENT;<br /> readonly属性short TRACK_TYPE_TRACK;<br /> readonly属性short TRACK_TYPE_MANIFEST;<br /> 只读属性短类型；<br /> readonly属性DomString trackName;<br /> readonly属性DomString trackType;<br /> readonly属性int trackIndex;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

### 查看 {#view}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0没有更改</td> 
   <td><p>interface View<br /> {<br /> readonly属性unsigned short x;<br /> 只读属性unsigned short y;<br /> 只读属性无符号短宽；<br /> 只读属性未签名短高度；<br /><br /> void setSize(unsigned short width, unsigned short height);<br /> void setPos(unsigned short x, unsigned short y);<br /> }</p> </td> 
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
   <td><p>interface PlaybackInformation<br /> {readonly<br /> attribute double timeToFirstByte;<br /> readonly属性double timeToLoad;<br /> readonly属性double timeToStart;<br /> readonly属性double timeToFail;<br /> readonly属性int totalSecondsPlayed;<br /> readonly属性int totalSecondsSpent;<br /> readonly属性double frameRate;<br /> readonly属性int droppedFrameCount;<br /> readonly属性int envericedBandwidth;<br /> 比特率的只读属性；<br /> readonly属性double bufferTime;<br /> readonly属性int bufferLength;<br /> readonly属性int emptyBufferCount;<br /> readonly属性double bufferingTime;<br /> };</p> </td> 
   <td><p>interface PlaybackInformation<br /> {readonly<br /> attribute double timeToFirstByte;<br /> readonly属性double timeToLoad;<br /> readonly属性double timeToStart;<br /> readonly属性double timeToFail;<br /> readonly属性int totalSecondsPlayed;<br /> readonly属性int totalSecondsSpent;<br /> readonly属性double frameRate;<br /> readonly属性int droppedFrameCount;<br /><br /> readonly属性int比特率；<br /> readonly属性double bufferTime;<br /> readonly属性int bufferLength;<br /> readonly属性int emptyBufferCount;<br /> readonly属性double bufferingTime;<br /> };</p> </td> 
  </tr> 
 </tbody> 
</table>

## 实用资源 {#helpful-resources}

* 请参阅 [Adobe Primetime学习和支持页面上的完整帮助文档](https://helpx.adobe.com/support/primetime.html) 。
