---
description: TVSDK播放器会派送事件来显示自定义广告加载状态或忽略加载时间过长或有错误的广告。 这些事件在事件.CustomAdEvents中定义。
seo-description: TVSDK播放器会派送事件来显示自定义广告加载状态或忽略加载时间过长或有错误的广告。 这些事件在事件.CustomAdEvents中定义。
seo-title: 自定义广告事件
title: 自定义广告事件
uuid: 78e2ccf4-5943-4c60-84be-623182d9a300
translation-type: tm+mt
source-git-commit: 040655d8ba5f91c98ed0584c08db226ffe1e0f4e
workflow-type: tm+mt
source-wordcount: '210'
ht-degree: 0%

---


# 自定义广告事件{#custom-ad-events}

TVSDK播放器会派送事件来显示自定义广告加载状态或忽略加载时间过长或有错误的广告。 这些事件在事件.CustomAdEvents中定义。

<table id="table_718700E0F0B042F882ED131F79E01D4E"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 事件 </th> 
   <th colname="col2" class="entry"> 定义 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdClickThru  </span> </td> 
   <td colname="col2"> 查看器点击自定义广告的次数。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdError  </span> </td> 
   <td colname="col2"> 自定义广告出错。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdLoaded  </span> </td> 
   <td colname="col2"> 自定义广告已加载。  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> 广告加载  </span> </td> 
   <td colname="col2"> 正在加载自定义广告。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPaused  </span> </td> 
   <td colname="col2"> 自定义广告已暂停。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdResuted  </span> </td> 
   <td colname="col2"> 暂停后，自定义广告继续播放。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdPlaying  </span> </td> 
   <td colname="col2"> 正在播放自定义广告。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> <span class="codeph"> AdProgress  </span> </td> 
   <td colname="col2"> <p>自定义广告播放器会通知TVSDK播放器自定义广告的进度。 &amp;nbsp </p> <p>广告的<span class="codeph"> currentTime </span>和<span class="codeph"> totalTime </span>是使用此事件传递的。 </p> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStarted </td> 
   <td colname="col2"> 自定义广告已开始播放，并显示给查看器。  </td> 
  </tr> 
  <tr> 
   <td colname="col1"> AdStopped </td> 
   <td colname="col2"> 自定义广告已播放完毕。 </td> 
  </tr> 
 </tbody> 
</table>

<!--<a id="section_027774C2A47C453BA9DED61C6F8567C3"></a>-->

