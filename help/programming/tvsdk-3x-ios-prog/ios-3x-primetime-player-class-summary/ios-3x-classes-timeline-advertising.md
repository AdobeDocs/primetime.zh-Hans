---
description: 这些类提供有关在时间轴中发生的广告的信息。
seo-description: 这些类提供有关在时间轴中发生的广告的信息。
seo-title: 时间轴广告课程
title: 时间轴广告课程
uuid: df970e8f-4bf8-4367-9d70-42ebcb11c025
translation-type: tm+mt
source-git-commit: 557f42cd9a6f356aa99e13386d9e8d65e043a6af

---


# 时间轴广告课程 {#timeline-advertising-classes}

这些类提供有关在时间轴中发生的广告的信息。

<table frame="all" colsep="1" rowsep="1" id="table_1A59E777BA99466793D586286F19E933"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"><b>名称</b></th> 
   <th colname="2" class="entry"><b>说明</b></th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAd.html" format="html" scope="external"> PTAd</a> </td> 
   <td colname="2">定义广告抽象并包含所有广告信息的类。 它由唯一ID、持续时间和MediaResource定义。 MediaResource包含实际广告内容所在的URL。 
    <ph>
      表示与内容拼接的主线性资源。 它可以选择包含必须与线性资产一起显示的配套资产数组。
    </ph> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdAsset.html" format="html" scope="external"> PTAdAsset</a> </td> 
   <td colname="2">表示要显示的资产的类。 
    <ph>
      表示要显示的资产。
    </ph> 
    <ph>
      表示广告资产的类。
    </ph> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBannerView.html" format="html" scope="external"> PTAdBannerView</a> </td> 
   <td colname="2">
    <ph>
      显示横幅资产。 应用程序必须创建此实用程序类的新实例，设置横幅资源，然后将其添加到视图。 此类在内部管理横幅的印象和点击跟踪。
    </ph> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBreak.html" format="html" scope="external"> PTAdBreak</a> </td> 
   <td colname="2">一个类，该类统一了将在播放期间某个点播放的多个广告。 
    <ph>
      表示拼接到内容中的连续广告序列。
    </ph> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdClick.html" format="html" scope="external"> PTAdClick</a> </td> 
   <td colname="2">表示与资产关联的单击实例的类。 此实例包含有关点进URL和标题的信息，这些信息可用于向用户提供其他信息。 
    <ph>
      表示与资产关联的单击实例。 此实例包含有关点进URL和标题的信息，这些信息可用于向用户提供其他信息。
    </ph> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdPolicyInfo.html" format="html" scope="external"> PTAdPolicyInfo</a> </td> 
   <td colname="2"> 定义AdPolicySelector API调用属性的协议。 这些属性提供了用于强制实施每个广告行为的上下文。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTAdPolicySelector.html" format="html" scope="external">PTAdPolicySelector</a></td> 
   <td colname="2"> 用于实施广告行为的广告策略选择器协议。 应用程序可以通过实现所有必需的方法或通过扩展现有的默认策略选择器类来自定义特定行为，来符合本协议。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdTimeline.html" format="html" scope="external">PTAdTimeline</a></td> 
   <td colname="2"> 表示内容中分段时间轴的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 
    <ph>
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTContentResolver.html" format="html" scope="external"> PTContentResolver类</a> , <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> 协议
    </ph> </td> 
   <td colname="2"> 处理Adobe Primetime广告决策过程中广告解析部分的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolverDelegate.html" format="html" scope="external"> PTContentResolverDelegate</a> </td> 
   <td colname="2"> 描述自定义内容解析程序( <span class="codeph"> PTContentResolver</span> )用来向委派内容解析状态的方法的协议。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Constants/PTPlacementType.html" format="html" scope="external"> PTPlacementType</a> </td> 
   <td colname="2">可抽象化职位安排信息请求的类。 每个已解析的广告都必须附加一个位置信息。 位置信息描述广告在时间轴上的放置位置。 它包含以下信息： 
    <ul id="ul_A9105A78F0C24488BCD5E3F2EE62A3EE"> 
     <li id="li_01E968A4330D4B40BA1EB6F4A6000FFD">放置位置（毫秒） </li> 
     <li id="li_A3DC9498BEE14FBA9E7A5D26874F3984">放置的类型（前置、中置或后置） </li> 
     <li id="li_4B9094DD318B4792854A377CC6064232">将要替换的主内容块的持续时间 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>