---
description: TVSDK播放器会调度事件以显示自定义广告加载状态，或忽略加载时间过长或有错误的广告。 这些事件在events.CustomAdEvents中定义。
title: 自定义广告事件
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '175'
ht-degree: 0%

---

# 自定义广告事件{#custom-ad-events}

TVSDK播放器会调度事件以显示自定义广告加载状态，或忽略加载时间过长或有错误的广告。 这些事件在events.CustomAdEvents中定义。

<table id="table_718700E0F0B042F882ED131F79E01D4E"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 事件 </th> 
   <th colname="col2" class="entry"> 定义 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdClickThru </span> </td> 
   <td colname="col2"> 查看者点击自定义广告的次数。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdError </span> </td> 
   <td colname="col2"> 自定义广告出错。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> adloaded </span> </td> 
   <td colname="col2"> 已加载自定义广告。  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoading </span> </td> 
   <td colname="col2"> 正在加载自定义广告。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPaused </span> </td> 
   <td colname="col2"> 自定义广告已暂停。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdResumed </span> </td> 
   <td colname="col2"> 自定义广告在暂停后继续播放。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> Adplaying </span> </td> 
   <td colname="col2"> 正在播放自定义广告。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdProgress </span> </td> 
   <td colname="col2"> <p>自定义广告播放器会通知TVSDK播放器自定义广告的进度。 &amp;nbsp； </p> <p>此 <span class="codeph"> currenttime </span> 和 <span class="codeph"> totalTime </span> 的广告的点击量。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStarted </td> 
   <td colname="col2"> 自定义广告已开始播放，并向查看器显示。  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStopped </td> 
   <td colname="col2"> 自定义广告已播放完毕。 </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->
