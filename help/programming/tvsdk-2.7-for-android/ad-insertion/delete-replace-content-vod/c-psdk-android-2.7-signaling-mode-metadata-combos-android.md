---
description: 您可以使用不同的广告信令模式和广告元数据组合来标记、删除和替换VOD流中的时间范围。 不同的信令模式和元数据组合会导致不同的行为。
title: 广告插入和删除对广告信令模式和广告元数据组合的影响
translation-type: tm+mt
source-git-commit: 89bdda1d4bd5c126f19ba75a819942df901183d1
workflow-type: tm+mt
source-wordcount: '434'
ht-degree: 0%

---


# 广告插入和删除对广告信令模式和广告元数据组合的影响{#effect-on-ad-insertion-and-deletion-from-ad-signaling-mode-and-ad-metadata-combinations}

您可以使用不同的广告信令模式和广告元数据组合来标记、删除和替换VOD流中的时间范围。 不同的信令模式和元数据组合会导致不同的行为。

>[!TIP]
>
>当时间范围与广告信令模式之间存在冲突时，TVSDK会给予时间范围优先级。

下表提供了有关信令模式和元数据组合行为的详细信息：

<table id="table_6044AA1ACFA244FA814EA2D0766C6D12"> 
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
   <td colname="1"> <p><b>服务器映射</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr> 
   <td> </td> 
   <td> 删除 </td> 
   <td> 删除 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </td> 
   <td> 已删除的范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除，Auditude </td> 
   <td> 删除，Auditude </td> 
   <td> 
    <ul id="ul_E0A2F885E93B4D23A486C37B305E17D8"> 
     <li id="li_D977B398D3904A44AFEC4B05AB0E3340"><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.DELETE),  </span> </li> 
     <li id="li_439886CB38AA46239C2E40352443888A"><span class="codeph"> PlacementInfo(Type.SERVER_MAP，Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> 删除范围，插入广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.SERVER_MAP，Mode.INSERT)</span> </td> 
   <td> 插入的广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 替换，Auditude </td> 
   <td> 删除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.DELETE)、PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.REPLACE)</span> </td> 
   <td> 已替换范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 标记的范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark， Auditude </td> 
   <td> CustomAd， Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 标记范围，未插入广告 </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p><b>清单提示</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.PRE_ROLL， Mode.INSERT)</span> </td> 
   <td> 插入的广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除，Auditude </td> 
   <td> 删除，Auditude </td> 
   <td> 
    <ul id="ul_2DD298538E9344B9BAB882485BB57747"> 
     <li id="li_F39A69EFA7ED45C18978A2C462AF7641"><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </li> 
     <li id="li_8CCDA3B1C63F4BC396F28F443D8C42F8"><span class="codeph"> PlacementInfo(Type.PRE_ROLL， Mode.INSERT)</span> </li> 
    </ul> </td> 
   <td> 删除范围，插入广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark， Auditude </td> 
   <td> Mark， Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 标记范围，未插入广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除 </td> 
   <td> 删除 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </td> 
   <td> 已删除的范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 标记的范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 替换，Auditude </td> 
   <td> 删除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.DELETE)、PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.REPLACE)</span> </td> 
   <td> 已替换范围 </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p><b>自定义时间范围</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除 </td> 
   <td> 删除 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </td> 
   <td> 已删除的范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除，Auditude </td> 
   <td> 删除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </td> 
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
   <td> 替换，Auditude </td> 
   <td> 删除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.DELETE)、PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.REPLACE)</span> </td> 
   <td> 范围已替换为广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 标记的范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark， Auditude </td> 
   <td> 自定义广告，Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 标记范围，未插入广告 </td> 
  </tr> 
  <tr> 
   <td colname="1"> <p><b>未设置（默认）</b> </p> </td> 
   <td colname="2"> </td> 
   <td colname="3"> </td> 
   <td colname="4"> </td> 
   <td colname="5"> </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除 </td> 
   <td> 删除 </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.DELETE)</span> </td> 
   <td> 已删除的范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 删除，Auditude </td> 
   <td> 删除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.DELETE)、PlacementInfo(Type.SERVER_MAP， Mode.INSERT)</span> </td> 
   <td> 删除范围，插入广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Auditude </td> 
   <td> Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.SERVER_MAP，Mode.INSERT)</span> </td> 
   <td> 插入的广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> 替换，Auditude </td> 
   <td> 删除，Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.DELETE)、PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.REPLACE)</span> </td> 
   <td> 范围已替换为广告 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark </td> 
   <td> CustomAd </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 标记的范围 </td> 
  </tr> 
  <tr> 
   <td></td> 
   <td> Mark， Auditude </td> 
   <td> CustomAd， Auditude </td> 
   <td><span class="codeph"> PlacementInfo(Type.CUSTOM_TIME_RANGE， Mode.MARK)</span> </td> 
   <td> 标记的范围 </td> 
  </tr> 
 </tbody> 
</table>

