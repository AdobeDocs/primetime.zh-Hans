---
description: AdAsset的内容描述随附横幅。
title: 随附横幅数据
exl-id: 922577fd-bc58-4669-b051-fe54b197a5f5
source-git-commit: be43bbbd1051886c8979ff590a3197b2a7249b6a
workflow-type: tm+mt
source-wordcount: '160'
ht-degree: 0%

---

# 随附横幅数据 {#companion-banner-data}

AdAsset的内容描述随附横幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

每个 `AdAsset` 提供了有关显示资产的信息。

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 可用信息 </th> 
   <th colname="col2" class="entry"> 描述 </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 宽度 </td> 
   <td colname="col2"> 随附横幅的宽度（以像素为单位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 高度 </td> 
   <td colname="col2"> 随附横幅的高度（以像素为单位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 资源类型 </td> 
   <td colname="col2">此随附横幅的资源类型： 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html：数据采用HTML代码。 </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe：数据是iframe URL (src)。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 静态URL </td> 
   <td colname="col2"> <p>有时，随附横幅也会显示 <span class="codeph"> staticURL</span> 即指向图像或的直接URL <span class="codeph"> .swf</span> (flash banner)。 </p> <p>如果不想使用html或iframe，则可以使用图像的直接URL或swf来显示Flash舞台中的横幅。 在这种情况下，您可以使用 <span class="codeph"> staticURL</span> 以显示横幅。 </p> <p>重要信息：您必须检查静态URL是否为有效字符串，因为此属性可能并非始终可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>
