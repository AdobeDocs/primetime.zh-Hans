---
description: 您可以使用不同的广告信号模式和广告元数据组合来标记、删除和替换VOD流中的时间范围。 不同的信令模式和元数据组合会导致不同的行为。
seo-description: 您可以使用不同的广告信号模式和广告元数据组合来标记、删除和替换VOD流中的时间范围。 不同的信令模式和元数据组合会导致不同的行为。
seo-title: 广告信号模式和广告元数据组合对广告插入和删除的影响
title: 广告信号模式和广告元数据组合对广告插入和删除的影响
uuid: c2ae8148-889d-46ae-848a-5f45d993a0e2
translation-type: tm+mt
source-git-commit: 5908e5a3521966496aeec0ef730e4a704fddfb68
workflow-type: tm+mt
source-wordcount: '472'
ht-degree: 0%

---


# 广告信号模式和广告元数据组合对广告插入和删除的影响{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

您可以使用不同的广告信号模式和广告元数据组合来标记、删除和替换VOD流中的时间范围。 不同的信令模式和元数据组合会导致不同的行为。

>[!NOTE]
>
>当时间范围与广告信令模式之间存在冲突时，TVSDK会优先选择时间范围。

**表3:信令模式／元数据组合行为**

<table>  
 <thead> 
  <tr> 
   <th class="entry"> 广告信令模式 </th> 
   <th class="entry"> 广告元数据 </th> 
   <th class="entry"> 已创建解析器 </th> 
   <th class="entry"><span class="codeph"> 放置信</span> 息已创建 </th> 
   <th class="entry"> 结果行为 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td> <b>服务器映射</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> 删除 </td> 
   <td> 删除 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 已删除范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除，Auditude </td> 
   <td> 删除，Auditude </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE),  </span> </li> 
     <li><span class="codeph"> PlacementInfo(Type.SERVER_MAP,Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> 删除范围、插入广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.SERVER_MAP,Mode.INSERT)</span> </td> 
   <td> 插入的广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 替换， Auditude </td> 
   <td> 删除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)、PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> 已替换范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 标记 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 标记的范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 标记范围，未插入广告 </td> 
  </tr> 
  <tr> 
   <td> <b>清单提示</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.PRE_ROLL, Mode.INSERT)</span> </td> 
   <td> 插入的广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除，Auditude </td> 
   <td> 删除，Auditude </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </li> 
     <li><span class="codeph"> PlacementInfo(Type.PRE_ROLL, Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> 删除范围，插入广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> Mark, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 标记范围，未插入广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除 </td> 
   <td> 删除 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 已删除范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 标记 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 标记的范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 替换， Auditude </td> 
   <td> 删除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)、PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> 已替换范围 </td> 
  </tr> 
  <tr> 
   <td> <b>自定义时间范围</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除 </td> 
   <td> 删除 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 已删除范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除，Auditude </td> 
   <td> 删除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 范围已删除，未插入任何广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td> 无 </td> 
   <td> 未插入广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 替换， Auditude </td> 
   <td> 删除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)、PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> 用广告替换范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 标记 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 标记的范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> 自定义广告， Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 标记范围，未插入广告 </td> 
  </tr> 
  <tr> 
   <td> <b>未设置（默认）</b> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
   <td> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除 </td> 
   <td> 删除 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)</span> </td> 
   <td> 已删除范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除，Auditude </td> 
   <td> 删除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)、PlacementInfo(Type.SERVER_MAP, Mode.INSERT)</span> </td> 
   <td> 删除范围，插入广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.SERVER_MAP,Mode.INSERT)</span> </td> 
   <td> 插入的广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 替换， Auditude </td> 
   <td> 删除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.DELETE)、PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.REPLACE)</span> </td> 
   <td> 用广告替换范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 标记 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 标记的范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark, Auditude </td> 
   <td> CustomAd, Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE, Mode.MARK)</span> </td> 
   <td> 标记的范围 </td> 
  </tr> 
 </tbody> 
</table>

