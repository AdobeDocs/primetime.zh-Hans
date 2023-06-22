---
description: 这些类提供有关时间轴内发生的广告的信息。
title: 时间轴广告类
exl-id: 004c706a-55cc-446a-93b1-c5c7c011ba42
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '515'
ht-degree: 0%

---

# 时间轴广告类{#timeline-advertising-classes}

这些类提供有关时间轴内发生的广告的信息。

<table frame="all" colsep="1" rowsep="1" id="table_1A59E777BA99466793D586286F19E933"> 
 <thead> 
  <tr rowsep="1"> 
   <th colname="1" class="entry"> 名称 </th> 
   <th colname="2" class="entry"> 描述 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAd.html" format="html" scope="external"> PTAd</a> </td> 
   <td colname="2">定义广告抽象并保存所有广告信息的类。 它由唯一ID、持续时间和MediaResource定义。 MediaResource包含实际广告内容所在的URL。 
    <pre>
      表示拼接到内容中的主要线性资源。 可以选择包含一系列必须随线性资产一起显示的伴随资产。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdAsset.html" format="html" scope="external"> PTAdAsset</a> </td> 
   <td colname="2">表示要显示的资源的类。 
    <pre>
      表示要显示的资产。
    </pre> 
    <pre>
      表示广告资源的类。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBannerView.html" format="html" scope="external"> PTAdBannerView</a> </td> 
   <td colname="2">
    <pre>
      显示横幅资源。 您的应用程序必须创建一个该实用程序类的新实例，设置横幅资产，并将其添加到视图中。 横幅的展示和点击跟踪由此类进行内部管理。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdBreak.html" format="html" scope="external"> PTAdBreak</a> </td> 
   <td colname="2">类可统一查看将在播放过程中的某个时间点播放的多个广告。 
    <pre>
      表示粘贴到内容中的连续广告序列。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdClick.html" format="html" scope="external"> PTAdClick</a> </td> 
   <td colname="2">表示与资产关联的点击实例的类。 此实例包含有关点进URL和标题的信息，可用于向用户提供其他信息。 
    <pre>
      表示与资源关联的点击实例。 此实例包含有关点进URL和标题的信息，可用于向用户提供其他信息。
    </pre> </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTAdPolicyInfo.html" format="html" scope="external"> PTAdPolicyInfo</a> </td> 
   <td colname="2"> 定义AdPolicySelector API调用的属性的协议。 这些属性提供了用于实施每个广告行为的上下文。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1">ptadPolicySelector</td> 
   <td colname="2"> 用于实施广告行为的广告策略选择器协议。 应用程序可以通过实现所有所需的方法或通过扩展现有的默认策略选择器类来自定义特定行为，来遵守此协议。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> PTAd时间轴</td> 
   <td colname="2"> 表示内容中分隔符时间轴的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"> 
    <pre>
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Classes/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> 类， 
     <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolver.html" format="html" scope="external"> PTContentResolver</a> 协议
    </pre> </td> 
   <td colname="2"> 在Adobe Primetime广告决策流程中处理广告解析部分的类。 </td> 
  </tr> 
  <tr rowsep="1"> 
   <td colname="1"><a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Protocols/PTContentResolverDelegate.html" format="html" scope="external"> PTContentResolverDelegate</a> </td> 
   <td colname="2"> 描述自定义内容解析器( <span class="codeph"> PTContentResolver</span> )应该使用向委派传达内容解析的状态。 </td> 
  </tr> 
  <tr rowsep="0"> 
   <td colname="1"> <a href="https://help.adobe.com/en_US/primetime/api/psdk/appledoc/Constants/PTPlacementType.html" format="html" scope="external"> PTPlacementType</a> </td> 
   <td colname="2">抽象放置信息请求的类。 每个已解析广告必须附加一个版面信息。 投放位置信息描述广告在时间轴上的放置位置。 它包含如下信息： 
    <ul id="ul_A9105A78F0C24488BCD5E3F2EE62A3EE"> 
     <li id="li_01E968A4330D4B40BA1EB6F4A6000FFD">投放位置（以毫秒为单位） </li> 
     <li id="li_A3DC9498BEE14FBA9E7A5D26874F3984">投放类型（前置、中置或后置） </li> 
     <li id="li_4B9094DD318B4792854A377CC6064232">即将替换的主内容块的持续时间 </li> 
    </ul> </td> 
  </tr> 
 </tbody> 
</table>
