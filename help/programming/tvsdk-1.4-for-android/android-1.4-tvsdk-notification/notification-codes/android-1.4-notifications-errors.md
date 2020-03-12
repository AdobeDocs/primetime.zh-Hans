---
description: 此表提供了有关ERROR类型通知的详细信息。
seo-description: 此表提供了有关ERROR类型通知的详细信息。
seo-title: 错误通知代码
title: 错误通知代码
uuid: cc21473d-924e-475d-96ea-352233f664ef
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

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
   <td colname="1"><b>播放</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101000 </span> </td> 
   <td colname="2"><span class="codeph"> PLAYBACK_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明</span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101004 </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="4"> </td> 
   <td colname="5"> 下载片段或段（视频和音频）时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE </span><span class="codeph"> DESIRED_SEEK_POSITION </span><span class="codeph"> DESIRED_SEEK_PERIOD </span> </td> 
   <td colname="5"> 执行搜索操作时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009 </span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明</span> </td> 
   <td colname="5"> 执行暂停操作时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101102 </span> </td> 
   <td colname="2"><span class="codeph"> PERIOD_INFO_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> 检索有关内容句点的信息时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101103 </span> </td> 
   <td colname="2"><span class="codeph"> RETRIEVE_TIME_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> 尝试检索播放位置时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101104 </span> </td> 
   <td colname="2"><span class="codeph"> GET_QOS_DATA_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> 尝试检索QOS信息时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101200 </span> </td> 
   <td colname="2"><span class="codeph"> DOWNLOAD_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> URL </span> </td> 
   <td colname="5"> 尝试下载数据时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>资源无效</b> </td> 
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
   <td colname="5"> 加载资源项时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102101 </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_PLACEMENT_FAILED </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID </span> </td> 
   <td colname="5"> 将资源放置到播放时间线时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>广告处理</b> </td> 
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
   <td colname="4"><span class="codeph"> 说明</span> </td> 
   <td colname="5"> 由于广告元数据格式无效，广告解析失败。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_CODE </span> </td> 
   <td colname="5"> 广告插件无法解析广告。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> POPSED_AD_BREAK</span> </td> 
   <td colname="5"> 广告解析阶段已失败。 </td> 
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
   <td colname="4"> <span class="codeph"> NATIVE_ERROR_CODE </span> NATIVE_ERROR_NAME说明 <span class="codeph"> 说 </span> 明 <span class="codeph"> 说 </span><span class="codeph"> 明</span> <p><b>DRM详细信息：</b> </p> <span class="codeph"> DRM_ERROR_STRING</span><span class="codeph"> NATIVE_SUBERROR_CODE</span> </td> 
   <td colname="5"> <p>低级AVE库发出错误。 </p> <p>有关 <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> 这些元数据键的值的信息，请参阅NATIVE_ERROR通知的详细信息</a> 。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106001 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_CREATION_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> 实例化AVE低级库时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106002 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RELEASE_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> 释放AVE低级库时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106003 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESOURCES_RELEASE_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> 释放AVE库使用的GPU资源时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106004 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESET_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> 重置AVE库时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106005 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_SET_VIEW_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明</span> </td> 
   <td colname="5"> 将视图附加到AVE库时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>配置</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107000 </span> </td> 
   <td colname="2"><span class="codeph"> SET_VOLUME_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明卷 </span> </td> 
   <td colname="5"> 尝试设置卷级别时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107001 </span> </td> 
   <td colname="2"><span class="codeph"> SET_BUFFER_TIME_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span><span class="codeph"> PLAY_BUFFER_TIME </span> </td> 
   <td colname="5"> 尝试更改缓冲参数时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107002 </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_VISIBILITY_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明</span> </td> 
   <td colname="5"> 尝试更改CC轨道的可见性时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107003 </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_STYLING_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明</span> </td> 
   <td colname="5"> 尝试更改CC音轨的样式选项时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107004 </span> </td> 
   <td colname="2"><span class="codeph"> SET_ABR_PARAMETERS_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说明 </span> </td> 
   <td colname="5"> 尝试更改ABR控制参数时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107005 </span> </td> 
   <td colname="2"><span class="codeph"> SET_BUFFER_PARAMETERS_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 说 </span><span class="codeph"> 明INITIAL_BUFFER_TIME </span><span class="codeph"> PLAY_BUFFER_TIME </span> </td> 
   <td colname="5"> 尝试更改缓冲控制参数时出错。 </td> 
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
   <td colname="5"> 与音轨相关的错误。 </td> 
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
   <td colname="2"><span class="codeph"> GENERIC_ERROR</span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"> 无 </td> 
   <td colname="5"> 标记通用错误事件。 实际上并非由TVSDK发布。 这仅是与TVSDK错误事件对应的数字代码范围末尾的标记。 </td> 
  </tr> 
 </tbody> 
</table>

