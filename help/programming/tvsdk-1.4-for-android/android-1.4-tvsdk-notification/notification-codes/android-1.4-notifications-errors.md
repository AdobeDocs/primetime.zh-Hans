---
description: 此表提供有关ERROR类型通知的详细信息。
title: 错误通知代码
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '615'
ht-degree: 4%

---

# 错误通知代码{#error-notification-codes}

此表提供有关ERROR类型通知的详细信息。

<!--<a id="section_D29404228F5E4B818642CBA6A0D39546"></a>-->

大多数错误都包含相关元数据，例如，无法下载的资源的URL。 某些通知包含元数据，用于指定问题出现在主视频内容、备用音频内容还是广告中。

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
   <td colname="4"><span class="codeph"> 描述</span> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101004 </span> </td> 
   <td colname="2"><span class="codeph"> CONTENT_ERROR</span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR</span> </td> 
   <td colname="4"> </td> 
   <td colname="5"> 下载片段或区段（视频和音频）时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101008 </span> </td> 
   <td colname="2"><span class="codeph"> SEEK_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_Code </span><span class="codeph"> DESIRED_SEEK_POSITION </span><span class="codeph"> DESIRED_SEEK_PERIOD </span> </td> 
   <td colname="5"> 执行搜寻操作时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101009 </span> </td> 
   <td colname="2"><span class="codeph"> PAUSE_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 描述</span> </td> 
   <td colname="5"> 执行暂停操作时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101102 </span> </td> 
   <td colname="2"><span class="codeph"> PERIOD_INFO_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 描述 </span> </td> 
   <td colname="5"> 检索有关内容时段的信息时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101103 </span> </td> 
   <td colname="2"><span class="codeph"> RETRIEVE_TIME_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 描述 </span> </td> 
   <td colname="5"> 尝试检索播放位置时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 101104 </span> </td> 
   <td colname="2"><span class="codeph"> GET_QOS_DATA_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 描述 </span> </td> 
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
   <td colname="4"><span class="codeph"> 描述 </span><span class="codeph"> 资源 </span> </td> 
   <td colname="5"> 加载资源项时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 102101 </span> </td> 
   <td colname="2"><span class="codeph"> RESOURCE_PLACEMENT_失败 </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> CONTENT_ID </span> </td> 
   <td colname="5"> 将资源放在播放时间轴上时出错。 </td> 
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
   <td colname="3"><span class="codeph"> AD_METADATA_INVALID </span><span class="codeph"> AD_RESOLVER_INITIALIZATION_FAIL </span><span class="codeph"> AD_RESOLVER_RESOLVE_FAIL </span><span class="codeph"> AD_RESOLVER_SERVER_UNREACHABLE </span> </td> 
   <td colname="4"> 无 </td> 
   <td colname="5"> 无 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104001 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_METADATA_无效 </span> </td> 
   <td colname="3"> <p>无 </p> </td> 
   <td colname="4"><span class="codeph"> 描述</span> </td> 
   <td colname="5"> 由于广告元数据格式无效，广告解析失败。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104003 </span> </td> 
   <td colname="2"><span class="codeph"> AD_RESOLVER_RESOLVE_失败 </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> NATIVE_ERROR_Code </span> </td> 
   <td colname="5"> 广告插件未能解析广告。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 104005 </span> </td> 
   <td colname="2"><span class="codeph"> AD_INSERTION_FAIL </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> PROPOSED_AD_BREAK</span> </td> 
   <td colname="5"> 广告解析阶段失败。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>原生</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106000 </span> </td> 
   <td colname="2"><span class="codeph"> NATIVE_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"> <span class="codeph"> NATIVE_ERROR_Code </span> <span class="codeph"> 本机错误名称 </span> <span class="codeph"> 描述 </span> <span class="codeph"> 描述</span> <p><b>DRM详细信息：</b> </p> <span class="codeph"> DRM_ERROR_STRING</span> <span class="codeph"> NATIVE_SUBERROR_CODE</span> </td> 
   <td colname="5"> <p>低级AVE库发出错误。 </p> <p>请参阅 <a href="../../../tvsdk-1.4-for-android/android-1.4-tvsdk-notification/notification-codes/native-error-summary/android-1.4-native-error-summary.md" format="html" scope="external"> NATIVE_ERROR通知的详细信息</a> 以了解有关这些元数据键值的信息。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106001 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_CREATION_错误 </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 描述 </span> </td> 
   <td colname="5"> 实例化AVE低级库时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106002 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RELEASE_错误 </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 描述 </span> </td> 
   <td colname="5"> 发布AVE低级库时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106003 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESOURCES_ RELEASE_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 描述 </span> </td> 
   <td colname="5"> 释放AVE库使用的GPU资源时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106004 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_RESET_ERROR </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 描述 </span> </td> 
   <td colname="5"> 重置AVE库时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 106005 </span> </td> 
   <td colname="2"><span class="codeph"> ENGINE_SET_视图错误 </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 描述</span> </td> 
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
   <td colname="4"><span class="codeph"> 描述数量 </span> </td> 
   <td colname="5"> 尝试设置卷级别时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107001 </span> </td> 
   <td colname="2"><span class="codeph"> SET_BUFFER_TIME_错误 </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 描述 </span><span class="codeph"> PLAY_BUFFER_TIME </span> </td> 
   <td colname="5"> 尝试更改缓冲参数时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107002 </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_VISIBILITY_错误 </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 描述</span> </td> 
   <td colname="5"> 尝试更改CC磁道的可见性时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107003 </span> </td> 
   <td colname="2"><span class="codeph"> SET_CC_STYLING_错误 </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 描述</span> </td> 
   <td colname="5"> 尝试更改CC磁道的样式选项时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107004 </span> </td> 
   <td colname="2"><span class="codeph"> SET_ABR_PARAMETERS_错误 </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 描述 </span> </td> 
   <td colname="5"> 尝试更改ABR控制参数时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 107005 </span> </td> 
   <td colname="2"><span class="codeph"> SET_BUFFER_参数_错误 </span> </td> 
   <td colname="3"> 无 </td> 
   <td colname="4"><span class="codeph"> 描述 </span><span class="codeph"> INITIAL_BUFFER_TIME </span><span class="codeph"> PLAY_BUFFER_TIME </span> </td> 
   <td colname="5"> 尝试更改缓冲控制参数时出错。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><b>备用音频</b> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"> 109000 </span> </td> 
   <td colname="2"><span class="codeph"> AUDIO_TRACK_ERROR </span> </td> 
   <td colname="3"><span class="codeph"> DOWNLOAD_ERROR </span> </td> 
   <td colname="4"><span class="codeph"> AUDIO_TRACK名称 </span><span class="codeph"> AUDIO_TRACK_LANGUAGE </span> </td> 
   <td colname="5"> 发生与音轨相关的错误。 </td> 
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
   <td colname="5"> 标记一般错误事件。 不是由TVSDK实际颁发的。 这只是一个标记，表示与TVSDK错误事件对应的数字代码范围的结尾。 </td> 
  </tr> 
 </tbody> 
</table>
