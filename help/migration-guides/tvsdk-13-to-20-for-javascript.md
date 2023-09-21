---
title: TVSDK转换 — 适用于JavaScript的1.3到2.0
description: 对于2.0，许多方法签名和API元素名称已更改。查看这些表以查看所有API更改详细信息。
contentOwner: asgupta
products: SG_PRIMETIME
topic-tags: migration
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '5034'
ht-degree: 0%

---

# TVSDK转换 — 适用于JavaScript的1.3到2.0 {#tvsdk-conversion-to-for-javascript}

对于2.0，许多方法签名和API元素名称已更改。查看这些表以查看所有API更改详细信息。

## 在JavaScript中实施回调函数 {#implement-callback-functions-in-javascript}

方法文档中的注释为您需要实施的回调建议了签名。

对于JavaScript，API语法基于Web ID。 对于TVSDK接口，将调用方法名称 *方法名称*()。 对于由应用程序实施的方法，一个读/写属性称为 *方法名称* CallbackFunc已添加到接口中，应用程序应将其设置为指向实现方法的函数。 例如：

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

## 针对2.0的广告工作流API元素更改 {#advertising-workflow-api-element-changes-for}

下表比较了1.3版和2.0版中JavaScript TVSDK的广告工作流API元素。

本主题中的表：

* Timedatadata
* AdSignalingMode
* AdvertisingMetadata
* CustomRangeMetadata
* ReplaceTimeRange
* 投放
* 机会
* 预订
* 时间线/时间线项目/时间线标记
* AdBreak
* Ad / AdAsset / AdClick / AdList / AdAssetList / AdBannerAsset
* AdBreakTimelineItem / AdTimelineItem
* AdBreakPolicy / AdBreakWatchedPolicy / AdPolicy / AdPolicyMode / AdPolicyInfo / AdPolicySelector
* 时间线操作
* AdBreakPlacement
* Auditudesettings

### Timedatadata {#timedmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p> <strong>Timedatadata</strong>：接口TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ； <br /> const无符号短METADATA_TYPE_ID3 = 1 ； <br /> 只读属性无符号短类型； <br /> 只读属性长时间；<br /> 只读属性DomString ID；<br /> 只读属性DomString名称；<br /> 只读属性DomString内容； <br /> 只读属性对象元数据；<br /> }； </p> </td> 
   <td><p>接口TimedMetadata {<br /> const unsigned short METADATA_TYPE_TAG = 0 ；<br /> const无符号短METADATA_TYPE_ID3 = 1 ；<br /> 只读属性不带符号的短metadataType；<br /> 只读属性长时间；<br /> 只读属性长ID；<br /> 只读属性DomString名称；<br /> <br /> 只读属性对象元数据；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><strong>TimedMetadataList</strong>：（2.0无更改）</td> 
   <td><p>接口TimedMetadataList {<br /> 只读属性无符号长长度；<br /> getter TimedMetadata（无符号长索引）；<br /> }；</p> </td> 
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
   <td><p>接口AdSignalingMode { <br /> const unsigned short MODE_DEFAULT， <br /> const unsigned short MODE_MANIFEST_CUE ， <br /> const unsigned short MODE_SERVER_MAP ， <br /> const unsigned short MODE_CUSTOM_RANGES <br /> }；</p> </td> 
   <td>这将替换MetadataKeys：：MANIFEST_CUE键。</td> 
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
   <td><p>界面AdvertisingMetadata { <br /> 属性AdSignalingMode模式； <br /> 属性AdBreakWatchedPolicy adBreakAsWatched； <br /> 属性布尔值livePreroll； <br /> 属性布尔值delayAdLoading ； <br /> }；</p> </td> 
   <td>此功能由提供<p>元数据键：：ADVERTISING_METADATA</p> 键。</td> 
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
   <td><p>界面CustomRangeMetadata { <br /> const unsigned short TYPE_MARK_RANGE； <br /> const unsigned short TYPE_DELETE_RANGE； <br /> const unsigned short TYPE_REPLACE_RANGE； <br /> 属性无符号短类型； <br /> 属性布尔值adjustSeekPosition； <br /> 属性TimeRangeList timeRangeList； <br /> }；</p> </td> 
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
   <td><p>界面ReplaceTimeRange { <br /> 属性无符号长开始； <br /> 只读属性无符号长端； <br /> 属性无符号长持续时间； <br /> 属性unsigned long replaceDuration； <br /> }；</p> </td> 
   <td>（2.0的新增功能）</td> 
  </tr> 
 </tbody> 
</table>

### 投放 {#placement}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>界面放置{ <br /> const unsigned short TYPE_MID_ROLL； <br /> const unsigned short TYPE_PRE_ROLL； <br /> const unsigned short TYPE_POST_ROLL； <br /> const unsigned short TYPE_SERVER_MAP； <br /> const unsigned short TYPE_CUSTOM_RANGE；<br /> 只读属性无符号短类型； <br /> 只读属性长时间； <br /> 只读属性长持续时间； <br /> const unsigned short MODE_DEFAULT； <br /> const unsigned short MODE_INSERT； <br /> const unsigned short MODE_REPLACE； <br /> const unsigned short MODE_DELETE； <br /> const unsigned short MODE_MARK； <br /> const unsigned short MODE_FREE_REPLACE； <br /> 只读属性无符号短模式； <br /> 只读属性TimeRange； <br /> }；</p> </td> 
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
   <td><p>界面销售机会{ <br /> 只读属性DomString ID； <br /> 只读属性投放位置； <br /> 只读属性Object设置； <br /> 只读属性Object customParameters； <br /> }； </p> </td> 
   <td>（2.0的新增功能）</td> 
  </tr> 
 </tbody> 
</table>

### 预订 {#reservation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>界面预订{ <br /> 只读属性TimeRange； <br /> 只读属性长保留； <br /> }； </p> </td> 
   <td> （2.0的新增功能）</td> 
  </tr> 
 </tbody> 
</table>

### 时间线/时间线项目/时间线标记 {#timeline-timelineitem-timelinemarker}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p><strong>时间线</strong>：界面时间轴 <br /> { readonly attribute TimelineMarkerList timelineMargers； <br /> 只读属性TimelineItemList timelineItems； <br /> double convertToLocalTime( double time)； <br /> 两次convertToVirtualTime( double time)； <br /> }；</p> </td> 
   <td><p>界面时间线{<br /> 只读属性TimelineMarkerList timelineMargers；<br /> <br /> <br /> <br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><p> <strong>时间线项目</strong>：界面TimelineItem ：<br /> 时间线标记{<br /> 只读属性长ID； <br /> 只读属性TimeRange virtualRange； <br /> 只读属性TimeRange localRange； <br /> 只读属性布尔值被观看； <br /> 只读属性布尔值临时； <br /> }； </p> </td> 
   <td>（2.0的新增功能）</td> 
  </tr> 
  <tr> 
   <td><strong>时间线标记</strong>：（2.0无更改）</td> 
   <td><p>界面时间线标记{<br /> 只读属性双倍时间；<br /> 只读属性双倍持续时间；<br /> }；</p> </td> 
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
   <td><p>界面AdBreak {<br /> <br /> <br /> <br /> 只读属性双倍持续时间；<br /> 只读属性广告列表广告；<br /> <br /> <br /> 只读属性AdInsertionType insertionType；<br /> }； </p> </td> 
   <td><p>界面AdBreak {<br /> 只读属性双倍时间；<br /> 只读属性double replaceDuration；<br /> <br /> 只读属性双倍持续时间；<br /> 只读属性AdList adList；<br /> <br /> 只读属性DomString数据；<br /> <br /> }； </p> </td> 
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
   <td><p> <strong>广告</strong>：界面广告{<br /> 只读属性AdAsset primaryAsset；<br /> 只读属性AdAssetList companionAssets；<br /> <br /> 只读属性双倍持续时间；<br /> 只读属性DomString ID；<br /> const无符号短ADTYPE_LINEAR = 0 ；<br /> const无符号短ADTYPE_NONLINEAR = 1 ；<br /> <br /> 只读属性不带符号的短adType；<br /> 只读属性AdInsertionType adInsertionType； <br /> <br /> 只读属性布尔值可点击； <br /> 只读属性布尔值isCustomAdMarker；<br /> }； </p> </td> 
   <td><p>界面广告{<br /> 只读属性AdAsset primaryAsset；<br /> 只读属性AdAssetList companionAssets；<br /> <br /> 只读属性双倍持续时间；<br /> 只读属性DomString ID；<br /> const无符号短ADTYPE_LINEAR = 0 ；<br /> const无符号短ADTYPE_NONLINEAR = 1 ；<br /> <br /> 只读属性无符号短类型；<br /> 只读属性AdInsertionType insertionType； <br /> 只读属性Object tracker；<br /> <br /> <br /> }； </p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAsset</strong>：（2.0无更改）</td> 
   <td><p>界面AdAsset {<br /> 只读属性DomString ID；<br /> 只读属性双倍持续时间；<br /> 只读属性MediaResource；<br /> 只读属性AdClick adClick；<br /> 只读属性对象元数据；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdClick</strong>：（2.0无更改）</td> 
   <td><p>界面AdClick {<br /> 只读属性DomString ID；<br /> 只读属性DomString title；<br /> 只读属性DomString url；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><strong>广告列表</strong>：（2.0无更改）</td> 
   <td><p>界面AdList {<br /> 只读属性无符号长长度；<br /> getter Ad（无符号长索引）；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><strong>AdAssetList</strong>：（2.0无更改）</td> 
   <td><p>界面AdAssetList {<br /> 只读属性无符号长长度；<br /> getter AdAsset（无符号长索引）；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBannerAsset</strong>：界面AdBannerAsset ： AdAsset<br /> {<br /> 只读属性int宽度；<br /> 只读属性int高度；<br /> 只读属性DomString staticUrl；<br /> 只读属性DomString高度；<br /> 只读属性DomString宽度；<br /> }；</p> </td> 
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
   <td><p> <strong>AdBreakTimelineItem</strong>：接口AdBreakTimelineItem ：时间线项目{ <br /> 只读属性AdBreak adBreak； <br /> 只读属性AdTimelineItemList项； <br /> }； </p> </td> 
   <td> （2.0的新增功能）</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdTimelineItem</strong>：界面AdTimelineItem ： TimelineItem { <br /> 只读属性AdBreak adBreak； <br /> 只读属性广告广告； <br /> }； </p> </td> 
   <td> （2.0的新增功能）</td> 
  </tr> 
  <tr> 
   <td><p><strong>AdBreakTimelineItemList</strong>：接口AdBreakTimelineItemList { <br /> 只读属性无符号长长度； <br /> getter AdBreakTimelineItem （无符号加载索引）； <br /> }；</p> </td> 
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
   <td><p>接口AdBreakPolicy {<br /> 只读属性短AD_BREAK_POLICY_SKIP；<br /> 只读属性短AD_BREAK_POLICY_PLAY；<br /> 只读属性短AD_BREAK_POLICY_REMOVE；<br /> 只读属性短AD_BREAK_POLICY_REMOVE_AFTER_PLAY；<br /> }；</p> </td> 
   <td><p> 接口AdPolicyConstants {<br /> 只读属性短AD_BREAK_POLICY_SKIP；<br /> 只读属性短AD_BREAK_POLICY_PLAY；<br /> 只读属性短AD_BREAK_POLICY_REMOVE；<br /> 只读属性短AD_BREAK_POLICY_REMOVE_AFTER_PLAY；}<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p> 接口AdBreakWatchedPolicy {<br /> 只读属性短AD_BREAK_AS_WATCHED_ON_BEGIN；<br /> 只读属性短AD_BREAK_AS_WATCHED_ON_END；<br /> 只读属性短AD_BREAK_AS_WATCHED_NEVER；<br /> }； </p> </td> 
   <td><p> ...<br /> 只读属性短AD_BREAK_AS_WATCHED_ON_BEGIN；<br /> 只读属性短AD_BREAK_AS_WATCHED_ON_END；<br /> 只读属性短AD_BREAK_AS_WATCHED_NEVER；<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>界面AdPolicy {<br /> 只读属性短AD_POLICY_PLAY；<br /> 只读属性短AD_POLICY_PLAY_FROM_AD_BEGIN；<br /> 只读属性短AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN；只读属性短AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK；<br /> <br /> 只读属性短AD_POLICY_SKIP_AD_BREAK；<br /> }；</p> </td> 
   <td><p> ... <br /> 只读属性短AD_POLICY_PLAY；<br /> 只读属性短AD_POLICY_PLAY_FROM_AD_BEGIN；<br /> 只读属性短AD_POLICY_PLAY_FROM_AD_BREAK_BEGIN；<br /> 只读属性短AD_POLICY_SKIP_TO_NEXT_AD_IN_BREAK；<br /> 只读属性短AD_POLICY_SKIP_AD_BREAK；<br /> ...</p> </td> 
  </tr> 
  <tr> 
   <td><p>接口AdPolicyMode {<br /> 只读属性短AD_POLICY_MODE_PLAY；<br /> 只读属性短AD_POLICY_MODE_SEEK；<br /> 只读属性短AD_POLICY_MODE_TRICKPLAY；<br /> }；</p> </td> 
   <td><p> ...<br /> {readonly attribute short AD_POLICY_MODE_PLAY；<br /> 只读属性短AD_POLICY_MODE_SEEK；<br /> 只读属性短AD_POLICY_MODE_TRICKPLAY；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><p>接口AdPolicyInfo {<br /> 只读属性AdBreakTimelineItemList <br /> adBreakTimelineItems；<br /> 只读属性AdTimelineItem adTimelineItem；<br /> 只读属性double currentTime；<br /> 只读属性double seekToTime；<br /> 只读属性双倍速率；<br /> 只读属性短模式； //AdPolicyMode<br /> }；</p> </td> 
   <td><p>接口AdPolicyInfo {<br /> 只读属性AdBreakPlacementList <br /> adBreakPlacement；<br /> 只读属性广告广告；<br /> 只读属性double currentTime；<br /> 只读属性double seekToTime；<br /> 只读属性双倍速率；<br /> 只读属性短模式； //AdPolicyMode<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><p>界面AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo)；<br /> */<br /> 属性对象selectPolicyForAdBreakCallbackFunc；<br /> /**<br /> * AdBreakTimelineItemList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo)；<br /> */<br /> 属性对象selectAdBreaksToPlayCallbackFunc；<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo)；<br /> */<br /> 属性对象selectPolicyForSeekIntoAdCallbackFunc； <br /> /**<br /> * AdBreakWatchedPolicy selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo)；<br /> */<br /> 属性对象selectWatchedPolicyForAdBreakCallbackFunc；<br /> }；</p> </td> 
   <td><p>界面AdPolicySelector {<br /> /**<br /> * AdbreakPolicy selectPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo)；<br /> */<br /> 属性对象selectPolicyForAdBreakFuncCallback；<br /> /**<br /> * AdBreakPlacementList selectAdBreaksToPlay(<br /> * AdPolicyInfo adPolicyInfo)；<br /> */<br /> 属性对象selectAdBreaksToPlayCallback；<br /> /**<br /> * AdPolicy selectPolicyForSeekIntoAd(AdPolicyInfo adPolicyInfo)；<br /> */<br /> 属性对象selectPolicyForSeekIntoAdCallback； <br /> /**<br /> * AdBreakAsWatched selectWatchedPolicyForAdBreak(<br /> * AdPolicyInfo adPolicyInfo)；<br /> */<br /> 属性对象selectWatchedPolicyForAdBreakCallback；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### 时间线操作 {#timelineoperation}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>界面时间线操作{ <br /> 只读属性投放位置； <br /> }；</p> </td> 
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
   <td><p>界面AdBreakPlacement ： TimelineOperation {<br /> 只读属性AdBreak adBreak；<br /> 只读属性Placement placement； //从TimelineOperation<br /> 只读属性双倍时间；<br /> 只读属性双倍持续时间；<br /> }；</p> </td> 
   <td><p>界面AdBreakPlacement {<br /> 只读属性AdBreak adBreak；<br /> 只读属性投放位置；<br /> 只读属性双倍时间；<br /> 只读属性双倍持续时间；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### Auditudesettings {#auditudesettings}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>界面审核设置：AdvertisingMetadata { <br /> 属性DomString zoneId； <br /> 属性DomString mediaId； <br /> 属性DomString defaultMediaId ； <br /> 属性DomString域； <br /> 属性Object targetingInfo ； <br /> 属性Object customParameters ； <br /> 属性Boolean creativePackingEnabled ；<br /> 属性布尔值showStaticBanners ；<br /> }；</p> </td> 
   <td>功能由MetadataKeys：：metadata_METADATA_KEYAUDITUDE提供。</td> 
  </tr> 
 </tbody> 
</table>

## 针对2.0的自定义API元素更改 {#customization-api-element-changes-for}

下表比较了版本1.3和2.0中JavaScript TVSDK的自定义API元素。

本主题中的表：

* MediaPlayerItemConfig
* Contentfactory
* 网络配置

### MediaPlayerItemConfig {#mediaplayeritemconfig}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>界面MediaPlayerItemConfig {<br /> 属性ContentFactory adFactory；<br /> 属性StringList subscribeTags；<br /> <br /> 属性StringList adTags；<br /> <br /> <br /> 属性AdSignalingMode adSignalingMode；<br /> 属性CustomRangeMetadata customRangeMetadata；<br /> 属性NetworkConfiguration networkConfiguration；<br /> 属性AdvertisingMetadata advertisingMetadata；<br /> 属性布尔值useHardwareDecoder；<br /> }；</p> </td> 
   <td><p>界面MediaPlayerConfig {<br /> <br /> <br /> <br /> 属性StringList adTags；<br /> 属性StringList subscribedTags；<br /> 属性MediaPlayerClientFactory clientFactory；<br /> <br /> <br /> <br /> <br /> <br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### Contentfactory {#contentfactory}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>界面ContentFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem)；<br /> */<br /> 属性Object retrieveAdPolicySelectorCallbackFunc；<br /> }；</p> </td> 
   <td><p>界面MediaPlayerClientFactory {<br /> /*<br /> * AdPolicySelector retrieveAdPolicySelector(<br /> * MediaPlayerItem)；<br /> */<br /> 属性Object retrieveAdPolicySelectorFunc；<br /> }；</p> </td> 
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
   <td><p>接口网络配置<br /> {<br /> 属性布尔值forceNativeNetworking；<br /> 属性布尔值useRedirectedUrl；<br /> 属性Object cookieHeader；<br /> 属性布尔值readSetCookieHeader；<br /> 属性int masterUpdateInterval； <br /> 属性布尔值useCookieHeaderForAllRequests；<br /> 属性int readLimit；<br /> }；</p> </td> 
   <td>在1.3中，部分此功能由MetadataKeys提供</td> 
  </tr> 
 </tbody> 
</table>

## 针对2.0的DRM API元素更改 {#drm-api-element-changes-for}

下表比较了版本1.3和2.0中JavaScript TVSDK的DRM API元素。

本主题中的表：

* DRM工作流初始化
* DRMAcquireLicenseSettings / DRMAuthenticationMethod
* DRM元数据
* DRMPlaybackTimeWindows
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
   <td>应用程序需要调用AdobePSDK.initiateDRMWorkflow来启动DRM工作流。 如果没有此调用，DRM视频将无法播放。<p>界面AdobePSDK<br /> {<br /> void initiateDRMWorkFlow(<br /> DomString appStoratePath， <br /> DomString publisherId， <br /> DomString appId， <br /> DomString appVersion， <br /> boolean privacyModeOn)；<br /> }；</p> </td> 
   <td>初始化已在内部完成，不需要显式调用。</td> 
  </tr> 
 </tbody> 
</table>

### DRMAcquireLicenseSettings/DRMAuthenticationMethod {#drmacquirelicensesettings-drmauthenticationmethod}

| 2.0 API | 1.3 API |
|--- |--- |
| **DRMAcquireLicenseSettings** |  |
| 2.0无更改。 | 枚举DRMAcquireLicenseSettings <br>{<br> const unsigned int FORCE_REFRESH = 0；<br> const unsigned int LOCAL_ONLY = 1；<br> const unsigned int ALLOW_SERVER = 2；<br> }； |
| **DRMAuthenticationMethod** |  |
| 2.0无更改。 | 枚举DRMAuthenticationMethod <br>{<br> const无符号int UNKNOWN = 0；<br> const unsigned int ANONYMOUS = 1；<br> const unsigned int USERNAME_AND_PASSWORD = 2；<br> } |

### DRM元数据 {#drmmetadata}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0无更改。</td> 
   <td><p>接口DRM元数据<br /> {<br /> 只读属性DomString serverUrl；<br /> 只读属性DomString licenseId；<br /> 只读属性DRMPolicyArray策略； <br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### DRMPlaybackTimeWindows {#drmplaybacktimewindow}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口DRMPlaybackTimeWindow {<br /> 只读属性int playbackPeriodInSeconds；<br /> 只读属性long playbackStartDate；<br /> 只读属性long playbackEndDate；<br /> }；</p> </td> 
   <td><p>接口DRMPlaybackTimeWindow {<br /> 只读属性int periodInSeconds；<br /> 只读属性int startDate；<br /> 只读属性int endDate；<br /> }；</p> </td> 
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
   <td>2.0无更改。</td> 
   <td><p>界面DRMLicense {<br /> 只读属性Uint8Array字节；<br /> 只读属性Date licenseStartDate；<br /> 只读属性Date licenseEndDate；<br /> 只读属性Date offlineStorageStartDate；<br /> 只读属性Date offlineStorageEndDate； <br /> 只读属性DomString serverUrl；<br /> 只读属性DomString licenseID；<br /> 只读属性DomString policyID；<br /> 只读属性DRMPlaybackTimeWindow playbackTimeWindow；<br /> 只读属性Object customProperties；<br /> }； </p> </td> 
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
   <td><p>界面DRMLicenseDomain {<br /> 只读属性DomString authenticationDomain；<br /> 只读属性DRMAuthenticationMethod authenticationMethod； <br /> 只读属性DomString serverUrl；<br /> }；</p> </td> 
   <td><p>界面DRMLicenseDomain {<br /> 只读属性DomString authDomain；<br /> 只读属性DRMAuthenticationMethod authMethod； <br /> 只读属性DomString serverURL；<br /> }；</p> </td> 
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
   <td><p>接口DRMPolicy<br /> {<br /> 只读属性DomString authenticationDomain；<br /> 只读属性DRMAuthenticationMethod authenticationMethod；<br /> <br /> 只读属性DomString displayName；<br /> 只读属性DRMLicenseDomain licenseDomain；<br /> }；</p> </td> 
   <td><p>接口DRMPolicy<br /> {<br /> 只读属性DomString authDomain；<br /> 只读属性DRMAuthenticationMethod authMethod；<br /> 只读属性DomString dispName；<br /> 只读属性DRMLicenseDomain licenseDomain；<br /> }；</p> </td> 
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
   <td><p>界面DRManager ：EventTarget {<br /> 无效acquireLicense(DRMMetadata元数据， <br /> DRMAcquireLicenseSettings设置， <br /> DRMAquireLicenseListener侦听器)；<br /> 无效acquirePreviewLicense(DRMMetadata元数据， <br /> DRMAquireLicenseListener侦听器)；<br /> 无效验证(DRMMetadata元数据， <br /> DomString url，<br /> DomString &amp;authenticationDomain， <br /> DomString用户， <br /> DomString密码， <br /> DRMAuthenticateListener)；<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array数组、DRMErrorListener侦听器)；<br /> void initialize（DRMOperationCompleteListener侦听器）；<br /> 属性long maxOperationTime；<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain， <br /> 布尔值forceRefresh， <br /> DRMOperationCompleteListener)；<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain， <br /> DRMOperationCompleteListener)；<br /> <br /> void resetDRM(DRMOperationCompleteListener listener)；<br /> void returnLicense(DomString serverURL， <br /> DomString licenseID、 <br /> DomString policyID， <br /> 布尔型commitImmediately，<br /> DRMReturnLicenseListener侦听器)；<br /> void setAuthenticationToken(<br /> DRM元数据， <br /> DomString authenticationDomain， <br /> Uint8Array令牌， <br /> DRMOperationCompleteListener)；<br /> void storeLicenseBytes(Uint8Array licenseBytes， <br /> DRMOperationCompleteListener)；<br /> }；</p> </td> 
   <td><p>界面DRManager ：EventTarget {<br /> 无效acquireLicense(DRMMetadata元数据， <br /> DRMAcquireLicenseSettings设置， <br /> EventContext eventContext)；<br /> 无效acquirePreviewLicense(DRMMetadata元数据， <br /> EventContext eventContext)；<br /> 无效验证(DRMMetadata元数据， <br /> DomString url，<br /> DomString &amp;authenticationDomain， <br /> DomString用户， <br /> DomString密码， <br /> EventContext eventContext)；<br /> <br /> DRMMetadata createMetadataFromBytes(<br /> Uint8Array数组、EventContext eventContext)；<br /> void initialize(EventContext eventContext)；<br /> 属性long maxOperationTime；<br /> <br /> void joinLicenseDomain(<br /> DRMLicenseDomain licenseDomain， <br /> 布尔值forceRefresh， <br /> EventContext eventContext)；<br /> void leaveLicenseDomain(<br /> DRMLicenseDomain licenseDomain， <br /> EventContext eventContext)；<br /> <br /> void resetDRM(EventContext eventContext)；<br /> void returnLicense(DomString serverURL， <br /> DomString licenseID、<br /> DomString policyID， <br /> 布尔型commitImmediately，<br /> EventContext eventContext)；<br /> void setAuthenticationToken(<br /> DRM元数据， <br /> DomString authenticationDomain， <br /> Uint8Array令牌， <br /> EventContext eventContext)；<br /> void storeLicenseBytes(Uint8Array licenseBytes， <br /> EventContext eventContext)；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMErrorListener ： <br /> public psdkutils：：PSDKInterfaceWithUserData {<br /> 公共：<br /> 虚拟void onDRMError(uint32_t major， <br /> uint32_t次要， <br /> const psdkutils：： PSDKString&amp; errorString， <br /> const psdkutils：：PSDKString&amp; errorServerUrl) = 0；<br /> <br /> 受保护：<br /> virtual ~DRMErrorListener() {}<br /> }</p> </td> 
   <td>事件/界面/描述 
    <ul> 
     <li>kEventDRMOperationError<p>/ DRMOperationErrorEvent</p> <p>在DRMManger的某个异步方法期间发生错误时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMOperationCompleteListener ： <br /> 公共DRM错误侦听器{<br /> 公共：<br /> 虚拟void onDRMOperationComplete() = 0；<br /> <br /> 受保护：<br /> virtual ~DRMOperationCompleteListener() {}<br /> }；</p> </td> 
   <td>事件/界面/描述 
    <ul> 
     <li>kEventDRMIinitializationComplete<p>/ PSDKEvent</p> <p>DRM初始化完成后。</p> </li> 
     <li>kEventDRMJoinLicenseDomainComplete<p>/ PSDKEvent</p> <p>当joinLicenseDomain()操作成功完成时。</p> </li> 
     <li>kEventDRMLeaveLicenseDomainComplete<p>/ PSDKEvent</p> <p>当leaveLicenseDomain()操作成功完成时。</p> </li> 
     <li>kEventDRMResetCompletePSDKEvent<p>/ PSDKEvent</p> <p>当resetDRM()操作成功完成时。</p> </li> 
     <li>kEventDRMAuthenticationTokenSet<p>/ PSDKEvent</p> <p>当setAuthenticationTokenSet()操作成功完成时。</p> </li> 
     <li>kEventDRMLicenseStore<p>/ PSDKEvent</p> <p>当storeLicenseBytes()操作成功完成时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>DRMAuthenticateListener类： <br /> 公共DRM错误侦听器{<br /> 公共：<br /> virtual void onAuthenticationComplete(<br /> psdkutils：：PSDKImmutableByteArray* <br /> authenticationToken) = 0；<br /> <br /> 受保护：<br /> virtual ~DRMAuthenticateListener() {}<br /> }</p> </td> 
   <td>事件/界面/描述 
    <ul> 
     <li>kEventDRMAuthenticationComplete<p>/ DRMAuthenticationCompleteEvent</p> <p>当DRMManager：：authenticate方法调用成功时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>DRMAquireLicenseListener类： <br /> 公共DRM错误侦听器{<br /> 公共：<br /> 虚拟void onLicenseAcquired(const DRMLicense*) = 0；<br /> <br /> 受保护：<br /> virtual ~DRMAquireLicenseListener() {}<br /> }；</p> </td> 
   <td>事件/界面/描述 
    <ul> 
     <li>kEventDRMPreviewLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>当DRMManager：：acquirePreviewLicense方法调用成功时。</p> </li> 
     <li>kEventDRMLicenseAcquired<p>/ DRMLicenseAcquiredEvent</p> <p>当DRMManager：：acquireLicense方法调用成功时。</p> </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td><p>类DRMReturnLicenseListener： <br /> 公共DRM错误侦听器{<br /> 公共：<br /> 虚拟void onLicenseReturnComplete(uint32_t numReturned ) = 0；<br /> <br /> 受保护：<br /> virtual ~DRMReturnLicenseListener() {}<br /> }；</p> </td> 
   <td>事件/界面/描述 
    <ul> 
     <li>kEventDRMLicenseReturnComplete<p>/ DRMLicenseReturnCompleteEvent</p> <p>当DRMManager：：returnLicense方法调用成功时。</p> </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>

## 2.0的常规播放API元素更改 {#generic-playback-api-element-changes-for}

这些表对JavaScript TVSDK 1.3和2.0之间的常规播放API元素进行了比较。

本主题中的表：

* MediaResource
* MediaPlayer
* ABRControlParameters
* buffercontrolparameters
* 文本格式
* MediaPlayerItemLoader

### MediaResource {#mediaresource}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口MediaResource {<br /> 属性DomString url； <br /> 属性无符号短类型；<br /> 属性对象元数据；<br /> const unsigned short TYPE_HLS；<br /> const unsigned short TYPE_HDS；<br /> const unsigned short TYPE_DASH；<br /> const unsigned short TYPE_CUSTOM；<br /> const unsigned short TYPE_UNKNOWN；<br /> }；</p> </td> 
   <td><p>接口MediaResource {<br /> 属性DomString url；<br /> 属性DomString类型；<br /> 属性对象元数据；<br /> <br /> <br /> <br /> <br /> <br /> }；</p> </td> 
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
   <td><p>界面MediaPlayer ：EventTarget<br /> {<br /> void prepareToPlay( double position)；<br /> void play()；<br /> void pause()；<br /> void seek( double position)；<br /> void seekToLocal( double position)；<br /> void reset()；<br /> void release()；<br /> void replaceCurrentItem（MediaPlayerItem项目）；<br /> void replaceCurrentResource(MediaResource资源， <br /> MediaPlayerItemConfig)； <br /> void suspend()；<br /> void restore()；<br /> 无效notifyClick()；<br /> <br /> 只读属性TimeRange playbackRange；<br /> 只读属性TimeRange seekableRange；<br /> 只读属性double currentTime；<br /> 只读属性double localTime；<br /> 只读属性TimeRange bufferedRange；<br /> 只读属性DRMManager drmManager；<br /> 只读属性MediaPlayerItem currentItem；<br /> <br /> //播放器状态<br /> <br /> <br /> const unsigned short PLAYER_STATUS_INITIALIZED；<br /> const unsigned short PLAYER_STATUS_PREPARING；<br /> const unsigned short PLAYER_STATUS_PREPARED；<br /> const unsigned short PLAYER_STATUS_PLAYING；<br /> const unsigned short PLAYER_STATUS_PAUSED；<br /> const unsigned short PLAYER_STATUS_SEEKING；<br /> const unsigned short PLAYER_STATUS_COMPLETE；<br /> const unsigned short PLAYER_STATUS_ERROR；<br /> const unsigned short PLAYER_STATUS_RELEASED；<br /> <br /> 只读属性无符号短状态；<br /> <br /> 属性无符号短卷；<br /> 属性ABRControlParameters abrControlParameters；<br /> 属性BufferControlParameters bufferControlParameters；<br /> <br /> const unsigned short VISIBLE； //For CC visibility<br /> const unsigned short INVISIBLE； //用于CC可见性<br /> 属性无符号短可见性；<br /> 属性TextFormat样式；<br /> 只读属性PlaybackMetrics playbackMetrics；<br /> <br /> 属性倍率；<br /> 属性MediaPlayerView；<br /> 只读属性时间线时间线；<br /> 属性双currentTimeUpdateInterval； <br /> //设置2.0不支持此设置<br /> }；</p> </td> 
   <td><p>界面MediaPlayer ：EventTarget<br /> {<br /> void prepareToPlay( int position)；<br /> void play()；<br /> void pause()；<br /> void seek( int position)；<br /> void seekToLocalTime( int position)；<br /> void reset()；<br /> void release()；<br /> void replaceCurrentItem(MediaResource source)；<br /> <br /> <br /> <br /> <br /> <br /> <br /> 只读属性TimeRange playbackRange；<br /> 只读属性TimeRange seekableRange；<br /> 只读属性double currentTime；<br /> 只读属性double localTime；<br /> 只读属性TimeRange bufferedRange；<br /> 只读属性DRMManager drmManager；<br /> 只读属性MediaPlayerItem currentItem；<br /> <br /> //播放器状态<br /> const unsigned short PLAYER_STATE_IDLE；<br /> const unsigned short PLAYER_STATE_INITIALIZING；<br /> const unsigned short PLAYER_STATE_INITIALIZED；<br /> const unsigned short PLAYER_STATE_PREPARING；<br /> const unsigned short PLAYER_STATE_PREPARED；<br /> const unsigned short PLAYER_STATE_PLAYING；<br /> const unsigned short PLAYER_STATE_PAUSED；<br /> const unsigned short PLAYER_STATE_SEEKING；<br /> const unsigned short PLAYER_STATE_COMPLETE；<br /> const unsigned short PLAYER_STATE_ERROR；<br /> const unsigned short PLAYER_STATE_RELEASED；<br /> const unsigned short PLAYER_STATUS_SUSPENDED；<br /> 只读属性无符号短状态；<br /> <br /> 属性无符号短卷；<br /> 属性ABRControlParameters abrControlParameters；<br /> 属性BufferControlParameters bufferControlParameters；<br /> <br /> 只读无符号短VISIBLE； //用于CC可见性<br /> 只读无符号短不可见； //用于CC可见性<br /> 属性无符号短可见性；<br /> 属性TextFormat样式；<br /> 只读属性PlaybackMetrics playbackMetrics；<br /> 属性MediaPlayerConfig mediaPlayerConfig；<br /> 属性倍率；<br /> 属性MediaPlayerView；<br /> 只读属性时间线时间线；<br /> <br /> <br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><p>界面MediaPlayerStatus<br /> {<br /> //播放器状态<br /> const unsigned short PLAYER_STATUS_IDLE；<br /> const unsigned short PLAYER_STATUS_INITIALIZING；<br /> const unsigned short PLAYER_STATUS_INITIALIZED；<br /> const unsigned short PLAYER_STATUS_PREPARING；<br /> const unsigned short PLAYER_STATUS_PREPARED；<br /> const unsigned short PLAYER_STATUS_PLAYING；<br /> const unsigned short PLAYER_STATUS_PAUSED；<br /> const unsigned short PLAYER_STATUS_SEEKING；<br /> const unsigned short PLAYER_STATUS_COMPLETE；<br /> const unsigned short PLAYER_STATUS_ERROR；<br /> const unsigned short PLAYER_STATUS_RELEASED；<br /> const unsigned short PLAYER_STATUS_SUSPENDED；<br /> }；</p> </td> 
   <td>（2.0的新增功能）</td> 
  </tr> 
 </tbody> 
</table>

#### MediaPlayer支持的事件 {#events-supported-by-mediaplayer}

<table> 
 <tbody> 
  <tr> 
   <th>2.0事件名称</th> 
   <th>2.0界面</th> 
   <th> </th> 
   <th>1.3事件名称</th> 
   <th>1.3接口</th> 
  </tr> 
  <tr> 
   <td><p>（为2.0删除）</p> </td> 
   <td> </td> 
   <td> </td> 
   <td>已准备</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td><p>itemUpdates</p> <p>更新媒体播放器项目时。</p> </td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>已更新</p> <p>媒体播放器已成功更新媒体时。</p> </td> 
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
   <td>时间线已更新</td> 
   <td>事件</td> 
   <td> </td> 
   <td>时间线已更新</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>在2.0中删除</td> 
   <td> </td> 
   <td> </td> 
   <td>playstart</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>为2.0删除</td> 
   <td> </td> 
   <td> </td> 
   <td>playComplete</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>statusChanged</td> 
   <td>StatusEvent</td> 
   <td> </td> 
   <td>状态已更改</td> 
   <td>StateEvent</td> 
  </tr> 
  <tr> 
   <td>sizeAvailable</td> 
   <td>大小事件</td> 
   <td> </td> 
   <td>大小</td> 
   <td>大小事件</td> 
  </tr> 
  <tr> 
   <td>adbreakstarted</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adbreakstart</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adstarted</td> 
   <td>AdEvent</td> 
   <td> </td> 
   <td>adstart</td> 
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
   <td>timeChange</td> 
   <td>时间事件</td> 
   <td> </td> 
   <td>进度</td> 
   <td>ProgressEvent</td> 
  </tr> 
  <tr> 
   <td>缓冲开始</td> 
   <td>事件</td> 
   <td> </td> 
   <td>缓冲</td> 
   <td>事件</td> 
  </tr> 
  <tr> 
   <td>缓冲结束</td> 
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
   <td>时间事件</td> 
  </tr> 
  <tr> 
   <td>loadInformationAvailable</td> 
   <td>loadinformevent</td> 
   <td> </td> 
   <td>loadInfo</td> 
   <td>LoadInfoEvent</td> 
  </tr> 
  <tr> 
   <td>操作失败</td> 
   <td>通知事件</td> 
   <td> </td> 
   <td>操作失败</td> 
   <td>错误事件</td> 
  </tr> 
  <tr> 
   <td>drmMetadataInfoAvailable</td> 
   <td>DRMetadataEvent</td> 
   <td> </td> 
   <td>drmMetadata</td> 
   <td>DRMetadataEvent</td> 
  </tr> 
  <tr> 
   <td>预订已实现</td> 
   <td>Reservationevent</td> 
   <td> </td> 
   <td>已到达时间线持有者</td> 
   <td>时间线持有者事件</td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td>bitrateChanged</td> 
   <td>BitrateChangedEvent</td> 
  </tr> 
  <tr> 
   <td>已选择费率</td> 
   <td>PlaybackRateEvent</td> 
   <td> </td> 
   <td>已选择费率</td> 
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
   <td>adBreakSkipped</td> 
   <td>AdBreakEvent</td> 
   <td> </td> 
   <td>adBreakSkipped</td> 
   <td>AdBreakEvent</td> 
  </tr> 
  <tr> 
   <td>adclicked<br /> 用户点击广告时。</td> 
   <td>AdClickedEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>profileChange<br /> 播放配置文件发生更改时。</td> 
   <td>配置文件事件</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>seekPositionAdjusted<br /> 当搜寻位置因内部或外部规则而调整时。</td> 
   <td>SeekEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>音频已更新<br /> 更新媒体播放器项目时。 对于某些包含只能在播放时检测到的音频轨道的流，此事件将在有新音频轨道可用时触发。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>字幕已更新 <br /> 更新媒体播放器项目时。 对于实时/线性流，客户端必须定期刷新媒体资源以检测新的可用内容。 发生这种情况时，某些媒体特性可能会发生变化。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>主更新 <br /> 更新媒体播放器项目时。 对于实时/线性流，客户端必须定期刷新媒体资源以检测新的可用内容。 发生这种情况时，某些媒体特性可能会发生变化。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>playbackRangeUpdated<br /> 更新媒体播放器项目时。 对于实时/线性流，客户端必须定期刷新媒体资源以检测新的可用内容。 发生这种情况时，某些媒体特性可能会发生变化。</td> 
   <td>MediaPlayerItemEvent</td> 
   <td> </td> 
   <td><p>2.0中的新增功能</p> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td>timedEvent<br /> 生成定时事件时发送。</td> 
   <td>Timedevent</td> 
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
   <td><p>接口ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ；<br /> const unsigned short ABR_POLICY_MODERATE = 1 ；<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ；<br /> <br /> 属性无符号短abrPolicy；<br /> 属性unsigned int initialBitRate；<br /> 属性unsigned int minBitRate；<br /> 属性无符号int maxBitRate；<br /> const unsigned short DEFAULT_ABR_INITIAL_BITRATE；<br /> 约束无符号短DEFAULT_ABR_MIN_BITRATE；<br /> 约束无符号短DEFAULT_ABR_MAX_BITRATE；<br /> 常量ABRPolicy DEFAULT_ABR_POLICY；<br /> }；</p> </td> 
   <td><p>接口ABRControlParameters<br /> {<br /> const unsigned short ABR_POLICY_CONSERVATIVE = 0 ；<br /> const unsigned short ABR_POLICY_MODERATE = 1 ；<br /> const unsigned short ABR_POLICY_AGGRESIVE = 2 ；<br /> <br /> 属性无符号短abrPolicy；<br /> 属性unsigned int initialBitRate；<br /> 属性unsigned int minBitRate；<br /> 属性无符号int maxBitRate；<br /> <br /> <br /> <br /> <br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### buffercontrolparameters {#buffercontrolparameters}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>接口BufferControlParameters<br /> {<br /> 属性双重initialBufferTime；<br /> 属性double playBufferTime；<br /> 常双精度DEFAULT_INITIAL_BUFFER_TIME；<br /> 常双DEFAULT_PLAY_BUFFER_TIME；<br /> }；</p> </td> 
   <td><p>接口BufferControlParameters<br /> {<br /> 属性双重initialBufferTime；<br /> 属性double playBufferTime；<br /> <br /> <br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### 文本格式 {#textformat}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0无更改</td> 
   <td><p>界面文本格式<br /> {<br /> //颜色<br /> const unsigned short COLOR_DEFAULT = 0 ；<br /> const unsigned short COLOR_BLACK = 1 ；<br /> const unsigned short COLOR_GRAY = 2 ；<br /> const unsigned short COLOR_WHITE = 3 ；<br /> const unsigned short COLOR_BRIGHT_WHITE = 4 ；<br /> const unsigned short COLOR_DARK_RED = 5 ；<br /> const unsigned short COLOR_RED = 6 ；<br /> const unsigned short COLOR_BRIGHT_RED = 7 ；<br /> const unsigned short COLOR_DARK_GREEN = 8 ；<br /> const unsigned short COLOR_GREEN = 9 ；<br /> const unsigned short COLOR_BRIGHT_GREEN = 10 ；<br /> const unsigned short COLOR_DARK_BLUE = 11 ；<br /> const unsigned short COLOR_BLUE = 12 ；<br /> const unsigned short COLOR_BRIGHT_BLUE = 13 ；<br /> const unsigned short COLOR_DARK_YELLOW = 14 ；<br /> const unsigned short COLOR_YELLOW = 15 ；<br /> const unsigned short COLOR_BRIGHT_YELLOW = 16 ；<br /> const unsigned short COLOR_DARK_MAGENTA = 17 ；<br /> const unsigned short COLOR_MAGENTA = 18 ；<br /> const unsigned short COLOR_BRIGHT_MAGENTA = 19 ；<br /> const unsigned short COLOR_DARK_CYAN = 20 ；<br /> const unsigned short COLOR_CYAN = 21 ；<br /> const unsigned short COLOR_BRIGHT_CYAN = 22 ；<br /> <br /> 只读属性unsigned short fontColor；<br /> 只读属性unsigned short backgroundColor；<br /> 只读属性unsigned short fillColor；<br /> 只读属性不带符号的短edgeColor；<br /> <br /> //大小<br /> const unsigned short SIZE_DEFAULT = 0 ；<br /> const unsigned short SIZE_SMALL = 1 ；<br /> const unsigned short SIZE_MEDIUM = 2 ；<br /> const unsigned short SIZE_LARGE = 3 ；<br /> <br /> 只读属性无符号短大小；<br /> <br /> //字体边缘<br /> const unsigned short FONT_EDGE_DEFAULT = 0 ；<br /> const unsigned short FONT_EDGE_NONE = 1 ；<br /> const unsigned short FONT_EDGE_RAULED = 2 ；<br /> const unsigned short FONT_EDGE_DEPRESSED = 3 ；<br /> const unsigned short FONT_EDGE_UNIFORM = 4 ；<br /> const unsigned short FONT_EDGE_DROP_SHADOW_LEFT = 5 ；<br /> const unsigned short FONT_EDGE_DROP_SHADOW_RIGHT = 6 ；<br /> 只读属性unsigned short fontEdge；<br /> <br /> //字体<br /> const unsigned short FONT_DEFAULT = 0 ；<br /> const unsigned short FONT_MONOSPACE_WITH_SERIFS = 1 ；<br /> const unsigned short FONT_PROPORTIONAL_WITH_SERIFS = 2 ；<br /> const unsigned short FONT_MONSPACE_WITHOUT_SERIFS = 3 ；<br /> const unsigned short FONT_CASUAL = 4 ；<br /> const unsigned short FONT_CURSIVE = 5 ；<br /> const unsigned short FONT_SMALL_CAPTINGS = 6 ；<br /> 只读属性无符号短字体；<br /> 只读属性unsigned short fontOpacity；<br /> 只读属性无符号短背景不透明度；<br /> 只读属性无符号短填充不透明度；<br /> 只读属性不带符号的短DEFAULT_OPACITY；<br /> }；</p> </td> 
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
   <td><p>界面MediaPlayerItemLoader：<br /> {<br /> void load(MediaResource资源， long resourceId，<br /> ItemLoaderListener侦听器， <br /> MediaPlayerItemConfig) ；<br /> 撤消取消()；<br /> 只读属性MediaPlayerItem currentItem；<br /> }；</p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
  <tr> 
   <td><p>接口ItemLoaderListener<br /> {<br /> //onLoadCompleteCallbackFunc(MediaPlayerItem)<br /> var onLoadCompleteCallbackFunc；<br /> //onErrorCallbackFunc(PSDKErrorCode)<br /> var onErrorCallbackFunc；<br /> }</p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
 </tbody> 
</table>

## 针对2.0的媒体特征API元素更改 {#media-characteristics-api-element-changes-for}

下表比较了1.3和2.0版本之间C++ TVSDK的媒体特征API元素。

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
   <td><p>界面MediaPlayerItem {<br /> 只读属性MediaResource；<br /> 只读属性long resourceId；<br /> 只读属性布尔值live；<br /> <br /> 只读属性布尔值hasAlternateAudio；<br /> 只读属性AudioTrackList audioTracks；<br /> 只读属性AudioTrack selectedAudioTrack；<br /> void selectAudioTrack(AudioTrack track)； <br /> <br /> 只读属性布尔值hasClosedCaptions；<br /> 只读属性ClosedCaptionsTrackList closedCaptionsTracks；<br /> 只读属性ClosedCaptionsTrack selectedClosedCaptionsTrack；<br /> void selectClosedCaptionsTrack(<br /> ClosedCaptionsTrack)； <br /> <br /> 只读属性布尔值hasTimedMetadata；<br /> 只读属性TimedMetadataList timedMetadata；<br /> 只读属性布尔动态；<br /> <br /> 只读属性布尔值isProtected；<br /> 只读属性DRMetadataInfoList drmMetadataInfos；<br /> 只读属性ProfileList配置文件；<br /> 只读属性Profile selectedProfile；<br /> <br /> 只读属性boolean trickPlaySupported；<br /> 只读属性FloatArray availablePlaybackRates；<br /> 只读属性浮动selectedPlaybackRate；<br /> <br /> <br /> 只读属性MediaPlayer mediaPlayer；<br /> 只读属性MediaPlayerItemConfig；<br /> }；</p> </td> 
   <td><p>界面MediaPlayerItem {<br /> 只读属性MediaResource；<br /> 只读属性long resourceId；<br /> 只读属性布尔值live；<br /> <br /> 只读属性布尔值hasAlternateAudio；<br /> 只读属性AudioTrackList audioTracks；<br /> 属性AudioTrack selectedAudioTrack；<br /> <br /> <br /> 只读属性布尔值hasClosedCaptions；<br /> 只读属性ClosedCaptionsTrackList ccTrack；<br /> 属性ClosedCaptionsTrack selectedCCTrack；<br /> <br /> <br /> <br /> 只读属性布尔值hasTimedMetadata；<br /> 只读属性TimedMetadataList timedMetadata；<br /> 只读属性布尔动态；<br /> <br /> 只读属性布尔值isProtected；<br /> 只读属性DRMetadataInfoList drmMetadataInfos；<br /> 只读属性ProfileList配置文件；<br /> <br /> <br /> 只读属性boolean trickPlaySupported；<br /> 只读属性Int32Array availablePlaybackRates；<br /> <br /> 只读属性StringList adTags；<br /> <br /> 只读属性MediaPlayer mediaPlayer；<br /> <br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### Track / AudioTrack / ClosedCaptionsTrack {#track-audiotrack-closedcaptionstrack}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td><p>界面跟踪<br /> {<br /> 只读属性DomString名称；<br /> 只读属性DomString语言；<br /> 只读属性布尔默认值；<br /> 只读属性布尔值autoSelect；<br /> }； </p> </td> 
   <td>2.0的新增功能</td> 
  </tr> 
  <tr> 
   <td><p>interface AudioTrack ：跟踪<br /> {<br /> 只读属性DomString name； //FromTrack<br /> 只读属性DomString语言；//FromTrack<br /> 只读属性布尔值默认值；//从跟踪<br /> 只读属性布尔值autoSelect；//FromTrack<br /> <br /> 只读属性unsigned int pid；<br /> }；</p> </td> 
   <td><p>界面AudioTrack<br /> {<br /> 只读属性DomString名称；<br /> 只读属性DomString语言； <br /> 只读属性布尔默认值；<br /> 只读属性布尔值autoSelect；<br /> 强制只读属性布尔值；<br /> <br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td>2.0无更改</td> 
   <td><p>接口AudioTrackList<br /> {<br /> 只读属性无符号长长度；<br /> getter AudioTrack （无符号长索引）；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><p>界面ClosedCaptionsTrack ： Track<br /> {<br /> 只读属性DomString name； //FromTrack<br /> 只读属性DomString语言；//FromTrack<br /> 只读属性布尔值默认值；// FromTrack<br /> 只读属性布尔值autoSelect；//FromTrack<br /> <br /> <br /> const unsigned short SERVICE_608_CAPTIONS = 0；<br /> const unsigned short SERVICE_708_CAPTIONS = 1；<br /> const unsigned short SERVICE_WEB_VTT_CAPTIONS = 2；<br /> 只读属性unsigned short serviceType；<br /> 强制只读属性布尔值；<br /> }；</p> </td> 
   <td><p>界面ClosedCaptionsTrack<br /> {<br /> 只读属性DomString名称；<br /> 只读属性DomString语言；<br /> 只读属性布尔默认值；<br /> <br /> <br /> 只读属性布尔值处于活动状态；<br /> <br /> <br /> <br /> <br /> <br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td>2.0无更改</td> 
   <td><p>界面ClosedCaptionsTrackList<br /> {<br /> 只读属性无符号长长度；<br /> getter ClosedCaptionsTrack（无符号长索引）；<br /> }；</p> </td> 
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
   <td>配置文件：2.0无更改</td> 
   <td><p>接口配置文件<br /> {<br /> 只读属性unsigned int width；<br /> 只读属性unsigned int height；<br /> readonly attribute unsigned int bitRate；<br /> }； </p> </td> 
  </tr> 
  <tr> 
   <td>ProfileList： 2.0无更改</td> 
   <td><p>接口ProfileList<br /> {<br /> 只读属性无符号长长度；<br /> getter配置文件（无符号长索引）；<br /> }；</p> </td> 
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
   <td><strong>DRMMetadataInfo</strong>：2.0无更改</td> 
   <td><p>接口DRMetadataInfo<br /> { <br /> 只读属性DRMMetadata元数据；<br /> 只读属性long prefetchTimestamp；<br /> 只读属性TimeRange timeRange；<br /> }；</p> </td> 
  </tr> 
  <tr> 
   <td><strong>DRMMetadataInfoList</strong>：2.0无更改</td> 
   <td><p>接口DRMMetadataInfoList<br /> {<br /> 只读属性无符号长长度；<br /> getter DRMMetadataInfo（无符号长索引）；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

## 将C++错误映射到不同语言中的例外 {#mapping-c-errors-to-exceptions-in-different-languages}

您可以将C++错误代码映射到不同语言的异常。

C++ PSDK在其API中具有“no throw”策略。 大多数API方法会返回PSDKErrorCode值以指示是否已成功执行方法。 通过错误事件通知异步错误。

ActionScript和JAVA PSDK具有不同的策略。 大多数错误都将引发ArgumentError或IllegalStateException以指示无法执行方法的同步部分。 不会捕获这些异常，应用程序代码负责处理异常。 它们通常包含有关方法调用失败原因的有用信息。 例如，如果在无效状态下调用prepareToPlay命令，则会引发以下异常：

```shell
throw new IllegalStateException("Invalid player state. prepareToPlay method 
must be called only once after replaceCurrentItem or replaceCurrentResource method.");
```

ActionScript/JAVA还会从构造函数中引发异常，以指示某些内部对象创建不正确。 这些异常在内部处理，不会传播到应用程序。 异常将包含在发送给应用程序的警告通知中

例如，如果没有为接收的广告响应找到有效的媒体文件，则无法创建有效的广告资源对象或广告。 因此，时间轴上不会放置任何广告，并且会调度NotificationEvent.OperationFailed通知。

从Adobe视频引擎(AVE)异步接收的错误或警告代码将作为正常事件调度到应用程序。 通知事件包含收到的所有错误代码和任何其他元数据，例如URL、资源标识符、句柄等。 如果错误严重，无法继续播放当前媒体，则MediaPlayer将转换为ERROR状态，并调度onStatusChanged回调或MediaPlayerStatusChanged.STATUS_CHANGED事件。 如果可以继续播放，则会调度常规通知事件。

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
   <td>代码= 1、描述= "INVALID_ARGUMENT"和additionalInfo=时出现异常 &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNullPoint</td> 
   <td> </td> 
   <td>IllegalArgumentException</td> 
   <td>参数错误</td> 
   <td>代码= 2、描述=“GENERIC_ERROR”和additionalInfo=时出现异常 &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECIllegalState</td> 
   <td> </td> 
   <td>IllegalstateException</td> 
   <td>IllegalstateException</td> 
   <td>出现异常，代码= 3，描述= "ILLEGAL_STATE"，additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInterfaceNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>代码= 4、描述=“GENERIC_ERROR”和additionalInfo=时出现异常 &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCreationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外情况，代码= 5，描述= "CREATION_FAILED"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedOperation</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外情况，代码= 5，描述= "CREATION_FAILED"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECDataNotAvailable</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外，代码为7，说明为“DATA_NOT_AVAILABLE”，其他信息为 &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECSeekError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>异常代码= 8，描述= "SEEK_ERROR"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECUnsupportedFeature</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>异常代码= 9，描述=“UNSUPPORTED_FEATURE”和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECRangeError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外，代码为10，说明为“RANGE_ERROR”，其他信息为 &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECCodecNotSupported</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外情况，代码= 11，说明= "CODEC_NOT_SUPPORTED"，additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECMmediaError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外情况，代码= 12，描述=“MEDIA_ERROR”和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNetworkError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>异常代码= 13，描述=“NETWORK_ERROR”和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECGenericError</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Error或MediaPlayerNotification.Warning</td> 
   <td>MediaError或NotificationEvent</td> 
   <td>出现异常，代码为14，说明为“GENERIC_ERROR”，其他信息为 &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECInvalidSeekTime</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>出现异常，代码为15，说明为“INVALID_SEEK_TIME”，其他信息为 &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAudioTrackError</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>例外情况，代码= 16，描述= "AUDIO_TRACK_ERROR"和additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAccessFromDifferent<p>线程错误</p> </td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>出现异常，代码为17，说明为“GENERIC_ERROR”，其他信息为 &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECElementNotFound</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>出现异常，代码为18，说明为“GENERIC_ERROR”，其他信息为 &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNotImplemented</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>出现异常，代码为19，说明为“GENERIC_ERROR”，其他信息为 &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECPlaybackOperationFailed</td> 
   <td> </td> 
   <td>-</td> 
   <td>-</td> 
   <td>出现异常，代码为200，描述为“PLAYBACK_OPERATION_FAILED”且additionalInfo= &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECNativeWarning</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>通知事件</td> 
   <td>例外，代码为201，说明为“NATIVE_WARNING”，其他信息为 &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
  <tr> 
   <td>kECAdResolverFailed</td> 
   <td> </td> 
   <td>MediaPlayerNotification.Warning</td> 
   <td>-</td> 
   <td>出现异常，代码为202，说明为“AD_RESOLVER_FAILED”，其他信息为 &lt;as passed="" by="" method="" which="" threw="" this="" exception=""&gt;</td> 
  </tr> 
 </tbody> 
</table>

## 针对2.0的实用程序和帮助程序API元素更改 {#utility-and-helper-api-element-changes-for}

这些表比较了版本1.3和2.0中JavaScript TVSDK的实用程序和帮助程序API元素。

本主题中的表：

* 版本
* 时间范围
* QOSProviser
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
   <td><p>界面版本<br /> {<br /> 只读属性DomString版本；<br /> 只读属性DomString描述；<br /> 只读属性长主；<br /> 只读属性long minor；<br /> 只读属性长修订；<br /> 只读属性long apiVersion；<br /> }；</p> </td> 
   <td><p>界面版本<br /> {<br /> 只读属性DomString版本；<br /> 只读属性DomString描述；<br /> 只读属性DomString major；<br /> 只读属性DomString minor；<br /> 只读属性DomString revision；<br /> 只读属性DomString apiVersion；<br /> }；</p> </td> 
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
   <td>2.0无更改</td> 
   <td><p>接口TimeRange<br /> {<br /> 只读属性unsigned long begin；<br /> 只读属性无符号长端；<br /> 只读属性无符号长持续时间；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

### QOSProviser {#qosprovider}

<table> 
 <tbody> 
  <tr> 
   <th>2.0 API</th> 
   <th>1.3 API</th> 
  </tr> 
  <tr> 
   <td>2.0无更改</td> 
   <td><p>接口QOSProvider<br /> {<br /> void attachMediaPlayer(MediaPlayer)；<br /> void detachMediaPlayer()；<br /> <br /> 只读属性DeviceInformation deviceInformation；<br /> 只读属性PlaybackInformation playbackInformation；<br /> }；</p> </td> 
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
   <td><p>接口设备信息<br /> {<br /> 只读属性DomString os；<br /> <br /> <br /> <br /> 只读属性DomString ID；<br /> 只读属性int densityDPI；<br /> 只读属性int heightPixels；<br /> 只读属性int widthPixels；<br /> 只读属性boolean seekToKeyFrame；<br /> }；</p> </td> 
   <td><p>接口设备信息<br /> {<br /> 只读属性DomString os；<br /> 只读属性int sdk；<br /> 只读属性DomString模型；<br /> 只读属性DomString制造商；<br /> 只读属性DomString ID；<br /> 只读属性int densityDPI；<br /> 只读属性int heightPixels；<br /> 只读属性int widthPixels；<br /> <br /> }；</p> </td> 
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
   <td>2.0无更改</td> 
   <td><p>接口LoadInfo<br /> {<br /> 只读属性DomString url；<br /> 只读属性int大小；<br /> 只读属性double downloadDuration；<br /> 只读属性int periodIndex；<br /> 只读属性double mediaDuration；<br /> 只读属性短TRACK_TYPE_FRAGMENT；<br /> 只读属性简短TRACK_TYPE_TRACK；<br /> 只读属性短TRACK_TYPE_MANIFEST；<br /> 只读属性短类型；<br /> 只读属性DomString trackName；<br /> 只读属性DomString trackType；<br /> 只读属性int trackIndex；<br /> }；</p> </td> 
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
   <td>2.0无更改</td> 
   <td><p>界面视图<br /> {<br /> 只读属性不带符号的短x；<br /> 只读属性不带符号的短y；<br /> 只读属性不带符号的短宽度；<br /> 只读属性不带符号的短高度；<br /> <br /> void setSize（无符号短宽度，无符号短高度）；<br /> void setPos(unsigned short x， unsigned short y)；<br /> }</p> </td> 
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
   <td><p>界面PlaybackInformation<br /> {<br /> 只读属性double timeToFirstByte；<br /> 只读属性double timeToLoad；<br /> 只读属性double timeToStart；<br /> 只读属性double timeToFail；<br /> readonly attribute int totalSecondsPlayed；<br /> 只读属性int totalSecondsSpent；<br /> 只读属性double frameRate；<br /> 只读属性int droppedFrameCount；<br /> 只读属性int感知带宽；<br /> 只读属性int bitrate；<br /> 只读属性double bufferTime；<br /> 只读属性int bufferLength；<br /> 只读属性int emptyBufferCount；<br /> 只读属性double bufferingTime；<br /> }；</p> </td> 
   <td><p>界面PlaybackInformation<br /> {<br /> 只读属性double timeToFirstByte；<br /> 只读属性double timeToLoad；<br /> 只读属性double timeToStart；<br /> 只读属性double timeToFail；<br /> readonly attribute int totalSecondsPlayed；<br /> 只读属性int totalSecondsSpent；<br /> 只读属性double frameRate；<br /> 只读属性int droppedFrameCount；<br /> <br /> 只读属性int bitrate；<br /> 只读属性double bufferTime；<br /> 只读属性int bufferLength；<br /> 只读属性int emptyBufferCount；<br /> 只读属性double bufferingTime；<br /> }；</p> </td> 
  </tr> 
 </tbody> 
</table>

## 有用资源 {#helpful-resources}

* 请参阅完整的帮助文档，网址为 [Adobe Primetime学习与支持](https://helpx.adobe.com/support/primetime.html) 页面。
