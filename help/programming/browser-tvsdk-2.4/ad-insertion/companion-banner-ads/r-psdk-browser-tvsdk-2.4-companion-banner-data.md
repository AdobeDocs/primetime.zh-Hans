---
description: AdBannerAsset的内容描述随附横幅。
title: 随附横幅数据
source-git-commit: 02ebc3548a254b2a6554f1ab34afbb3ea5f09bb8
workflow-type: tm+mt
source-wordcount: '178'
ht-degree: 0%

---

# 随附横幅数据{#companion-banner-data}

AdBannerAsset的内容描述随附横幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

此 `AdobePSDK.PSDKEventType.AD_STARTED` 事件返回 `Ad` 包含 `companionAssets` 属性( `Array<AdBannerAsset>`)。
每个 `AdBannerAsset` 提供了有关显示资产的信息。

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
   <td colname="col2"> 伴随横幅的宽度（像素）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 高度 </td> 
   <td colname="col2"> 伴随横幅的高度（以像素为单位）。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 资源类型 </td> 
   <td colname="col2">此随附横幅的资源类型： 
    <ul id="ul_A067787FE49E4B6095BE0AC1D447DBB3"> 
     <li id="li_02B7224C67004095B3F6E50FD21E507E">html：数据采用HTML代码。 </li> 
     <li id="li_5F37E14472424F808C6094F42009E676">iframe：数据是iframe URL (src)。 </li> 
     <li id="li_48E74AC5F00640EC8A4DE2CB31E106EC">静态：数据是静态图像URL (src)。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">
    <pre>
      横幅数据
    </pre> </td> 
   <td colname="col2"> 由指定的类型的数据 <span class="codeph"> resourceType</span> 为这个同伴横幅准备的。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 静态URL </td> 
   <td colname="col2"> <p>有时，随附横幅也可能具有作为图像的直接URL的staticURL。 </p> <p>如果您不想使用html或iframe，则可以使用图像的直接URL。 在这种情况下，您可以使用staticURL显示横幅。 </p> <p>重要信息：您必须检查静态URL是否为有效的字符串，因为此属性可能并不总是可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>
