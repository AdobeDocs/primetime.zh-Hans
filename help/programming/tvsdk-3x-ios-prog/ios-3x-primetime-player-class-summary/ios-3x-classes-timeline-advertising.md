---
description: 这些类提供有关时间轴内发生的广告的信息。
title: 时间轴广告课程
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '535'
ht-degree: 0%

---


# 时间轴广告类{#timeline-advertising-classes}

这些类提供有关时间轴内发生的广告的信息。

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
    <pre>
      表示与内容拼接的主线性资源。 它可以选择包含必须与线性资产一起显示的配套资源的数组。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdAsset.html" format="html" scope="external"> PTAdAsset</a> </td> 
   <td colname="2">表示要显示的资产的类。 
    <pre>
      表示要显示的资产。
    </pre> 
    <pre>
      表示广告资产的类。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBannerView.html" format="html" scope="external"> PTAdBannerView</a> </td> 
   <td colname="2">
    <pre>
      显示横幅资源。 您的应用程序必须创建此实用程序类的新实例，设置横幅资源，并将其添加到视图。 横幅的印象和点击跟踪由此类在内部管理。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBreak.html" format="html" scope="external"> PTAdBreak</a> </td> 
   <td colname="2">在播放过程中某个点将播放的多个广告上提供统一视图的类。 
    <pre>
      表示拼接到内容中的连续广告序列。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdClick.html" format="html" scope="external"> PTAdClick</a> </td> 
   <td colname="2">表示与资产关联的单击实例的类。 此实例包含有关点进URL和标题的信息，这些信息可用于向用户提供其他信息。 
    <pre>
      表示与资产关联的单击实例。 此实例包含有关点进URL和标题的信息，这些信息可用于向用户提供其他信息。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdPolicyInfo.html" format="html" scope="external"> PTAdPolicyInfo</a> </td> 
   <td colname="2"> 定义AdPolicySelector API调用属性的协议。 这些属性提供了用于强制实施每个广告行为的上下文。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTAdPolicySelector.html" format="html" scope="external">PTAdPolicySelector</a></td> 
   <td colname="2"> 用于强制广告行为的广告策略选择器协议。 通过实现所有所需的方法或通过扩展现有默认策略选择器类来自定义特定行为，应用程序可以符合此协议。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdTimeline.html" format="html" scope="external">PTAdTimeline</a></td> 
   <td colname="2"> 表示内容中分页时间轴的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 
    <pre>
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTContentResolver.html" format="html" scope="external"> PTContentResolverclass </a> 、PTContentResolver 
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolver.html" format="html" scope="external"> </a> 协议
    </pre> </td> 
   <td colname="2"> 在Adobe Primetime广告决策过程中处理广告解析部分的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolverDelegate.html" format="html" scope="external"> PTContentResolverDelegate</a> </td> 
   <td colname="2"> 描述自定义内容解析程序(<span class="codeph"> PTContentResolver</span>)用来向委派内容解析状态的方法的协议。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Constants/PTPlacementType.html" format="html" scope="external"> PTPlacementType</a> </td> 
   <td colname="2">抽象版面信息请求的类。 每个已解析的广告都必须附加一个位置信息。 版面信息描述广告在时间轴上的放置位置。 它包含以下信息： 
    <ul id="ul_A9105A78F0C24488BCD5E3F2EE62A3EE"> 
     <li id="li_01E968A4330D4B40BA1EB6F4A6000FFD">位置（毫秒） </li> 
     <li id="li_A3DC9498BEE14FBA9E7A5D26874F3984">放置的类型（前滚、中滚或后滚） </li> 
     <li id="li_4B9094DD318B4792854A377CC6064232">将要替换的主内容块的持续时间 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>