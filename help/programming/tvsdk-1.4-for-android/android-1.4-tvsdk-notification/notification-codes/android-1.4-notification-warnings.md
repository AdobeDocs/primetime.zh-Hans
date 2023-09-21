---
description: 此表证明有关WARN类型通知的详细信息。
title: 警告通知代码
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '407'
ht-degree: 2%

---

# 警告通知代码 {#warning-notification-codes}

此表证明有关WARN类型通知的详细信息。

<!--<a id="section_F25366B6703040E3ADA993C113618F01"></a>-->

大多数警告包含相关元数据，例如下载失败的资源的URL。 某些通知包含元数据，用于指定问题出现在主视频内容、备用音频内容还是广告中。

<table frame="all" colsep="1" rowsep="1" id="table_C24772DF203B4DB2ACE6B475698C4C58"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 代码 </th> 
   <th colname="2" class="entry"> 名称 </th> 
   <th colname="3" class="entry"> InnerNotification </th> 
   <th colname="4" class="entry"> 元数据键 </th> 
   <th colname="5" class="entry"> 评论 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>播放</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 200000 </span> </td> 
   <td colname="2"><span class="codeph"> 回放操作失败(_F) </span> </td> 
   <td colname="3"><span class="codeph"> AUDIO_TRACK_ERROR </span><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="4"><span class="codeph"> 描述 </span> </td> 
   <td colname="5"> <p>与播放相关的操作失败，但播放可能会继续。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>广告解析</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL </span><span class="codeph"> RESOURCE_PLACEMENT_失败 </span><span class="codeph"> AD_RESOLVER_ METADATA_INVALID </span> </td> 
   <td colname="4"> <p>无 </p> </td> 
   <td colname="5"> <p>广告解析程序无法解析/插入广告内容。 可继续播放。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201002</span> </td> 
   <td colname="2"><span class="codeph"> AD_ASSET_ FAILED_TO_LOAD</span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"><span class="codeph"> AD_ASSET， INTERNAL_ERROR</span> </td> 
   <td colname="5"> <p>尝试加载广告创意时出错。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 201003</span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_返回的_NO_ADS</span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"><span class="codeph"> INTERNAL_ERROR， AD_ID，描述</span> </td> 
   <td colname="5"> <p>广告解析失败，因为VAST URL无效或因为VAST包装器未返回任何广告。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>背景清单</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204000 </span> </td> 
   <td colname="2"><span class="codeph"> BACKGROUND_MANIFEST_警告</span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"><span class="codeph"> BACKGROUND_MANIFEST_WARNING_ERROR</span> <span class="codeph"> BACKGROUND_MANIFEST_WARNING_NAME</span> <span class="codeph"> 描述</span> </td> 
   <td colname="5"> <p> 后台清单下载时出错。 更新后台清单时出现的任何问题都会作为TVSDK警告分发，而不会导致播放停止。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 204001 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_SEEK_警告</span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"><span class="codeph"> 描述</span> </td> 
   <td colname="5"> <p> </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>原生</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1" morerows="1"><span class="codeph"> 209100 </span> </td> 
   <td colname="2" morerows="1"><span class="codeph"> NATIVE_WARNING </span> </td> 
   <td colname="3" morerows="1"> <p>无 </p> </td> 
   <td colname="4"><b>AVE</b> <p><span class="codeph"> NATIVE_ERROR_Code </span><span class="codeph"> 本机错误名称 </span><span class="codeph"> 描述 </span> </p> </td> 
   <td colname="5"> <p>低级AVE库发出错误。 </p> <p>请参阅 <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> NATIVE_ERROR通知的详细信息</a> 以了解有关这些元数据字段值的详细信息。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="4"><b>DRM</b> <p><span class="codeph"> NATIVE_SUBERROR_CODE</span> <span class="codeph"> DRM_ERROR_STRING</span> </p> </td> 
   <td colname="5"> DRM次要错误代码和DRM服务器错误字符串。 请参阅 <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> NATIVE_ERROR通知的详细信息</a> 以了解有关这些元数据字段值的详细信息。</td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>TimeRangeCollection</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210000 </span> </td> 
   <td colname="2"><span class="codeph"> 未定义_时间范围 </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"> 无 </td> 
   <td colname="5"> 广告信令模式被定义为自定义范围，但没有定义任何范围。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 210001 </span> </td> 
   <td colname="2"><span class="codeph"> INVALID_TIME_范围 </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"><span class="codeph"> 描述 </span> </td> 
   <td colname="5"> <p> 一个或多个时间范围无效，将被忽略或修改。 </p> <p> DESCRIPTION是一个包含无效范围说明的字符串。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>特技模式</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 280000 </span> </td> 
   <td colname="2"><span class="codeph"> TRICKPLAY_RATE_更改_失败</span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"><span class="codeph"> 描述</span> </td> 
   <td colname="5"> <p> 速率更改失败。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>通用</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 299999 </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_WARNING </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"> <p>无 </p> </td> 
   <td colname="5"> <p>标记一般警告事件。 不是由TVSDK实际颁发的。 它只是对应于警告事件的数字代码范围的结束标记。 </p> </td> 
  </tr> 
 </tbody> 
</table>

>[注意！] 通过通知元数据中的PTAdAsset，可以检索adID和源(URL)，并使用 `AD_ASSET` 键。
