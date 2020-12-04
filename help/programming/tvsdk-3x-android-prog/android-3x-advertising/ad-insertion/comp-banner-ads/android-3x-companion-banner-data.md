---
description: AdAsset的内容描述了配套横幅。
seo-description: AdAsset的内容描述了配套横幅。
seo-title: 配套横幅数据
title: 配套横幅数据
uuid: f54aecea-5e11-45dd-97d0-5774ca631a4d
translation-type: tm+mt
source-git-commit: bc35da8b258056809ceaf18e33bed631047bc81b
workflow-type: tm+mt
source-wordcount: '172'
ht-degree: 0%

---


# 配套横幅数据{#companion-banner-data}

AdAsset的内容描述了配套横幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

每个`AdAsset`都提供有关显示资产的信息。

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> <b>可用信息  </b></th> 
   <th colname="col2" class="entry"> <b>说明</b> </th> 
  </tr> 
 </thead>
 <tbody> 
  <tr> 
   <td colname="col1"> 宽度 </td> 
   <td colname="col2"> 配套横幅的宽度（以像素为单位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 高度 </td> 
   <td colname="col2"> 配套横幅的高度（以像素为单位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 资源类型 </td> 
   <td colname="col2">此配套横幅的资源类型： 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html:数据以HTML代码显示。 </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe:数据是iframe URL(src)。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 静态URL </td> 
   <td colname="col2"> <p>有时，配套横幅还具有<span class="codeph"> staticURL</span>，它是指向图像或<span class="codeph"> .swf</span>（flash横幅）的直接URL。 </p> <p>如果不想使用html或iframe，可以使用图像或swf的直接URL在Flash阶段显示横幅。 在这种情况下，可以使用<span class="codeph"> staticURL</span>显示横幅。 </p> <p>重要： 您必须检查静态URL是否是有效字符串，因为此属性可能不总是可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>