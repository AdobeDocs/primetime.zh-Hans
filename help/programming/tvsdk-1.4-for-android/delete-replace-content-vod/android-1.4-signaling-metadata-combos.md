---
description: 您可以使用不同的广告信令模式和广告元数据组合来标记、删除和替换VOD流中的时间范围。 信令模式和元数据的不同组合导致不同的行为。
title: 对广告信令模式和广告元数据组合中的广告插入和删除的影响
exl-id: 0b265471-2d5c-432b-b1c9-c850ce99f2f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '426'
ht-degree: 0%

---

# 对广告信令模式和广告元数据组合中的广告插入和删除的影响{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

您可以使用不同的广告信令模式和广告元数据组合来标记、删除和替换VOD流中的时间范围。 信令模式和元数据的不同组合导致不同的行为。

>[!NOTE]
>
>当时间范围与广告信令模式存在冲突时，TVSDK给出时间范围的优先级。

**表3：信令模式/元数据组合行为**

<table>  
 <thead> 
  <tr> 
   <th class="entry"> 广告信令模式 </th> 
   <th class="entry"> 广告元数据 </th> 
   <th class="entry"> 已创建解析程序 </th> 
   <th class="entry"><span class="codeph"> 投放位置信息</span> 已创建 </th> 
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
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </td> 
   <td> 已删除范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除，审核 </td> 
   <td> 删除，审核 </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)， </span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.SERVER_MAP， Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> 已删除范围，插入广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP， Mode.INSERT)</span> </td> 
   <td> 广告已插入 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 替换，审计 </td> 
   <td> 删除，审核 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)、PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)DELETE</span> </td> 
   <td> 已替换范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 标记 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 标记的范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark， Auditude </td> 
   <td> CustomAd， Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 已标记范围，未插入广告 </td> 
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
   <td><span class="codeph"> PlacementInfo (Type.PRE_ROLL， Mode.INSERT)</span> </td> 
   <td> 广告已插入 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除，审核 </td> 
   <td> 删除，审核 </td> 
   <td> 
    <ul> 
     <li><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </li> 
     <li><span class="codeph"> PlacementInfo (Type.PRE_ROLL， Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> 已删除范围，插入广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark， Auditude </td> 
   <td> Mark， Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 已标记范围，未插入广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除 </td> 
   <td> 删除 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </td> 
   <td> 已删除范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 标记 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 标记的范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 替换，审计 </td> 
   <td> 删除，审核 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)、PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)DELETE</span> </td> 
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
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </td> 
   <td> 已删除范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除，审核 </td> 
   <td> 删除，审核 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </td> 
   <td> 已删除范围，未插入广告 </td> 
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
   <td> 替换，审计 </td> 
   <td> 删除，审核 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)、PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)DELETE</span> </td> 
   <td> 范围已替换为广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 标记 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 标记的范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark， Auditude </td> 
   <td> 自定义广告、审核 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 已标记范围，未插入广告 </td> 
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
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </td> 
   <td> 已删除范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除，审核 </td> 
   <td> 删除，审核 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.INSERT)、PlacementInfo (Type.SERVER_MAP， Mode.INSERT)DELETE</span> </td> 
   <td> 已删除范围，插入广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.SERVER_MAP， Mode.INSERT)</span> </td> 
   <td> 广告已插入 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 替换，审计 </td> 
   <td> 删除，审核 </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)、PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.REPLACE)DELETE</span> </td> 
   <td> 范围已替换为广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 标记 </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 标记的范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark， Auditude </td> 
   <td> CustomAd， Auditude </td> 
   <td><span class="codeph"> PlacementInfo (Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 标记的范围 </td> 
  </tr> 
 </tbody> 
</table>
