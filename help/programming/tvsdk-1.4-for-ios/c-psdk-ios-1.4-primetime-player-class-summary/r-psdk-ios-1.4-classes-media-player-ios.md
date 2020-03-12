---
description: 这些类描述您的媒体播放器及其资源。
seo-description: 这些类描述您的媒体播放器及其资源。
seo-title: 媒体播放器类
title: 媒体播放器类
uuid: 6b59dcff-9722-4a84-9049-f6f10f7b3e82
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68

---


# 媒体播放器类 {#media-player-classes}

您可以使用Primetime Player Objective-C API自定义播放器的行为。

这些类描述您的媒体播放器及其资源。

<table frame="all" colsep="1" rowsep="1" id="table_bm2_wl2_2m"> 
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><b>类</b> </td> 
   <td colname="2"><b>说明</b> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTABRControlParameters.html" format="html" scope="external"> PTABRControlParameters</a></span> </td> 
   <td colname="2">封装所有自适应比特率控制参数。 支持的参数有： 
    <ul id="ul_pnh_hm2_2m"> 
     <li id="li_46572FE1EB514AFF8C9F731E44DAF30B"><span class="codeph"> minBitRate</span> </li> 
     <li id="li_A10C75C9A5234241A5B84A4139F4D143"><span class="codeph"> maxBitRate</span> </li> 
     <li id="li_4E77E367A2E848D2B3E1A9C52209A7B2"><span class="codeph"> initialBitRate</span> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTDefaultMediaPlayerClientFactory.html" format="html" scope="external"> PTDefaultMediaPlayerClientFactory</a></span> </td> 
   <td colname="2"> 在TVSDK中默 <span class="codeph"> 认实现PTMediaPlayerClientFactory</span> 。 它提供可用的 <span class="codeph"> PTOpportunityResolver</span>、 <span class="codeph"> PTContentResolver</span>和 <span class="codeph"></span> PTAdPolicySelector实例。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayer.html" format="html" scope="external"> PTMediaPlayer</a></span> </td> 
   <td colname="2">定义Primetime Player框架的根组件。 <p>应用程序创建此类的实例以播放媒体。 此组件会发送通知，让应用程序知道播放器在任何给定时间的状态。 </p> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTMediaPlayerClientFactory.html" format="html" scope="external"> PTMediaPlayerClientFactory</a></span> </td> 
   <td colname="2"> 描述自定义媒体播放器客户端工厂应实施的方法以提供可用的 <span class="codeph"> PTOpportunityResolver</span> 、 <span class="codeph"> PTContentResolver</span> 和 <span class="codeph"></span> PTAdPolicySelector实例的协议。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerItem.html" format="html" scope="external"> PTMediaPlayerItem</a></span> </td> 
   <td colname="2"> 表示特定的音频——视频媒体。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaPlayerView.html" format="html" scope="external"> PTMediaPlayerView</a></span> </td> 
   <td colname="2"> 管理Primetime Player框架的视图组件。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaProfile.html" format="html" scope="external"> PTMediaProfile</a></span> </td> 
   <td colname="2"> 表示变体播放列表中单个流的配置文件。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTMediaSelectionOption.html" format="html" scope="external"> PTMediaSelectionOption</a></span> </td> 
   <td colname="2">表示音像媒体资源，以适应不同的语言首选项、辅助功能要求或自定义应用程序配置。 有效的选项类型： 
    <ul id="ul_p2q_gn2_2m"> 
     <li id="li_46BE5AE49732481FB6D336FFF896E5AD">字幕(<span class="codeph"> PTMediaSelectionOptionTypeSubtitle</span>) </li> 
     <li id="li_6CEADCA12D4A48B7AE4A539985F32119">替代音频(<span class="codeph"> PTMediaSelectionOptionTypeAudio</span>) </li> 
     <li id="li_248D3D997F8A4B6E9B48869F84060D1F"> <p>Undefined(<span class="codeph"> PTMediaSelectionOptionTypeUndefined</span>) </p> </li> 
    </ul> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTOpportunityResolver.html" format="html" scope="external"> PTOpportunityResolver类</a> 、 </span> PTOportunityResolver协议 <span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTOpportunityResolver.html" format="html" scope="external"></a></span> </td> 
   <td colname="2"> 用于处理清单内提示的类，这些提示将用作Adobe Primetime广告决策过程的位置。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTOpportunityResolverDelegate.html" format="html" scope="external"> PTOpportunityResolverDelegate</a></span> </td> 
   <td colname="2"> 描述自定义业务机会解析程序( <span class="codeph"> PTOportunityResolver</span> )应使用的方法来向委托通信业务机会解析状态的协议。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTSDK.html" format="html" scope="external"> PTSDK</a></span> </td> 
   <td colname="2"> 介绍TVSDK的版本及其功能。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTSDKConfig.html" format="html" scope="external"> PTSDKConfig</a></span> </td> 
   <td colname="2"> 公开TVSDK全局设置并允许应用程序订阅自定义HLS标记。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><span class="codeph"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTTextStyleRule.html" format="html" scope="external"> PTTextStyleRule</a></span> </td> 
   <td colname="2"> 定义表示构成规则字典的文本样式属性键的常量。 </td> 
  </tr> 
 </tbody> 
</table>

