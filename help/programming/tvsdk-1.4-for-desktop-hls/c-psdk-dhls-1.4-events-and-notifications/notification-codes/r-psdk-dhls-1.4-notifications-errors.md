---
description: 此表提供了有关ERROR类型通知的详细信息。
seo-description: 此表提供了有关ERROR类型通知的详细信息。
seo-title: 错误通知代码
title: 错误通知代码
uuid: 50624782-3d0b-4ac4-b883-355c1f7e9bff
translation-type: tm+mt
source-git-commit: 91cea7acb8127e02b82e5242b9ad6ab0d12ce0eb

---


# 错误通知代码{#error-notification-codes}

此表提供了有关ERROR类型通知的详细信息。

<!--<a id="section_D29404228F5E4B818642CBA6A0D39546"></a>-->

大多数错误都包含相关元数据，例如，无法下载的资源的URL。 某些通知包含元数据，用于指定问题是在主视频内容、备用音频内容中还是在广告中发生。

<table frame="all" colsep="1" rowsep="1" id="table_8B61210A406A45ACBE37FC29729DDE22"> 
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
   <td colname="1"><b>DRM</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 100000 </span> </td> 
   <td colname="2"><span class="codeph"> DRM_ERROR </span> </td> 
   <td colname="3"> </td> 
   <td colname="4"><span class="codeph"> MAJOR_DRM_CODE </span><span class="codeph"> MINOR_DRM_CODE说 </span><span class="codeph"> 明 </span> </td> 
   <td colname="5">另请参阅106000( <span class="codeph"> NATIVE_ERROR</span>)。
   </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>播放</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_ERROR </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101004 </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_ERROR </span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR </span> </td> 
   <td colname="4"> </td> 
   <td colname="5"> <p>下载片段或段（视频和音频）时出错。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101006 </span> </td> 
   <td colname="2"><span class="codeph"> SECURITY_ERROR </span> </td> 
   <td colname="3"> </td> 
   <td colname="4"><span class="codeph"> URL </span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008</span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"> <span class="codeph"> 说明 </span> </td> 
   <td colname="5"> <p>执行暂停操作时出错。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE </span><span class="codeph"> DESIRED_SEEK_POSITION </span><span class="codeph"> DESIRED_SEEK_PERIOD </span> </td> 
   <td colname="5"> <p>执行搜索操作时出错。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101102 </span> </td> 
   <td colname="2"><span class="codeph"> PERIOD_INFO_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> <p>检索有关内容句点的信息时出错。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101103 </span> </td> 
   <td colname="2"><span class="codeph"> RETRIEVE_TIME_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> <p>尝试检索播放位置时出错。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101104 </span> </td> 
   <td colname="2"><span class="codeph"> GET_QOS_DATA_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> <p>尝试检索QOS信息时出错。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101200 </span> </td> 
   <td colname="2"><span class="codeph"> DOWNLOAD_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> URL </span> </td> 
   <td colname="5"> <p>尝试下载数据时出错。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>资源无效 </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102100 </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_LOAD_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 描述资 </span><span class="codeph"> 源 </span> </td> 
   <td colname="5"> <p>加载资源项时出错。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102101 </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_PLACEMENT_FAILED </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID </span> </td> 
   <td colname="5"> <p>将资源放置到播放时间线时出错。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>广告处理 </b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104000 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_FAIL </span> </td> 
   <td colname="3"><span class="codeph"> AD_METADATA_INVALID </span><span class="codeph"> AD_RESOLVER_INITIALIZATION_FAIL </span><span class="codeph"> AD_RESOLVE_FAIL </span><span class="codeph"> AD_RESOLVER_SERVER_UNREACHABLE </span> </td> 
   <td colname="4"> 无 </td> 
   <td colname="5"> 无 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_无效 </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"> </td> 
   <td colname="5"> <p>由于广告元数据格式无效，广告解析失败。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE </span> </td> 
   <td colname="5"> <p>广告插件无法解析广告。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="3">无</td> 
   <td colname="4"><span class="codeph"> POPSED_AD_BREAK</span> </td> 
   <td colname="5"> <p>广告解析阶段已失败。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104006 </span> </td> 
   <td colname="2"><span class="codeph"> AD_UNREACHABLE </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"> 无 </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>本机</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106000 </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> RUNTIME_CODE</span> _CODE <span class="codeph"> _MESSAGE</span> RESOURCE_URL资源 <span class="codeph"> _TYPE</span><span class="codeph"></span><span class="codeph"> RESOURCE_ID</span> <p><b>DRM详细信息：</b> </p> <span class="codeph"> DRM_ERROR_STRING</span><span class="codeph"> RUNTIME_SUBERROR_CODE</span> </td> 
   <td colname="5"> <p>低级AVE库发出错误。 </p> <p>有关 <a href="../../c-psdk-dhls-1.4-events-and-notifications/notification-codes/c-psdk-dhls-1.4-native-error-summary.md" format="html" scope="external"> 这些元数据键的值的信息，请参阅NATIVE_ERROR通知的详细信息</a> 。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106001 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_CREATION_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> <p>实例化AVE低级库时出错。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106002 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RELEASE_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> <p>释放AVE低级库时出错。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106003 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESOURCES_RELEASE_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> <p>释放AVE库使用的GPU资源时出错。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106004 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESET_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> <p>重置AVE库时出错。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106005 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_SET_VIEW_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> <p>将视图附加到AVE库时出错。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>替代音频</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 109000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_ERROR </span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR </span> </td> 
   <td colname="4"><span class="codeph"> AUDIO_TRACK_NAME </span><span class="codeph"> AUDIO_TRACK_LANGUAGE </span> </td> 
   <td colname="5"> <p>与音轨相关的错误。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>通用</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"><span class="codeph"> 199999 </span> </td> 
   <td colname="2"><span class="codeph"> GENERIC_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"> 无 </td> 
   <td colname="5"> <p>标记通用错误事件。 实际上并非由TVSDK发布。 它只是与TVSDK错误事件对应的数字代码范围的结尾的标记。 </p> </td> 
  </tr> 
 </tbody> 
</table>

