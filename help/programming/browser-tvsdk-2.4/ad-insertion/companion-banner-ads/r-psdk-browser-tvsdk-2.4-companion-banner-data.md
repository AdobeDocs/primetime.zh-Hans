---
description: AdBannerAsset的内容描述了配套横幅。
seo-description: AdBannerAsset的内容描述了配套横幅。
seo-title: 配套横幅数据
title: 配套横幅数据
uuid: b2c709da-9d19-49d1-8116-9c947371b77c
translation-type: tm+mt
source-git-commit: d2b8cb67c54fadb8e0e7d2bdc15e393fdce8550e
workflow-type: tm+mt
source-wordcount: '190'
ht-degree: 0%

---


# 配套横幅数据{#companion-banner-data}

AdBannerAsset的内容描述了配套横幅。

<!--<a id="section_D730B4FD6FD749E9860B6A07FC110552"></a>-->

`AdobePSDK.PSDKEventType.AD_STARTED`事件返回一个`Ad`实例，该实例包含`companionAssets`属性(`Array<AdBannerAsset>`)。
每个`AdBannerAsset`都提供有关显示资产的信息。

<table id="table_760C885E2DCA4BE983CC57FDA7BD5B14"> 
 <thead> 
  <tr> 
   <th colname="col1" class="entry"> 可用信息 </th> 
   <th colname="col2" class="entry"> 说明 </th> 
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
     <li id="li_48E74AC5F00640EC8A4DE2CB31E106EC">静态：数据是静态图像URL(src)。 </li> 
    </ul> </td> 
  </tr> 
  <tr> 
   <td colname="col1">
    <pre>
      横幅数据
    </pre> </td> 
   <td colname="col2"> 由<span class="codeph"> resourceType</span>为此配套横幅指定的类型的数据。 </td> 
  </tr> 
  <tr> 
   <td colname="col1"> 静态URL </td> 
   <td colname="col2"> <p>有时，配套横幅也可能包含静态URL，该URL是图像的直接URL。 </p> <p>如果不想使用html或iframe，可以使用图像的直接URL。 在这种情况下，您可以使用staticURL显示横幅。 </p> <p>重要： 您必须检查静态URL是否是有效字符串，因为此属性可能不总是可用。 </p> </td> 
  </tr> 
 </tbody> 
</table>

